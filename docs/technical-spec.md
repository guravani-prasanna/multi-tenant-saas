# Technical Specification

## 1. Project Structure

This project follows a **MERN stack architecture** with separate backend and frontend codebases for scalability and maintainability.

---

### Backend Structure

`backend/`
`| |src/`
`│ │── controllers/`
`│ │── models/`
`│ │── routes/`
`│ │── middleware/`
`│ │── services/`
`│ │── utils/`
`│ │── config/`
`│ │── app.js`
`│── tests/`
`│── package.json`
`│── .env`

#### Folder Purpose

- **controllers/**  
  Handles request–response logic. Each controller contains business logic for an API endpoint.

- **models/**  
  Defines MongoDB schemas using Mongoose.

- **routes/**  
  Maps HTTP routes to controller functions.

- **middleware/**  
  Contains authentication, authorization, error handling, and request validation middleware.

- **services/**  
  Contains reusable business logic (email service, token service, etc.).

- **utils/**  
  Helper functions such as response formatters and constants.

- **config/**  
  Database connection, environment configuration, and app settings.

- **tests/**  
  Unit and integration tests for backend APIs.

---

### Frontend Structure

`frontend/`
`│── src/`
`│ │── components/`
`│ │── pages/`
`│ │── services/`
`│ │── hooks/`
`│ │── context/`
`│ │── utils/`
`│ │── assets/`
`│ │── App.jsx`
`│ │── main.jsx`
`│── public/`
`│── package.json`
`│── .env`

#### Folder Purpose

- **components/**  
  Reusable UI components (buttons, forms, modals).

- **pages/**  
  Page-level components mapped to routes (Login, Dashboard, Projects).

- **services/**  
  API communication logic using Axios or Fetch.

- **hooks/**  
  Custom React hooks for shared logic.

- **context/**  
  Global state management (AuthContext, UserContext).

- **utils/**  
  Helper functions and constants.

- **assets/**  
  Images, icons, and static resources.

---

## 2. Development Setup Guide

### Prerequisites

- Node.js v18+
- npm v9+
- MongoDB (local or Atlas)
- Git

---

### Environment Variables

#### Backend (`backend/.env`)

PORT=5000
MONGO_URI=your_mongodb_connection_string
JWT_SECRET=your_jwt_secret
NODE_ENV=development
