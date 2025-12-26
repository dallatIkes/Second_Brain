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

## [[SQLAlchemy]]

![[SQLAlchemy]]

## [[MongoDB]]

![[MongoDB]]

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

