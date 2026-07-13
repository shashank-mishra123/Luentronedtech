# 06 - API Design

## Project Name
**Lunetron EdTech Platform**

**Version:** 1.0  
**API Version:** v1  
**Architecture:** REST API  
**Framework:** Django REST Framework (DRF)  
**Authentication:** JWT + Refresh Token  
**Database:** PostgreSQL  
**Content-Type:** application/json

---

# 1. Introduction

This document defines the REST API design for the Lunetron EdTech Platform. The API follows RESTful principles and provides secure, scalable endpoints for web and mobile applications.

---

# 2. Base URL

```
Development
http://localhost:8000/api/v1/

Staging
https://staging-api.lunetron.com/api/v1/

Production
https://api.lunetron.com/api/v1/
```

---

# 3. Authentication

Authentication Method

```
JWT Bearer Token
```

Header

```
Authorization: Bearer <access_token>
```

Protected endpoints require a valid access token.

---

# 4. API Versioning

```
/api/v1/
/api/v2/
```

Future versions must maintain backward compatibility where possible.

---

# 5. Standard HTTP Methods

| Method | Purpose |
|----------|---------|
| GET | Retrieve resource(s) |
| POST | Create resource |
| PUT | Replace resource |
| PATCH | Partially update resource |
| DELETE | Delete resource |

---

# 6. Authentication APIs

## Register

```
POST /auth/register
```

Request

```json
{
  "first_name": "John",
  "last_name": "Doe",
  "email": "john@example.com",
  "password": "StrongPassword@123",
  "role": "student"
}
```

Response

```json
{
  "message": "Registration successful. Verify your email."
}
```

---

## Login

```
POST /auth/login
```

Request

```json
{
  "email": "john@example.com",
  "password": "StrongPassword@123"
}
```

Response

```json
{
  "access_token": "...",
  "refresh_token": "...",
  "user": {
    "id": "...",
    "role": "student"
  }
}
```

---

## Refresh Token

```
POST /auth/refresh
```

---

## Logout

```
POST /auth/logout
```

---

## Forgot Password

```
POST /auth/forgot-password
```

---

## Reset Password

```
POST /auth/reset-password
```

---

# 7. User APIs

```
GET    /users/me
PATCH  /users/me
DELETE /users/me
GET    /users/{id}
GET    /users
```

Admin only:

```
POST   /users
PATCH  /users/{id}
DELETE /users/{id}
```

---

# 8. Categories APIs

```
GET    /categories
GET    /categories/{id}
POST   /categories
PATCH  /categories/{id}
DELETE /categories/{id}
```

---

# 9. Course APIs

```
GET    /courses
GET    /courses/{id}
POST   /courses
PATCH  /courses/{id}
DELETE /courses/{id}
```

Query Parameters

```
?page=1
&page_size=20
&category=python
&level=beginner
&price=free
&search=django
&ordering=rating
```

---

# 10. Course Sections

```
GET
POST
PATCH
DELETE

/courses/{course_id}/sections
```

---

# 11. Lessons

```
GET
POST
PATCH
DELETE

/sections/{section_id}/lessons
```

---

# 12. Resources

```
GET
POST
DELETE

/lessons/{lesson_id}/resources
```

---

# 13. Enrollment APIs

Enroll

```
POST /courses/{course_id}/enroll
```

My Courses

```
GET /students/me/courses
```

Course Progress

```
GET /courses/{course_id}/progress
```

---

# 14. Assignment APIs

```
GET    /assignments
GET    /assignments/{id}
POST   /assignments
PATCH  /assignments/{id}
DELETE /assignments/{id}
```

Submit Assignment

```
POST /assignments/{id}/submit
```

Grade Assignment

```
POST /assignments/{id}/grade
```

---

# 15. Quiz APIs

```
GET    /quizzes
GET    /quizzes/{id}
POST   /quizzes
PATCH  /quizzes/{id}
DELETE /quizzes/{id}
```

Start Quiz

```
POST /quizzes/{id}/start
```

Submit Quiz

```
POST /quizzes/{id}/submit
```

Quiz Result

```
GET /quizzes/{id}/result
```

---

# 16. Wishlist APIs

```
GET    /wishlist
POST   /wishlist
DELETE /wishlist/{course_id}
```

---

# 17. Cart APIs

```
GET    /cart
POST   /cart
PATCH  /cart
DELETE /cart/{course_id}
```

---

# 18. Order APIs

```
GET    /orders
GET    /orders/{id}
POST   /orders
```

---

# 19. Payment APIs

Create Payment

```
POST /payments/create
```

Verify Payment

```
POST /payments/verify
```

Payment History

```
GET /payments
```

Invoice

```
GET /payments/{id}/invoice
```

---

# 20. Coupon APIs

```
GET /coupons

POST /coupons

PATCH /coupons/{id}

DELETE /coupons/{id}

POST /coupons/apply
```

---

# 21. Certificate APIs

```
GET /certificates

GET /certificates/{id}

GET /certificates/download/{id}

GET /certificates/verify/{certificate_number}
```

---

# 22. Review APIs

```
GET /courses/{id}/reviews

POST /courses/{id}/reviews

PATCH /reviews/{id}

DELETE /reviews/{id}
```

---

# 23. Blog APIs

```
GET /blogs

GET /blogs/{slug}

POST /blogs

PATCH /blogs/{id}

DELETE /blogs/{id}
```

---

# 24. Notification APIs

```
GET /notifications

PATCH /notifications/{id}/read

PATCH /notifications/read-all
```

---

# 25. Live Class APIs

```
GET /live-classes

POST /live-classes

PATCH /live-classes/{id}

DELETE /live-classes/{id}

POST /live-classes/{id}/join
```

---

# 26. AI APIs

AI Tutor

```
POST /ai/chat
```

Generate Notes

```
POST /ai/notes
```

Generate Quiz

```
POST /ai/quiz
```

Summarize Lesson

```
POST /ai/summarize
```

Translate Content

```
POST /ai/translate
```

Learning Recommendations

```
GET /ai/recommendations
```

---

# 27. Admin APIs

```
GET /admin/dashboard

GET /admin/users

GET /admin/courses

GET /admin/payments

GET /admin/reports

GET /admin/analytics
```

---

# 28. Search APIs

```
GET /search

Example

/search?q=python
```

Advanced Search

```
GET /courses?search=django&category=backend&level=advanced
```

---

# 29. Upload APIs

```
POST /upload/image

POST /upload/video

POST /upload/document
```

Supported file types:

- JPEG
- PNG
- PDF
- DOCX
- MP4
- ZIP

---

# 30. Standard Success Response

```json
{
  "success": true,
  "message": "Operation completed successfully.",
  "data": {}
}
```

---

# 31. Standard Error Response

```json
{
  "success": false,
  "message": "Validation failed.",
  "errors": {
    "email": [
      "This field is required."
    ]
  }
}
```

---

# 32. HTTP Status Codes

| Code | Meaning |
|------|---------|
| 200 | OK |
| 201 | Created |
| 204 | No Content |
| 400 | Bad Request |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |
| 409 | Conflict |
| 422 | Validation Error |
| 429 | Too Many Requests |
| 500 | Internal Server Error |

---

# 33. Pagination

Example

```
GET /courses?page=2&page_size=20
```

Response

```json
{
  "count": 250,
  "next": "...",
  "previous": "...",
  "results": []
}
```

---

# 34. Filtering & Sorting

Supported query parameters:

```
?search=python
?category=backend
?level=beginner
?language=english
?price=free
?rating=4
?ordering=-created_at
```

---

# 35. Rate Limiting

Recommended limits:

| Endpoint | Limit |
|----------|-------|
| Login | 5 requests/minute/IP |
| Register | 3 requests/minute/IP |
| Password Reset | 3 requests/15 minutes |
| AI APIs | 30 requests/hour/user |
| General API | 100 requests/minute/user |

---

# 36. Security

- HTTPS only
- JWT Authentication
- Role-Based Access Control (RBAC)
- Input validation
- Output sanitization
- CORS configuration
- CSRF protection (where applicable)
- SQL Injection protection
- XSS protection
- Secure file upload validation
- Audit logging

---

# 37. API Documentation

The API should expose interactive documentation:

- Swagger UI
- OpenAPI 3.0 Specification
- ReDoc

Documentation should include:

- Request examples
- Response examples
- Authentication requirements
- Error codes
- Endpoint descriptions

---

# 38. API Lifecycle

```
Client
   │
   ▼
API Gateway / Nginx
   │
   ▼
Authentication Middleware
   │
   ▼
Permission Check
   │
   ▼
Serializer Validation
   │
   ▼
Business Logic (Service Layer)
   │
   ▼
Django ORM
   │
   ▼
PostgreSQL
   │
   ▼
JSON Response
```

---

# 39. Naming Conventions

- Use plural resource names (`/courses`, `/users`).
- Use kebab-case for multi-word endpoints (`/forgot-password`).
- Use nouns instead of verbs where practical.
- Keep URLs lowercase.
- Version APIs under `/api/v1/`.

---

# 40. Production Checklist

- JWT authentication enabled
- RBAC enforced
- Input validation completed
- Pagination implemented
- Filtering and sorting supported
- Rate limiting configured
- OpenAPI documentation published
- Centralized logging enabled
- Monitoring and metrics integrated
- Automated API tests passing

---

# Document Approval

**Prepared By:** Lunetron Development Team

**Reviewed By:** Backend Architect

**Approved By:** Technical Lead

**Version:** 1.0