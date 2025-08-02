# intelli-complaint-hub

Intelli Complaint Hub is an AI-powered ticketing and support platform designed to streamline technical issue triage, assignment, and resolution. It leverages modern technologies including React, Vite, Node.js, Express, MongoDB, and AI (Gemini via Inngest) to automate ticket prioritization and moderator assignment.

---

## Table of Contents

- [Features](#features)
- [Architecture](#architecture)
- [Tech Stack](#tech-stack)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Environment Variables](#environment-variables)
  - [Installation](#installation)
  - [Running the Application](#running-the-application)
- [Usage](#usage)
  - [User Roles](#user-roles)
  - [Ticket Lifecycle](#ticket-lifecycle)
  - [Admin Panel](#admin-panel)
- [API Endpoints](#api-endpoints)
- [AI Integration](#ai-integration)
- [Folder Structure](#folder-structure)
- [Contributing](#contributing)
- [License](#license)

---

## Features

- **User Authentication:** Signup, login, and JWT-based session management.
- **Ticket Submission:** Users can submit support tickets with title and description.
- **AI Triage:** Tickets are analyzed by an AI agent for summary, priority, helpful notes, and required skills.
- **Automated Assignment:** Moderators are auto-assigned based on skill match; fallback to admin if no match.
- **Email Notifications:** Moderators receive email notifications for assigned tickets.
- **Admin Panel:** Admins can view, search, and update user roles and skills.
- **Role-Based Access:** Permissions enforced for users, moderators, and admins.

---

## Architecture

- **Client:** React SPA built with Vite, styled using TailwindCSS and DaisyUI.
- **Server:** Node.js/Express REST API, MongoDB for persistence, Inngest for event-driven workflows.
- **AI Integration:** Gemini model via Inngest Agent Kit for ticket analysis.
- **Email:** Nodemailer with Mailtrap for transactional emails.

---

## Tech Stack

- **Frontend:** React, Vite, TailwindCSS, DaisyUI, React Router
- **Backend:** Node.js, Express, Mongoose (MongoDB), JWT, Inngest
- **AI:** Gemini via @inngest/agent-kit
- **Email:** Nodemailer
- **Dev Tools:** ESLint, Nodemon

---

## Getting Started

### Prerequisites

- Node.js (v18+ recommended)
- npm or yarn
- MongoDB instance (local or cloud)
- Mailtrap account (for email testing)
- Gemini API key (for AI ticket analysis)

### Environment Variables

Copy `.env.sample` in the `server/` folder to `.env` and fill in the required values:

```env
PORT=3000
MONGO_URI=your_mongodb_connection_string
JWT_SECRET=your_jwt_secret
MAILTRAP_SMTP_HOST=smtp.mailtrap.io
MAILTRAP_SMTP_PORT=2525
MAILTRAP_SMTP_USER=your_mailtrap_user
MAILTRAP_SMTP_PASS=your_mailtrap_pass
GEMINI_API_KEY=your_gemini_api_key
```

### Installation

#### 1. Clone the repository

```sh
git clone https://github.com/yourusername/intelli-complaint-hub.git
cd intelli-complaint-hub
```

#### 2. Install dependencies

**Server:**

```sh
cd server
npm install
```

**Client:**

```sh
cd client
npm install
```

### Running the Application

#### 1. Start MongoDB

Ensure your MongoDB instance is running and accessible.

#### 2. Start the server

```sh
cd server
npm run dev
```

#### 3. Start the client

```sh
cd client
npm run dev
```

The client will be available at [http://localhost:5173](http://localhost:5173) (default Vite port).

---

## Usage

### User Roles

- **User:** Can submit tickets and view their own tickets.
- **Moderator:** Assigned tickets based on skill match; can view and resolve assigned tickets.
- **Admin:** Full access to all tickets and users; can update user roles and skills via the admin panel.

### Ticket Lifecycle

1. **Submission:** User submits a ticket.
2. **AI Triage:** Ticket is analyzed for summary, priority, helpful notes, and required skills.
3. **Assignment:** Moderator is auto-assigned based on skills; fallback to admin if no match.
4. **Notification:** Moderator receives an email notification.
5. **Resolution:** Moderator/admin resolves the ticket.

### Admin Panel

Accessible via `/admin` route for users with the `admin` role. Features include:

- Search users by email
- Edit user roles and skills
- Save changes and update user permissions

---

## API Endpoints

### Auth

- `POST /api/auth/signup` — Register a new user
- `POST /api/auth/login` — Login and receive JWT
- `POST /api/auth/logout` — Logout user
- `GET /api/auth/users` — List all users (admin only)
- `POST /api/auth/update-user` — Update user role/skills (admin only)

### Tickets

- `GET /api/tickets` — List tickets (role-based)
- `GET /api/tickets/:id` — Get ticket details
- `POST /api/tickets` — Create a new ticket

---

## AI Integration

- Uses Gemini model via Inngest Agent Kit.
- On ticket creation, AI analyzes the ticket and returns:
  - Summary
  - Priority (`low`, `medium`, `high`)
  - Helpful notes (technical guidance, links)
  - Related skills (array)
- Output is stored in the ticket and used for moderator assignment.

---

## Folder Structure

```
intelli-complaint-hub/
├── client/
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── index.css
│   │   └── main.jsx
│   ├── public/
│   ├── package.json
│   └── vite.config.js
├── server/
│   ├── controllers/
│   ├── inngest/
│   ├── middlewares/
│   ├── models/
│   ├── routes/
│   ├── utils/
│   ├── index.js
│   ├── package.json
│   └── .env.sample
├── README.md
└── LICENSE
```

---

## Contributing

Contributions are welcome! Please open issues or submit pull requests for improvements and bug fixes.

---

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.
