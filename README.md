<p align="center">
  <img src="djangomart/static/img/logo.png" alt="HambaMart Logo" width="200"/>
</p>

<h1 align="center">HambaMart — Online Livestock & Agricultural Marketplace</h1>

<p align="center">
  A full-stack e-commerce web application built with Django & MariaDB for buying and selling livestock, animal feed, and agricultural equipment.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.12-blue?logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/Django-5.1-green?logo=django&logoColor=white" alt="Django">
  <img src="https://img.shields.io/badge/MariaDB-10.5+-blue?logo=mariadb&logoColor=white" alt="MariaDB">
  <img src="https://img.shields.io/badge/Bootstrap-4.5-purple?logo=bootstrap&logoColor=white" alt="Bootstrap">
  <img src="https://img.shields.io/badge/License-MIT-yellow" alt="License">
</p>

---

## 📖 Table of Contents

- [About](#about)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Database Schema](#database-schema)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Database Setup](#database-setup)
  - [Running the Server](#running-the-server)
- [Usage](#usage)
- [Design Documents](#design-documents)
- [Screenshots](#screenshots)
- [Contributors](#contributors)

---

## About

**HambaMart** is an online marketplace designed for buying and selling livestock (cows, goats, bulls), agricultural tools & equipment, and related products. It features a complete e-commerce flow — from product browsing and searching, to shopping cart management, checkout, and payment processing. The platform supports two distinct user roles: **Customers** and **Admins**, each with dedicated dashboards and capabilities.

The currency used is **Bangladeshi Taka (৳ BDT)**, and the platform supports local payment methods such as **bKash** alongside traditional credit/debit card options and cash on delivery.

---

## Features

### 🛒 Customer Features
- **User Registration & Authentication** — Sign up with email, first name, last name, phone number, and password. Secure authentication with hashed passwords (PBKDF2 + SHA-256).
- **Product Browsing** — Browse all available products on the homepage with image previews, titles, and prices.
- **Product Details** — View detailed product information including description, stock availability, price, and product image.
- **Advanced Search & Filtering** — Search products by name, description, or tags. Filter by category (Cows, Goats, Tools & Equipment, Animal Feed) and price range with an interactive dual-handle slider (noUiSlider).
- **Shopping Cart** — Add products to cart, view cart contents, adjust quantities, remove items, and see real-time total price calculations.
- **Checkout & Order Placement** — Review order summary, confirm shipping address, and proceed to payment.
- **Payment Processing** — Select from multiple payment methods: Credit Card, Debit Card, bKash, Cash on Delivery.
- **Account Management** — View and update profile information (name, email, phone, address) from a dedicated account page.
- **Order Tracking** — Placed orders are saved with status tracking (Pending → Paid).

### 🔧 Admin Features
- **Admin Dashboard** — Overview panel showing total products and total registered customers.
- **Add Products** — Create new product listings with title, description, stock, price, image URL, and comma-separated tags.
- **Edit Products** — Search for existing products by ID and edit their details inline.
- **Delete Products** — Search for products and delete them with confirmation.
- **Role-Based Access Control** — Admin pages are protected; only authenticated staff users can access admin functionality. Customers are redirected to the homepage if they attempt to access admin routes.

### 🔐 Authentication System
- **Dual Authentication Backends** — Separate custom backends for Customer and Admin authentication, both extending Django's `BaseBackend`.
- **Email-based Login** — Users log in using their email address and password.
- **Contextual Redirects** — Customers are redirected to the homepage after login; Admins are redirected to the admin dashboard.
- **Session Management** — Django session-based authentication with automatic session expiry.

---

## Tech Stack

| Layer         | Technology                                                           |
|---------------|----------------------------------------------------------------------|
| **Backend**   | Python 3.12, Django 5.1                                              |
| **Database**  | MariaDB 10.5+ (via XAMPP)                                            |
| **Frontend**  | HTML5, CSS3, Bootstrap 4.5, JavaScript                               |
| **Libraries** | [noUiSlider](https://refreshless.com/nouislider/) (price range slider) |
| **Auth**      | Custom dual authentication backends (Customer + Admin)               |
| **IDE**       | PyCharm Professional (JetBrains Student License)                     |

---

## Project Structure

```
HambaMart/
├── djangomart/                     # Django project root
│   ├── manage.py                   # Django management script
│   │
│   ├── djangomart/                 # Project configuration
│   │   ├── settings.py             # Django settings (DB, auth backends, etc.)
│   │   ├── urls.py                 # Root URL configuration
│   │   ├── backends.py             # Custom authentication backends
│   │   ├── wsgi.py                 # WSGI entry point
│   │   └── asgi.py                 # ASGI entry point
│   │
│   ├── apps/                       # Django applications
│   │   ├── customers/              # Customer management app
│   │   │   ├── models.py           # Customer, Cart, CartProduct models
│   │   │   ├── views.py            # Login, signup, cart, profile views
│   │   │   └── forms.py            # CustomerSignUpForm, CustomerProfileForm
│   │   │
│   │   ├── products/               # Product management app
│   │   │   ├── models.py           # Admin, Product, ProductTags models
│   │   │   ├── views.py            # Home, search, CRUD, admin dashboard views
│   │   │   └── forms.py            # ProductForm with tag support
│   │   │
│   │   └── orders/                 # Order processing app
│   │       ├── models.py           # Orders, OrderProduct, Payment models
│   │       └── views.py            # Checkout, payment, order confirmation views
│   │
│   ├── templates/                  # HTML templates
│   │   ├── base.html               # Base layout (navbar, footer, search bar)
│   │   ├── home.html               # Homepage with product grid
│   │   ├── product_details.html    # Individual product page
│   │   ├── product_search.html     # Search results with filter sidebar
│   │   ├── login.html              # Login form
│   │   ├── signup.html             # Registration form
│   │   ├── account.html            # User profile page
│   │   ├── cart.html               # Shopping cart
│   │   ├── checkout.html           # Order checkout
│   │   ├── payment.html            # Payment method selection
│   │   ├── payment_success.html    # Payment confirmation
│   │   ├── order_confirmation.html # Order details confirmation
│   │   ├── admin_dashboard.html    # Admin panel
│   │   ├── add_product.html        # Add new product form
│   │   ├── search_edit_product.html# Search & edit product
│   │   └── delete_product.html     # Product deletion
│   │
│   └── static/                     # Static assets
│       ├── base/
│       │   └── styles.css          # Base/header/footer styles
│       ├── styles/                 # Page-specific CSS files
│       │   ├── base.css
│       │   ├── home.css
│       │   ├── product_details.css
│       │   ├── product_search.css
│       │   ├── login.css
│       │   ├── signup.css
│       │   ├── account.css
│       │   ├── cart.css
│       │   ├── checkout.css
│       │   ├── payment.css
│       │   ├── payment_success.css
│       │   ├── admin_dashboard.css
│       │   ├── add_product.css
│       │   ├── search_edit_product.css
│       │   └── delete_product.css
│       └── img/                    # Image assets
│           ├── logo.png
│           ├── cart-icon.png
│           └── magnifying-glass-icon.png
│
├── hambamartdb.sql                 # Database dump (schema + sample data)
├── requirements.txt                # Setup notes & environment info
└── .gitignore                      # Git ignore rules
```

---

## Database Schema

The application uses **8 core tables** (plus Django system tables):

```
┌──────────────┐     ┌──────────────────┐     ┌──────────────┐
│   customer   │     │     product      │     │    admin     │
├──────────────┤     ├──────────────────┤     ├──────────────┤
│ CustomerID   │◄──┐ │ Product_ID       │  ┌──│ AdminID      │
│ FName        │   │ │ Title            │  │  │ Name         │
│ MName        │   │ │ Description      │  │  │ Email        │
│ LName        │   │ │ Stock            │  │  │ password     │
│ Address      │   │ │ Price            │  │  │ is_staff     │
│ Phone        │   │ │ product_img      │  │  │ is_active    │
│ Email        │   │ │ AdminID (FK) ────│──┘  └──────────────┘
│ password     │   │ └────────┬─────────┘
│ is_active    │   │          │
│ is_staff     │   │          │ 1:N
└──────┬───────┘   │          ▼
       │           │  ┌──────────────────┐
       │ 1:1       │  │  product_tags    │
       ▼           │  ├──────────────────┤
┌──────────────┐   │  │ Product_ID (FK)  │
│    cart      │   │  │ Tag              │
├──────────────┤   │  └──────────────────┘
│ Cart_ID      │   │
│ CustomerID   │───┘
└──────┬───────┘        ┌──────────────────┐
       │ 1:N            │     orders       │
       ▼                ├──────────────────┤
┌──────────────┐     ┌──│ Order_ID         │
│ cart_product │     │  │ Total_Price      │
├──────────────┤     │  │ Status           │
│ Product_ID   │     │  │ Address          │
│ CustomerID   │     │  │ created_at       │
│ Cart_ID      │     │  └──────┬───────────┘
│ Quantity     │     │         │ 1:N
└──────────────┘     │         ▼
                     │  ┌──────────────────┐
                     │  │  order_product   │
                     │  ├──────────────────┤
                     │  │ Product_ID (FK)  │
                     │  │ Order_ID (FK)    │
                     │  │ product_quantity │
                     │  └──────────────────┘
                     │
                     │  ┌──────────────────┐
                     │  │    payment       │
                     │  ├──────────────────┤
                     └──│ P_ID             │
                        │ CustomerID (FK)  │
                        │ Order_ID (FK)    │
                        │ Amount           │
                        │ Method           │
                        └──────────────────┘
```

---

## Getting Started

### Prerequisites

- **Python 3.12** (recommended via [Miniconda](https://docs.conda.io/en/latest/miniconda.html))
- **MariaDB 10.5+** (via [XAMPP](https://www.apachefriends.org/))
  - ⚠️ XAMPP's latest version ships with MariaDB 10.4. You need to **upgrade to 10.5+**. Follow [this guide](https://www.youtube.com/watch?v=-GmyjYEfuzE&ab_channel=DecorZone).
- **pip** (Python package manager)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/your-username/HambaMart.git
   cd HambaMart
   ```

2. **Create and activate a virtual environment**
   ```bash
   # Using conda
   conda create -n hambamart python=3.12
   conda activate hambamart

   # Or using venv
   python -m venv venv
   source venv/bin/activate        # Linux/macOS
   venv\Scripts\activate           # Windows
   ```

3. **Install dependencies**
   ```bash
   pip install django mysqlclient
   ```

### Database Setup

1. **Start XAMPP** and ensure **Apache** and **MySQL (MariaDB)** are running.

2. **Create the database** using phpMyAdmin or the command line:
   ```sql
   CREATE DATABASE hambamartdb;
   ```

3. **Import the database dump**:
   ```bash
   mysql -u root hambamartdb < hambamartdb.sql
   ```
   Or import via phpMyAdmin: select `hambamartdb` → Import → Choose `hambamartdb.sql`.

4. **Verify database settings** in `djangomart/djangomart/settings.py`:
   ```python
   DATABASES = {
       'default': {
           'ENGINE': 'django.db.backends.mysql',
           'NAME': 'hambamartdb',
           'USER': 'root',
           'PASSWORD': '',
           'HOST': 'localhost',
           'PORT': '3306',
       }
   }
   ```

### Running the Server

```bash
cd djangomart
python manage.py runserver
```

Visit **http://127.0.0.1:8000/** in your browser.

---

## Usage

### As a Customer

1. **Sign Up** — Navigate to `/signup/` and create an account with your email, name, and phone number.
2. **Log In** — Go to `/login/` and authenticate with your email and password.
3. **Browse Products** — The homepage displays all available products in a card grid layout.
4. **Search & Filter** — Use the search bar or visit `/search/` to find products. Filter by category and price range.
5. **Add to Cart** — Hover over a product card and click "Add to Cart", or click from the product details page.
6. **Checkout** — View your cart, confirm the order summary, select a payment method, and place your order.
7. **Manage Account** — Visit `/account` to view and update your profile information.

### As an Admin

1. **Log In** — Admins log in via the same `/login/` page using their admin email and password.
2. **Dashboard** — Access the admin dashboard at `/admin_dashboard/` to view platform statistics.
3. **Add Products** — Navigate to `/add_product/` to create new product listings with tags.
4. **Edit Products** — Go to `/search-edit-product/` to find and update existing products.
5. **Delete Products** — Visit `/deleteproduct_view/` to search for and remove products.

---

## Design Documents

- 📐 [ER/EER Diagram](https://drive.google.com/file/d/1MpOR6LZZtUh07fei__TzPCUCM4Xm4-U2/view?usp=sharing)
- 📋 [Relational Schema Mapping](https://drive.google.com/file/d/1gTEwrp6DHdO-Ogx1xrB0cZkYTFqWeP9J/view?usp=sharing)

---

## URL Routes

| Route                                       | Method   | Description                      | Access    |
|---------------------------------------------|----------|----------------------------------|-----------|
| `/`                                         | GET      | Homepage with product listing    | Public    |
| `/login/`                                   | GET/POST | User login                       | Public    |
| `/signup/`                                  | GET/POST | Customer registration            | Public    |
| `/logout/`                                  | GET      | Logout and redirect              | Auth      |
| `/account`                                  | GET/POST | View/edit customer profile       | Customer  |
| `/search/`                                  | GET      | Product search with filters      | Public    |
| `/product/<int:product_id>/`                | GET      | Product details page             | Public    |
| `/cart/`                                    | GET      | View shopping cart               | Customer  |
| `/add_to_cart/<int:product_id>/`            | GET      | Add product to cart              | Customer  |
| `/remove_from_cart/<cart_id>/<product_id>/`  | GET      | Remove item from cart            | Customer  |
| `/checkout/`                                | GET/POST | Order checkout                   | Customer  |
| `/process_payment/<int:order_id>/`          | GET/POST | Payment processing               | Customer  |
| `/payment-success/`                         | GET      | Payment confirmation page        | Customer  |
| `/order_confirmation/<int:order_id>/`       | GET      | Order details confirmation       | Customer  |
| `/admin_dashboard/`                         | GET      | Admin dashboard                  | Admin     |
| `/add_product/`                             | GET/POST | Add new product                  | Admin     |
| `/search-edit-product/`                     | GET/POST | Search and edit products         | Admin     |
| `/edit_product/`                            | GET      | Edit product page                | Admin     |
| `/deleteproduct_view/`                      | GET/POST | Delete products                  | Admin     |
| `/product_delete/`                          | GET/POST | Product deletion handler         | Admin     |

---

## Contributors

This project was developed as part of an academic coursework project.

| Name                       | Email                                    |
|----------------------------|------------------------------------------|
| Tasfia Zaman               | tasfia.zaman@g.bracu.ac.bd               |
| Al Irfan Alve              | al.irfan.alve@g.bracu.ac.bd             |
| Md. Rezaur Rahman Bhuiyan  | rezaur.rahman.bhuiyan@g.bracu.ac.bd     |

---

<p align="center">
  © 2024 HambaMart Online Store. All rights reserved.
</p>
