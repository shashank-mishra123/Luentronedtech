# 09 - Deployment Guide

## Project Name
**Lunetron EdTech Platform**

**Version:** 1.0  
**Environment:** Development, Staging, Production  
**Last Updated:** July 2026

---

# 1. Purpose

This document describes how to deploy the Lunetron EdTech Platform from development to production. It covers infrastructure, environment configuration, Docker, CI/CD, database migrations, monitoring, backups, and rollback procedures.

---

# 2. Technology Stack

## Frontend

- Next.js
- React
- TypeScript
- Tailwind CSS

## Backend

- Python
- Django
- Django REST Framework
- Gunicorn
- Celery

## Database

- PostgreSQL

## Cache & Queue

- Redis

## Reverse Proxy

- Nginx

## Containerization

- Docker
- Docker Compose

## CI/CD

- GitHub Actions

## Cloud

- AWS EC2
- AWS RDS
- AWS S3
- AWS CloudFront

---

# 3. Deployment Environments

| Environment | Purpose |
|-------------|---------|
| Development | Local development |
| Staging | QA and pre-production validation |
| Production | Live application |

---

# 4. Infrastructure Architecture

```
Users
   │
   ▼
CloudFront CDN
   │
   ▼
Nginx
   │
   ├───────────────┐
   ▼               ▼
Next.js        Django API
Frontend       Gunicorn
   │               │
   ▼               ▼
AWS S3       PostgreSQL (RDS)
                  │
                  ▼
                Redis
                  │
                  ▼
                Celery Worker
```

---

# 5. Server Requirements

Minimum Production Server

| Resource | Recommendation |
|----------|----------------|
| CPU | 4 vCPU |
| Memory | 8 GB RAM |
| Storage | 100 GB SSD |
| OS | Ubuntu 24.04 LTS |
| Python | 3.12+ |
| Node.js | 22 LTS |
| PostgreSQL | 16+ |
| Redis | 7+ |

---

# 6. Required Software

Install:

- Git
- Docker
- Docker Compose
- Nginx
- Node.js
- Python
- PostgreSQL
- Redis
- Certbot (Let's Encrypt)

---

# 7. Environment Variables

## Backend (.env)

```env
DEBUG=False
SECRET_KEY=your-secret-key

ALLOWED_HOSTS=api.lunetron.com

DATABASE_URL=postgres://user:password@db:5432/lunetron

REDIS_URL=redis://redis:6379/0

JWT_SECRET=jwt-secret

EMAIL_HOST=smtp.example.com
EMAIL_PORT=587
EMAIL_USER=your-email
EMAIL_PASSWORD=your-password

AWS_ACCESS_KEY_ID=xxxxxxxx
AWS_SECRET_ACCESS_KEY=xxxxxxxx
AWS_STORAGE_BUCKET_NAME=lunetron-media

RAZORPAY_KEY_ID=xxxx
RAZORPAY_SECRET=xxxx

STRIPE_SECRET_KEY=xxxx

PAYPAL_CLIENT_ID=xxxx
PAYPAL_SECRET=xxxx
```

---

## Frontend (.env.local)

```env
NEXT_PUBLIC_API_URL=https://api.lunetron.com/api/v1

NEXT_PUBLIC_APP_NAME=Lunetron
```

---

# 8. Docker Structure

```
project/

docker-compose.yml

backend/
    Dockerfile

frontend/
    Dockerfile

nginx/
    nginx.conf
```

---

# 9. Docker Services

- frontend
- backend
- postgres
- redis
- celery
- celery-beat
- nginx

---

# 10. Deployment Steps

## Step 1

Clone repository

```bash
git clone https://github.com/company/lunetron.git
```

---

## Step 2

Create environment variables

```bash
cp .env.example .env
```

---

## Step 3

Build Docker images

```bash
docker compose build
```

---

## Step 4

Start containers

```bash
docker compose up -d
```

---

## Step 5

Run database migrations

```bash
docker compose exec backend python manage.py migrate
```

---

## Step 6

Create superuser

```bash
docker compose exec backend python manage.py createsuperuser
```

---

## Step 7

Collect static files

```bash
docker compose exec backend python manage.py collectstatic --noinput
```

---

## Step 8

Verify deployment

```
https://api.lunetron.com/admin

https://api.lunetron.com/api/v1

https://lunetron.com
```

---

# 11. CI/CD Pipeline

Pipeline Stages

```
Developer Push

↓

GitHub

↓

GitHub Actions

↓

Run Tests

↓

Lint

↓

Build Docker Images

↓

Security Scan

↓

Deploy to Staging

↓

QA Approval

↓

Deploy to Production
```

---

# 12. Database Migration Process

Before deployment:

```bash
python manage.py makemigrations

python manage.py migrate
```

Never edit production database tables manually unless following an approved maintenance procedure.

---

# 13. Static & Media Files

Static Files

```
AWS S3
```

Media Files

```
AWS S3
```

Delivery

```
CloudFront CDN
```

---

# 14. SSL Configuration

Use:

- Let's Encrypt
- Certbot
- Automatic certificate renewal

HTTPS must be enforced across the application.

---

# 15. Monitoring

Recommended tools:

- Prometheus
- Grafana
- Sentry

Monitor:

- API response time
- CPU usage
- Memory usage
- Disk usage
- Database health
- Redis health
- Celery queue
- Error rate

---

# 16. Logging

Application Logs

- Django
- Gunicorn
- Celery
- Nginx

Log retention:

- 30 days

Centralized logging is recommended.

---

# 17. Backups

Database

- Daily incremental backup
- Weekly full backup

Media

- Daily backup

Retention

- 30–90 days

---

# 18. Rollback Procedure

If deployment fails:

1. Stop the new release.
2. Restore the previous Docker image.
3. Restore the previous environment configuration.
4. Restore the database if schema changes are incompatible.
5. Verify application health before reopening traffic.

---

# 19. Security Checklist

- HTTPS enabled
- Strong SECRET_KEY
- DEBUG=False
- Secure cookies
- HTTPOnly cookies
- CSRF protection
- CORS configured
- Firewall enabled
- SSH key authentication
- Regular dependency updates
- Database credentials stored securely

---

# 20. Health Checks

Application

```
GET /health
```

Database

```
Database connectivity
```

Redis

```
Redis ping
```

Celery

```
Worker heartbeat
```

Health checks should be integrated with your monitoring platform.

---

# 21. Scaling Strategy

Horizontal Scaling

- Multiple Django instances
- Multiple Next.js instances
- Load balancer
- Redis cache
- Read replicas for PostgreSQL

Vertical Scaling

- Increase CPU
- Increase RAM
- Increase storage

---

# 22. Disaster Recovery

Recovery Time Objective (RTO)

- Less than 2 hours

Recovery Point Objective (RPO)

- Less than 15 minutes

---

# 23. Production Checklist

Before going live:

- Environment variables configured
- Database migrations applied
- Static files collected
- SSL active
- Monitoring enabled
- Logging enabled
- Backups configured
- CI/CD passing
- Performance tested
- Security tested
- Admin account verified
- DNS configured
- Payment gateways tested
- Email service tested

---

# 24. Maintenance

Regular tasks:

- Update dependencies
- Rotate secrets
- Review logs
- Verify backups
- Renew SSL certificates
- Optimize database indexes
- Clean temporary files
- Review monitoring alerts

---

# 25. Deployment Summary

| Component | Technology |
|-----------|------------|
| Frontend | Next.js |
| Backend | Django + DRF |
| Database | PostgreSQL |
| Cache | Redis |
| Queue | Celery |
| Reverse Proxy | Nginx |
| Storage | AWS S3 |
| CDN | CloudFront |
| CI/CD | GitHub Actions |
| Containers | Docker |
| Monitoring | Prometheus + Grafana + Sentry |

---

# 26. Document Approval

**Prepared By:** Lunetron Development Team

**Reviewed By:** DevOps Engineer

**Approved By:** Technical Lead

**Version:** 1.0