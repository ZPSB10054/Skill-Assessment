# 🚀CRUD Operations using FastAPI and MongoDB

## 📌INTRODUCTION

Modern web applications require fast and efficient backend APIs for creating, reading, updating, and deleting data — commonly referred to as **CRUD operations**. In this presentation, we'll explore how to build a high-performance API using **FastAPI**, a modern Python web framework, and **MongoDB**, a NoSQL database perfect for scalable applications. 

## 🛠️ Tech Stack Overview

- **FastAPI**: A modern, asynchronous web framework for Python. FastAPI is known for automatic OpenAPI docs, fast performance, and async support.
- **MongoDB**: A document-oriented NoSQL database that stores data in JSON-like format.

### 📖 What is FastAPI?

- FastAPI is a modern, high-performance, web framework for building APIs with Python 3.7+ based on standard Python type hints.
- It is one of the fastest Python frameworks available today, rivaling Node.js and Go in performance thanks to its use of asynchronous programming with async/await.

#### 🌟 Key Features of FastAPI
       
- 🚀 High Performance	     
- 📚 Automatic Docs	         
- 🧠 Type Hints Support	     
- 🔐 Dependency Injection	 
- ⏱️ Async Support	         
- ✅ Data Validation	 

### 🍃 MongoDB: The Powerhouse NoSQL Database for Modern Applications

MongoDB is a **document-oriented NoSQL database** that stores data in **BSON**(Binary JSON) format. It’s designed to handle **unstructured or semi-structured data**, offering flexible schema definitions and scalability across distributed systems.

#### 🌟 Key Features of MongoDB

- 🍃 Document Model
- 📈 Scalable	
- 🚀 High Performance	
- 🔍 Rich Queries	
- 🧠 Schema Flexibility	
- 🔒 Security	
- 🔄 Replication


## 🧱Why FastAPI + MongoDB

- FastAPI is asynchronous, type-hinted, and incredibly fast.
- MongoDB offers a flexible schema, ideal for dynamic data.
- Together, they form a lightweight, highly scalable stack perfect for modern apps and microservices.

## 🗂️ Project Structure
Here's a clean, modular structure for your application:

```graphql

fastapi-mongo-crud/
│
├── main.py             # FastAPI app and routes
├── app                 # 
├──── data              # Data
├──── models            # Data models (Pydantic)
└──── utils             # Helpers, Decorators and Loggers

```

## Setting up MongoDB Connection

```python
from pymongo import MongoClient

myclient = MongoClient("mongodb://localhost:27017/")
mydb = myclient["USER-DATABASE"]
mycol = mydb["USER-DATA"]
```

💡 Tip: Use environment variables or config files in production for connection strings.

## 🧪 Testing the API

FastAPI provides Swagger UI at `http://localhost:8000/docs` for testing:

- POST /users → Add user
- GET /users → List all users
- GET /users/{id} → Fetch user by ID
- PUT /users/{id} → Update user
- DELETE /users/{id} → Delete user

## ✅ Benefits of This Stack

- ⚡ High Performance: FastAPI + async MongoDB (Motor) ensures non-blocking I/O.
- 🔄 Real-time Read/Write: MongoDB is excellent for dynamic schemas.
- 🧩 Modular Code: Clear separation of concerns.

## 📌 Conclusion

With just a few lines of code, we created a full-fledged CRUD API using **FastAPI** and **MongoDB**. This combination is ideal for startups, prototypes, or even scalable microservices thanks to its simplicity, performance, and flexibility.

## 🧠 FastAPI + MongoDB Interview Questions and Answers

### ❓ Question 1:
What is FastAPI, and why is it popular for building APIs?

#### ✅ Answer:
FastAPI is a modern Python web framework used to build APIs quickly with automatic validation, asynchronous support, and interactive API documentation. It’s fast (built on Starlette and Pydantic) and developer-friendly.

---

### ❓ Question 2:
How do you connect FastAPI to MongoDB using Motor?

#### ✅ Answer:
Use the `motor` async MongoDB driver like this:

```python
from motor.motor_asyncio import AsyncIOMotorClient

client = AsyncIOMotorClient("mongodb://localhost:27017")
db = client.mydatabase
```
Inject db into FastAPI endpoints or dependencies.

---

### ❓ Question 3:
Explain how FastAPI handles request validation.

#### ✅ Answer:
FastAPI uses Pydantic models to validate and parse incoming request bodies. It checks data types and required fields before the route logic runs.

---

### ❓ Question 4:
What is a Pydantic model and how do you use it with MongoDB documents?

#### ✅ Answer:
A Pydantic model defines the structure of request or response data using type annotations. With MongoDB, you often convert _id (ObjectId) to a string before returning it via a Pydantic model.

---

### ❓ Question 5:
How do you perform asynchronous CRUD operations in FastAPI with MongoDB?

#### ✅ Answer:
Use Motor’s async methods inside FastAPI's async def routes:

```python
await db.users.insert_one(user.dict())
```

Other operations include find_one, update_one, delete_one, etc.

---

### ❓ Question 6:
How do you serialize MongoDB’s ObjectId in a FastAPI response?

#### ✅ Answer:
Convert it using str() or a helper function:

```python
def serialize_user(user):
    return {
        "id": str(user["_id"]),
        "name": user["name"]
    }
```

---

### ❓ Question 7:
How does FastAPI automatically generate API docs?

#### ✅ Answer:
FastAPI uses the OpenAPI standard to generate interactive Swagger UI at /docs and ReDoc at /redoc automatically, based on your routes and Pydantic models.

---

### ❓ Question 8:
What are the differences between insert_one() and insert_many() in Motor?

#### ✅ Answer:
insert_one() inserts a single document and returns its inserted ID.

insert_many() inserts multiple documents and returns a list of inserted IDs.
Both are asynchronous and return InsertOneResult or InsertManyResult.

---

### ❓ Question 9:
How can you update only certain fields in a MongoDB document using FastAPI?

#### ✅ Answer:
Use the $set operator with update_one():

```python
await db.users.update_one(
    {"_id": ObjectId(id)},
    {"$set": {"name": "Updated"}}
)
```

---

### ❓ Question 10:
How do you define a POST route in FastAPI that adds a document to MongoDB?

#### ✅ Answer:
```python
@app.post("/users")
async def add_user(user: User):
    result = await db.users.insert_one(user.dict())
    return {"id": str(result.inserted_id)}
```

---

### ❓ Question 11:
How would you handle 404 Not Found in FastAPI when a document isn’t found?

#### ✅ Answer:
Raise an HTTPException:

```python
if not user:
    raise HTTPException(status_code=404, detail="User not found")
```

---

### ❓ Input 12:
What is the benefit of using async def in FastAPI routes when working with MongoDB?

#### ✅ Answer:
Motor’s operations are non-blocking. Using async def allows FastAPI to process many concurrent requests efficiently without waiting for I/O.

---

### ❓ Question 13:
What’s a good use case for embedding documents in MongoDB in a FastAPI project?

#### ✅ Answer:
Embedding is useful when related data is frequently read together—for example, storing an array of comments inside a blog post document to avoid multiple queries.

---

### ❓ Question 14:
How do you test FastAPI endpoints that use MongoDB?

#### ✅ Answer:
Use TestClient from fastapi.testclient to test routes. Use dependency overrides to inject a mock DB like mongomock or a test instance of MongoDB.

---

### ❓ Question 15:
Explain how FastAPI and MongoDB together support flexible, scalable development.

#### ✅ Answer:
FastAPI allows rapid, async API development with automatic validation. MongoDB provides flexible schemas and horizontal scaling. Together, they allow teams to build scalable, data-rich apps quickly.

