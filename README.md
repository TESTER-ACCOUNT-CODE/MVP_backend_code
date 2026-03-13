# MVP_backend_code
MVP backend code for THE CODE web, no frontend, no database. MVP code only
# SaaS AI Tool – Backend MVP

## Overview

This repository contains the **Minimum Viable Product (MVP) backend** for an AI-powered SaaS platform designed for **students and developers**.

The backend is built using **Django** and provides the core infrastructure required for:

* User authentication
* Role-based access control
* Subscription management
* Usage tracking
* AI request proxying
* Rate limiting
* Admin management

The system is designed to support an initial user base of approximately **100 users** while maintaining a structure that can scale into a full SaaS platform.

---

# Architecture Overview

The backend follows a modular Django architecture where each major feature is separated into its own application.

```
saas_platform/
│
├── manage.py
│
├── config/
│   ├── settings.py
│   ├── urls.py
│   ├── wsgi.py
│
├── apps/
│   ├── accounts/
│   ├── subscriptions/
│   ├── usage/
│   ├── ai_engine/
```

Each module has a clear responsibility.

| Module        | Purpose                                 |
| ------------- | --------------------------------------- |
| accounts      | User authentication and role management |
| subscriptions | Plans and subscription management       |
| usage         | Tracks AI usage per user                |
| ai_engine     | Handles AI requests and usage logging   |

---

# Core Features

## Authentication System

* Email-based login
* Session-based authentication
* CSRF protection via Django
* Role-based user permissions

Supported user roles:

* Student
* Developer
* Intern
* Admin
* Founder

---

## Subscription System

Users can subscribe to different plans that define usage limits and pricing.

Plan attributes:

* plan name
* price per usage unit
* usage limit
* active status

Subscriptions link users to plans and track lifecycle status.

---

## Usage Tracking

Every AI request generates a usage record.

Tracked information:

* user
* endpoint accessed
* tokens or compute used
* timestamp

Usage logs allow accurate billing and system monitoring.

---

## AI Request Proxy Layer

The backend acts as a **secure intermediary** between the frontend and external AI APIs.

Flow:

```
Frontend
   ↓
Django API
   ↓
AI Service Layer
   ↓
External AI Provider
```

Advantages:

* API keys remain secure
* usage tracking is enforced
* rate limiting is applied
* centralized logging

---

## Rate Limiting

Redis is used to implement request throttling.

The system limits excessive requests by tracking IP-based request counts.

Example policy:

* Maximum requests per minute per IP
* Automatic reset after expiration

---

# Technology Stack

| Layer                   | Technology            |
| ----------------------- | --------------------- |
| Backend Framework       | Django                |
| API Framework           | Django REST Framework |
| Database                | PostgreSQL            |
| Caching / Rate Limiting | Redis                 |
| Authentication          | Session-based         |
| Deployment              | Self-hosted           |

---

# Installation

## 1. Clone the repository

```
git clone https://github.com/your-repo/saas-backend.git
cd saas-backend
```

---

## 2. Create a virtual environment

```
python -m venv venv
source venv/bin/activate
```

Windows:

```
venv\Scripts\activate
```

---

## 3. Install dependencies

```
pip install django
pip install djangorestframework
pip install psycopg2-binary
pip install redis
pip install django-redis
pip install python-dotenv
```

---

## 4. Configure PostgreSQL

Create a database:

```
CREATE DATABASE saas_db;
```

Update `settings.py` with your credentials.

---

## 5. Configure Redis

Ensure Redis is running locally:

```
redis-server
```

---

## 6. Apply migrations

```
python manage.py makemigrations
python manage.py migrate
```

---

## 7. Create admin account

```
python manage.py createsuperuser
```

---

## 8. Run development server

```
python manage.py runserver
```

The API will be available at:

```
http://127.0.0.1:8000
```

---

# API Endpoint

### AI Generation Endpoint

```
POST /api/ai/generate/
```

Example request:

```
{
  "prompt": "Explain recursion in Python"
}
```

Authentication is required.

---

# Security Considerations

The MVP includes several important security features:

* Session authentication
* CSRF protection
* Rate limiting via Redis
* AI API key isolation
* Role-based access control
* Server-side usage tracking

For production deployments, additional measures such as HTTPS enforcement and request logging should be implemented.

---

# Future Improvements

The MVP focuses on core functionality. The following improvements are recommended for future development:

* Payment integration (Stripe or Razorpay)
* Wallet-based usage billing
* API key access for developers
* Celery worker queue for background AI jobs
* Advanced rate limiting per user
* Monitoring and logging infrastructure
* Docker-based deployment
* Horizontal scaling

---

# Intended Scale

This MVP is designed for:

* early-stage startups
* internal testing
* pilot user groups

Expected capacity:

* approximately **100 concurrent users**

With infrastructure upgrades, the architecture can evolve into a full SaaS platform.

---

# License

This project is intended for educational and startup prototype use. Licensing can be adapted based on organizational requirements.

---

# Contributing

Contributions can include:

* new features
* performance improvements
* security enhancements
* documentation improvements

All contributions should follow clean code practices and proper documentation standards.

---

# Summary

This backend MVP provides the essential foundation for an AI-powered SaaS platform by combining:

* structured Django architecture
* secure AI request handling
* usage-based tracking
* scalable database design

It is designed to be simple enough for rapid development while remaining structured enough to grow into a production-grade system.

