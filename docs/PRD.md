### Super Admin

- Role description: System-level administrator who manages the whole multi-tenant platform.
- Key responsibilities: Create tenants, manage subscription plans, monitor system health.
- Main goals: Keep the system secure, stable, and compliant.
- Pain points: Hard to monitor many tenants, manual billing operations.

### Tenant Admin

- Role description: Organization admin managing one tenant’s users, projects, and settings.
- Key responsibilities: Invite users, assign roles, configure tenant settings.
- Main goals: Let their team work smoothly and stay within plan limits.
- Pain points: Onboarding users, handling access changes, seeing usage vs plan.

### End User

- Role description: Regular team member using projects/tasks to do daily work.
- Key responsibilities: Create and update tasks, collaborate with team.
- Main goals: Finish work efficiently, see priorities clearly.
- Pain points: Confusing UI, slow system, unclear task ownership.

## Functional Requirements

### Authentication Module

FR-001: The system shall allow users to register and log in using email and password.
FR-002: The system shall authenticate users using role-based access control.
FR-003: The system shall allow users to reset passwords using email verification.
FR-004: The system shall issue JWT tokens upon successful authentication.

### Tenant Module

FR-005: The system shall allow the Super Admin to create and manage tenants.
FR-006: The system shall allow the Super Admin to assign subscription plans to tenants.
FR-007: The system shall allow Tenant Admins to configure tenant-specific settings.
FR-008: The system shall isolate tenant data to prevent cross-tenant access.

### User Module

FR-009: The system shall allow Tenant Admins to create and manage end users.
FR-010: The system shall assign roles (Super Admin, Tenant Admin, End User) to users.
FR-011: The system shall allow users to update their profile information.

### Project Module

FR-012: The system shall allow Tenant Admins to create and manage projects.
FR-013: The system shall allow users to view projects assigned to them.
FR-014: The system shall restrict project access based on user roles.

### Task Module

FR-015: The system shall allow users to create tasks within a project.
FR-016: The system shall allow users to assign tasks to other users.
FR-017: The system shall allow users to update task status and priority.
FR-018: The system shall allow users to view task history and updates.

## Non-Functional Requirements

NFR-001 (Performance): The system shall respond to API requests within 200ms for 90% of requests.
NFR-002 (Security): The system shall hash all passwords using a secure hashing algorithm and enforce JWT expiration of 24 hours.
NFR-003 (Scalability): The system shall support at least 100 concurrent users per tenant.
NFR-004 (Availability): The system shall maintain an uptime of at least 99%.
NFR-005 (Usability): The system shall provide a responsive user interface compatible with mobile and desktop devices.

## Database ERD

The database structure for our multi-tenant SaaS project is shown below:

![Database ERD](docs/image/database-erd.png)

## API architecture

Auth Module

| Endpoint                  | Method | Auth Required | Role Required | Description                      |
| ------------------------- | ------ | ------------- | ------------- | -------------------------------- |
| `/api/auth/register`      | POST   | No            | N/A           | Register a new user              |
| `/api/auth/login`         | POST   | No            | N/A           | Login and receive JWT token      |
| `/api/auth/logout`        | POST   | Yes           | Any           | Logout user and invalidate token |
| `/api/auth/refresh-token` | POST   | Yes           | Any           | Refresh JWT token                |

Users Module

| Endpoint         | Method | Auth Required | Role Required | Description                     |
| ---------------- | ------ | ------------- | ------------- | ------------------------------- |
| `/api/users`     | GET    | Yes           | Admin         | Get all users in all tenants    |
| `/api/users/me`  | GET    | Yes           | Any           | Get current logged-in user info |
| `/api/users/:id` | GET    | Yes           | Admin         | Get a specific user             |
| `/api/users/:id` | PUT    | Yes           | Admin/User    | Update a user (self or admin)   |
| `/api/users/:id` | DELETE | Yes           | Admin         | Delete a user                   |

Projects Module

| Endpoint            | Method | Auth Required | Role Required | Description                 |
| ------------------- | ------ | ------------- | ------------- | --------------------------- |
| `/api/projects`     | GET    | Yes           | Any           | Get all projects for tenant |
| `/api/projects`     | POST   | Yes           | Any           | Create a new project        |
| `/api/projects/:id` | GET    | Yes           | Any           | Get project details         |
| `/api/projects/:id` | PUT    | Yes           | Any           | Update project info         |
| `/api/projects/:id` | DELETE | Yes           | Admin         | Delete project              |

Tasks Module

| Endpoint         | Method | Auth Required | Role Required | Description              |
| ---------------- | ------ | ------------- | ------------- | ------------------------ |
| `/api/tasks`     | GET    | Yes           | Any           | Get all tasks for tenant |
| `/api/tasks/:id` | GET    | Yes           | Any           | Get task details         |
| `/api/tasks`     | POST   | Yes           | Any           | Create a new task        |
| `/api/tasks/:id` | PUT    | Yes           | Any           | Update task info         |
| `/api/tasks/:id` | DELETE | Yes           | Admin         | Delete task              |
