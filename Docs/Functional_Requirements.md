# 03 - Functional Requirements

## Project Name
**Lunetron EdTech Platform**

---

# 1. Introduction

This document defines the functional requirements for the Lunetron EdTech Platform. It describes the features that the application must provide to users and administrators.

---

# 2. User Roles

The system supports the following roles:

- Guest
- Student
- Instructor
- Admin
- Super Admin

---

# 3. Authentication Module

### User Registration
- User can register using email.
- User can register using Google Authentication.
- Email verification is required.
- Strong password validation.
- Duplicate email is not allowed.

### User Login
- Email and Password login.
- Google Login.
- Remember Me.
- Forgot Password.
- Reset Password.
- JWT Authentication.
- Refresh Token.

### User Logout
- Logout from current device.
- Logout from all devices.

---

# 4. User Profile

Users can:

- View profile
- Update profile
- Upload profile picture
- Change password
- Manage notification settings
- Manage privacy settings

---

# 5. Course Module

Students can:

- Browse courses
- Search courses
- Filter by category
- Filter by instructor
- Filter by level
- View course details
- Add to wishlist
- Purchase course
- Enroll in free course
- Continue learning
- Track progress
- Rate course
- Review course

Instructors can:

- Create course
- Edit course
- Delete own course
- Upload thumbnail
- Upload videos
- Upload PDFs
- Upload assignments
- Publish course
- Unpublish course

Admins can:

- Approve courses
- Reject courses
- Remove inappropriate courses

---

# 6. Learning Module

Students can:

- Watch videos
- Resume from last watched position
- Download resources
- Take notes
- Bookmark lessons
- Complete lessons
- View progress
- Receive completion certificate

---

# 7. Assignment Module

Instructor can:

- Create assignment
- Upload assignment files
- Set deadline
- Define marks

Student can:

- Submit assignment
- Upload solution
- View submission status

Instructor can:

- Evaluate submission
- Give marks
- Give feedback

---

# 8. Quiz Module

Instructor can:

- Create quizzes
- Add MCQs
- Add True/False questions
- Add descriptive questions
- Set timer
- Set passing marks

Student can:

- Attempt quiz
- View score
- Review answers

---

# 9. Certificate Module

Students can:

- Download certificate
- Share certificate
- Verify certificate

Admin can:

- Configure certificate template

---

# 10. Payment Module

Students can:

- Purchase courses
- Apply coupon
- View payment history
- Download invoice

Supported Payment Methods

- Razorpay
- Stripe
- PayPal
- UPI
- Credit Card
- Debit Card
- Net Banking

Admin can:

- Refund payment
- View transactions

---

# 11. Wishlist Module

Students can:

- Add course
- Remove course
- Move wishlist to cart

---

# 12. Shopping Cart

Students can:

- Add multiple courses
- Remove course
- Update cart
- Apply coupon
- Checkout

---

# 13. Live Classes

Instructor can:

- Schedule class
- Edit class
- Cancel class
- Upload recordings

Students can:

- Join class
- View recordings
- Receive reminders

---

# 14. Discussion Forum

Students can:

- Ask questions
- Reply to questions
- Like answers
- Report inappropriate content

Instructor can:

- Answer questions
- Pin answers
- Delete spam

---

# 15. Notification Module

Notifications via:

- Email
- SMS (optional)
- Push Notifications
- In-App Notifications

Events include:

- Course enrollment
- Payment success
- Assignment deadline
- Quiz result
- Live class reminder
- Certificate issued

---

# 16. Search Module

Users can:

- Search by course title
- Search by instructor
- Search by category
- Search by tags

Filters:

- Price
- Rating
- Level
- Duration
- Language

---

# 17. Dashboard

### Student Dashboard

- Enrolled courses
- Progress overview
- Upcoming assignments
- Certificates
- Wishlist
- Payment history

### Instructor Dashboard

- Total students
- Revenue
- Course analytics
- Reviews
- Pending assignments

### Admin Dashboard

- Total users
- Total instructors
- Total students
- Total courses
- Revenue reports
- Active subscriptions
- Pending approvals

---

# 18. Admin Management

Admin can:

- Manage users
- Manage instructors
- Manage categories
- Manage banners
- Manage FAQs
- Manage blogs
- Manage testimonials
- Manage coupons
- Manage payments
- Manage certificates

---

# 19. Blog Module

Admin/Instructor can:

- Create blog
- Edit blog
- Delete blog
- Publish blog
- Schedule blog

Users can:

- Read blog
- Like blog
- Comment

---

# 20. Reviews & Ratings

Students can:

- Give ratings (1–5 stars)
- Write reviews
- Edit reviews
- Delete reviews

Admins can:

- Moderate reviews

---

# 21. AI Features

Students can:

- Chat with AI Tutor
- Generate study notes
- Generate quizzes
- Summarize lectures
- Translate content
- Get coding assistance
- Receive personalized learning recommendations

---

# 22. Analytics

Track:

- Course completion rate
- Student engagement
- Quiz performance
- Assignment completion
- Revenue
- Instructor performance

---

# 23. Reports

Admin can generate:

- User reports
- Revenue reports
- Course reports
- Payment reports
- Instructor reports
- Student performance reports

---

# 24. Security

- JWT Authentication
- Role-Based Access Control (RBAC)
- Password hashing
- Email verification
- Two-Factor Authentication (optional)
- Session management
- Audit logs
- CSRF protection
- XSS protection
- SQL injection prevention
- API rate limiting

---

# 25. API Requirements

REST APIs for:

- Authentication
- Users
- Courses
- Lessons
- Assignments
- Quizzes
- Payments
- Certificates
- Notifications
- Blogs
- Reviews
- Analytics

---

# 26. Functional Summary

| Module | Status |
|----------|--------|
| Authentication | ✅ |
| User Management | ✅ |
| Course Management | ✅ |
| Learning | ✅ |
| Assignment | ✅ |
| Quiz | ✅ |
| Certificates | ✅ |
| Payments | ✅ |
| Wishlist | ✅ |
| Cart | ✅ |
| Live Classes | ✅ |
| Discussion Forum | ✅ |
| Notifications | ✅ |
| Blog | ✅ |
| Reviews | ✅ |
| AI Tutor | ✅ |
| Analytics | ✅ |
| Reports | ✅ |
| Security | ✅ |
| REST APIs | ✅ |

---

# Version

**Version:** 1.0

**Document Owner:** Lunetron EdTech Development Team

**Last Updated:** July 2026