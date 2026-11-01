1.🔐 Login Credentials Matrix:

Admin: admin / admin123 (Full system oversight, reports, user & settings management)
Librarians:
 -librarian1 / lib123 (Sabin Shrestha)
 -librarian2 / lib123 (Sabita Joshi)
Students:
 -student1 / student123 (Aarav Shrestha)
 -student2 / student123 (Bina Thapa)
 -student3 / student123 (Sujan Adhikari)
Guest Access: Catalog browsing without authentication
Note on SHA-256 password encryption in database.py

2. 🌟 System Description & Feature Breakdown:
-Admin Dashboard: System analytics, user CRUD, dynamic system policy configuration (loan duration, fine rates, book limits), transaction audit.
-Librarian Dashboard: Catalog inventory control, circulation (book issue & return with automatic overdue fine calculation), fine collection, reservations.
-Student Portal: Book catalog search, active loan and due date tracking, title reservations, fine balance tracking.
-Guest Mode: Quick search without login.

3. 🛠️ Technical Specifications & Quick Start:
-Technology stack badges (Python 3.8+, SQLite3, MIT License, Test status).
-Project structure tree breakdown.
-Instructions to launch the CLI (python main.py) and run automated tests (python -m unittest test_system.py -v).
-SQLite relational schema overview (6 tables with foreign keys and CASCADE constraints).
