"[[FastAPI]] is a modern, fast web framework for building [[API|APIs]] with [[Python]] based on standard [[Python]] type hints."

The key features that define [[FastAPI]] are its :
- speed
- ease of use
- automatic documentation

---
# First steps with [[FastAPI]]

## Applying asynchronous programming

Allows an application to handle more requests simultaneously 

```python
async def read_root():
	return {"Hello": "World"}
```

## Exploring routers and endpoints

**Endpoints** are the points at which [[API]] interactions happen. In [[FastAPI]], an endpoint is created by decorating a function with an [[HTTP]] method

```python
# Exemple with the HTTP GET method
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
async def read_root():
	return {"Hello": "World"}
```

**Routers** assist us in grouping our endpoints into different modules, which makes our code base easier to maintain and understand

```python
# router_example.py
from fastapi import APIRouter

router = APIRouter()

@router.get("/items/{item_id}")
async def read_item(item_id: int):
	return {"item_id": item_id}
```

```python
# main.py
from fastapi import FastAPI
import router_example

app = FastAPI()
app.include_router(router_example.router)
```

## Working with path parameters and query parameters

**Path parameters** are part of the URL that are expected to change. For instance, in an endpoint such as `/books/{book_id}`, `book_id` is a path parameter

```python
@app.get("/authors/{author_id}")
async def read_author(author_id: int):
	return {
		"author_id": author_id,
		"name": "Ernest Hemingway"
	}
```

**Query parameters** are used to refine or customize the response of an [[API]] endpoint. They can be included in the URL after a `?`. For instance `/books?genre=fiction&year=2010`

```python
@app.get("/books")
async def read_books(year: int = None):
	if year:
		return {
			"year": year,
			"books": ["Book 1", "Book 2"]
		}
	return {"books": ["All Books"]}
```

## Defining and using request and response models

**[[Pydantic]]** models are a powerful feature for data validation and conversion

```python
from pydantic import BaseModel

class Book(BaseModel):
	title: str
	author: str
	year: int
```

---

# Working with data

- Data handling is the backbone of any web application
- [[SQL]] vs [[NoSQL]]
- [[CRUD]] operations

## [[SQL]] [[Bases de données|Databases]] : [[SQLAlchemy]]

![[SQLAlchemy]]

## [[NoSQL]] [[Bases de données|Databases]] : [[MongoDB]]

![[MongoDB]]

### Handling relationships in [[NoSQL]] [[Bases de données|Databases]]

Two primary approches can be used :
- **Embedding :** storing the data within the document (frequent access, more expensive in storage) (ex:  album)
- **Referencing :** storing references using object IDs or other unique identifiers (better for many-to-one or many-to-many relationships) (ex: playlist)
The issue here is to find a compromise between **complexity** (reading, operations, ...) and **flexibility** (less storage but more complex queries)
## Working with data validation ans serialization

We use [[Pydantic]] for :
- Data [[Serialization vs Deserialization|serialization]] ([[Pydantic]] models $\rightarrow$ [[JSON]])
- Data [[Serialization vs Deserialization|deserialization]]
- Data validation

## Working with file uploads and downloads

- **File uploads** can be handled with the `File` and `UploadFile` [[Classe|classes]]
- **File downloads** can be handled with the `UploadFile` [[Classe|class]]

## Handling asynchronous data operations

Allows our app to handle multiple tasks concurrently which is well-suited for [[IO]] operations such as [[Bases de données|database]] interactions, file handling or network communication.

Using asynchronous data operations can significantly improve our app performances (cf. [async_example](https://github.com/PacktPublishing/FastAPI-Cookbook/tree/main/Chapter02/async_example). Indeed, by not blocking the main [[Thread|thread]] while waiting for these operations to complete, the application remains responsive and capable of handling other incoming requests or tasks.

Asynchronous data operations are handled by : 
- [[SQLAlchemy]] with the [[asyncio]] library
- [[pymongo]] with the [[motor]] package

The best practices for using asynchronous programming in [[FastAPI]] are : 
- [[IO]]-bound operations
- [[Bases de données|Database]] transactions
- Error handling
- [[Test|Testing]]

## Securing sensitive data and best practices

[[FastAPI]] doesn't handle [[Cryptographie|encryption]] directly but libraries such as **bcrypt** or **passlib** can be used

Some best practices when securing an application : 
- Validation and sanitization
- Access control
- Secure communication
- [[Bases de données|Database]] security
- Regular updates

---

# Testing your [[API]]

[[FastAPI]] has a built-in utility for testing the app's endpoints : `TestClient`

```python
# main.py
from fastapi import FastAPI
app = FastAPI()

@app.get("/ping")
def ping():
    return {"message": "pong"}
```

```python
# test_main.py
from fastapi.testclient import TestClient
from main import app  # Import your FastAPI application

client = TestClient(app)

def test_ping():
    response = client.get("/ping")
    assert response.status_code == 200
    assert response.json() == {"message": "pong"}
```

[[Pytest]] can be used to test the app's logic

Performance testing is also important to test the [[API]] in real-world usage scenarios. [[locust]] can be used to simulate high traffic

---

# Versioning your [[API]]

There are many ways to version an [[API]], the most common ones are : 
- **[[URL]] versioning :** The version number is included in the [[URL]] (ex: `https://example-api.com/v1/products`)
- **Query parameter versioning :** The version number is now a query parameter (ex: `https://example-api.com/products?version=v1`)
- **Header versioning :** The version number is passed as a header by the consumer
- **Consumer-based versioning :** The user chooses the version at the first call, it it then stored in their information and is automatically used for the next requests (unless changed)

More to learn on the topic at : https://www.postman.com/api-platform/api-versioning/

---

# [[Authentication]] and [[Authorization]]

##  [[Authentication]]

For [[Authentication]] [[Oauth2]] and [[JWT]]s can be used :

1. **Authenticate the user (with their username and password)**
2. **Create function to generate [[Token|token]]**
3. **Create the `/token` endpoint that calls the [[Token|token]] creation function**
4. **Use the `OAuth2PasswordBearer` [[FastAPI]] helper to extract the [[Token|token]] from the header**
5. **Create the `/users/me` endpoint that decodes the [[Token|token]]**

### Login endpoint

```python
@app.post("/token")
def login(
    form_data: OAuth2PasswordRequestForm = Depends(),
    db: Session = Depends(get_db)
):
    user = db.query(User).filter(User.username == form_data.username).first()
    if not user or not verify_password(form_data.password, user.hashed_password):
        raise HTTPException(status_code=400, detail="Invalid credentials")

    token = create_access_token({"sub": user.username})
    return {"access_token": token, "token_type": "bearer"}
```

### Get current user from token

```python
def get_current_user(
    token: str = Depends(oauth2_scheme),
    db: Session = Depends(get_db)
):
    try:
        payload = jwt.decode(token, SECRET_KEY, algorithms=[ALGORITHM])
        username: str = payload.get("sub")
        if username is None:
            raise HTTPException(status_code=401)
    except JWTError:
        raise HTTPException(status_code=401)

    user = db.query(User).filter(User.username == username).first()
    if user is None:
        raise HTTPException(status_code=401)
    return user
```

### Protected `/me` endpoint

```python
@app.get("/me")
def read_me(current_user: User = Depends(get_current_user)):
    return {
        "id": current_user.id,
        "username": current_user.username
    }
```


## [[Authorization]]

For [[Authorization]] [[RBAC]] needs to be setup :
1. **Create the roles ([[Énumération|enum class]])** 
2. **Check in the different endpoints for the role using the [[Token|token]]**

## Implementing [[MFA]]

[[pyotp]] can be used to implement [[TOTP]]

## [[API]] key [[Authentication]]

Effective way to control access to an application by generating a unique key for each user or service that need access to the [[API]]

## Handling session [[Cookie|cookies]] and logout functionality

- **On Login :** create a [[Cookie|cookie]] for the session
- **On Logout :** delete the [[Cookie|cookie]]

---

# Advanced Features and Best Practices

## Implementing dependency injection

A dependency is a function annotated with `Depends` that is called and resolved before executing the endpoint

> Note : nested dependencies are possible

```python
@users_crud_router.get("/users")
def get_users(
    db: Session = Depends(get_db)
):
    """Reading all the users.
    """
    
    return db.query(User).all()
```

## Creating custom [[Middleware|middleware]] 

## Optimizing application performance

[[pyinstrument]] can be used to create a profiler for the application to spot code bottlenecks (usual solutions require asynchronous programming, scaling workers, caching)

## Implementing rate limiting

[[slowapi]] can be used to control the traffic flows. It can be done by restricting the number of requests in a predetermined period according to [[Adresse IP|IP Address]] (2 req/min). It can be applied to specific endpoints or to the whole app.

## Implementing background tasks

Tasks that need processing power but don't necessarily need to be completed by the same process can be enqueued in the `BackgroundTaasks` object.

---

# Working with [[WebSocket]]

```python
from fastapi import WebSocket

@app.websocket("/ws")
async def ws_endpoint(websocket: WebSocket):
	await websocket.accept()
	await websocket.send_text("Welcome to the chat room!")
	await websocket.close()
```

---

# [[Middleware]] and [[Webhook|Webhooks]] 

---

# Deploying and Managing [[FastAPI]] Applications