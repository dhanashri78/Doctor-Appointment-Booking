# Prescripto — Doctor Appointment Booking System

A full-stack web application that connects patients with doctors and helps manage doctor appointments through separate patient, doctor, and admin interfaces.

> **Project type:** Full-stack web application  
> **Stack:** MongoDB, Express.js, React.js, Node.js (MERN)  
> **Status:** Academic/portfolio project

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Technology Stack](#technology-stack)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Environment Variables](#environment-variables)
- [Running the Application](#running-the-application)
- [API Route Groups](#api-route-groups)
- [Application Flow](#application-flow)
- [Security Notes](#security-notes)
- [Future Improvements](#future-improvements)

## Overview

Prescripto is designed to make the doctor appointment process easier. Patients can explore doctors and manage bookings, doctors can review their appointments, and administrators can manage doctors and monitor appointment activity.

The application uses a React-based frontend, a Node.js/Express REST API, and MongoDB for data storage. JWT-based authentication is used for protected areas of the application. Cloudinary is used for image handling, and Razorpay integration is included for payment functionality when the required credentials are configured.

## Features

### Patient

- Register and log in to an account.
- Browse the available doctors and view doctor details.
- Book appointments based on the available options.
- View and manage personal appointments.
- Access profile information.
- Use the payment flow when payment credentials and configuration are enabled.

### Doctor

- Log in to the doctor dashboard.
- View appointment information.
- Manage appointment status and availability, where supported by the application.
- View doctor dashboard and profile information.

### Admin

- Log in to the admin dashboard.
- Add and manage doctor records.
- View the doctors list.
- View and manage appointments.
- Review dashboard statistics, such as doctors and appointments.

## Technology Stack

| Area | Technologies |
|---|---|
| Frontend | React.js, Vite, JavaScript, CSS/Tailwind CSS (as configured in the project) |
| Backend | Node.js, Express.js |
| Database | MongoDB Atlas / MongoDB |
| Authentication | JSON Web Tokens (JWT) |
| Image storage | Cloudinary |
| Payments | Razorpay (requires valid test/live credentials) |
| Development tools | npm, VS Code, Postman, Nodemon |

## Project Structure

The repository is organized into separate application areas. Folder names can vary slightly depending on the version you pushed to GitHub.

```text
DocterBooking/
├── frontend/       # Patient-facing React application
├── admin/          # Admin dashboard (and doctor dashboard, if included here)
├── backend/        # Express API, database connection, controllers and routes
└── README.md
```

If your local repository uses different folder names, use the names present in your project directory.

## Getting Started

### Prerequisites

Install the following before running the application:

- [Node.js](https://nodejs.org/) and npm
- A MongoDB database, such as MongoDB Atlas
- A Cloudinary account for image uploads
- Razorpay test credentials if you want to test payments

### 1. Clone the repository

```bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
cd DocterBooking
```

Replace `<YOUR_GITHUB_REPOSITORY_URL>` with the HTTPS or SSH URL of your GitHub repository.

### 2. Install dependencies

Open a terminal in each application folder and install its dependencies:

```bash
cd backend
npm install
```

In a second terminal:

```bash
cd frontend
npm install
```

In another terminal, if your repository has a separate admin app:

```bash
cd admin
npm install
```

### 3. Configure environment variables

Create a `.env` file in the backend folder and add the variables required by your backend configuration. A typical setup looks like this:

```env
PORT=4000
MONGODB_URI=your_mongodb_connection_string
JWT_SECRET=replace_with_a_long_random_secret

CLOUDINARY_NAME=your_cloudinary_cloud_name
CLOUDINARY_API_KEY=your_cloudinary_api_key
CLOUDINARY_SECRET_KEY=your_cloudinary_api_secret

RAZORPAY_KEY_ID=your_razorpay_test_key_id
RAZORPAY_KEY_SECRET=your_razorpay_test_key_secret
```

The exact names must match the names read by your backend code. For example, if your code uses `MONGO_URI` instead of `MONGODB_URI`, keep the name used in your code. Do not commit real credentials to GitHub.

For the Vite frontend, create or update its `.env` file:

```env
VITE_BACKEND_URL=http://localhost:4000
```

If the admin application also reads `VITE_BACKEND_URL`, configure it in the admin folder as well. Restart each Vite server after changing environment variables.

### 4. Start the applications

Run each application in a separate terminal. Use the scripts defined in that folder's `package.json`.

**Backend** (the project commonly uses the `server` script):

```bash
cd backend
npm run server
```

If that script does not exist, open `backend/package.json` and use the available development/start script, such as `npm run dev` or `npm start`.

**Patient frontend:**

```bash
cd frontend
npm run dev
```

**Admin frontend, if separate:**

```bash
cd admin
npm run dev -- --port 5174
```

The project has previously been run with the backend on port `4000`, the patient frontend on port `5173`, and the admin frontend on port `5174`. Vite may select a different port if the requested port is already in use; check the terminal output.

## Environment Variables

| Variable | Used for |
|---|---|
| `PORT` | Backend server port |
| `MONGODB_URI` or the database variable used in your code | MongoDB connection string |
| `JWT_SECRET` | Signing and verifying authentication tokens |
| `CLOUDINARY_NAME` | Cloudinary cloud name |
| `CLOUDINARY_API_KEY` | Cloudinary API key |
| `CLOUDINARY_SECRET_KEY` | Cloudinary API secret |
| `RAZORPAY_KEY_ID` | Razorpay key ID for the payment integration |
| `RAZORPAY_KEY_SECRET` | Razorpay secret for server-side payment verification |
| `VITE_BACKEND_URL` | Backend base URL used by the Vite frontend(s) |

Use the exact variable names expected by the source code. The list above is a setup guide, not a guarantee that every variable name matches every version of the project.

## API Route Groups

The backend exposes REST API routes under these prefixes:

| Route prefix | Responsibility |
|---|---|
| `/api/user` | Patient registration/login, profile, appointments and related user operations |
| `/api/doctor` | Doctor authentication, appointments, profile and doctor operations |
| `/api/admin` | Admin authentication, doctor management, appointments and dashboard data |

The exact endpoints and HTTP methods are defined in the route files inside the backend. Check those files before using a specific endpoint in Postman.

## Application Flow

1. The user interacts with the React frontend.
2. The frontend sends an HTTP request to the Express backend using `VITE_BACKEND_URL`.
3. The backend validates the request and checks authentication where required.
4. Controllers perform the requested operation and read/write data in MongoDB.
5. The backend returns a response to the frontend, which updates the interface.
6. Where configured, Cloudinary handles image uploads and Razorpay handles the payment workflow.

## Security Notes

- Never commit `.env` files, database credentials, JWT secrets, Cloudinary secrets, or Razorpay secrets.
- Keep private keys only on the backend. Do not expose secret keys through variables prefixed with `VITE_`.
- Use Razorpay test keys during development and verify payments on the backend.
- Use a strong, unique `JWT_SECRET` and validate protected requests on the server.
- Add `.env` files to `.gitignore`; if a real secret was already pushed to GitHub, revoke/rotate it.

## Future Improvements

- Add email/SMS reminders for upcoming appointments.
- Improve filtering and searching by doctor specialization and availability.
- Add automated tests for authentication, booking, and payment workflows.
- Add clear loading, empty, and error states throughout the UI.
- Deploy the frontend, admin interface, and backend with production environment variables.

## Author

**Dhanashri Shinde**

Built as a full-stack project to practise React, Node.js, Express, MongoDB, authentication, API integration, and appointment-management workflows.
