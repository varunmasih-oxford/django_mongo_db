# Step 3: Create the `tasks` App

# Why Are We Creating an App?

Django follows a **project-app architecture**.

- A **Project** is the complete website.
- An **App** is a reusable module that performs a specific job.

For example:

```
Project
│
├── Blog App
├── Shop App
├── Payment App
├── Chat App
└── Tasks App
```

Our project only needs one app:

```
Task Manager
│
└── tasks
```

Everything related to task management will be stored inside this app.

---

# Current Project Structure

After completing Step 2, your project should look like this:

```
task_manager/
│
├── task_manager/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   ├── asgi.py
│   └── wsgi.py
│
├── manage.py
├── requirements.txt
└── venv/
```

---

# Create the App

Open your terminal inside the project folder.

Run:

```bash
python manage.py startapp tasks
```

---

# Project Structure After Creating the App

```
task_manager/
│
├── task_manager/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   ├── asgi.py
│   └── wsgi.py
│
├── tasks/
│   ├── migrations/
│   │   └── __init__.py
│   │
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── models.py
│   ├── tests.py
│   └── views.py
│
├── manage.py
├── requirements.txt
└── venv/
```

---

# Understanding Each File

---

## 1. `tasks/__init__.py`

**Location**

```
tasks/__init__.py
```

### Purpose

Marks the `tasks` folder as a Python package.

Current file:

```python
# Empty file
```

No changes are required.

---

## 2. `tasks/admin.py`

**Location**

```
tasks/admin.py
```

### Purpose

Registers Django models in the Django Admin Panel.

Current code:

```python
from django.contrib import admin
```

### Will We Use It?

No.

Since this project uses **MongoDB + PyMongo**, we won't register any Django models.

Leave it unchanged.

---

## 3. `tasks/apps.py`

**Location**

```
tasks/apps.py
```

Current code:

```python
from django.apps import AppConfig


class TasksConfig(AppConfig):
    default_auto_field = "django.db.models.BigAutoField"
    name = "tasks"
```

### Explanation

```python
class TasksConfig(AppConfig):
```

Registers the application with Django.

---

```python
default_auto_field = "django.db.models.BigAutoField"
```

Sets the default primary key type for Django models.

Although we won't use Django models, this setting can remain as generated.

---

```python
name = "tasks"
```

The app name that you'll later add to `INSTALLED_APPS`.

---

## 4. `tasks/models.py`

**Location**

```
tasks/models.py
```

Current code:

```python
from django.db import models
```

### Purpose

Normally, Django models are defined here.

Example:

```python
class Task(models.Model):
    title = models.CharField(max_length=100)
```

### Will We Use It?

No.

We'll store data directly in MongoDB using **PyMongo**, so we won't define Django ORM models.

Leave this file unchanged.

---

## 5. `tasks/tests.py`

**Location**

```
tasks/tests.py
```

Current code:

```python
from django.test import TestCase
```

### Purpose

Contains automated tests.

We'll skip writing tests during this tutorial.

---

## 6. `tasks/views.py`

**Location**

```
tasks/views.py
```

Current code:

```python
from django.shortcuts import render

# Create your views here.
```

### Purpose

This file will contain all of our application logic, including:

- Register user
- Login
- Logout
- Dashboard
- Create task
- View tasks
- Update task
- Delete task
- Search
- Filter
- Statistics

Leave it unchanged for now.

---

# Create Additional Files

To keep the project organized, create the following files now.

---

## File: `tasks/forms.py`

```python
# Forms will be created in later steps.
```

---

## File: `tasks/urls.py`

```python
from django.urls import path

urlpatterns = [
]
```

---

## File: `tasks/mongodb.py`

```python
# MongoDB connection code will be added in Step 5.
```

---

## File: `tasks/utils.py`

```python
# Utility functions will be added later.
```

---

# Create the Templates Folder

Create the following folder structure:

```
tasks/
│
└── templates/
    │
    └── tasks/
```

The inner `tasks` folder helps Django distinguish templates from different apps.

---

# Create the Static Folder

Create this structure:

```
tasks/
│
└── static/
    │
    └── tasks/
        │
        ├── css/
        ├── js/
        └── images/
```

We'll store CSS, JavaScript, and images here.

---

# Updated Project Structure

```
task_manager/
│
├── task_manager/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   ├── asgi.py
│   └── wsgi.py
│
├── tasks/
│   ├── migrations/
│   │   └── __init__.py
│   │
│   ├── static/
│   │   └── tasks/
│   │       ├── css/
│   │       ├── js/
│   │       └── images/
│   │
│   ├── templates/
│   │   └── tasks/
│   │
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── forms.py
│   ├── models.py
│   ├── mongodb.py
│   ├── tests.py
│   ├── urls.py
│   ├── utils.py
│   └── views.py
│
├── manage.py
├── requirements.txt
└── venv/
```

---

# Files Created in This Step

| File | Purpose |
|------|---------|
| `tasks/forms.py` | Django forms |
| `tasks/urls.py` | Application routes |
| `tasks/mongodb.py` | MongoDB connection |
| `tasks/utils.py` | Helper functions |
| `tasks/templates/tasks/` | HTML templates |
| `tasks/static/tasks/css/` | CSS files |
| `tasks/static/tasks/js/` | JavaScript files |
| `tasks/static/tasks/images/` | Images |

---

# Step 3 Checklist

- [ ] Run `python manage.py startapp tasks`
- [ ] Understand the generated files
- [ ] Create `forms.py`
- [ ] Create `urls.py`
- [ ] Create `mongodb.py`
- [ ] Create `utils.py`
- [ ] Create the `templates/tasks` folder
- [ ] Create the `static/tasks/css` folder
- [ ] Create the `static/tasks/js` folder
- [ ] Create the `static/tasks/images` folder
