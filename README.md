# 🏭 Product Chain Distribution Management System

> A comprehensive web-based solution for managing product distribution across manufacturers, distributors, and customers with real-time inventory tracking, dynamic pricing, and complete order processing.

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![Flask](https://img.shields.io/badge/Flask-2.3.0-green.svg)](https://flask.palletsprojects.com/)
[![MySQL](https://img.shields.io/badge/MySQL-8.0-orange.svg)](https://www.mysql.com/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [System Architecture](#system-architecture)
- [Installation](#installation)
- [Database Setup](#database-setup)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [User Roles](#user-roles)
- [Technologies Used](#technologies-used)
- [Screenshots](#screenshots)
- [Contributing](#contributing)
- [License](#license)

---

## 🎯 Overview

The **Product Chain Distribution Management System** is a full-stack web application built with Flask and MySQL that digitizes and automates the entire product distribution lifecycle. The system supports three distinct user roles—**Manufacturers**, **Distributors**, and **Customers**—each with specialized features for their operational needs.

### Key Highlights

- ✅ **13 Normalized Database Tables** (3NF compliance)
- ✅ **Role-Based Access Control** with secure authentication
- ✅ **Real-Time Inventory Management** across supply chain
- ✅ **Dynamic Pricing** with 10% minimum markup validation
- ✅ **Automated Allocation System** from manufacturers to distributors
- ✅ **Complete Order Processing** with payment and shipment tracking
- ✅ **Analytics Dashboards** for business intelligence
- ✅ **Audit Trail** for price changes and transactions

---

## ✨ Features

### 🏭 Manufacturer Features
- Product creation and management with SKU tracking
- Inventory management with reorder level alerts
- Allocate products to distributors
- View allocation history and audit trail
- Dashboard with key performance metrics

### 🚚 Distributor Features
- Receive allocated inventory from manufacturers
- Set and update product pricing (with markup validation)
- Track price change history
- View and manage customer orders
- Analytics dashboard (top products, top customers, revenue)
- Low-stock alerts

### 👤 Customer Features
- Browse available products with search and filters
- Place orders from multiple sellers
- Track order status and shipment details
- View order history
- Loyalty points system

---

## 🏗️ System Architecture

┌─────────────────────────────────────────────────────────────┐
│                    Flask Web Application                     │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐      │
│  │ Manufacturer │  │ Distributor  │  │   Customer   │      │
│  │    Routes    │  │    Routes    │  │    Routes    │      │
│  └──────────────┘  └──────────────┘  └──────────────┘      │
│           │                 │                 │              │
│           └─────────────────┴─────────────────┘              │
│                           │                                  │
│                    Authentication Layer                      │
│                  (Session Management + RBAC)                 │
│                           │                                  │
│                    MySQL Connector                           │
│                           │                                  │
└───────────────────────────┼──────────────────────────────────┘
                            │
                            ▼
              ┌─────────────────────────┐
              │   MySQL Database        │
              │  (13 Normalized Tables) │
              └─────────────────────────┘

---

## 🚀 Installation

### Prerequisites

- **Python 3.8+**
- **MySQL 8.0+**
- **pip** (Python package manager)
- **Git** (for cloning repository)

### Step 1: Clone Repository

git clone https://github.com/yourusername/product-chain-distribution.git
cd product-chain-distribution

### Step 2: Create Virtual Environment

# Windows
python -m venv venv
venv\Scripts\activate

# macOS/Linux
python3 -m venv venv
source venv/bin/activate

### Step 3: Install Dependencies

pip install -r requirements.txt

**requirements.txt:**
Flask==2.3.0
mysql-connector-python==8.0.33
Werkzeug==2.3.0

---

## 🗄️ Database Setup

### Step 1: Create Database

mysql -u root -p

CREATE DATABASE product_chain_distribution;
USE product_chain_distribution;

### Step 2: Run Schema Script

mysql -u root -p product_chain_distribution < schema.sql

### Step 3: Insert Sample Data

mysql -u root -p product_chain_distribution < insert_data_final.sql

### Step 4: Configure Database Connection

Edit `app.py` and update the database configuration:

db_config = {
    'user': 'root',
    'password': 'YOUR_MYSQL_PASSWORD',  # Change this
    'host': 'localhost',
    'database': 'product_chain_distribution',
    'raise_on_warnings': True,
    'autocommit': True
}

---

## 🎮 Usage

### Start the Application

python app.py

The application will be available at: **http://127.0.0.1:5000**

### Default Login Credentials

**Manufacturer:**
- Username: `nike_mfg`
- Password: `nike123`
- Type: `manufacturer`

**Distributor:**
- Username: `global_dist`
- Password: `global123`
- Type: `distributor`

**Customer:**
- Username: `john_doe`
- Password: `john123`
- Type: `customer`

*(See `insert_data_final.sql` for all test accounts)*

---

## 📁 Project Structure

product-chain-distribution/
│
├── app.py                          # Main Flask application
├── schema.sql                      # Database schema (DDL)
├── insert_data_final.sql          # Sample data with hashed passwords
├── queries.sql                    # Complex SQL queries
├── requirements.txt               # Python dependencies
├── README.md                      # This file
│
├── templates/                     # HTML templates
│   ├── base.html                  # Base template with navigation
│   ├── login.html                 # Login page
│   │
│   ├── manufacturer_dashboard.html
│   ├── manufacturer_products.html
│   ├── manufacturer_inventory.html
│   ├── manufacturer_add_product.html
│   ├── manufacturer_allocate.html
│   ├── manufacturer_allocations.html
│   │
│   ├── distributor_dashboard.html
│   ├── distributor_inventory.html
│   ├── distributor_orders.html
│   ├── distributor_pricing.html
│   ├── distributor_analytics.html
│   │
│   ├── customer_dashboard.html
│   ├── customer_browse_products.html
│   ├── customer_orders.html
│   └── customer_order_details.html
│
└── static/                        # CSS/JS/Images
    └── style.css                  # Application styles

---

## 👥 User Roles

### 🏭 Manufacturer
**Purpose:** Produce and distribute products to distributors

**Key Actions:**
- Add/edit/delete products
- Manage inventory levels
- Allocate products to distributors
- Monitor low-stock alerts
- View allocation history

**Dashboard Metrics:**
- Total products
- Inventory value
- Low-stock items
- Recent allocations

---

### 🚚 Distributor
**Purpose:** Receive products from manufacturers and sell to customers

**Key Actions:**
- View allocated inventory
- Set selling prices (min 10% markup)
- Track price changes
- Manage customer orders
- View analytics (top products/customers)

**Dashboard Metrics:**
- Unique products
- Total inventory units
- Inventory value
- Total orders
- Total revenue
- Low-stock alerts

---

### 👤 Customer
**Purpose:** Purchase products from distributors

**Key Actions:**
- Browse product catalog
- Place orders
- Track order status
- View shipment details
- Access order history

**Dashboard Metrics:**
- Total orders
- Total spent
- Loyalty points

---

## 🛠️ Technologies Used

| Category | Technology |
|----------|-----------|
| **Backend** | Python 3.8+, Flask 2.3.0 |
| **Database** | MySQL 8.0 |
| **Frontend** | HTML5, CSS3, JavaScript |
| **Authentication** | Werkzeug (pbkdf2:sha256 password hashing) |
| **DB Connectivity** | mysql-connector-python |
| **Development Tools** | VS Code, MySQL Workbench, Git |

---

## 📊 Database Schema Overview

### Core Tables (13 Total)

1. **users** - Authentication and user management
2. **manufacturer** - Manufacturer company details
3. **distributor** - Distributor company details
4. **customer** - Customer profiles and loyalty points
5. **product** - Product catalog with SKU and pricing
6. **inventory** - Manufacturer stock levels
7. **allocation** - Manufacturer → Distributor transfers
8. **distributor_inventory** - Distributor stock with pricing
9. **customer_order** - Customer orders and status
10. **order_item** - Order line items with seller info
11. **shipment** - Shipment tracking details
12. **payment** - Payment records and transactions
13. **price_change_history** - Audit trail for pricing

**Relationships:**
- One-to-Many: Users → Manufacturer/Distributor/Customer
- One-to-Many: Manufacturer → Products → Inventory
- Many-to-Many: Manufacturer ↔ Distributor (via Allocation)
- One-to-Many: Customer → Orders → Order Items

---

## 📸 Screenshots

### Login Screen
![Login](screenshots/login.png)

### Manufacturer Dashboard
![Manufacturer Dashboard](screenshots/manufacturer_dashboard.png)

### Distributor Pricing Control
![Distributor Pricing](screenshots/distributor_pricing.png)

### Customer Browse Products
![Customer Products](screenshots/customer_browse.png)

---

## 🧪 Testing

### Run Test Suite

# Execute all test queries
mysql -u root -p product_chain_distribution < queries.sql

### Test Data Summary
- **23 Users** (4 manufacturers, 6 distributors, 13 customers)
- **16 Products** across 4 manufacturers
- **18 Allocations** from manufacturers to distributors
- **15 Customer Orders** with multiple items
- **12 Shipments** with tracking information
- **15 Payment Records**

---

## 🔒 Security Features

- ✅ **Password Hashing:** Werkzeug pbkdf2:sha256 with 600,000 rounds
- ✅ **SQL Injection Prevention:** Parameterized queries throughout
- ✅ **Role-Based Access Control:** Route-level authorization
- ✅ **Session Management:** Secure Flask sessions with secret key
- ✅ **Input Validation:** Server-side validation for all forms
- ✅ **CSRF Protection:** Flask built-in CSRF handling

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details

---

## 🙏 Acknowledgments

- Flask documentation for comprehensive guides
- MySQL community for database optimization tips
- Stack Overflow community for troubleshooting support
- PES University for project guidance

---

## 📈 Future Enhancements

- [ ] REST API for mobile app integration
- [ ] Email notifications for order updates
- [ ] Advanced analytics with charts and graphs
- [ ] Multi-currency support
- [ ] Review and rating system
- [ ] Shopping cart functionality
- [ ] Export reports to PDF/Excel
- [ ] Real-time notifications using WebSockets
- [ ] Two-factor authentication
- [ ] Docker containerization

---

**Made with ❤️ for DBMS Mini Project**
