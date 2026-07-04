# Step 1: Install Python Packages

## Why are we doing this?

These packages provide the foundation for the project:

| Package | Purpose |
|----------|---------|
| Django | Web framework |
| PyMongo | Connect Django with MongoDB |
| python-dotenv | Load environment variables |
| dnspython | Required for MongoDB Atlas connections |
| bcrypt | Secure password hashing |
| Pillow | Image processing (optional for future features) |

---

# Create a Virtual Environment

## Windows

```bash
python -m venv venv
```

Activate it:

```bash
venv\Scripts\activate
```

---

## macOS/Linux

```bash
python3 -m venv venv
```

Activate it:

```bash
source venv/bin/activate
```

---

# Install Required Packages

```bash
pip install django pymongo python-dotenv dnspython bcrypt Pillow
```

---

# Verify Installation

```bash
pip list
```

Expected packages:

```
Django
pymongo
python-dotenv
dnspython
bcrypt
Pillow
```

---

# Create requirements.txt

Generate automatically:

```bash
pip freeze > requirements.txt
```

---

# File Name

```
requirements.txt
```

Location:

```
task_manager/
│
└── requirements.txt
```

---

# requirements.txt

```txt
Django>=5.2
pymongo>=4.13
python-dotenv>=1.1
dnspython>=2.8
bcrypt>=4.3
Pillow>=11.0
```

---

# Package Explanation

## Django

```txt
Django>=5.2
```

Provides:

- URL Routing
- Views
- Templates
- Authentication
- Forms
- Sessions

---

## PyMongo

```txt
pymongo>=4.13
```

Official MongoDB driver.

Used for:

- Insert documents
- Read documents
- Update documents
- Delete documents
- Aggregate data

---

## python-dotenv

```txt
python-dotenv>=1.1
```

Loads environment variables from a `.env` file.

Example:

```
SECRET_KEY=your_secret_key
MONGO_URI=mongodb://localhost:27017
DATABASE_NAME=task_manager
```

---

## dnspython

```txt
dnspython>=2.8
```

Required for MongoDB Atlas (`mongodb+srv://...`) connections.

---

## bcrypt

```txt
bcrypt>=4.3
```

Used for secure password hashing.

Example:

```python
import bcrypt

password = "admin123"

hashed = bcrypt.hashpw(password.encode(), bcrypt.gensalt())
```

---

## Pillow

```txt
Pillow>=11.0
```

Supports image uploads if you later add profile pictures or task attachments.

---

# Project Structure After Step 1

```
task_manager/
│
├── venv/
├── requirements.txt
```

---

# Step 1 Checklist

- [ ] Install Python
- [ ] Create virtual environment
- [ ] Activate virtual environment
- [ ] Install required packages
- [ ] Verify installation
- [ ] Create `requirements.txt`
