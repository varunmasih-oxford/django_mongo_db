## Module Overview

In this lesson, you will connect your Django application to MongoDB using **PyMongo**. Unlike Django's default relational databases (SQLite, MySQL, PostgreSQL), MongoDB is a NoSQL database that stores data as **documents** inside **collections**.

By the end of this lesson, your Django project will be able to establish a successful connection with MongoDB.

---

# Learning Objectives

After completing this lesson, you will be able to:

- Understand what PyMongo is
- Install the required packages
- Create a MongoDB database
- Configure MongoDB connection settings
- Connect Django with MongoDB
- Test the database connection
- Handle connection errors gracefully

---

# Prerequisites

Before starting this lesson, you should have completed:

- ✅ 01 Install Python Packages
- ✅ 02 Create the Django Project
- ✅ 03 Create the `tasks` App
- ✅ 04 Configure Django Settings

---

# What is MongoDB?

MongoDB is a **NoSQL database** that stores data in **documents** instead of tables.

### SQL Database

```
Database
    │
    ├── Table
    │      ├── Row
    │      ├── Row
    │      └── Row
```

---

### MongoDB Database

```
Database
    │
    ├── Collection
           ├── Document
           ├── Document
           └── Document
```

---

## Example SQL Record

| id | name | age |
|----|------|-----|
| 1 | John | 25 |

---

## Example MongoDB Document

```json
{
    "_id": ObjectId("665df4f5b1c45d"),
    "name": "John",
    "age": 25
}
```

---

# Why Use PyMongo?

PyMongo is the official MongoDB driver for Python.

It allows Python applications to:

- Connect to MongoDB
- Create databases
- Create collections
- Insert documents
- Read documents
- Update documents
- Delete documents

---

# Step 1: Install Required Packages

Open the terminal.

Install PyMongo.

```bash
pip install pymongo
```

Install BSON support.

```bash
pip install bson
```

Install DNS support.

```bash
pip install dnspython
```

Verify installation.

```bash
pip show pymongo
```

Example Output

```
Name: pymongo
Version: 4.x.x
```

---

# Step 2: Start MongoDB

If MongoDB is installed locally, start the MongoDB server.

Example:

```bash
mongod
```

If you are using **MongoDB Atlas**, ensure you have:

- Created a cluster
- Created a database user
- Whitelisted your IP address
- Copied the connection string

---

# Step 3: Create the Database

MongoDB creates databases automatically when data is inserted.

We will use:

```
Database Name

task_manager_db
```

---

# Step 4: Configure the .env File

Open the `.env` file.

Example

```text
SECRET_KEY=your-secret-key

DEBUG=True

MONGO_URI=mongodb://localhost:27017/

DATABASE_NAME=task_manager_db
```

For MongoDB Atlas:

```text
MONGO_URI=mongodb+srv://username:password@cluster.mongodb.net/

DATABASE_NAME=task_manager_db
```

> **Note:** Never upload your `.env` file to GitHub.

---

# Step 5: Create mongodb.py

Inside the **tasks** application, create a new file.

```
tasks/

mongodb.py
```

Project structure

```
tasks/

├── views.py
├── urls.py
├── mongodb.py
├── forms.py
└── apps.py
```

---

# Step 6: Import Required Libraries

Inside `mongodb.py`

```python
import os

from dotenv import load_dotenv

from pymongo import MongoClient
```

---

# Step 7: Load Environment Variables

```python
load_dotenv()

MONGO_URI = os.getenv("MONGO_URI")

DATABASE_NAME = os.getenv("DATABASE_NAME")
```

---

# Step 8: Create MongoDB Client

```python
client = MongoClient(MONGO_URI)
```

The client acts as a bridge between Django and MongoDB.

```
Django

↓

MongoClient

↓

MongoDB Server
```

---

# Step 9: Connect to the Database

```python
db = client[DATABASE_NAME]
```

Now the variable `db` represents your MongoDB database.

---

# Step 10: Access Collections

Create collection variables.

```python
users_collection = db["users"]

tasks_collection = db["tasks"]
```

Whenever you need to store or retrieve data, you will use these collection objects.

---

# Complete mongodb.py

```python
import os

from dotenv import load_dotenv

from pymongo import MongoClient

load_dotenv()

MONGO_URI = os.getenv("MONGO_URI")

DATABASE_NAME = os.getenv("DATABASE_NAME")

client = MongoClient(MONGO_URI)

db = client[DATABASE_NAME]

users_collection = db["users"]

tasks_collection = db["tasks"]
```

---

# Step 11: Test the Connection

Create a temporary file.

```
test_connection.py
```

```python
from tasks.mongodb import client

try:

    client.admin.command("ping")

    print("MongoDB Connected Successfully!")

except Exception as e:

    print(e)
```

Run

```bash
python test_connection.py
```

Expected Output

```
MongoDB Connected Successfully!
```

---

# Step 12: Verify Using MongoDB Compass

Open MongoDB Compass.

Connect using your connection string.

You should see

```
task_manager_db
```

Initially the database may not appear until the first document is inserted.

---

# Step 13: Test by Creating a Collection

Open Django Shell.

```bash
python manage.py shell
```

Run

```python
from tasks.mongodb import db

db.create_collection("sample")
```

If successful, MongoDB will create a collection named **sample**.

---

# Step 14: Verify in MongoDB Compass

Refresh Compass.

You should now see

```
task_manager_db

│

├── sample
```

Congratulations!

Your Django application is now communicating with MongoDB.

---

# Common Errors

## Error

```
ServerSelectionTimeoutError
```

### Solution

- MongoDB server is not running.
- Incorrect connection string.
- Atlas IP not whitelisted.

---

## Error

```
Authentication failed
```

### Solution

- Check username.
- Check password.
- Verify database user permissions.

---

## Error

```
ModuleNotFoundError: pymongo
```

### Solution

```bash
pip install pymongo
```

---

## Error

```
MONGO_URI is None
```

### Solution

- Verify `.env` file exists.
- Check variable names.
- Restart the Django server after modifying `.env`.

---

