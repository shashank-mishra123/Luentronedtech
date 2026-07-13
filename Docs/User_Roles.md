# User Roles

## Overview

This document defines the different user roles available in the application and their permissions.

---

## 1. Super Admin

### Description
Has complete control over the system.

### Permissions
- Manage all users
- Create, update, and delete courses
- Manage instructors
- Manage students
- View analytics and reports
- Manage payments
- Configure system settings

---

## 2. Admin

### Description
Manages the day-to-day operations.

### Permissions
- Manage students
- Manage instructors
- Approve courses
- View reports
- Handle support requests

---

## 3. Instructor

### Description
Creates and manages educational content.

### Permissions
- Create courses
- Upload videos
- Upload study materials
- Create quizzes
- Grade assignments
- View enrolled students

---

## 4. Student

### Description
Learns through the platform.

### Permissions
- Register and log in
- Enroll in courses
- Watch lectures
- Download resources
- Submit assignments
- Take quizzes
- View certificates

---

## 5. Guest

### Description
A visitor who has not registered.

### Permissions
- Browse public courses
- View landing pages
- Register/Login

---

# Permission Matrix

| Feature | Super Admin | Admin | Instructor | Student | Guest |
|----------|------------|-------|------------|---------|-------|
| Manage Users | ✅ | ✅ | ❌ | ❌ | ❌ |
| Create Courses | ✅ | ✅ | ✅ | ❌ | ❌ |
| Edit Courses | ✅ | ✅ | ✅ | ❌ | ❌ |
| Delete Courses | ✅ | ✅ | ❌ | ❌ | ❌ |
| Enroll in Course | ❌ | ❌ | ❌ | ✅ | ❌ |
| Watch Videos | ✅ | ✅ | ✅ | ✅ | ❌ |
| Submit Assignment | ❌ | ❌ | ❌ | ✅ | ❌ |
| View Analytics | ✅ | ✅ | Limited | ❌ | ❌ |
| Manage Payments | ✅ | ✅ | ❌ | ❌ | ❌ |
| Download Certificate | ❌ | ❌ | ❌ | ✅ | ❌ |

---

# Notes

- Super Admin has full system access.
- Admin manages platform operations.
- Instructor manages learning content.
- Student consumes learning content.
- Guest has read-only access to public resources.
