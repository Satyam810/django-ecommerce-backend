# 🛒 Django Ecommerce Backend API

> A fully functional RESTful ecommerce backend built with Django & Django REST Framework — designed to simulate real-world ecommerce logic with proper relational database architecture.

[![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python&logoColor=white)](https://python.org)
[![Django](https://img.shields.io/badge/Django-4.x-green?logo=django&logoColor=white)](https://djangoproject.com)
[![DRF](https://img.shields.io/badge/Django_REST_Framework-red)](https://www.django-rest-framework.org/)
[![License](https://img.shields.io/badge/License-MIT-yellow)](LICENSE)

---

## 📌 Table of Contents

- [Overview](#-overview)
- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Database Architecture](#-database-architecture)
- [API Endpoints](#-api-endpoints)
- [Getting Started](#-getting-started)
- [Project Structure](#-project-structure)
- [Future Improvements](#-future-improvements)
- [Author](#-author)

---

## 📖 Overview

This project is a backend ecommerce system built from scratch as part of my backend skill development. The goal was to move from theory to practical implementation — understanding how real ecommerce platforms handle products, orders, users, and relationships under the hood.

Key learning areas covered:
- RESTful API design principles
- Relational database modeling
- Django ORM & relationships
- Real-world ecommerce order flow

---

## ✨ Features

- 📦 Product & category management
- 👤 User profile creation and management
- 🧾 Order placement with multiple products
- 🔗 Proper relational data modeling (1:1, 1:N, M:N)
- 🔍 Product filtering by category
- 🔄 Full CRUD operations on all resources
- 🛠 Built with `ModelViewSet` and `DefaultRouter` for clean, scalable routing

---

## 🛠 Tech Stack

| Technology | Purpose |
|---|---|
| Python | Core language |
| Django | Web framework |
| Django REST Framework | API layer |
| SQLite | Database |
| Postman | API testing |
| Git & GitHub | Version control |

---

## 🗄 Database Architecture

The project implements three core relationship types that mirror a real ecommerce system:

```
User ──────────────────── UserProfile
 │                         (One-to-One)
 │
 └──► Order ──────────────────────────► OrderItem ◄──── Product
       (One-to-Many)      (Junction Table / Many-to-Many)    │
                                                              │
                                               Category ──────┘
                                               (One-to-Many)
```

### Relationship Breakdown

**One-to-One**
- `User` ↔ `UserProfile` — each user has exactly one profile

**One-to-Many**
- `Category` → `Products` — a category contains many products
- `User` → `Orders` — a user can place multiple orders
- `Order` → `OrderItems` — an order holds multiple line items

**Many-to-Many** *(via junction table)*
- `Order` ↔ `Product` — handled through `OrderItem`, storing product, quantity, and price per line

---

## 🔌 API Endpoints

**Base URL:** `http://127.0.0.1:8000/api/`

| Endpoint | Methods | Description |
|---|---|---|
| `/api/categories/` | GET, POST | List or create categories |
| `/api/categories/{id}/` | GET, PUT, DELETE | Retrieve, update, or delete a category |
| `/api/products/` | GET, POST | List or create products |
| `/api/products/{id}/` | GET, PUT, DELETE | Retrieve, update, or delete a product |
| `/api/orders/` | GET, POST | List or create orders |
| `/api/orders/{id}/` | GET, PUT, DELETE | Retrieve, update, or delete an order |
| `/api/order-items/` | GET, POST | List or create order items |
| `/api/order-items/{id}/` | GET, PUT, DELETE | Retrieve, update, or delete an order item |
| `/api/profiles/` | GET, POST | List or create user profiles |
| `/api/profiles/{id}/` | GET, PUT, DELETE | Retrieve, update, or delete a profile |

### Query Parameters

Filter products by category:
```
GET /api/products/?category=1
```

---

## 🧪 API Testing with Postman

All endpoints were tested using **Postman** during development.

### How to Test

**1. Start the development server**
```bash
python manage.py runserver
```

**2. Open Postman and create a new request**

**3. Example requests to try:**

| Action | Method | URL |
|---|---|---|
| Get all products | `GET` | `http://127.0.0.1:8000/api/products/` |
| Get products by category | `GET` | `http://127.0.0.1:8000/api/products/?category=1` |
| Create a category | `POST` | `http://127.0.0.1:8000/api/categories/` |
| Place an order | `POST` | `http://127.0.0.1:8000/api/orders/` |
| Add item to order | `POST` | `http://127.0.0.1:8000/api/order-items/` |
| Get a specific product | `GET` | `http://127.0.0.1:8000/api/products/{id}/` |
| Update a product | `PUT` | `http://127.0.0.1:8000/api/products/{id}/` |
| Delete an order | `DELETE` | `http://127.0.0.1:8000/api/orders/{id}/` |

**4. For POST/PUT requests**, set the header:
```
Content-Type: application/json
```

And pass JSON in the request body. Example — creating a product:
```json
{
  "name": "Wireless Headphones",
  "price": "1999.00",
  "category": 1
}
```

---

## 🚀 Getting Started

### Prerequisites

- Python 3.x installed
- pip package manager

### Installation

**1. Clone the repository**
```bash
git clone https://github.com/Satyam810/django-ecommerce-backend.git
cd django-ecommerce-backend
```

**2. Create and activate a virtual environment**
```bash
# Create
python -m venv venv

# Activate (Windows)
venv\Scripts\activate

# Activate (macOS/Linux)
source venv/bin/activate
```

**3. Install dependencies**
```bash
pip install -r requirements.txt
```

**4. Apply database migrations**
```bash
python manage.py migrate
```

**5. (Optional) Create a superuser for Django Admin**
```bash
python manage.py createsuperuser
```

**6. Start the development server**
```bash
python manage.py runserver
```

The API will be available at: **`http://127.0.0.1:8000/`**

---

## 📁 Project Structure

```
django-ecommerce-backend/
│
├── core/                       # Django project configuration
│   └── core/
│       ├── __init__.py
│       ├── settings.py         # Project settings
│       ├── urls.py             # Root URL configuration
│       ├── asgi.py
│       └── wsgi.py
│
├── store/                      # Main ecommerce app
│   ├── migrations/             # Database migrations
│   ├── __init__.py
│   ├── admin.py                # Admin panel registration
│   ├── apps.py
│   ├── models.py               # Category, Product, Order, OrderItem, UserProfile
│   ├── serializers.py          # DRF serializers for all models
│   ├── views.py                # ModelViewSet-based views
│   ├── urls.py                 # Router-based URL configuration
│   └── tests.py
│
├── venv/                       # Virtual environment (git-ignored)
├── db.sqlite3                  # SQLite database (git-ignored)
├── manage.py
├── requirements.txt
└── .gitignore
```

---

## 🔮 Future Improvements

- [ ] JWT Authentication & token-based auth
- [ ] Admin-only endpoints for product management
- [ ] Pagination on list endpoints
- [ ] Deployment to a cloud platform (Railway / Render / AWS)
- [ ] Payment integration simulation (Stripe/Razorpay)
- [ ] Search functionality across products
- [ ] Order status tracking (pending → shipped → delivered)

---

## 👨‍💻 Author

**Satyam**
Aspiring Software Engineer | AI & Machine Learning Enthusiast
Backend Development & API Design Practice Project

[![GitHub](https://img.shields.io/badge/GitHub-Satyam810-black?logo=github)](https://github.com/Satyam810)

---

> ⭐ If you found this project useful or interesting, consider giving it a star!
