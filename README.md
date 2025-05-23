# Simple Banking App

## a. Project Title
**Simple Banking App** — A secure and user-friendly web-based banking application built with Flask, designed to simulate core banking functions with added emphasis on security.

## b. Group Members
- Member 1: [Full Name]
- Member 2: [Full Name]
- Member 3: [Full Name]
- Member 4: [Full Name]

## c. Introduction
This project is a simulation of a core banking system developed as part of a security-focused software engineering course. It allows users to register, manage their accounts, perform transfers, and view transaction history, all while enforcing role-based access and integrating security best practices.

## d. Objectives
- To develop a secure, full-featured online banking prototype.
- To assess and mitigate potential security vulnerabilities.
- To integrate Philippine geographic address validation via PSGC API.
- To deploy the application on a live server using PythonAnywhere.

## e. Original Application Features
- User authentication and session management.
- Balance inquiry and transaction history.
- Peer-to-peer fund transfer.
- Role-based access for Users, Admins, and Managers.
- Admin control over user accounts and deposits.
- PSGC location API integration.

## f. Security Assessment Findings
The original application exhibited the following vulnerabilities:
- Brute-force attack susceptibility on login.
- No rate limiting on registration and password reset.
- Password reset token not expiring after use.
- Lack of audit logs for admin activities.
- No CSRF protection on sensitive forms.

## g. Security Improvements Implemented
- Integrated Flask-Limiter for brute-force and abuse protection.
- Token-based password reset with expiration.
- Enabled CSRF protection on all Flask-WTF forms.
- Added bcrypt hashing for password storage.
- Admin activity logging for auditability.

## h. Penetration Testing Report
Penetration testing identified:
- Weakness: Unlimited login attempts — patched with rate limiting.
- Exploit: Manipulating user roles via direct POST requests — resolved by validating server-side roles.
- Issue: Session persistence after logout — mitigated via Flask session clearing.
- Recommendation: Use Redis-backed rate limiting in production for persistence.

## i. Remediation Plan
- Added `Flask-Limiter` to endpoints.
- CSRF enabled via `Flask-WTF`.
- Refactored role logic to enforce on server side.
- Implemented audit logs for admin actions.
- Configured `.env` file to secure credentials and secret keys.

## j. Technology Stack
- **Backend**: Python 3.8+, Flask
- **Frontend**: HTML, CSS, Bootstrap 5
- **Database**: MySQL + SQLAlchemy ORM
- **Authentication**: Flask-Login, Flask-Bcrypt
- **Security Tools**: Flask-WTF, Flask-Limiter, Redis (optional)
- **External API**: PSGC API (Philippine Geographic Data)

## k. Setup Instructions

### Prerequisites
- Python 3.8+
- pip
- MySQL Server 5.7+ or MariaDB

### Steps
1. Clone the repository:
   ```
   git clone https://github.com/lanlanjr/simple-banking-app.git
   cd simple-banking-app
   
   # Set up your own repository
   # First, create a new repository named 'simple-banking-app-v2' on GitHub
   
   # Reconfigure your remote
   git remote remove origin
   git remote add origin https://github.com/yourusername/simple-banking-app-v2.git
   git remote set-url origin https://yourusername@github.com/yourusername/simple-banking-app-v2.git
   git branch -M main
   git push -u origin main
   
   # Note: Replace 'yourusername' with your actual GitHub username
   ```

### 🔧 Database Setup
1. Install MySQL or MariaDB
2. Create a database and user:
   ```sql
   CREATE USER 'bankapp'@'localhost' IDENTIFIED BY 'your_password';
   GRANT ALL PRIVILEGES ON *.* TO 'bankapp'@'localhost';
   FLUSH PRIVILEGES;


3. Configure .env file:
   bash
   ```
   DATABASE_URL=mysql+pymysql://bankapp:your_password@localhost/simple_banking
   MYSQL_USER=bankapp
   MYSQL_PASSWORD=your_password
   MYSQL_HOST=localhost
   MYSQL_PORT=3306
   MYSQL_DATABASE=simple_banking
   ```

4. Install dependencies:
   ```
   pip install -r requirements.txt
   ```

5. Initialize the database:
   ```
   python init_db.py
   ```

6. run the app:
   ```
   python app.py
   ```

7. Access the application at `http://localhost:5000`

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

## Usage Guide

### Registration
- Navigate to the registration page
- Enter username, email, and password
- Confirm your password
- Submit the form to create your account (pending admin approval)

Create a new account and await admin approval
Login with verified credentials

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

Region → Province → City → Barangay

This integration ensures addresses are standardized and validates location data according to the Philippine geographical structure.

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

---

### ✅ Next Steps
You can commit this with a message like:
```bash
git add README.md
git commit -m "Update README with structured sections and detailed usage"
git push origin main
