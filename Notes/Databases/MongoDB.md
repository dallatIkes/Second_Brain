Popular [[NoSQL]] [[Bases de données|database]] integrated into [[FastAPI]] applications using [[pymongo]]

# Establish a connection

1. **Define connection configuration in a `database.py` file**
```python
from pymongo import MongoClient

client = MongoClient()
database = client.mydatabase
# mydatabase is the name of the database
# the default port on which runs the MongoDB instance is 27017
```
2. **Define the collections :** collections are equivalent to tables in [[SQL]] [[Bases de données|databases]]
```python
user_collection = database["users"]
# user_collection is a reference to the users collection in the MongoDB database
```
3. **Test the connection**
```python
from database import user_collection
from fastapi import FasstAPI, HTTPException
from pydantic import BaseModel

app = FastAPI()

class User(BaseModel):
	name: str
	email: str
	
@app.get("/users")
def read_users() -> list[User]:
	return [user for user in user_collection.find()]
```
4. **Run the `mongod` instance**
```bash
$ mongod
```

# [[CRUD]] operations

```python
# Creating a new user
@app.post("/user")
def create_user(user: User) -> UserResponse:
    result = user_collection.insert_one(
        user.model_dump(exclude_none=True)
    )
    user_response = UserResponse(
        id=str(result.inserted_id), **user.model_dump()
    )
    return user_response
```

```python
# Reading a user
@app.get("/user")
def get_user(user_id: str) -> UserResponse:
    db_user = user_collection.find_one(
        {
            "_id": ObjectId(user_id)
            if ObjectId.is_valid(user_id)
            else None
        }
    )
    if db_user is None:
        raise HTTPException(
            status_code=404, detail="User not found"
        )
    db_user["id"] = str(db_user["_id"])
    return db_user
```