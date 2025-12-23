# Research Document

## Multi-Tenant SaaS Platform – Project & Task Management System

---

## 1. Multi-Tenancy Analysis

### 1.1 Shared Database + Shared Schema

In the shared database and shared schema approach, all tenants use the same
database and the same set of tables. Each record in the database is associated
with a specific tenant using a `tenant_id` column. This column ensures that
data belonging to one tenant can be logically separated from others.

For example, tables such as users, projects, and tasks will contain a
tenant_id field. Whenever the application queries data, it must always include
a filter condition on tenant_id to ensure that only the requesting tenant’s
data is returned.

This approach is cost-effective and easier to manage because only one database
and one schema need to be maintained. It is commonly used by startups and
medium-scale SaaS platforms. However, the major challenge is enforcing strict
data isolation at the application level. Any missing tenant_id filter in API
queries could potentially lead to data leakage between tenants.

### 1.2 Shared Database + Separate Schema

### 1.3 Separate Database per Tenant

### 1.4 Comparison of Multi-Tenancy Approaches

| Approach                    | Description | Pros | Cons | Suitable Use Cases |
| --------------------------- | ----------- | ---- | ---- | ------------------ |
| Shared DB + Shared Schema   |             |      |      |                    |
| Shared DB + Separate Schema |             |      |      |                    |
| Separate Database           |             |      |      |                    |

### Chosen Approach: Shared Database + Shared Schema

We choose this approach because:

- Easier to manage
- Required tenant_id isolation
- Matches assignment requirements
- Works well with RBAC

## 2. Technology Stack Justification

### Backend Framework

### Frontend Framework

### Database

### Authentication Method

### Deployment & Containerization

---

## 3. Security Considerations

### Data Isolation Strategy

### Authentication & Authorization

### Password Hashing Strategy

### API Security Measures

### Audit Logging
