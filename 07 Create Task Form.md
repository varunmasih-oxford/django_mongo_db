# 07 Create Task Form

# Module Overview

In the previous lesson, you created reusable MongoDB helper functions for performing CRUD operations. The next step is to allow users to enter task information through a web form.

In this lesson, you will create a Django Form that validates user input before sending it to MongoDB. Although we are using MongoDB instead of Django Models, Django Forms still provide powerful validation and make handling HTML forms much easier.

By the end of this lesson, you will have a fully functional Task Form that can be used for creating and updating tasks.

---

# Learning Objectives

After completing this lesson, you will be able to:

- Understand Django Forms
- Create a custom Form
- Add different form fields
- Apply field validation
- Customize widgets
- Display forms in templates
- Validate user input

---

# Prerequisites

Before starting this lesson, you should have completed:

- ✅ 01 Install Python Packages
- ✅ 02 Create the Django Project
- ✅ 03 Create the tasks App
- ✅ 04 Configure Django Settings
- ✅ 05 Connect Django with MongoDB
- ✅ 06 MongoDB Helper

---

# Why Use Django Forms?

Instead of manually reading data from `request.POST`, Django Forms provide:

- Automatic validation
- Cleaner code
- Error handling
- HTML generation
- Security against invalid input

Without Django Forms

```python
title = request.POST.get("title")
description = request.POST.get("description")
completed = request.POST.get("completed")
```

With Django Forms

```python
form = TaskForm(request.POST)

if form.is_valid():
    data = form.cleaned_data
```

---

# Step 1: Open forms.py

Navigate to

```
tasks/

├── forms.py
```

---

# Step 2: Import Forms Library

```python
from django import forms
```

---

# Step 3: Create TaskForm Class

```python
class TaskForm(forms.Form):

    title = forms.CharField()

    description = forms.CharField()

    completed = forms.BooleanField(required=False)
```

Explanation

- **title** → Task title
- **description** → Task description
- **completed** → Checkbox (optional)

---

# Step 4: Add Maximum Length Validation

```python
class TaskForm(forms.Form):

    title = forms.CharField(
        max_length=100
    )

    description = forms.CharField(
        max_length=500
    )

    completed = forms.BooleanField(
        required=False
    )
```

---

# Step 5: Add Labels

```python
class TaskForm(forms.Form):

    title = forms.CharField(
        label="Task Title",
        max_length=100
    )

    description = forms.CharField(
        label="Description",
        max_length=500
    )

    completed = forms.BooleanField(
        label="Completed",
        required=False
    )
```

Labels improve the appearance of forms in templates.

---

# Step 6: Customize Widgets

```python
class TaskForm(forms.Form):

    title = forms.CharField(
        label="Task Title",
        max_length=100,
        widget=forms.TextInput(
            attrs={
                "class": "form-control",
                "placeholder": "Enter task title"
            }
        )
    )

    description = forms.CharField(
        label="Description",
        max_length=500,
        widget=forms.Textarea(
            attrs={
                "class": "form-control",
                "rows": 5,
                "placeholder": "Enter task description"
            }
        )
    )

    completed = forms.BooleanField(
        required=False,
        widget=forms.CheckboxInput(
            attrs={
                "class": "form-check-input"
            }
        )
    )
```

Widgets control how fields appear in HTML.

---

# Step 7: Complete forms.py

```python
from django import forms


class TaskForm(forms.Form):

    title = forms.CharField(
        label="Task Title",
        max_length=100,
        widget=forms.TextInput(
            attrs={
                "class": "form-control",
                "placeholder": "Enter task title"
            }
        )
    )

    description = forms.CharField(
        label="Description",
        max_length=500,
        widget=forms.Textarea(
            attrs={
                "class": "form-control",
                "rows": 5,
                "placeholder": "Enter task description"
            }
        )
    )

    completed = forms.BooleanField(
        required=False,
        widget=forms.CheckboxInput(
            attrs={
                "class": "form-check-input"
            }
        )
    )
```

---

# Step 8: Test the Form in Django Shell

Open the shell

```bash
python manage.py shell
```

Import the form

```python
from tasks.forms import TaskForm
```

Create form data

```python
form = TaskForm({
    "title": "Learn Django",
    "description": "Practice Forms",
    "completed": True
})
```

Validate

```python
form.is_valid()
```

Expected Output

```python
True
```

View cleaned data

```python
form.cleaned_data
```

Expected Output

```python
{
    "title": "Learn Django",
    "description": "Practice Forms",
    "completed": True
}
```

---

# Step 9: Test Invalid Data

```python
form = TaskForm({
    "title": "",
    "description": ""
})

form.is_valid()
```

Expected Output

```python
False
```

View Errors

```python
form.errors
```

Example Output

```python
{
    "title": [
        "This field is required."
    ],
    "description": [
        "This field is required."
    ]
}
```

---

# Understanding cleaned_data

When validation succeeds

```python
form.cleaned_data
```

Returns

```python
{
    "title": "...",
    "description": "...",
    "completed": False
}
```

Always use `cleaned_data` instead of `request.POST`.

---

# Form Workflow

```
User

│

▼

HTML Form

│

▼

TaskForm

│

▼

Validation

│

▼

cleaned_data

│

▼

MongoDB Helper

│

▼

MongoDB
```

---

# Project Structure

```
task_manager/

│

├── tasks/

│   ├── forms.py
│   ├── helper.py
│   ├── mongodb.py
│   ├── views.py
│   └── urls.py

│

├── manage.py
```

---

# Common Errors

## Error

```
This field is required.
```

### Reason

Required field left empty.

### Solution

Enter a value before submitting the form.

---

## Error

```
Ensure this value has at most 100 characters.
```

### Reason

Title exceeds maximum length.

### Solution

Reduce the number of characters.

---

## Error

```
AttributeError: module 'tasks.forms' has no attribute 'TaskForm'
```

### Reason

Incorrect class name or import.

### Solution

Verify the class name and import statement.

---

# Best Practices

- Keep validation inside forms.
- Use `cleaned_data` after validation.
- Add placeholders for better user experience.
- Apply CSS classes using widgets.
- Reuse the same form for both Create and Update pages.

---

# Summary

In this lesson, you learned how to:

- Create a custom Django Form
- Add text and checkbox fields
- Apply validation rules
- Customize widgets
- Validate user input
- Access cleaned data
- Prepare data for MongoDB insertion

Your application is now ready to collect task information safely before storing it in MongoDB.

---

# Next Lesson

**08 Create Task (Create View & Save to MongoDB)**

In the next lesson, you will connect the `TaskForm` with a Django View, create an HTML template, process form submissions, and save validated task data into MongoDB using the helper functions.
