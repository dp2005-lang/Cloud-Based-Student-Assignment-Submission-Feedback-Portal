# Cloud-Based-Student-Assignment-Submission-Feedback-Portal
Cloud-based student assignment submission and feedback portal built with Python and Gradio. Features role-based authentication, object-storage-style file handling, SQLite database, server-side deadline validation, versioned resubmissions, teacher grading and feedback, notifications, dashboards, and CSV gradebook export.
# ☁️ Cloud-Based Student Assignment Submission & Feedback Portal

> **A secure, role-based academic portal for assignment creation, submission, version management, grading, feedback, notifications, analytics, and cloud-ready file storage.**

[![Python](https://img.shields.io/badge/Python-3.x-3776AB?logo=python\&logoColor=white)](https://www.python.org/)
[![Google Colab](https://img.shields.io/badge/Platform-Google%20Colab-F9AB00?logo=googlecolab\&logoColor=white)](https://colab.research.google.com/)
[![Gradio](https://img.shields.io/badge/UI-Gradio-FF7C00)](https://www.gradio.app/)
[![SQLite](https://img.shields.io/badge/Database-SQLite-003B57?logo=sqlite\&logoColor=white)](https://www.sqlite.org/)
[![Pandas](https://img.shields.io/badge/Data-Pandas-150458?logo=pandas\&logoColor=white)](https://pandas.pydata.org/)
[![Matplotlib](https://img.shields.io/badge/Visualization-Matplotlib-11557C)](https://matplotlib.org/)

---

## 📌 Overview

The **Cloud-Based Student Assignment Submission & Feedback Portal** is an interactive academic management application developed in **Python and Google Colab** using **Gradio**.

The platform connects two primary roles:

* 🎓 **Student**
* 👩‍🏫 **Teacher**

Students can view assignments, upload submissions, resubmit versions where permitted, download their previous files, and receive marks and feedback.

Teachers can create courses and assignments, configure deadlines and submission rules, review submissions, grade work, provide feedback, inspect text-submission similarity, and export gradebooks.

The application also demonstrates important cloud-computing concepts through a **local/simulated cloud architecture**, including authentication, role-based access control, database persistence, object-storage patterns, server-side deadline validation, audit logging, notifications, and analytics.

---

# 🎯 Problem Statement

Traditional assignment workflows often rely on multiple disconnected tools for:

* Assignment distribution
* File submission
* Deadline tracking
* Resubmission
* Grading
* Feedback
* Notifications
* Record keeping

This can make academic workflows harder to manage and can lead to inconsistent file handling, unclear submission status, and inefficient communication.

This project aims to bring these activities into a **single role-based academic portal** with structured data storage and controlled access.

---

# 💡 Objectives

The main objectives are to:

* Build a centralized assignment management platform.
* Separate student and teacher functionality using RBAC.
* Provide secure user authentication.
* Support assignment deadlines and submission rules.
* Validate uploaded files on the server.
* Maintain submission versions.
* Prevent duplicate uploads through file hashing.
* Enable teacher grading and feedback.
* Notify users about important academic events.
* Maintain audit records.
* Provide assignment-status analytics.
* Export gradebook data for further processing.
* Demonstrate cloud application architecture using a Colab-based implementation.

---

# 🚀 Key Features

## 🔐 Authentication & Role-Based Access

The portal supports:

* Student registration
* Teacher registration
* Secure password hashing using PBKDF2
* Login/logout
* Teacher invite-code validation
* Role-based access control
* User-specific authorization checks

Students cannot perform teacher-only operations, and teachers can manage only their own courses and assignments.

---

## 📚 Course Management

Teachers can:

* Create courses
* View their courses
* Associate assignments with their courses
* Manage course-specific academic workflows

---

## 📝 Assignment Management

Teachers can create assignments with configurable:

* Title
* Description
* Deadline
* Maximum marks
* Allowed file extensions
* Maximum upload size
* Late-submission policy
* Resubmission policy

Example:

```text
Assignment
├── Course
├── Title
├── Description
├── Deadline
├── Maximum Marks
├── Allowed File Types
├── Maximum File Size
├── Late Submission Policy
└── Resubmission Policy
```

---

# 📤 Student Submission System

Students can submit assignments directly through the portal.

The application validates:

### File Type

Only teacher-approved extensions are accepted.

Example:

```text
PDF
DOCX
TXT
PNG
JPG
ZIP
```

### File Size

The uploaded file is checked against the assignment's maximum size.

### Deadline

The server-side application clock determines whether a submission is late.

The client does not control the deadline decision.

### Resubmission

Where enabled, students can upload a new version.

Submission versions are tracked as:

```text
v1
v2
v3
...
```

### Duplicate Upload Protection

SHA-256 hashing is used to detect an identical file submitted again, preventing unnecessary duplicate versions.

---

# ☁️ Object Storage Architecture

The application includes an `ObjectStorage` abstraction that acts as a **local stand-in for a cloud object-storage service**.

Current implementation:

```text
Google Colab
     │
     ▼
ObjectStorage Class
     │
     ▼
Local Private Bucket Directory
```

The abstraction is designed so that the local storage layer can later be replaced by services such as:

* Amazon S3
* Google Cloud Storage
* Firebase Storage

without changing the higher-level submission workflow.

> **Important:** The current implementation uses local filesystem storage inside the Colab environment; it does not directly connect to AWS S3, Google Cloud Storage, or Firebase Storage.

---

# 👩‍🏫 Teacher Grading & Feedback

Teachers can:

* Load assignment submissions
* View submission versions
* Review student files
* Enter marks
* Add written feedback
* Mark submissions as graded
* Notify students after grading

Marks are validated against the assignment's maximum score.

Example:

```text
Assignment: Cloud Service Models
Maximum Marks: 20

Student Score: 17/20

Feedback:
"Good comparison of IaaS, PaaS and SaaS.
Add more detail about deployment responsibility."
```

---

# 🔍 Similarity Checking

The portal includes a starter similarity-analysis feature for **text-based submissions**.

Supported text-oriented formats include:

```text
.txt
.md
.py
.csv
.java
.c
.cpp
```

The system uses:

```text
TF-IDF Vectorization
        ↓
Cosine Similarity
        ↓
Pairwise Similarity %
```

Example output:

| Student A | Student B | Similarity |
| --------- | --------- | ---------: |
| Student 1 | Student 2 |      78.4% |
| Student 1 | Student 3 |      31.2% |

This is intended as a **basic similarity-analysis feature**, not a complete plagiarism-detection system.

---

# 🔔 Notifications

The portal generates notifications for events such as:

* New assignment creation
* Student submission
* Late submission
* Grading completion

Users can view notifications through the dedicated notification interface and mark them as read.

---

# 🧾 Audit Logging

Important actions are recorded in an audit table.

Examples include:

```text
REGISTER
LOGIN
LOGOUT
CREATE_COURSE
CREATE_ASSIGNMENT
SUBMIT
UPLOAD_FAILED
GRADE
DENIED_DOWNLOAD
```

This provides a basic activity trail for the application.

---

# 📊 Dashboards

The application provides role-specific dashboards.

## 🎓 Student Dashboard

Displays:

* Total assignments
* Pending assignments
* Submitted assignments
* Late submissions
* Graded assignments
* Unread notifications
* Upcoming deadlines
* Recent feedback
* Assignment-status visualization

---

## 👩‍🏫 Teacher Dashboard

Displays:

* Number of assignments
* Number of students
* Total submissions
* Pending reviews
* Late submissions
* Graded submissions
* Recent uploads
* Upcoming deadlines
* Unread notifications

---

# 🗄️ Database Design

SQLite is used as the current database layer.

### Users

```text
users
├── id
├── username
├── name
├── role
├── password_hash
├── salt
└── created_at
```

### Courses

```text
courses
├── id
├── name
├── teacher_id
└── created_at
```

### Assignments

```text
assignments
├── id
├── course_id
├── title
├── description
├── deadline
├── max_marks
├── allowed_ext
├── max_mb
├── allow_late
├── allow_resubmit
├── created_by
└── created_at
```

### Submissions

```text
submissions
├── id
├── assignment_id
├── student_id
├── version
├── file_name
├── storage_path
├── file_hash
├── size
├── submitted_at
├── status
├── is_late
├── marks
├── feedback
├── graded_at
└── graded_by
```

### Notifications

```text
notifications
├── id
├── user_id
├── message
├── created_at
└── is_read
```

### Audit

```text
audit
├── id
├── user_id
├── action
├── detail
└── created_at
```

---

# 🏗️ System Architecture

```text
                         USER
                           │
              ┌────────────┴────────────┐
              │                         │
              ▼                         ▼
         🎓 Student                👩‍🏫 Teacher
              │                         │
              └────────────┬────────────┘
                           ▼
                  ┌─────────────────┐
                  │  Gradio Web UI  │
                  └────────┬────────┘
                           ▼
                  ┌─────────────────┐
                  │ Authentication  │
                  │    + RBAC       │
                  └────────┬────────┘
                           ▼
                  ┌─────────────────┐
                  │ Application     │
                  │ Logic           │
                  └──────┬─────┬────┘
                         │     │
               ┌─────────┘     └─────────┐
               ▼                         ▼
        ┌─────────────┐          ┌──────────────┐
        │   SQLite    │          │ ObjectStorage│
        │  Database   │          │   Simulation │
        └──────┬──────┘          └──────┬───────┘
               │                        │
               └────────────┬───────────┘
                            ▼
                   ┌─────────────────┐
                   │ Dashboards /    │
                   │ Analytics / CSV │
                   └─────────────────┘
```

---

# 🔄 End-to-End Workflow

## Student Workflow

```text
Register
   ↓
Login
   ↓
View Assignments
   ↓
Select Assignment
   ↓
Upload File
   ↓
Server Validation
   ↓
Deadline Check
   ↓
Hash / Duplicate Check
   ↓
Store Submission
   ↓
Receive Submission Receipt
   ↓
Teacher Reviews
   ↓
Marks + Feedback
   ↓
Student Notification
```

## Teacher Workflow

```text
Register / Login
      ↓
Create Course
      ↓
Create Assignment
      ↓
Configure Deadline & Rules
      ↓
Students Receive Notification
      ↓
Receive Submissions
      ↓
Review Files
      ↓
Grade Submission
      ↓
Provide Feedback
      ↓
Student Notified
      ↓
Export Gradebook
```

---

# 🛠️ Technology Stack

| Category            | Technology                      |
| ------------------- | ------------------------------- |
| Language            | Python                          |
| Platform            | Google Colab                    |
| UI Framework        | Gradio 6                        |
| Database            | SQLite                          |
| Data Processing     | Pandas                          |
| Visualization       | Matplotlib                      |
| Authentication      | PBKDF2 + Salt                   |
| File Integrity      | SHA-256                         |
| Similarity Analysis | TF-IDF + Cosine Similarity      |
| Storage             | Local ObjectStorage abstraction |
| Data Export         | CSV                             |
| Interface Styling   | HTML + CSS                      |

---

# ☁️ Cloud Computing Concepts Demonstrated

Although the project runs in Google Colab, it demonstrates several concepts used in cloud applications.

| Cloud Concept             | Project Implementation                      |
| ------------------------- | ------------------------------------------- |
| Client-server application | Gradio web interface + Python backend logic |
| Authentication            | PBKDF2-based credential verification        |
| Authorization             | Role-based access control                   |
| Cloud database pattern    | SQLite abstraction                          |
| Object storage pattern    | `ObjectStorage` abstraction                 |
| Data persistence          | SQLite                                      |
| File storage              | Private bucket-style directory              |
| Server-side validation    | File, size and deadline checks              |
| Auditability              | Audit log                                   |
| Notifications             | Database-backed notification system         |
| Analytics                 | Dashboard aggregation                       |
| Export                    | CSV gradebook                               |
| Scalability preparation   | Swappable storage/database architecture     |

---

# 🔒 Security Features

The implementation includes several security-oriented mechanisms:

### Password Security

Passwords are protected using salted PBKDF2 hashing.

### Role-Based Authorization

Teacher and student operations are explicitly separated.

### Ownership Checks

Teachers can operate on their own courses and assignments.

Students can access their own submissions.

### Server-Side Validation

The server checks:

* File extension
* File size
* Deadline
* Resubmission permissions
* Assignment ownership
* Grade limits

### Duplicate Protection

SHA-256 file hashes help detect repeated identical uploads.

### No Hardcoded Production Credentials

Configuration values are read through environment variables with demo-safe defaults.

---

# 📁 Project Runtime Structure

When executed in Google Colab, the application creates a structure similar to:

```text
/content/AssignmentPortal/
│
├── database/
│   └── portal.db
│
├── object_storage/
│   └── assignment-bucket/
│       └── assignments/
│           └── assignment_001/
│               └── student_002/
│
└── exports/
    ├── gradebook_assignment_1.csv
    └── ...
```

---

# ▶️ Running the Project

## Google Colab

### 1. Open Google Colab

```text
https://colab.research.google.com/
```

### 2. Create a new Python notebook

### 3. Copy the complete application into one cell

### 4. Run the cell

The notebook installs Gradio and launches the application.

### 5. Open the generated Gradio URL

The application is launched with public sharing enabled for demonstration.

---

# 👤 Demo Accounts

The notebook seeds dummy accounts on first run.

### Teacher

```text
Username: prof_rao
Password: Teach@123
Role: teacher
```

### Students

```text
Username: asha
Password: Stud@123
Role: student
```

```text
Username: ravi
Password: Stud@123
Role: student
```

### Teacher Registration

A teacher registration requires the configured invite code:

```text
TEACH-2026
```

These credentials are **demo-only** and should not be reused in a production deployment.

---

# 🧪 Testing Scenarios

Recommended validation scenarios include:

| Test                          | Expected Result                    |
| ----------------------------- | ---------------------------------- |
| Register student              | Account created                    |
| Duplicate username            | Registration rejected              |
| Valid login                   | User authenticated                 |
| Invalid login                 | Access rejected                    |
| Teacher creates course        | Course created                     |
| Teacher creates assignment    | Assignment created                 |
| Invalid deadline              | Assignment rejected                |
| Unsupported file              | Submission rejected                |
| Oversized file                | Submission rejected                |
| Late submission disabled      | Submission rejected                |
| Late submission enabled       | Submission marked `LATE`           |
| Resubmission enabled          | New version created                |
| Same file submitted again     | Duplicate prevented                |
| Student downloads own file    | Download allowed                   |
| Unauthorized download         | Access denied                      |
| Teacher grades own submission | Grade saved                        |
| Invalid marks                 | Grade rejected                     |
| Empty feedback                | Grade rejected                     |
| Similarity check              | Pairwise text similarity generated |
| Gradebook export              | CSV generated                      |
| Notifications                 | User receives event notification   |
| Logout                        | Session cleared                    |

---

# 📈 Scalability Roadmap

The current implementation is designed as a **cloud-ready prototype** rather than a production-scale deployment.

A future architecture could evolve into:

```text
                     Web Browser
                          │
                          ▼
                    React / Next.js
                          │
                          ▼
                    API Gateway
                          │
                          ▼
                   FastAPI / Flask
                    │      │      │
                    ▼      ▼      ▼
                 Auth   Database  Storage
                    │      │      │
                    └──────┼──────┘
                           ▼
                    Cloud Monitoring
```

Possible production replacements include:

* Firebase Authentication
* Firestore / PostgreSQL
* Amazon S3 / Google Cloud Storage
* FastAPI
* React / Next.js
* Cloud Run / AWS / Azure
* CDN
* Managed logging and monitoring
* Background queues for large workloads

---

# 🔮 Future Enhancements

Potential future improvements include:

* Real cloud database integration
* Real S3/GCS/Firebase Storage
* React-based frontend
* REST API layer
* Email notifications
* Push notifications
* Real-time submission updates
* Assignment search and filtering
* Rubric-based grading
* Inline document preview
* Advanced plagiarism detection
* OCR for scanned submissions
* Cloud deployment
* Automated backups
* CI/CD pipeline
* Teacher analytics
* Course-wise performance analytics
* Student performance history
* Automatic deadline reminders

---

# 📊 Project Advantages

### Centralized Workflow

Assignment management, submission, grading and feedback are available from one platform.

### Secure Access

Role-specific permissions reduce unauthorized actions.

### Version Control

Student resubmissions are preserved as separate versions.

### File Validation

Uploads are checked before being stored.

### Auditability

Important system actions are logged.

### Cloud-Ready Design

Database and object-storage abstractions make migration to managed cloud services easier.

### Data Visibility

Dashboards provide quick insight into assignments, submissions, deadlines and grading status.

---

# ⚠️ Current Limitations

The current version has some intentional prototype limitations:

* SQLite is used instead of a managed cloud database.
* Object storage is simulated using the Colab filesystem.
* Authentication is suitable for demonstration rather than production identity management.
* Gradio provides the frontend rather than a separate React application.
* The similarity checker is a basic TF-IDF/cosine-similarity implementation.
* Colab runtime persistence should not be treated as production storage.
* No real email or push-notification service is integrated.

These limitations provide a clear path toward converting the prototype into a deployable cloud application.

---

# 🎓 Learning Outcomes

This project provides practical experience with:

* Python web application development
* Gradio UI development
* Authentication
* Password hashing
* Role-Based Access Control
* SQLite database design
* CRUD operations
* File upload handling
* Object-storage architecture
* Server-side validation
* Deadline management
* Version control concepts
* Hash-based duplicate detection
* Grading workflows
* Notification systems
* Audit logging
* Data visualization
* TF-IDF and cosine similarity
* CSV export
* Cloud application architecture

---

# 📸 Recommended Screenshots

For a GitHub project showcase, capture:

```text
screenshots/
├── 01_login.png
├── 02_student_dashboard.png
├── 03_teacher_dashboard.png
├── 04_create_assignment.png
├── 05_assignment_submission.png
├── 06_submission_receipt.png
├── 07_grading_feedback.png
├── 08_notifications.png
├── 09_similarity_check.png
├── 10_gradebook_export.png
└── 11_colab_runtime.png
```

The most useful screenshots for recruiters are:

* Student dashboard
* Teacher dashboard
* Assignment creation
* Submission receipt
* Grading and feedback
* Similarity analysis
* Cloud-storage directory
* Gradebook CSV output

---

# 💼 Resume Project Description

**Cloud-Based Student Assignment Submission & Feedback Portal**
Developed a role-based academic portal using Python, Gradio, SQLite and local object-storage abstraction, supporting secure authentication, assignment management, validated submissions, version tracking, grading, feedback, notifications, similarity analysis and analytics.

---

# 🧑‍💻 Suggested GitHub Repository Description

```text
Cloud-ready student assignment portal with role-based authentication, file submissions, versioning, grading, feedback, notifications, analytics, and object-storage simulation using Python and Gradio.
```

---

# 🏷️ Suggested GitHub Topics

```text
cloud-computing
python
gradio
sqlite
student-portal
assignment-management
file-upload
authentication
rbac
cloud-storage
database
web-application
data-visualization
tfidf
cosine-similarity
google-colab
academic-portal
```

---

# 📜 Disclaimer

This project is an **educational cloud-computing and software-development prototype**.

The current implementation uses Google Colab, SQLite, and a local object-storage abstraction to simulate components that can later be replaced with managed cloud services.

Demo credentials and sample data are for demonstration purposes only.

---

# 👨‍💻 Author

**Debankita Panja**

GitHub: `https://github.com/dp2005-lang`

LinkedIn: `https://www.linkedin.com/in/debankita-8482a2403/`

---

# ⭐ Project Summary

The **Cloud-Based Student Assignment Submission & Feedback Portal** demonstrates how a traditional academic assignment workflow can be transformed into a structured digital platform.

The complete core workflow is:

```text
Authentication
      ↓
Course Creation
      ↓
Assignment Creation
      ↓
Student Submission
      ↓
Validation + Versioning
      ↓
Secure File Storage
      ↓
Teacher Review
      ↓
Grading + Feedback
      ↓
Notifications
      ↓
Analytics + Export
```

The project combines **web application development, database management, authentication, authorization, file storage, data analytics, and cloud architecture concepts** in a single Google Colab-based implementation.
