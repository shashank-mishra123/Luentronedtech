# ER Diagram

## Project Name
**Lunetron EdTech Platform**

**Version:** 1.0  
**Database:** PostgreSQL  
**ORM:** Django ORM

---

# 1. Overview

This Entity Relationship Diagram (ERD) represents the database structure of the Lunetron EdTech Platform.

Primary modules include:

- User Management
- Course Management
- Learning
- Assignments
- Quizzes
- Payments
- Certificates
- Reviews
- Notifications
- Blogs

---

# 2. Entity Relationship Diagram (Mermaid)

```mermaid
erDiagram

    USERS {
        UUID id PK
        string first_name
        string last_name
        string email
        string password
        string phone
        string role
        boolean is_active
        boolean is_verified
        datetime created_at
    }

    STUDENT_PROFILE {
        UUID id PK
        UUID user_id FK
        string education
        date dob
        string gender
    }

    INSTRUCTOR_PROFILE {
        UUID id PK
        UUID user_id FK
        string qualification
        int experience
        string specialization
    }

    CATEGORY {
        UUID id PK
        string name
        string slug
    }

    COURSE {
        UUID id PK
        UUID instructor_id FK
        UUID category_id FK
        string title
        decimal price
        string level
        string status
    }

    SECTION {
        UUID id PK
        UUID course_id FK
        string title
        int position
    }

    LESSON {
        UUID id PK
        UUID section_id FK
        string title
        string video_url
        int duration
    }

    RESOURCE {
        UUID id PK
        UUID lesson_id FK
        string file_url
        string file_type
    }

    ENROLLMENT {
        UUID id PK
        UUID student_id FK
        UUID course_id FK
        decimal progress
    }

    ASSIGNMENT {
        UUID id PK
        UUID course_id FK
        string title
        datetime due_date
    }

    ASSIGNMENT_SUBMISSION {
        UUID id PK
        UUID assignment_id FK
        UUID student_id FK
        decimal marks
        string status
    }

    QUIZ {
        UUID id PK
        UUID course_id FK
        string title
        int total_marks
    }

    QUESTION {
        UUID id PK
        UUID quiz_id FK
        string question
        string answer
    }

    QUIZ_ATTEMPT {
        UUID id PK
        UUID quiz_id FK
        UUID student_id FK
        decimal score
    }

    REVIEW {
        UUID id PK
        UUID course_id FK
        UUID student_id FK
        int rating
    }

    WISHLIST {
        UUID id PK
        UUID student_id FK
        UUID course_id FK
    }

    ORDER {
        UUID id PK
        UUID student_id FK
        decimal total
        string status
    }

    PAYMENT {
        UUID id PK
        UUID order_id FK
        decimal amount
        string gateway
        string payment_status
    }

    CERTIFICATE {
        UUID id PK
        UUID student_id FK
        UUID course_id FK
        string certificate_no
    }

    BLOG {
        UUID id PK
        UUID author_id FK
        string title
    }

    NOTIFICATION {
        UUID id PK
        UUID user_id FK
        string title
        boolean is_read
    }

    USERS ||--|| STUDENT_PROFILE : has
    USERS ||--|| INSTRUCTOR_PROFILE : has

    USERS ||--o{ COURSE : creates
    CATEGORY ||--o{ COURSE : contains

    COURSE ||--o{ SECTION : has
    SECTION ||--o{ LESSON : contains
    LESSON ||--o{ RESOURCE : has

    USERS ||--o{ ENROLLMENT : enrolls
    COURSE ||--o{ ENROLLMENT : includes

    COURSE ||--o{ ASSIGNMENT : has
    ASSIGNMENT ||--o{ ASSIGNMENT_SUBMISSION : receives
    USERS ||--o{ ASSIGNMENT_SUBMISSION : submits

    COURSE ||--o{ QUIZ : has
    QUIZ ||--o{ QUESTION : contains
    QUIZ ||--o{ QUIZ_ATTEMPT : records
    USERS ||--o{ QUIZ_ATTEMPT : attempts

    COURSE ||--o{ REVIEW : receives
    USERS ||--o{ REVIEW : writes

    USERS ||--o{ WISHLIST : owns
    COURSE ||--o{ WISHLIST : saved_in

    USERS ||--o{ ORDER : places
    ORDER ||--|| PAYMENT : paid_by

    USERS ||--o{ CERTIFICATE : receives
    COURSE ||--o{ CERTIFICATE : awards

    USERS ||--o{ BLOG : writes
    USERS ||--o{ NOTIFICATION : receives
```

---

# 3. Relationship Summary

| Parent Entity | Child Entity | Relationship |
|---------------|-------------|--------------|
| User | Student Profile | 1 : 1 |
| User | Instructor Profile | 1 : 1 |
| User | Course | 1 : N |
| Category | Course | 1 : N |
| Course | Section | 1 : N |
| Section | Lesson | 1 : N |
| Lesson | Resource | 1 : N |
| User | Enrollment | 1 : N |
| Course | Enrollment | 1 : N |
| Course | Assignment | 1 : N |
| Assignment | Assignment Submission | 1 : N |
| User | Assignment Submission | 1 : N |
| Course | Quiz | 1 : N |
| Quiz | Question | 1 : N |
| Quiz | Quiz Attempt | 1 : N |
| User | Quiz Attempt | 1 : N |
| Course | Review | 1 : N |
| User | Review | 1 : N |
| User | Wishlist | 1 : N |
| Course | Wishlist | 1 : N |
| User | Order | 1 : N |
| Order | Payment | 1 : 1 |
| User | Certificate | 1 : N |
| Course | Certificate | 1 : N |
| User | Blog | 1 : N |
| User | Notification | 1 : N |

---

# 4. Design Principles

- UUID used as the primary key for all tables.
- Foreign keys enforce referential integrity.
- PostgreSQL constraints ensure data consistency.
- Indexed columns improve query performance.
- Designed for scalability with Django ORM.
- Supports Role-Based Access Control (RBAC).
- Optimized for REST API development.

---

# 5. Future Extensions

Additional entities can be introduced without major schema changes:

- Live Classes
- Chat & Messaging
- Discussion Forum
- AI Tutor Conversations
- Learning Paths
- Course Bundles
- Subscription Plans
- Organizations
- Affiliate System
- Gamification (Badges, Points, Leaderboards)

---

# Document Approval

**Prepared By:** Lunetron Development Team

**Reviewed By:** Database Architect

**Approved By:** Technical Lead

**Version:** 1.0