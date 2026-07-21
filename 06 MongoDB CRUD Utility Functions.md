The next logical lesson after **05 Connect MongoDB** is:

# **06 MongoDB Helper (CRUD Utility Functions)**

This lesson creates reusable helper functions so you don't have to write PyMongo code repeatedly in every Django view. Instead of calling `insert_one()`, `find()`, `update_one()` everywhere, you'll call simple Python functions like `create_task()`, `get_all_tasks()`, etc.

It prepares the project for building the Task Manager in the next modules.

---

````md
# 06 MongoDB Helper

# Module Overview

In the previous lesson, you connected your Django application to MongoDB using PyMongo.

Writing database queries directly inside every Django view quickly becomes difficult to maintain. A better approach is to keep all MongoDB operations in one separate file.

In this lesson, you will create a reusable helper module that performs all CRUD (Create, Read, Update, Delete) operations for the Task Manager.

By the end of this lesson, your Django application will have reusable database functions that can be called from any view.

---

# Learning Objectives

After completing this lesson, you will be able to:

- Understand why helper functions are useful
- Separate database logic from Django views
- Create reusable CRUD functions
- Insert documents into MongoDB
- Retrieve documents
- Update documents
- Delete documents
- Find a document using its ObjectId

---

# Prerequisites

Before starting this lesson, you should have completed:

- ✅ 01 Install Python Packages
- ✅ 02 Create the Django Project
- ✅ 03 Create the tasks App
- ✅ 04 Configure Django Settings
- ✅ 05 Connect Django with MongoDB

---

# Why Use a Helper File?

Without a helper file, every Django view would contain MongoDB code.

Example

```python
tasks_collection.insert_one({...})

tasks_collection.find()

tasks_collection.update_one(...)

tasks_collection.delete_one(...)
```

This results in duplicated code.

Instead, we create one helper file.

```
View

↓

Helper Functions

↓

MongoDB
```

Benefits

- Cleaner views
- Reusable code
- Easier debugging
- Better project structure
- Easier future maintenance

---

# Step 1: Create helper.py

Inside the **tasks** application create a new file.

```
tasks/

├── helper.py
├── mongodb.py
├── views.py
├── urls.py
└── forms.py
```

---

# Step 2: Import Required Modules

Open **helper.py**

```python
from bson import ObjectId

from .mongodb import tasks_collection
```

---

# Step 3: Create Function to Insert a Task

```python
def create_task(data):
    return tasks_collection.insert_one(data)
```

Example

```python
task = {
    "title": "Learn Django",
    "description": "Study CRUD",
    "completed": False
}

create_task(task)
```

---

# Step 4: Create Function to Get All Tasks

```python
def get_all_tasks():
    return list(tasks_collection.find())
```

Example

```python
tasks = get_all_tasks()

for task in tasks:
    print(task)
```

---

# Step 5: Create Function to Get One Task

```python
def get_task(task_id):
    return tasks_collection.find_one({
        "_id": ObjectId(task_id)
    })
```

Example

```python
task = get_task("665df4f5b1c45d")
```

---

# Step 6: Create Function to Update a Task

```python
def update_task(task_id, data):
    return tasks_collection.update_one(
        {
            "_id": ObjectId(task_id)
        },
        {
            "$set": data
        }
    )
```

Example

```python
update_task(
    task_id,
    {
        "title": "Updated Title"
    }
)
```

---

# Step 7: Create Function to Delete a Task

```python
def delete_task(task_id):
    return tasks_collection.delete_one(
        {
            "_id": ObjectId(task_id)
        }
    )
```

---

# Step 8: Complete helper.py

```python
from bson import ObjectId

from .mongodb import tasks_collection


def create_task(data):
    return tasks_collection.insert_one(data)


def get_all_tasks():
    return list(tasks_collection.find())


def get_task(task_id):
    return tasks_collection.find_one(
        {
            "_id": ObjectId(task_id)
        }
    )


def update_task(task_id, data):
    return tasks_collection.update_one(
        {
            "_id": ObjectId(task_id)
        },
        {
            "$set": data
        }
    )


def delete_task(task_id):
    return tasks_collection.delete_one(
        {
            "_id": ObjectId(task_id)
        }
    )
```

---

# Step 9: Test Insert Operation

Open Django shell.

```bash
python manage.py shell
```

Run

```python
from tasks.helper import create_task

task = {
    "title": "Complete Django Project",
    "description": "Practice CRUD operations",
    "completed": False
}

result = create_task(task)

print(result.inserted_id)
```

Expected Output

```
665df4f5b1c45d......
```

---

# Step 10: Test Read Operation

```python
from tasks.helper import get_all_tasks

tasks = get_all_tasks()

for task in tasks:
    print(task)
```

Expected Output

```python
{
    "_id": ObjectId(...),
    "title": "Complete Django Project",
    "description": "Practice CRUD operations",
    "completed": False
}
```

---

# Step 11: Test Update Operation

```python
from tasks.helper import update_task

update_task(
    "YOUR_OBJECT_ID",
    {
        "completed": True
    }
)
```

---

# Step 12: Test Delete Operation

```python
from tasks.helper import delete_task

delete_task("YOUR_OBJECT_ID")
```

---

# Project Structure

```
task_manager/

│

├── tasks/

│   ├── helper.py
│   ├── mongodb.py
│   ├── views.py
│   ├── urls.py
│   └── forms.py

│

├── manage.py
```

---

# Flow Diagram

```
Django View

      │

      ▼

helper.py

      │

      ▼

mongodb.py

      │

      ▼

MongoDB Database
```

---

# Common Errors

## Error

```
InvalidId
```

### Reason

ObjectId is invalid.

### Solution

Pass a valid MongoDB ObjectId.

---

## Error

```
TypeError
```

### Reason

Task data is not a dictionary.

### Solution

Pass data in dictionary format.

Example

```python
{
    "title": "Task",
    "completed": False
}
```

---

## Error

```
CollectionInvalid
```

### Reason

Collection already exists.

### Solution

Ignore the error or check before creating the collection.

---

# Summary

In this lesson, you learned how to:

- Create reusable MongoDB helper functions
- Insert documents into MongoDB
- Retrieve documents
- Update existing documents
- Delete documents
- Organize database code separately from Django views

Your Django application now has a clean database layer that can be reused throughout the project.

---

# Next Lesson

**07 Create Task Form**

In the next lesson, you will create Django forms that allow users to submit task information from a web page and save it into MongoDB.
````
