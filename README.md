## Simple Banking App v-2

A user-friendly and responsive Flask-based banking application designed for deployment on PythonAnywhere. This application allows users to create accounts, perform simulated money transfers between accounts, view transaction history, and securely manage their credentials. Created by Group 5 members:
Sydrick Parra
Julie Mae Bermudo
Marcial Rempillo
Vladimir Ivan Pili

## 🎥 Project Demo Video

Watch the full walkthrough and demo of the Simple Banking App V2 on YouTube:

🔗 [Click to Watch on YouTube](https://youtu.be/wuia-6WqWcM)

This video covers:
- App features and roles
- Fund transfers and admin actions
- Security improvements and logging
- Live demonstration of core functionality


## Features

- **User Authentication**
  - Secure login with username/password
  - Registration of new users
  - Password recovery mechanism (email-based)

- **Account Management**
  - Display of account balance
  - View recent transaction history (last 10 transactions)

- **Fund Transfer**
  - Transfer money to other registered users
  - Confirmation screen before completing transfers
  - Transaction history updated after transfers

- **User Role Management**
  - Regular user accounts
  - Admin users with account approval capabilities
  - Manager users who can manage admin accounts

- **Location Data Integration**
  - Philippine Standard Geographic Code (PSGC) API integration
  - Hierarchical location data selection (Region, Province, City, Barangay)
  - Form fields pre-populated with location data

- **Admin Features**
  - User account approval workflow
  - Account activation/deactivation
  - Deposit funds to user accounts
  - Create new accounts
  - Edit user information

- **Manager Features**
  - Create and manage admin accounts
  - View admin transaction logs
  - Monitor all system transfers

- **Security**
  - Password hashing with bcrypt for secure storage
  - Secure session management
  - Token-based password reset
  - API rate limiting to prevent abuse
  - CSRF protection for all forms

## Getting Started

### Prerequisites
- Python 3.7+
- pip (Python package manager)
- MySQL Server 5.7+ or MariaDB 10.2+

### Database Setup

1. Install MySQL Server or MariaDB if you haven't already:
   ```
   # For Ubuntu/Debian
   sudo apt update
   sudo apt install mysql-server
   
   # For macOS with Homebrew
   brew install mysql
   
   # For Windows
   # Download and install from the official website
   ```

2. Create a database user and set privileges:
   ```
   mysql -u root -p
   
   # In MySQL prompt
   CREATE USER 'bankapp'@'localhost' IDENTIFIED BY 'your_password';
   GRANT ALL PRIVILEGES ON *.* TO 'bankapp'@'localhost';
   FLUSH PRIVILEGES;
   EXIT;
   ```

3. Update the `.env` file with your MySQL credentials:
   ```
   DATABASE_URL=mysql+pymysql://bankapp:your_password@localhost/simple_banking
   MYSQL_USER=bankapp
   MYSQL_PASSWORD=your_password
   MYSQL_HOST=localhost
   MYSQL_PORT=3306
   MYSQL_DATABASE=simple_banking
   ```

4. Initialize the database:
   ```
   python init_db.py
   ```

### Installation

1. Clone the repository:
   ```
   git clone https://github.com/lanlanjr/simple-banking-app.git
   cd simple-banking-app
   
   # Set up your own repository
   # First, create a new repository named 'simple-banking-app-v2' on GitHub
   
   # Then configure your local repository
   git remote remove origin
   git remote add origin https://github.com/yourusername/simple-banking-app-v2.git
   git remote set-url origin https://yourusername@github.com/yourusername/simple-banking-app-v2.git
   git branch -M main
   git push -u origin main
   
   # Note: Replace 'yourusername' with your actual GitHub username
   ```

2. Install the required packages:
   ```
   pip install -r requirements.txt
   ```

3. Run the application:
   ```
   python app.py
   ```

4. Access the application at `http://localhost:5000`

## Deploying to PythonAnywhere

1. Create a PythonAnywhere account at [www.pythonanywhere.com](https://www.pythonanywhere.com)

2. Upload your code using Git:
   ```
   git clone https://github.com/yourusername/simple-banking-app-v2.git
   ```

3. Install requirements:
   ```
   cd simple-banking-app-v2
   pip install -r requirements.txt
   ```

4. Set up MySQL database on PythonAnywhere:
   - Go to the Databases tab in your PythonAnywhere dashboard
   - Create a new MySQL database
   - Note the database name, username, and password
   - Update your .env file with these credentials

5. Initialize your database on PythonAnywhere:
   ```
   python init_db.py
   ```

6. Configure a new web app via the PythonAnywhere dashboard:
   - Select "Manual configuration"
   - Choose Python 3.8
   - Set source code directory to `/home/yourusername/simple-banking-app-v2`
   - Set working directory to `/home/yourusername/simple-banking-app-v2`
   - Set WSGI configuration file to point to your Flask app

7. Add environment variables in the PythonAnywhere dashboard for security

## Usage

### Registration
- Navigate to the registration page
- Enter username, email, and password
- Confirm your password
- Submit the form to create your account (pending admin approval)

### Login
- Enter your username and password
- Click "Sign In"

### Account Overview
- View your current balance
- See your recent transaction history

### Transfer Funds
- Navigate to the Transfer page
- Enter recipient's username or account number
- Enter the amount to transfer
- Confirm the transfer details on the confirmation screen
- Complete the transfer

### Password Reset
- Click "Forgot your password?" on the login page
- Enter your registered email address
- Follow the link in the email (simulated in this demo)
- Create a new password

### Admin Features
- Approve new user registrations
- Activate/deactivate user accounts
- Create new user accounts
- Make over-the-counter deposits to user accounts
- Edit user details including location information

### Manager Features
- Create new admin accounts
- Toggle admin status for users
- View all user transactions
- Monitor and audit admin activities

## User Roles

The system supports three types of user roles:

1. **Regular Users** - Can manage their own account, make transfers, and view their transaction history.

2. **Admin Users** - Have all regular user privileges plus:
   - Approve/reject new user registrations
   - Activate/deactivate user accounts
   - Create new user accounts
   - Make deposits to user accounts
   - Edit user information

3. **Manager Users** - Have all admin privileges plus:
   - Create and manage admin accounts
   - View admin transaction logs
   - Monitor all system transfers
   - System-wide oversight capabilities

## Address Management with PSGC API

The application integrates with the Philippine Standard Geographic Code (PSGC) API to provide standardized address selection for user profiles. The address system follows the Philippine geographical hierarchy:

- Region
- Province
- City/Municipality
- Barangay

This integration ensures addresses are standardized and validates location data according to the Philippine geographical structure.

## Technologies Used

- **Backend**: Python, Flask
- **Database**: MySQL (with SQLAlchemy ORM)
- **Frontend**: HTML, CSS, Bootstrap 5
- **Authentication**: Flask-Login, Werkzeug, Flask-Bcrypt
- **Forms**: Flask-WTF, WTForms
- **Security**: Flask-Limiter for API rate limiting, CSRF protection
- **External API**: PSGC API for Philippine geographic data

## Rate Limiting

The application uses Flask-Limiter to implement API rate limiting, which protects against potential DoS attacks and abusive bot activity. The rate limits are configured as follows:

- **Login**: 10 attempts per minute
- **Registration**: 5 attempts per minute
- **Password Reset**: 5 attempts per hour
- **Money Transfer**: 20 attempts per hour
- **API Endpoints**: 30 requests per minute
- **Admin Dashboard**: 60 requests per hour
- **Admin Account Creation**: 20 accounts per hour
- **Admin Deposits**: 30 deposits per hour
- **Manager Dashboard**: 60 requests per hour
- **Admin Creation**: 10 admin accounts per hour

By default, the rate limiting data is stored in memory. For production use, it's recommended to use Redis as a storage backend for persistence across application restarts. To enable Redis storage:

1. Install Redis server on your system
2. Update the `.env` file with your Redis URL:
   ```
   REDIS_URL=redis://localhost:6379/0
   ```

If Redis is not available, the application will automatically fall back to in-memory storage.

## License

This project is licensed under the MIT License - see the LICENSE file for details.

### 🔐 IMPROVEMENTS MADE BY SYDRICK B. PARRA


### 📋 Overview

As part of our security enhancement and audit tracking initiative, we implemented a robust **Admin Action Logging System** designed to record all critical actions performed by privileged users (i.e., admins and managers). This feature complements the existing `Transaction` model by focusing on **who did what**, not just money movement.

All additions are marked in the source code with:

```python
# (SYD) ADDED ADMIN LOG
```

---

### ⚡️ Why This Was Added

Modern web applications — especially those handling sensitive financial data — face several critical security risks:

* **Privilege Abuse**: Admin users may accidentally or intentionally make unauthorized changes without oversight.
* **Lack of Traceability**: Without proper logging, it is difficult to trace who made what change and when.
* **Insecure Audit Practices**: Applications often focus on transaction records but overlook administrative actions, which can have equal or greater impact.

To mitigate these vulnerabilities, we implemented a secure, centralized audit system:

* Ensures **transparency** for all administrative operations.
* Supports **accountability** through a non-repudiable log.
* Aligns with **OWASP best practices**, including "Logging & Monitoring" and "Security Misconfiguration" prevention.

By monitoring all privileged user activity, this system dramatically reduces the risk of silent privilege misuse and ensures that all critical changes are recorded.

---

### 🧱 New Components Introduced

#### ✅ `AdminActionLog` Model

A new SQLAlchemy model added to `models.py`:

```python
class AdminActionLog(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    admin_id = db.Column(db.Integer, db.ForeignKey('user.id'), nullable=False)
    action = db.Column(db.String(128), nullable=False)
    details = db.Column(db.Text, nullable=True)
    timestamp = db.Column(db.DateTime, default=datetime.utcnow)
```

Purpose:

* Tracks all privileged administrative actions (not only financial).
* Maintains accountability and supports audit/compliance requirements.
* Used only by admins and managers, not exposed to regular users.

---

#### ✅ `log_admin_action()` Utility Function

Added to `routes.py`:

```python
def log_admin_action(admin_id, action, details):
    print(f"[DEBUG] Logging admin action: {action}")  # (SYD) ADDED ADMIN LOG
    log = AdminActionLog(
        admin_id=admin_id,
        action=action,
        details=details,
        timestamp=datetime.utcnow()
    )
    db.session.add(log)
    db.session.commit()
```

This function is reusable across routes for all administrative events.

---

### 🔧 Routes Enhanced with Admin Logging

We added logging to the following administrative routes:

| Route                         | Action Logged                    | Example Entry                                      |
| ----------------------------- | -------------------------------- | -------------------------------------------------- |
| `/admin/deposit`              | Admin deposits to a user         | "Deposited ₱500 to user: johndoe"                  |
| `/execute_transfer`           | Transfers performed by admins    | "Transferred ₱500 to janedoe"                      |
| `/admin/activate_user/<id>`   | User account activation          | "Activated user: johndoe"                          |
| `/admin/deactivate_user/<id>` | User account deactivation        | "Deactivated user: janedoe"                        |
| `/admin/edit_user/<id>`       | User information updated         | "Edited user: johndoe. Changes made: email, phone" |
| `/admin/create_account`       | Admin creates a regular user     | "Created new user account: johndoe"                |
| `/manager/create_admin`       | Manager creates an admin account | "Created new admin account: admin1"                |
| `/manager/toggle_admin/<id>`  | Promote/demote admin role        | "Promoted user: staff1" / "Demoted user: admin1"   |
| `/login` and `/logout`        | Admin or manager login/logout    | "admin1 logged in" / "admin1 logged out"           |

All of the above contain `# (SYD) ADDED ADMIN LOG` comments in the codebase.

---

### 🗅️ Admin Logs Web Interface

#### 📄 `admin_logs.html`

* Added a new HTML template: `templates/admin/admin_logs.html`
* Table format showing:

  * Timestamp
  * Admin username
  * Action name
  * Details

#### 🔗 Route Added: `/admin/logs`

* Accessible only to users with `is_admin` or `is_manager`
* Allows admins to monitor recent privileged actions

---

### 💠 Database Integration

* Table auto-created via `db.create_all()` or Flask-Migrate
* Logs stored in the `admin_action_log` table
* Query example:

  ```sql
  SELECT * FROM admin_action_log ORDER BY timestamp DESC;
  ```

---

### 📌 Note for Reviewers/Developers

* Every new log entry is handled server-side via Python.
* Print statements like `[DEBUG] Logging admin action: XYZ` help trace execution in the terminal.
* All related code is clearly marked with:

  ```python
  # (SYD) ADDED ADMIN LOG
  ```

### 🚀 Deployment on PythonAnywhere

The **Simple Banking App V2** is live and hosted on [PythonAnywhere](https://www.pythonanywhere.com), providing secure access to the application via the link below:

🔗 **Live Demo:** [https://mocec58946.pythonanywhere.com/login?next=%2F](https://mocec58946.pythonanywhere.com/login?next=%2F)

---

### 🛠 Deployment Details

- **Hosting Platform:** PythonAnywhere (free tier)
- **Backend Framework:** Flask (Python 3.11)
- **Frontend:** HTML, CSS, Bootstrap 5
- **Database:** MySQL (hosted by PythonAnywhere)
- **Security Features Implemented:**
  - CSRF protection (via Flask-WTF)
  - Role-based access control (Admin, Manager, User)
  - Admin action logging (deposit, edit, activate/deactivate, etc.)
  - Session protection and secure headers
  - HTTPS enforced in production

---

### ⚙️ Deployment Steps Summary

1. **Code Upload:** Pushed via Git to PythonAnywhere working directory.
2. **Virtual Environment:** Created and all dependencies installed with `pip`.
3. **Database Setup:** MySQL database created using the PythonAnywhere Databases tab.
4. **App Configuration:** Updated `config.py` with production database URI.
5. **WSGI Configuration:** Modified PythonAnywhere WSGI file to point to the Flask app.
6. **Testing:** Verified all features work including login, fund transfer, and admin log tracking.

---

### 🔐 Test Account Credentials

You can log in using the following test credentials:

- **Username:** `mocec58946`
- **Email:** `mocec58946@nomrista.com`
- **Password:** `admin123`

> This account has administrative privileges and can be used to test fund transfers, deposits, user approvals, and other admin/manager functions.

---

### 📊 Viewing Admin Action Logs

To view audit logs for actions performed by admins and managers (e.g., login, logout, deposits, account activations):

1. Go to your [PythonAnywhere dashboard](https://www.pythonanywhere.com/user/mocec58946/consoles).
2. Click the console named:  
   **`MySQL: mocec58946$simple_banking`**
3. In the MySQL shell, run the following commands:

```sql
USE mocec58946$simple_banking;
SHOW TABLES;
SELECT * FROM admin_action_log ORDER BY id DESC;

---

This deployment supports live testing, secure transactions, and showcases the application’s full feature set for evaluation and demonstration.
