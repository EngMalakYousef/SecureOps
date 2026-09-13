# 🔐 SecureOps — Secure Organization Management System

> **A secure, multi-role organization management system built with Laravel, combining business functionality with practical web application security controls.**

SecureOps is a full-stack web application designed to manage users, departments, tasks, support tickets, notifications, secure file attachments, and security audit activities.

The project was developed with a **security-first approach**, focusing on access control, secure file handling, authentication protection, auditability, and defenses against common web application vulnerabilities.

---

## ✨ Key Features

### 👥 Role-Based Access Control

SecureOps provides three main user roles with different levels of access:

* **Administrator** — Full system and security management
* **Department Manager** — Manages department users, tasks, and tickets
* **Employee** — Accesses assigned tasks, tickets, and personal activities

The application combines role-based permissions with Laravel Policies for fine-grained authorization.

---

### 🏢 Organization Management

* Department management
* Department managers and employees
* User status management
* User profiles
* Role and department assignment
* Active / inactive / suspended accounts

---

### 📋 Task Management

* Create and assign tasks
* Priority levels: Low, Medium, High, Critical
* Task workflow and status tracking
* Due dates
* Task comments
* Department-based task visibility
* Authorization-controlled task access

---

### 🎫 Helpdesk Ticketing

* Create and manage support tickets
* Ticket assignment
* Priority and status management
* Ticket replies
* Internal notes for authorized users
* Department-based ticket routing
* Secure ticket attachments

---

### 📁 Secure File Management

File uploads were designed with security as a primary requirement.

Security controls include:

* Strict file extension allowlist
* MIME type verification using PHP `finfo`
* Private file storage outside the public web directory
* Random UUID-based filenames
* File size restrictions
* Path traversal protection
* Double-extension protection
* Authorization checks before downloads
* Safe download headers
* Protection against executable file uploads

Supported file types include:

`PDF` · `PNG` · `JPG` · `JPEG` · `DOCX` · `XLSX` · `TXT` · `ZIP`

---

### 🔔 Notification Center

Users receive database notifications for important activities such as:

* Task assignments
* Task status changes
* Ticket replies
* Ticket status updates

Includes unread notification indicators and notification management.

---

### 🕵️ Forensic Audit Logging

SecureOps maintains detailed audit records for security-sensitive and important application events.

Logged information can include:

* User and system actions
* Authentication events
* IP address
* User agent
* Request URL
* HTTP method
* Previous values
* New values
* Model changes
* Additional event metadata

Sensitive information such as passwords and credentials is excluded or redacted from audit records.

---

# 🛡️ Security Architecture

Security is one of the core components of SecureOps rather than an additional feature.

| Security Area                    | Protection                                                  |
| -------------------------------- | ----------------------------------------------------------- |
| **Broken Access Control / IDOR** | Laravel Policies and server-side authorization              |
| **Privilege Escalation**         | Role/permission enforcement and restricted field updates    |
| **File Upload Attacks**          | Extension allowlist, MIME validation, private storage       |
| **XSS**                          | Blade auto-escaping and Content Security Policy             |
| **SQL Injection**                | Eloquent ORM and parameterized queries                      |
| **CSRF**                         | Laravel CSRF protection                                     |
| **Brute Force**                  | Authentication rate limiting                                |
| **Session Security**             | Session regeneration and active-user verification           |
| **Information Disclosure**       | Production-safe error handling and sensitive-data redaction |
| **Clickjacking**                 | `X-Frame-Options` and CSP `frame-ancestors`                 |
| **MIME Confusion**               | `X-Content-Type-Options: nosniff`                           |
| **Inactive Accounts**            | Middleware-based session invalidation                       |

---

# 🔐 Defense-in-Depth Controls

SecureOps implements multiple security layers:

### Authentication

* Secure login and logout
* Password reset functionality
* Session regeneration
* Authentication rate limiting
* Password confirmation for sensitive actions

### Authorization

* Role-Based Access Control
* Granular permissions
* Laravel Policies
* Ownership checks
* Department-level authorization
* Protection against horizontal and vertical privilege escalation

### Application Security

* CSRF protection
* XSS mitigation
* SQL injection protection
* Security headers
* Secure validation using Form Requests
* Production-safe exception handling

### File Security

* Private storage
* MIME/magic-byte validation
* UUID-based storage names
* Download authorization
* Path traversal protection
* Executable file blocking

### Auditing

* Authentication event logging
* User lifecycle events
* Task and ticket activity
* File access events
* Model change tracking
* Sensitive data redaction

---

# 🧩 System Architecture

SecureOps follows the **Laravel MVC architecture** with dedicated security and application components.

```text
┌───────────────────────────────────────────┐
│              User Interface               │
│        Blade + Bootstrap + JavaScript     │
└─────────────────────┬─────────────────────┘
                      │
┌─────────────────────▼─────────────────────┐
│                Controllers                │
│     Requests → Validation → Responses     │
└─────────────────────┬─────────────────────┘
                      │
┌─────────────────────▼─────────────────────┐
│          Authorization Layer              │
│       Roles + Permissions + Policies      │
└─────────────────────┬─────────────────────┘
                      │
┌─────────────────────▼─────────────────────┐
│          Application / Services           │
│ Audit │ File Storage │ Notifications      │
└─────────────────────┬─────────────────────┘
                      │
┌─────────────────────▼─────────────────────┐
│              Eloquent ORM                 │
└─────────────────────┬─────────────────────┘
                      │
┌─────────────────────▼─────────────────────┐
│            MySQL / SQLite                 │
└───────────────────────────────────────────┘
```

---

# 🗄️ Main Modules

```text
SecureOps
│
├── Authentication
├── Users & Roles
├── Permissions
├── Departments
├── Tasks
├── Task Comments
├── Helpdesk Tickets
├── Ticket Replies
├── Secure Attachments
├── Notifications
└── Audit Logs
```

---

# 📊 Role-Based Dashboards

### Administrator Dashboard

Provides a system-wide security and operational overview:

* Total users
* Active departments
* Task completion statistics
* Open support tickets
* Critical task alerts
* Activity trends
* Recent audit events

### Manager Dashboard

Focused on department operations:

* Department task progress
* Team workload
* Pending tickets
* Team activity
* Department-level statistics

### Employee Dashboard

Focused on personal work:

* Assigned tasks
* Task deadlines
* Open tickets
* Notifications
* Recent activity

---

# 🧪 Security Testing

The project includes automated testing for important security and authorization scenarios.

### Tested Areas

* Authentication
* Login rate limiting
* Inactive user protection
* Role-based authorization
* IDOR prevention
* Task authorization
* Ticket access control
* Secure file uploads
* MIME validation
* Audit logging

### Test Results

**42 tests passed**
**85 assertions**

External security testing is also designed around common penetration-testing workflows using tools such as:

* Burp Suite
* OWASP ZAP
* Kali Linux

---

# 🛠️ Technology Stack

| Technology                    | Purpose               |
| ----------------------------- | --------------------- |
| **PHP 8.3**                   | Backend               |
| **Laravel 11**                | Application Framework |
| **Blade**                     | Server-side UI        |
| **Bootstrap 5.3**             | Frontend              |
| **Bootstrap Icons**           | Interface Icons       |
| **Chart.js**                  | Dashboard Analytics   |
| **MySQL 8**                   | Database              |
| **SQLite**                    | Development Database  |
| **Eloquent ORM**              | Database Layer        |
| **PHPUnit / Laravel Testing** | Automated Testing     |

---

# 🚀 Installation

### 1. Clone the repository

```bash
git clone <repository-url>
cd secure-organization-management-system
```

### 2. Install PHP dependencies

```bash
composer install
```

### 3. Install frontend dependencies

```bash
npm install
npm run build
```

### 4. Configure environment

```bash
cp .env.example .env
php artisan key:generate
```

Configure the database settings inside `.env`.

### 5. Run migrations and seeders

```bash
php artisan migrate --seed
```

### 6. Start the application

```bash
php artisan serve
```

Open:

```text
http://127.0.0.1:8000
```

---

# 🔑 Development Accounts

Development/demo accounts are provided through the database seeders.

> **Do not use development credentials in a production environment.**

---

# 📚 Documentation

Additional project documentation includes:

* `docs/architecture/ARCHITECTURE.md`
* `docs/database/SCHEMA.md`
* `docs/security/SECURITY_CONTROLS.md`
* `docs/testing/SECURITY_TESTING_GUIDE.md`
* `security-report/SECURITY_ASSESSMENT.md`

These documents provide deeper information about the system architecture, database design, security controls, testing methodology, and security assessment process.

---

# 🎯 Project Objectives

SecureOps was developed to demonstrate how a modern Laravel application can combine normal business functionality with practical security engineering principles.

The main objectives were to:

* Build a realistic multi-role web application
* Apply secure coding practices
* Implement strong authorization controls
* Protect sensitive file uploads
* Prevent common OWASP web vulnerabilities
* Create an auditable application environment
* Develop automated security-focused tests
* Prepare the application for penetration testing

---

# 👩‍💻 Project Focus

**SecureOps combines:**

`Web Development` · `Laravel` · `Cybersecurity` · `Secure Coding` · `RBAC` · `Access Control` · `File Security` · `Audit Logging` · `Security Testing`

---

> **Educational & Portfolio Project**
> Developed to demonstrate secure web application development and practical cybersecurity implementation using Laravel.
