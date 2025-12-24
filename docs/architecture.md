# System Architecture Design

## 1. High-Level System Architecture

The system follows a multi-tenant MERN architecture with role-based access control.

### Components:

- Client (Browser)
- Frontend Application (React)
- Backend API Server (Node.js + Express)
- Database (MongoDB)
- Authentication Service (JWT-based)

### Architecture Flow:

1. The client accesses the system via a web browser.
2. The frontend application communicates with the backend API using REST APIs.
3. The backend authenticates users using JWT tokens.
4. Requests are authorized based on user roles (Super Admin, Tenant Admin, End User).
5. Data is stored and retrieved from MongoDB with tenant-based isolation.

📌 **Diagram Location:** `docs/images/system-architecture.png`

---

## 2. Database Schema Design

The database follows a multi-tenant schema design where each entity is associated with a tenant_id to ensure data isolation.

### Core Entities:

- Tenant
- User
- Project
- Task
- SubscriptionPlan

### Relationships:

- A Tenant can have multiple Users.
- A Tenant can have multiple Projects.
- A Project can have multiple Tasks.
- Users can be assigned to multiple Tasks.

📌 **ERD Diagram Location:** `docs/images/database-erd.png`

---

## 3. API Architecture

### Authentication APIs

| Endpoint                 | Method | Auth Required | Role   |
| ------------------------ | ------ | ------------- | ------ |
| /api/auth/register       | POST   | No            | Public |
| /api/auth/login          | POST   | No            | Public |
| /api/auth/logout         | POST   | Yes           | All    |
| /api/auth/reset-password | POST   | No            | Public |

### Tenant APIs

| Endpoint         | Method | Auth Required | Role        |
| ---------------- | ------ | ------------- | ----------- |
| /api/tenants     | POST   | Yes           | Super Admin |
| /api/tenants     | GET    | Yes           | Super Admin |
| /api/tenants/:id | PUT    | Yes           | Super Admin |
| /api/tenants/:id | DELETE | Yes           | Super Admin |

### User APIs

| Endpoint       | Method | Auth Required | Role         |
| -------------- | ------ | ------------- | ------------ |
| /api/users     | POST   | Yes           | Tenant Admin |
| /api/users     | GET    | Yes           | Tenant Admin |
| /api/users/:id | PUT    | Yes           | Tenant Admin |
| /api/users/:id | DELETE | Yes           | Tenant Admin |

### Project APIs

| Endpoint          | Method | Auth Required | Role                   |
| ----------------- | ------ | ------------- | ---------------------- |
| /api/projects     | POST   | Yes           | Tenant Admin           |
| /api/projects     | GET    | Yes           | Tenant Admin, End User |
| /api/projects/:id | PUT    | Yes           | Tenant Admin           |
| /api/projects/:id | DELETE | Yes           | Tenant Admin           |

### Task APIs

| Endpoint       | Method | Auth Required | Role                   |
| -------------- | ------ | ------------- | ---------------------- |
| /api/tasks     | POST   | Yes           | Tenant Admin, End User |
| /api/tasks     | GET    | Yes           | All                    |
| /api/tasks/:id | PUT    | Yes           | Assigned User          |
| /api/tasks/:id | DELETE | Yes           | Tenant Admin           |
