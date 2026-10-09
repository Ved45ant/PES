# Peer Evaluation System

A full-stack web application that streamlines the peer evaluation process for academic courses. Students submit answers, evaluate each other's work, raise tickets, and track results — all through a role-based dashboard system.

> 🚧 Currently under active development.

---

## Table of Contents

- [Features](#features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Backend Setup](#backend-setup)
  - [Frontend Setup](#frontend-setup)
- [Environment Variables](#environment-variables)
- [API Overview](#api-overview)
- [Contributing](#contributing)

---

## Features

- **Role-based dashboards** for Students, Teaching Assistants (TAs), Teachers, and Admins
- **Peer evaluation workflow** — assign, submit, and track evaluations
- **PDF answer submission** with QR code support
- **Ticket system** — students raise disputes, TAs and Teachers resolve them
- **Email notifications** — OTP login, ticket resolution, TA assignment, batch reminders
- **Admin panel** — manage users, courses, batches, and exams
- **JWT authentication** with protected routes per role
- **Scheduled jobs** via cron for evaluation reminders

---

## Tech Stack

| Layer     | Technology                                      |
|-----------|-------------------------------------------------|
| Frontend  | React 19, TypeScript, Tailwind CSS v4, Vite     |
| Backend   | Node.js, Express 5, TypeScript                  |
| Database  | MongoDB with Mongoose                           |
| Auth      | JSON Web Tokens (JWT), bcryptjs                 |
| Email     | Nodemailer (Gmail)                              |
| PDF       | pdf-lib, pdfkit, pdf2pic, puppeteer             |
| Other     | node-cron, multer, QRCode, sharp, jszip         |

---

## Project Structure

```
PES/
├── backend/
│   ├── src/
│   │   ├── config/          # Database connection
│   │   ├── controllers/     # Route handlers (admin, auth, student, ta, teacher)
│   │   ├── middlewares/     # Auth, role authorization
│   │   ├── models/          # Mongoose schemas
│   │   ├── routes/          # Express routers
│   │   ├── utils/           # Email, PDF token, cron helpers
│   │   └── server.ts        # App entry point
│   ├── .env.example
│   └── package.json
├── frontend/
│   ├── src/
│   │   ├── components/      # Reusable UI (student, TA, teacher)
│   │   ├── pages/           # Route-level pages
│   │   └── main.tsx
│   ├── .env.example
│   └── package.json
└── README.md
```

---

## Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) v18+
- [Git](https://git-scm.com/)
- A MongoDB instance ([MongoDB Atlas](https://www.mongodb.com/atlas) or local)
- A Gmail account with an [App Password](https://support.google.com/accounts/answer/185833) for email features

### Backend Setup

```bash
cd backend
```

Copy the example env file and fill in your values:

```bash
cp .env.example .env
```

Install dependencies and start the dev server:

```bash
npm install
npm run dev
```

The backend runs on **http://localhost:5000** by default.

### Frontend Setup

```bash
cd frontend
```

Copy the example env file and fill in your values (only needed if you changed the backend port):

```bash
cp .env.example .env
```

Install dependencies and start the dev server:

```bash
npm install
npm run dev
```

The frontend runs on **http://localhost:5173** by default.

---

## Environment Variables

### Backend — `backend/.env`

| Variable        | Required | Description                                              |
|-----------------|----------|----------------------------------------------------------|
| `MONGO_URI`     | Yes      | MongoDB connection string                                |
| `JWT_SECRET`    | Yes      | Secret key for signing JWT tokens                        |
| `PORT`          | No       | Server port (default: `5000`)                            |
| `FRONTEND_URL`  | No       | Frontend origin for CORS (default: `http://localhost:5173`) |
| `EMAIL_USER`    | Yes      | Gmail address for sending reminder/ticket emails         |
| `EMAIL_PASS`    | Yes      | Gmail App Password for `EMAIL_USER`                      |
| `MAIL_SENDER`   | Yes      | Gmail address for sending OTP emails                     |
| `MAIL_PASSWORD` | Yes      | Gmail App Password for `MAIL_SENDER`                     |

See [`backend/.env.example`](./backend/.env.example) for a template.

### Frontend — `frontend/.env`

| Variable             | Required | Description                                        |
|----------------------|----------|----------------------------------------------------|
| `VITE_BACKEND_PORT`  | No       | Backend port override (default: `5000`)            |

See [`frontend/.env.example`](./frontend/.env.example) for a template.

---

## API Overview

### Auth — `/api/auth`

| Method | Endpoint             | Description               |
|--------|----------------------|---------------------------|
| POST   | `/api/auth/register` | Register a new user       |
| POST   | `/api/auth/login`    | Login and receive a JWT   |

### Student — `/api/student`

| Method | Endpoint                          | Description                          |
|--------|-----------------------------------|--------------------------------------|
| GET    | `/api/student/exams`              | Get ongoing exams for the student    |
| GET    | `/api/student/pending-evaluations`| Get pending peer evaluations         |
| POST   | `/api/student/evaluate`           | Submit a peer evaluation             |
| GET    | `/api/student/results`            | Get received evaluation results      |
| POST   | `/api/student/submit-answer`      | Upload a PDF answer for an exam      |
| GET    | `/api/student/submissions`        | Get submissions for a student + exam |

For full request/response details, see:
- [`backend/authorization_endpoints.md`](./backend/authorization_endpoints.md)
- [`backend/student_api_endpoints.md`](./backend/student_api_endpoints.md)

---

## Contributing

Contributions, feedback, and suggestions are welcome.

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/your-feature-name`
3. Commit your changes: `git commit -m "feat: add your feature"`
4. Push to your branch: `git push origin feature/your-feature-name`
5. Open a Pull Request
