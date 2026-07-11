## Module Overview

In this lesson, you will configure your Django project before connecting it to MongoDB. Proper configuration ensures that your project can use templates, static files, environment variables, and the custom `tasks` application.

---

# Learning Objectives

After completing this lesson, you will be able to:

- Understand the purpose of `settings.py`
- Register a Django application
- Configure the Templates directory
- Configure Static Files
- Configure Media Files
- Load Environment Variables using `python-dotenv`
- Store sensitive information securely
- Verify that the project runs successfully

---

# Prerequisites

Before starting this lesson, you should have completed:

- 01 Install Python Packages
- 02 Create the Django Project
- 03 Create the `tasks` App

---

# Project Structure

Your project should now look like this:

```text
task_manager/
│
├── manage.py
├── .env
├── task_manager/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   ├── asgi.py
│   └── wsgi.py
│
├── tasks/
│   ├── migrations/
│   ├── templates/
│   ├── static/
│   ├── views.py
│   ├── urls.py
│   └── apps.py
│
├── templates/
├── static/
└── media/
```

---

# Step 1: Open settings.py

Open the following file:

```
task_manager/settings.py
```

Most of the project configuration is done inside this file.

---

# Step 2: Register the Tasks App

Locate:

```python
INSTALLED_APPS = [
```

Add your application.

```python
INSTALLED_APPS = [
    "django.contrib.admin",
    "django.contrib.auth",
    "django.contrib.contenttypes",
    "django.contrib.sessions",
    "django.contrib.messages",
    "django.contrib.staticfiles",

    "tasks",
]
```

## Why?

Django only recognizes applications that are listed inside `INSTALLED_APPS`.

Without registering the app:

- URLs may not work
- Templates may not load
- Static files may not be found
- Views may not be discovered

---

# Step 3: Configure the Templates Folder

By default, Django looks for templates inside each application.

We also want a global `templates` folder.

Locate:

```python
TEMPLATES = [
```

Modify the `DIRS` option.

```python
from pathlib import Path

BASE_DIR = Path(__file__).resolve().parent.parent

TEMPLATES = [
    {
        "BACKEND": "django.template.backends.django.DjangoTemplates",

        "DIRS": [
            BASE_DIR / "templates",
        ],

        "APP_DIRS": True,

        "OPTIONS": {
            "context_processors": [
                "django.template.context_processors.request",
                "django.contrib.auth.context_processors.auth",
                "django.contrib.messages.context_processors.messages",
            ],
        },
    },
]
```

---

## Create the Templates Folder

Create a folder beside `manage.py`

```
task_manager/

templates/
```

Example:

```
templates/
│
├── base.html
├── login.html
├── register.html
└── dashboard.html
```

---

# Step 4: Configure Static Files

Static files include:

- CSS
- JavaScript
- Images
- Icons

Locate:

```python
STATIC_URL = 'static/'
```

Replace with:

```python
STATIC_URL = "static/"

STATICFILES_DIRS = [
    BASE_DIR / "static",
]
```

---

## Create the Static Folder

```
static/
│
├── css/
├── js/
└── images/
```

Example

```
static/

css/
    style.css

js/
    app.js

images/
    logo.png
```

---

# Step 5: Configure Media Files

Media files are uploaded by users.

Examples

- Profile pictures
- Documents
- Images

Add the following code below the static configuration.

```python
MEDIA_URL = "/media/"

MEDIA_ROOT = BASE_DIR / "media"
```

---

## Create the Media Folder

```
media/
```

Example

```
media/

profile1.png

resume.pdf
```

---

# Step 6: Install python-dotenv

Open Terminal

```bash
pip install python-dotenv
```

Verify Installation

```bash
pip show python-dotenv
```

---

# Step 7: Create the .env File

Create a file beside `manage.py`

```
.env
```

Example

```text
SECRET_KEY=django-secret-key-goes-here

DEBUG=True

MONGO_URI=mongodb://localhost:27017/

DATABASE_NAME=task_manager_db
```

Never upload this file to GitHub.

---

# Step 8: Load Environment Variables

At the top of `settings.py`

Add

```python
import os

from dotenv import load_dotenv
```

Load the environment variables.

```python
load_dotenv()
```

Your imports should look similar to:

```python
import os

from pathlib import Path

from dotenv import load_dotenv

load_dotenv()
```

---

# Step 9: Configure the Secret Key

Locate

```python
SECRET_KEY = "your-secret-key"
```

Replace with

```python
SECRET_KEY = os.getenv("SECRET_KEY")
```

Now Django will read the key from the `.env` file.

---

# Step 10: Configure Debug Mode

Replace

```python
DEBUG = True
```

with

```python
DEBUG = os.getenv("DEBUG") == "True"
```

This allows changing Debug mode without modifying your source code.

---

# Step 11: Configure Allowed Hosts

During development

```python
ALLOWED_HOSTS = []
```

Later in production

```python
ALLOWED_HOSTS = [
    "localhost",
    "127.0.0.1",
]
```

---

# Step 12: Verify BASE_DIR

Ensure

```python
from pathlib import Path

BASE_DIR = Path(__file__).resolve().parent.parent
```

Everything in the project uses this directory.

Example

```
BASE_DIR

│

├── templates
├── static
├── media
├── manage.py
```

---

# Step 13: Final Settings Example

```python
import os

from pathlib import Path

from dotenv import load_dotenv

load_dotenv()

BASE_DIR = Path(__file__).resolve().parent.parent

SECRET_KEY = os.getenv("SECRET_KEY")

DEBUG = os.getenv("DEBUG") == "True"

ALLOWED_HOSTS = []

INSTALLED_APPS = [

    "django.contrib.admin",
    "django.contrib.auth",
    "django.contrib.contenttypes",
    "django.contrib.sessions",
    "django.contrib.messages",
    "django.contrib.staticfiles",

    "tasks",
]

TEMPLATES = [
    {
        "BACKEND": "django.template.backends.django.DjangoTemplates",

        "DIRS": [
            BASE_DIR / "templates",
        ],

        "APP_DIRS": True,

        "OPTIONS": {
            "context_processors": [
                "django.template.context_processors.request",
                "django.contrib.auth.context_processors.auth",
                "django.contrib.messages.context_processors.messages",
            ],
        },
    },
]

STATIC_URL = "static/"

STATICFILES_DIRS = [
    BASE_DIR / "static",
]

MEDIA_URL = "/media/"

MEDIA_ROOT = BASE_DIR / "media"
```

---

# Step 14: Run the Server

Open Terminal

```bash
python manage.py runserver
```

Expected Output

```
Watching for file changes with StatReloader

Starting development server at

http://127.0.0.1:8000/
```

Open the browser

```
http://127.0.0.1:8000/
```

If you see the Django welcome page, your configuration is correct.

---

# Common Errors

## Error

```
ModuleNotFoundError: No module named 'dotenv'
```

Solution

```bash
pip install python-dotenv
```

---

## Error

```
TemplateDoesNotExist
```

Solution

Check

```python
DIRS = [
    BASE_DIR / "templates",
]
```

---

## Error

```
Static files not loading
```

Verify

```python
STATICFILES_DIRS = [
    BASE_DIR / "static",
]
```

---

## Error

```
KeyError: SECRET_KEY
```

Ensure

- `.env` exists
- `load_dotenv()` is called
- `SECRET_KEY` is defined in `.env`

---
