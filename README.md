# 📚 Library Management System (CLI)

[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![Database](https://img.shields.io/badge/database-SQLite3-green.svg)](https://www.sqlite.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Architecture](https://img.shields.io/badge/architecture-Service--Layer%20%26%20OOP-orange.svg)]()
[![Build Status](https://img.shields.io/badge/tests-7%20passing-brightgreen.svg)]()

A comprehensive, role-based **Library Management System** built with **Python 3** and **SQLite**. Designed with strict Object-Oriented Programming (OOP) principles, clean service-layer architecture, SHA-256 credential hashing, and relational database integrity.

The system provides dedicated dashboards and permissions for **Administrators**, **Librarians**, and **Students**, as well as a quick catalog search for **Guest** visitors.

---

## 🔐 Default Login Credentials

The system automatically initializes and seeds default user accounts upon first launch. Use any of the pre-configured credentials below to explore different roles and permissions:

| Role | Username | Password | Full Name | Email | Permissions / Capabilities |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Admin** | `admin` | `admin123` | System Administrator | `admin@library.org` | Full system oversight, audit analytics, manage users, modify loan & fine policies |
| **Librarian** | `librarian1` | `lib123` | Sabin Shrestha | `sabin.shrestha@library.org.np` | Manage catalog, issue/return books, assess fines, view reservations |
| **Librarian** | `librarian2` | `lib123` | Sabita Joshi | `sabita.joshi@library.org.np` | Manage catalog, issue/return books, assess fines, view reservations |
| **Student** | `student1` | `student123` | Aarav Shrestha | `aarav.shrestha@student.edu.np` | Search books, view active loans & due dates, reserve books, check fine balance |
| **Student** | `student2` | `student123` | Bina Thapa | `bina.thapa@student.edu.np` | Search books, view active loans & due dates, reserve books, check fine balance |
| **Student** | `student3` | `student123` | Sujan Adhikari | `sujan.adhikari@student.edu.np` | Search books, view active loans & due dates, reserve books, check fine balance |
| **Guest** | *(None)* | *(None)* | Public Visitor | N/A | Browse catalog & search titles without logging in |

> [!NOTE]
> All passwords are cryptographically hashed using **SHA-256** prior to database storage. Plaintext passwords are never stored in the database.

---

## 🌟 Key Features

### 🛡️ 1. Administrator Dashboard
- **System Analytics & Audit Metrics**: View real-time statistics including total registered users, catalog counts, active book loans, overdue loans, and total fines collected vs. pending.
- **User Account Management**: Create, view, and delete accounts for Librarians and Students with automated duplicate validation.
- **Dynamic Policy Configuration**: Dynamically adjust operational rules:
  - Default loan duration (default: `14 days`)
  - Daily overdue fine rate (default: `$1.50 / day`)
  - Maximum borrowing limit per student (default: `3 books`)
- **Global Transaction & Fine Auditing**: Inspect all book loan histories and fine settlements across the institution.

### 📖 2. Librarian Dashboard
- **Catalog & Inventory Control**: Add new book records with ISBN, title, author, category, total copies, publisher, and publication year.
- **Circulation Management (Issue & Return)**:
  - Issue available books to students (validates availability, student borrow limits, and overdue holds).
  - Process book returns with **automatic overdue calculation** based on dynamic due dates.
- **Fine Management**: Review student fine assessments and record fine payments.
- **Reservation Tracking**: Monitor pending student reservation requests for high-demand or checked-out books.

### 🎓 3. Student Portal
- **Interactive Catalog Search**: Search books across title, author, ISBN, and category with live inventory availability.
- **Loan Tracking**: View currently borrowed books, loan issue dates, and upcoming due dates.
- **Book Reservation**: Place hold/reservation requests on titles that are currently checked out.
- **Financial Status**: Check unpaid overdue fine balances and payment history.

### 🔍 4. Guest Mode
- Quick search and inventory lookup directly from the main menu without authentication.

---

## 🛠️ Technology Stack & Architecture

- **Language**: Python 3.8+ (Zero external dependencies — runs with standard library)
- **Database Engine**: SQLite 3 with Foreign Key constraints enabled (`PRAGMA foreign_keys = ON`)
- **Security**: SHA-256 password hashing via Python's standard `hashlib`
- **Testing**: Built-in unit test suite via `unittest`

### 📁 Project Structure

```text
Library-Management-System-LibraryV2/
│
├── main.py            # Main application entry point
├── cli.py             # Console User Interface (menus, dashboards, tables)
├── services.py        # Business logic layer (authentication, loans, fines, catalog)
├── models.py          # OOP entities (User, Admin, Librarian, Student, Book, Loan, Fine)
├── database.py        # SQLite schema initialization, connection pooling, seed data
├── library.db         # Persistent SQLite database file
├── test_system.py     # Comprehensive automated test suite
├── LICENSE            # MIT License
└── README.md          # Project documentation & login guide
```

---

## 🚀 Quick Start Guide

### 1. Prerequisites
Ensure you have **Python 3.8** or higher installed on your system:
```bash
python --version
```

### 2. Clone the Repository
```bash
git clone https://github.com/CookieMonster-coder/Library-Management-System.git
cd Library-Management-System
```

### 3. Run the Application
Launch the CLI directly:
```bash
python main.py
```

> The database `library.db` will automatically be generated and seeded with default books, users, and settings on the first run.

---

## 🧪 Running Automated Tests

A comprehensive unit test suite is included in [`test_system.py`](file:///c:/Users/shres/OneDrive/Documents/Project/Library-Management-System-LibraryV2/test_system.py) covering user authentication, book cataloging, circulation workflows, fine calculations, and system analytics.

To execute the test suite:
```bash
python -m unittest test_system.py -v
```

Expected output:
```text
test_01_authentication_and_roles (test_system.TestLibrarySystem) ... ok
test_02_user_management (test_system.TestLibrarySystem) ... ok
test_03_book_management (test_system.TestLibrarySystem) ... ok
test_04_issue_and_return_book (test_system.TestLibrarySystem) ... ok
test_05_overdue_fine_calculation (test_system.TestLibrarySystem) ... ok
test_06_reservations (test_system.TestLibrarySystem) ... ok
test_07_admin_analytics (test_system.TestLibrarySystem) ... ok

----------------------------------------------------------------------
Ran 7 tests in 0.27s

OK
```

---

## 🗄️ Database Schema Overview

The SQLite database consists of 6 interconnected tables:

1. **`users`**: User identities, roles (`admin`, `librarian`, `student`), and SHA-256 password hashes.
2. **`books`**: Book catalog metadata, total copies, and currently available inventory.
3. **`transactions`**: Loan records tracking student borrowers, issuing librarian, issue dates, due dates, and return status.
4. **`fines`**: Overdue penalties linked to specific loan transactions and students with `paid`/`unpaid` statuses.
5. **`reservations`**: Title hold queue for students reserving out-of-stock or popular titles.
6. **`settings`**: Configurable system parameters (`max_loan_days`, `fine_per_day`, `max_books_per_student`).

---

## 📜 License

This project is open-source and distributed under the [MIT License](LICENSE).
