# 05 - Database Design

## Project Name
**Lunetron EdTech Platform**

**Version:** 1.0  
**Database:** PostgreSQL 16+  
**ORM:** Django ORM  
**Last Updated:** July 2026

---

# 1. Introduction

This document defines the logical database design for the Lunetron EdTech Platform. The schema supports authentication, course management, learning, payments, quizzes, assignments, certificates, blogs, notifications, analytics, and role-based access control.

---

# 2. Database Overview

## Database Engine

- PostgreSQL
- UTF-8 Encoding
- ACID Compliant
- Daily Backups
- Read Replicas (Future)
- Redis for Caching

---

# 3. Entity Relationship Overview

```
User
 ├── Student Profile
 ├── Instructor Profile
 ├── Admin Profile
 ├── Notifications
 ├── Enrollments
 ├── Payments
 ├── Wishlist
 ├── Reviews
 ├── Certificates
 └── Orders

Course
 ├── Sections
 │     └── Lessons
 ├── Assignments
 ├── Quizzes
 ├── Resources
 ├── Reviews
 └── Enrollments

Quiz
 ├── Questions
 └── Attempts

Assignment
 └── Submissions

Order
 └── Payment

Course
 └── Category
```

---

# 4. Users Table

| Column | Type | Constraints |
|---------|------|-------------|
| id | UUID | PK |
| first_name | VARCHAR(100) | NOT NULL |
| last_name | VARCHAR(100) | |
| email | VARCHAR(255) | UNIQUE |
| password | VARCHAR(255) | HASHED |
| phone | VARCHAR(20) | UNIQUE |
| role | ENUM | Student, Instructor, Admin, SuperAdmin |
| profile_image | TEXT | |
| is_active | BOOLEAN | DEFAULT TRUE |
| is_verified | BOOLEAN | DEFAULT FALSE |
| last_login | TIMESTAMP | |
| created_at | TIMESTAMP | |
| updated_at | TIMESTAMP | |

---

# 5. Student Profile

| Column | Type |
|---------|------|
| id | UUID |
| user_id | FK(User) |
| education | VARCHAR |
| date_of_birth | DATE |
| gender | VARCHAR |
| bio | TEXT |

---

# 6. Instructor Profile

| Column | Type |
|---------|------|
| id | UUID |
| user_id | FK(User) |
| qualification | VARCHAR |
| experience | INTEGER |
| specialization | VARCHAR |
| expertise | TEXT |
| linkedin_url | TEXT |
| website | TEXT |

---

# 7. Categories

| Column | Type |
|---------|------|
| id | UUID |
| name | VARCHAR |
| slug | VARCHAR UNIQUE |
| description | TEXT |
| image | TEXT |
| created_at | TIMESTAMP |

---

# 8. Courses

| Column | Type |
|---------|------|
| id | UUID |
| instructor_id | FK(User) |
| category_id | FK(Category) |
| title | VARCHAR |
| slug | VARCHAR UNIQUE |
| short_description | TEXT |
| description | TEXT |
| thumbnail | TEXT |
| language | VARCHAR |
| level | ENUM |
| duration | INTEGER |
| price | DECIMAL |
| discount_price | DECIMAL |
| is_free | BOOLEAN |
| status | ENUM(Draft, Pending, Published, Rejected) |
| rating | DECIMAL |
| total_students | INTEGER |
| created_at | TIMESTAMP |
| updated_at | TIMESTAMP |

---

# 9. Course Sections

| Column | Type |
|---------|------|
| id | UUID |
| course_id | FK(Course) |
| title | VARCHAR |
| position | INTEGER |

---

# 10. Lessons

| Column | Type |
|---------|------|
| id | UUID |
| section_id | FK(Section) |
| title | VARCHAR |
| video_url | TEXT |
| duration | INTEGER |
| lesson_type | ENUM(Video, PDF, Article, Live) |
| is_preview | BOOLEAN |
| position | INTEGER |

---

# 11. Course Resources

| Column | Type |
|---------|------|
| id | UUID |
| lesson_id | FK(Lesson) |
| file_name | VARCHAR |
| file_url | TEXT |
| file_type | VARCHAR |

---

# 12. Enrollments

| Column | Type |
|---------|------|
| id | UUID |
| student_id | FK(User) |
| course_id | FK(Course) |
| progress | DECIMAL |
| enrolled_at | TIMESTAMP |
| completed_at | TIMESTAMP |

---

# 13. Wishlist

| Column | Type |
|---------|------|
| id | UUID |
| student_id | FK(User) |
| course_id | FK(Course) |

---

# 14. Assignments

| Column | Type |
|---------|------|
| id | UUID |
| course_id | FK(Course) |
| lesson_id | FK(Lesson) |
| title | VARCHAR |
| description | TEXT |
| due_date | TIMESTAMP |
| total_marks | INTEGER |

---

# 15. Assignment Submissions

| Column | Type |
|---------|------|
| id | UUID |
| assignment_id | FK(Assignment) |
| student_id | FK(User) |
| file_url | TEXT |
| submitted_at | TIMESTAMP |
| marks | DECIMAL |
| feedback | TEXT |
| status | ENUM |

---

# 16. Quizzes

| Column | Type |
|---------|------|
| id | UUID |
| course_id | FK(Course) |
| title | VARCHAR |
| passing_marks | INTEGER |
| duration | INTEGER |
| total_marks | INTEGER |

---

# 17. Quiz Questions

| Column | Type |
|---------|------|
| id | UUID |
| quiz_id | FK(Quiz) |
| question | TEXT |
| question_type | ENUM |
| option_a | TEXT |
| option_b | TEXT |
| option_c | TEXT |
| option_d | TEXT |
| correct_answer | VARCHAR |
| marks | INTEGER |

---

# 18. Quiz Attempts

| Column | Type |
|---------|------|
| id | UUID |
| quiz_id | FK(Quiz) |
| student_id | FK(User) |
| score | INTEGER |
| started_at | TIMESTAMP |
| completed_at | TIMESTAMP |

---

# 19. Reviews

| Column | Type |
|---------|------|
| id | UUID |
| course_id | FK(Course) |
| student_id | FK(User) |
| rating | INTEGER |
| review | TEXT |
| created_at | TIMESTAMP |

---

# 20. Orders

| Column | Type |
|---------|------|
| id | UUID |
| student_id | FK(User) |
| total_amount | DECIMAL |
| discount | DECIMAL |
| tax | DECIMAL |
| grand_total | DECIMAL |
| order_status | ENUM |
| created_at | TIMESTAMP |

---

# 21. Payments

| Column | Type |
|---------|------|
| id | UUID |
| order_id | FK(Order) |
| transaction_id | VARCHAR |
| gateway | VARCHAR |
| payment_status | ENUM |
| amount | DECIMAL |
| paid_at | TIMESTAMP |

---

# 22. Coupons

| Column | Type |
|---------|------|
| id | UUID |
| code | VARCHAR UNIQUE |
| discount_type | ENUM(Flat, Percentage) |
| value | DECIMAL |
| expiry_date | DATE |
| usage_limit | INTEGER |

---

# 23. Certificates

| Column | Type |
|---------|------|
| id | UUID |
| student_id | FK(User) |
| course_id | FK(Course) |
| certificate_number | VARCHAR UNIQUE |
| issue_date | DATE |
| certificate_url | TEXT |

---

# 24. Blogs

| Column | Type |
|---------|------|
| id | UUID |
| author_id | FK(User) |
| title | VARCHAR |
| slug | VARCHAR UNIQUE |
| content | TEXT |
| cover_image | TEXT |
| published_at | TIMESTAMP |

---

# 25. Notifications

| Column | Type |
|---------|------|
| id | UUID |
| user_id | FK(User) |
| title | VARCHAR |
| message | TEXT |
| notification_type | ENUM |
| is_read | BOOLEAN |
| created_at | TIMESTAMP |

---

# 26. Audit Logs

| Column | Type |
|---------|------|
| id | UUID |
| user_id | FK(User) |
| action | VARCHAR |
| entity | VARCHAR |
| entity_id | UUID |
| ip_address | VARCHAR |
| created_at | TIMESTAMP |

---

# 27. Indexing Strategy

Create indexes on:

- email
- phone
- course_id
- student_id
- instructor_id
- category_id
- slug
- created_at
- payment_status
- transaction_id

Use composite indexes where appropriate, for example:

- (student_id, course_id)
- (course_id, rating)
- (quiz_id, student_id)

---

# 28. Constraints

- Primary keys use UUID.
- Foreign keys enforce referential integrity.
- Email, phone, coupon code, certificate number, and slugs must be unique.
- Course price cannot be negative.
- Ratings must be between 1 and 5.
- Progress must be between 0 and 100.
- Deleting a course should cascade to sections, lessons, assignments, and quizzes.
- Deleting a user should preserve financial records where required by business rules.

---

# 29. Database Relationships

| Parent | Child | Relationship |
|---------|-------|--------------|
| User | Student Profile | 1 : 1 |
| User | Instructor Profile | 1 : 1 |
| User | Courses | 1 : N |
| Category | Courses | 1 : N |
| Course | Sections | 1 : N |
| Section | Lessons | 1 : N |
| Lesson | Resources | 1 : N |
| Course | Enrollments | 1 : N |
| User | Enrollments | 1 : N |
| Course | Assignments | 1 : N |
| Assignment | Submissions | 1 : N |
| Course | Quizzes | 1 : N |
| Quiz | Questions | 1 : N |
| Quiz | Attempts | 1 : N |
| Course | Reviews | 1 : N |
| Order | Payment | 1 : 1 |
| User | Notifications | 1 : N |

---

# 30. Future Enhancements

- Multi-instructor courses
- Learning paths
- Course bundles
- Affiliate management
- Subscription plans
- Organization/Enterprise accounts
- AI-generated learning analytics
- Multi-tenant architecture

---

# 31. Database Standards

- UUID primary keys
- UTC timestamps
- Soft delete for selected entities
- Optimistic locking where needed
- Audit logging for critical operations
- Transactional consistency for payments and enrollments
- Migration-driven schema changes
- Naming convention:
  - Tables: `snake_case`
  - Columns: `snake_case`
  - Foreign keys: `<table_name>_id`
  - Indexes: `idx_<table>_<column>`

---

# Document Approval

**Prepared By:** Lunetron Development Team

**Reviewed By:** Database Architect

**Approved By:** Technical Lead

**Version:** 1.0