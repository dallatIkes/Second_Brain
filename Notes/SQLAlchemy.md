# Introduction

[[SQLAlchemy]] is a popular [[ORM]] option for [[Python]]. It acts as a bridge between the [[Python]] code and the [[Bases de données|database]] enabling us to interact with the [[Bases de données|database]] using [[Python]] [[Classe|classes]] and [[Objet|object]] rather than writing ran [[SQL]] queries.

---

# Configuration

1. **Create the `Base` [[Classe|Class]]**
```python
   from sqlalchemy.orm import DeclarativeBase
   
   class Base(DeclarativeBase):
	   pass
```
2. **Define models**
```python
form sqlalchemy.orm import (Mapped, mapped_column)

class User(Base):
	__tablename__ = "user"
	id: Mapped[int] = mapped_column(primary_key=True)
	name: Mapped[str]
	email: Mapped[str]
```
3. **Define the connection string to connect to the [[Bases de données|database]]**
```python
# Here is an example of a connection string for a SQLite database
DATABASE_URL = "sqlite:///./test.db"
```
4. **Create an Engine**
```python
from sqlalchemy.orm import create_engine

engine = create_engine(DATABASE_URL)
```
5. **Create the tables in the [[Bases de données|database]]**
```python
Base.metadata.create_all(engine)
```


# Establishing a [[Bases de données|database]] connection

[[Bases de données|Database]] connection are managed with **sessions** : temporary workspaces for talking to the [[Bases de données|database]] (send queries, track objects, handle transactions)

You never want one global session shared by everyone. Each request should get its own session

```python
from sqlalchemy.orm import sessionmaker

SessionLocal = sessionmaker(
	autocommit=False,
	autoflush=False,
	bind=engine
)
```
Here `SessionLocal` is not a session but a session factory (a function that creates sessions)
```python
db = SessionLocal() # db is an actual Session instance
```
These parameters are important
- `bind=engine` : tells [[SQLAlchemy]] which [[Bases de données|database]] to talk to
- `autocommit=False` : we must explicitly call `db.commit()` (we control transactions)
- `autoflush=False` : [[SQLAlchemy]] won't auto-send changes to the [[Bases de données|db]] before queries

To get access to the [[Bases de données|database]] in an endpoint, we use the following function
```python
from database import SessionLocal

def get_db():
	db = SessionLocal()
	try:
		yield db
	finally:
		db.close()
```
This function does 3 critical things :
- **Creates a new session per request :** each [[HTTP]] request gets its own session and its own transaction scope
- **Gives the session to [[FastAPI]] via `yield`** : 
	- [[FastAPI]] pauses here
	- injects db into the endpoint
	- runs the endpoint code
	- resumes after the request is done
- **Guarantees cleanup via `db.close()`** : releases [[Bases de données|database]] connection and prevents connection leaks (even if an [[Exception|exception]] happens)

[[FastAPI]] uses this with `Depends`
```python
from fastapi import Depends, FastAPI
from sqlalchemy import Session
from database import SessionLocal

app = FastAPI()

@app.get("/users/")
def read_users(db: Session = Depends(get_db)):
	users = db.query(User).all()
	return users
```
What [[FastAPI]] does internally :
- sees `Depends(get_db)`
- calls `get_db()`
- gets a session from `yield`
- passes it as `db`
- runs the endpoint
- after response runs `finally` (`db.close()`)
**This pattern is called : Session per request**

# Understanding [[CRUD]] operations with [[SQLAlchemy]]

```python
# Creating a new user
@app.post("/user")
def add_new_user(
    user: UserBody, db: Session = Depends(get_db)
):
    new_user = User(name=user.name, email=user.email)
    db.add(new_user)
    db.commit()
    db.refresh(new_user)
    return new_user
```

```python
# Reading a specific user
@app.get("/user")
def get_user(
    user_id: int, db: Session = Depends(get_db)
):
    user = (
        db.query(User)
        .filter(User.id == user_id)
        .first()
    )
    if user is None:
        raise HTTPException(
            status_code=404, detail="User not found"
        )

    return user
```

```python
# Updating a user
@app.post("/user/{user_id}")
def update_user(
    user_id: int,
    user: UserBody,
    db: Session = Depends(get_db),
):
    db_user = (
        db.query(User)
        .filter(User.id == user_id)
        .first()
    )
    if db_user is None:
        raise HTTPException(
            status_code=404, detail="User not found"
        )
    db_user.name = user.name
    db_user.email = user.email
    db.commit()
    db.refresh(db_user)
    return db_user
```

```python
# Deleting a user
@app.delete("/user")
def delete_user(
    user_id: int, db: Session = Depends(get_db)
):
    db_user = (
        db.query(User)
        .filter(User.id == user_id)
        .first()
    )
    if db_user is None:
        raise HTTPException(
            status_code=404, detail="User not found"
        )
    db.delete(db_user)
    db.commit()
    return {"detail": "User deleted"}
```


