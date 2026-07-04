# Step 2: Create the Django Project

# Why are we doing this?

A Django project contains the global configuration for your application, including:

- Project settings
- URL routing
- WSGI/ASGI configuration
- Static files configuration
- Installed apps
- Security settings

Think of the **project** as the entire website, while **apps** are individual modules (such as the `tasks` app we'll create later).

---

# Create the Django Project

Open your terminal inside your project folder.

Run:

```bash
django-admin startproject task_manager .
```

> **Note:** The `.` at the end tells Django to create the project in the current directory instead of creating an extra nested folder.

---

# Verify the Project

Run:

```bash
python manage.py runserver
```

or on Linux/macOS:

```bash
python3 manage.py runserver
```

You should see:

```
Starting development server at http://127.0.0.1:8000/
```

Open your browser and visit:

```
http://127.0.0.1:8000/
```

You should see the default Django welcome page.

---

# Project Structure

```
task_manager/
│
├── venv/
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
```

---

# File Explanation

---

## manage.py

Location

```
task_manager/manage.py
```

Purpose

- Runs the development server
- Creates apps
- Applies migrations
- Opens the Django shell
- Executes management commands

Common commands:

```bash
python manage.py runserver
python manage.py startapp tasks
python manage.py migrate
python manage.py createsuperuser
```

---

## task_manager/

This folder contains your project's configuration.

```
task_manager/
```

Inside it are several important files.

---

## __init__.py

```
task_manager/__init__.py
```

Purpose:

Marks the folder as a Python package.

Current contents:

```python
# Empty file
```

Do not modify it.

---

## settings.py

```
task_manager/settings.py
```

Purpose:

Main configuration file for the project.

It controls:

- Installed apps
- Database configuration
- Templates
- Static files
- Secret key
- Middleware
- Time zone
- Internationalization

We will configure this file in **Step 4**.

---

## urls.py

```
task_manager/urls.py
```

Purpose:

Acts as the main URL router.

Example:

```
/login
/register
/dashboard
/tasks
```

Every request first reaches this file.

We will update it later.

---

## wsgi.py

```
task_manager/wsgi.py
```

Purpose:

Used when deploying Django on production servers such as:

- Apache
- Gunicorn
- uWSGI

No changes are needed for development.

---

## asgi.py

```
task_manager/asgi.py
```

Purpose:

Supports asynchronous applications.

Useful for:

- WebSockets
- Real-time notifications
- Async views

We won't modify it in this project.

---

# Complete Code

Since Django generates these files automatically, you do **not** need to write them manually.

The generated files are ready to use.

---

# Test the Project

Run:

```bash
python manage.py runserver
```

Visit:

```
http://127.0.0.1:8000/
```

Expected page:

```
The install worked successfully!
Congratulations!
```

---

# Common Django Commands

### Run Development Server

```bash
python manage.py runserver
```

---

### Run on Another Port

```bash
python manage.py runserver 8080
```

---

### Check for Errors

```bash
python manage.py check
```

---

### Show Django Version

```bash
python -m django --version
```

---

# Project Structure After Step 2

```
task_manager/
│
├── venv/
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
```

---

# Step 2 Checklist

- [ ] Create the Django project
- [ ] Verify the project structure
- [ ] Run the development server
- [ ] Open `http://127.0.0.1:8000/`
- [ ] Confirm the Django welcome page appears

