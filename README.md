# SIA Tourism Management System

A full-stack Tourism Management System built as a school project for **Systems Integration and Architecture (SIA)**. 
## System Integration Focus

This project was built to practice integrating independently developed systems rather than working as a single standalone app. It does this in two directions:

- **Outbound integration:** the backend calls out to an external Transportation Management System (a separate SIA project) to pull route data, via `EXTERNAL_TRANSPORT_BASE_URL`.
- **Inbound integration:** the backend exposes a dedicated `/api/external` layer (summary stats, transactions) protected by an API key (`INTERNAL_API_KEY`) so that other trusted systems can pull data from this one.

This mirrors a real-world scenario where separate teams/systems (transportation, transactions, tourism/bookings) need to talk to each other over HTTP using shared contracts and access control.

## Tech Stack

**Frontend**
- React 19 + Vite
- React Router
- Tailwind CSS + Ant Design
- Chart.js / react-chartjs-2 for analytics
- Axios for API calls
- jsPDF for report/receipt generation

**Backend**
- Node.js + Express 5
- MongoDB with Mongoose
- Multer + Cloudinary for image uploads
- Axios for outbound integration calls
- dotenv for configuration

## Project Structure

```
SIA-Tourism_Management_System/
├── backend/
│   ├── server.js                # Express app entry point
│   ├── sample.js                # Database seeding script
│   └── src/
│       ├── controllers/         # Business logic (users, bookings, packages, transactions, admin, external, transport, destinations)
│       ├── models/               # Mongoose schemas
│       ├── routers/              # Express route definitions
│       ├── middleware/           # Upload handling, etc.
│       └── database/              # MongoDB connection setup
└── frontend/
    └── src/
        ├── pages/                 # Landing, Login, Signup, User/Traveler and Admin views
        ├── api.js                 # Axios API client
        └── App.jsx                # App routes/entry
```

## Core Modules

| Module | Description |
|---|---|
| Users | Registration, login, user management |
| Destinations | Create/update/delete/rate tourist destinations (with image upload) |
| Packages | Tour package CRUD (with image upload) |
| Bookings | Create, view, and cancel bookings |
| Transactions | Payment/transaction records |
| Admin | Dashboard summary statistics |
| Transport (integration) | Fetches routes from the external Transportation Management System |
| External (integration) | Secured endpoints (`/api/external/summary`, `/api/external/transactions`) for other systems to consume this system's data |

## Getting Started

### Prerequisites
- Node.js (v18+ recommended)
- MongoDB database (local or Atlas)
- A Cloudinary account (for image uploads)

### Backend Setup

```bash
cd backend
npm install
```

Create a `.env` file in `backend/`:

```env
PORT=5000
MONGO_URI=your_mongodb_connection_string
INTERNAL_API_KEY=your_shared_api_key_for_external_requests
EXTERNAL_TRANSPORT_BASE_URL=http://url-of-transportation-system
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_cloudinary_key
CLOUDINARY_API_SECRET=your_cloudinary_secret
```

Run the server:

```bash
npm start
```

Optionally seed the database:

```bash
npm run seed
```

### Frontend Setup

```bash
cd frontend
npm install
npm run dev
```

The frontend will run on Vite's default port (typically `http://localhost:5173`) and communicate with the backend API.

## API Overview

| Base Route | Purpose |
|---|---|
| `/api/users` | Registration, login, user CRUD |
| `/api/destinations` | Destination CRUD + ratings |
| `/api/packages` | Tour package CRUD |
| `/api/bookings` | Booking creation, retrieval, cancellation |
| `/api/transactions` | Transaction records |
| `/api/admin` | Admin dashboard summary |
| `/api/transport` | Routes pulled from the external Transportation System |
| `/api/external` | Secured endpoints (API key required) for external systems to consume this system's summary/transaction data |

## Notes

- `INTERNAL_API_KEY` must match on both sides of an integration (this system and whatever external system calls `/api/external`) for requests to be authorized.
- This is an academic project intended to demonstrate integration patterns between independently built systems, not a production-ready deployment.

## Authors

School project developed for the Systems Integration and Architecture (SIA) course.
