# BidBurst

**BidBurst** is an online auction platform built with Django. It is designed to let users list items for auction, place bids, and manage listings through a simple, secure web application.

---

## Table of Contents

- [About the Project](#about-the-project)
- [Tech Stack](#tech-stack)
- [Prerequisites](#prerequisites)
- [Setup & Installation](#setup--installation)
- [Project Structure](#project-structure)
- [Configuration](#configuration)
- [Running the Application](#running-the-application)
- [Testing](#testing)
- [Contributing](#contributing)
- [License](#license)

---

## About the Project

BidBurst provides a full-featured auction experience:

- **User accounts** — Registration and authentication (Django built-in)
- **Auction listings** — Create and manage items for auction
- **Bidding** — Place and track bids on active auctions
- **Admin** — Django admin for managing users, listings, and bids
- **Database** — SQLite by default for development; easily switched to PostgreSQL for production

The project uses Django’s **MVT (Model–View–Template)** architecture and is structured for clarity and future extension (e.g. REST API, real-time updates, background tasks).

---

## Tech Stack

| Layer        | Technology | Purpose |
|-------------|------------|--------|
| **Language** | Python 3.10+ | Runtime and application logic |
| **Framework** | Django 5.2 | Web framework, ORM, auth, admin |
| **Database** | SQLite (default) | Development and lightweight deployment |
| **Templates** | Django templates | Server-rendered HTML |
| **Static** | Django staticfiles | CSS, JavaScript, images |

**Why Django?**

- Built-in admin, auth, and ORM speed up development.
- Strong security defaults (CSRF, XSS, SQL injection protection).
- Clear project/app structure and large ecosystem.

**Optional / future:** PostgreSQL, Redis, Celery, Django REST Framework, and Docker can be added as the project grows. The current codebase runs with Django and SQLite only.

---

## Prerequisites

Before setting up BidBurst, ensure you have:

- **Python** 3.10 or higher  
  Check: `python3 --version`
- **pip** (Python package manager)  
  Usually included with Python
- **Git** (for cloning the repository)

No database or Redis setup is required for the default SQLite configuration.

---

## Setup & Installation

Follow these steps to get BidBurst running locally.

### 1. Clone the repository

```bash
git clone https://github.com/yourusername/BidBurst.git
cd BidBurst
```

Replace `yourusername` with your GitHub username or your fork’s URL.

### 2. Create a virtual environment

Using the built-in `venv` module:

```bash
python3 -m venv venv
```

Activate it:

- **macOS / Linux:**  
  `source venv/bin/activate`
- **Windows (Command Prompt):**  
  `venv\Scripts\activate.bat`
- **Windows (PowerShell):**  
  `venv\Scripts\Activate.ps1`

Your prompt should show `(venv)` when the environment is active.

### 3. Install dependencies

From the project root (with `venv` activated):

```bash
pip install -r requirements.txt
```

This installs Django and any other listed packages.

### 4. Run database migrations

Django uses migrations to create and update database tables:

```bash
python manage.py migrate
```

With the default settings, this creates a SQLite database at `db.sqlite3` in the project root.

### 5. Create an admin user (optional)

To access the Django admin site:

```bash
python manage.py createsuperuser
```

Follow the prompts to set an email/username and password.

### 6. Run the development server

```bash
python manage.py runserver
```

Then open **http://127.0.0.1:8000/** in your browser.

- **Admin:** http://127.0.0.1:8000/admin/ (after creating a superuser)

---

## Project Structure

```
BidBurst/
├── Auction/                 # Django project package
│   ├── __init__.py
│   ├── asgi.py              # ASGI entry for async servers
│   ├── settings.py          # Project settings
│   ├── urls.py              # Root URL configuration
│   └── wsgi.py              # WSGI entry for deployment
├── bidburst/                # Main application (auctions & bidding)
│   ├── __init__.py
│   ├── admin.py             # Admin site registration
│   ├── apps.py              # App configuration
│   ├── models.py            # Database models
│   ├── views.py             # View logic
│   ├── tests.py             # Tests
│   └── migrations/          # Database migrations
├── manage.py                # Django management script
├── requirements.txt         # Python dependencies
└── README.md                # This file
```

- **Auction** — Project-wide settings and URL routing.
- **bidburst** — Core app for auction listings, bids, and related logic.
- **manage.py** — Used for `runserver`, `migrate`, `createsuperuser`, `test`, etc.

---

## Configuration

### Environment and secret key

For production, do **not** use the default `SECRET_KEY` in `Auction/settings.py`. Either:

- Set a strong `SECRET_KEY` in environment variables and read it in `settings.py`, or  
- Use a `.env` file with a package like `django-environ` and read from there.

### Database

The default configuration uses **SQLite** (`Auction/settings.py`):

```python
DATABASES = {
    "default": {
        "ENGINE": "django.db.backends.sqlite3",
        "NAME": BASE_DIR / "db.sqlite3",
    }
}
```

To use **PostgreSQL**, install `psycopg2-binary`, add it to `requirements.txt`, and switch `DATABASES` in `settings.py` to your PostgreSQL connection settings.

### Allowed hosts

For production, set `ALLOWED_HOSTS` in `settings.py` to your domain(s), e.g.:

```python
ALLOWED_HOSTS = ["yourdomain.com", "www.yourdomain.com"]
```

---

## Running the Application

| Command | Description |
|--------|-------------|
| `python manage.py runserver` | Start development server (default: http://127.0.0.1:8000/) |
| `python manage.py runserver 0.0.0.0:8000` | Allow access from other devices on your network |
| `python manage.py migrate` | Apply pending migrations |
| `python manage.py createsuperuser` | Create an admin user |
| `python manage.py test` | Run the test suite |

---

## Testing

Run the default Django test runner:

```bash
python manage.py test
```

Add tests in `bidburst/tests.py` (or new test modules under `bidburst/`) to cover models, views, and APIs as you build them.

---

## Contributing

1. Fork the repository.
2. Create a feature branch: `git checkout -b feature/your-feature-name`.
3. Commit your changes: `git commit -m 'Add some feature'`.
4. Push to the branch: `git push origin feature/your-feature-name`.
5. Open a Pull Request against the main repository.

---

## License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

## Acknowledgments

- [Django Documentation](https://docs.djangoproject.com/)
- [Django Admin](https://docs.djangoproject.com/en/stable/ref/contrib/admin/)
- [PEP 8 – Style Guide for Python Code](https://peps.python.org/pep-0008/)

---

**BidBurst** — *Auction platform built with Django.*
