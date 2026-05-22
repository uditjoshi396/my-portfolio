# UDIT JOSHI Portfolio - Full Stack Project

Production-ready MERN stack portfolio project for fresher job applications. It includes a polished React portfolio UI, secure Express API, JWT auth, OTP flows, upload endpoints, search/filter/pagination, realtime Socket.io events, and deployment scaffolding.

## Tech Stack

- Frontend: React, Vite, React Router, Axios, Framer Motion, Lucide icons
- Backend: Node.js, Express.js, MongoDB, Mongoose, JWT, Socket.io
- Security: Helmet, rate limiting, protected routes, role authorization
- Uploads: Multer file upload and Cloudinary image upload route
- Deployment: Vercel frontend, Render/Railway backend, MongoDB Atlas, Cloudinary
- CI/CD: GitHub Actions workflow included

## Features

- Dark mode toggle
- Scroll progress bar
- Animated hero and cards
- Fully responsive layout for mobile, tablet, laptop, and desktop
- Download resume button
- LinkedIn, GitHub, coding profile links
- Contact form with toast feedback
- About, skills, education, experience, projects, roadmap, resources, and contact sections
- Role based authentication
- JWT login/register
- Email verification OTP
- Forgot password OTP
- OTP login
- Protected profile route
- Admin-only project CRUD
- Admin dashboard UI
- Search, filter and pagination for projects
- Optional Redis caching for project lists
- Stripe checkout session endpoint
- Cloudinary image upload
- Generic file upload endpoint
- Helmet security headers
- Express rate limiting
- Socket.io realtime event channel
- Docker and Kubernetes deployment examples
- Responsive portfolio UI

## Local Setup

### Backend

```bash
cd backend
cp .env.example .env
npm install
npm run dev
```

Update `.env` with MongoDB Atlas, JWT, and Cloudinary values.

Seed demo data and admin user:

```bash
npm run seed
```

Reset MongoDB database collections and create fresh demo data:

```bash
npm run reset-db
```

Demo admin:

- Email: `admin@uditjoshi.com`
- Password: `Admin@123`

### Frontend

```bash
cd frontend
npm install
npm run dev
```

Create `frontend/.env` if your API URL is different:

```bash
VITE_API_URL=http://localhost:5000/api
```

## API Routes

- `GET /api/health`
- `POST /api/auth/register`
- `POST /api/auth/login`
- `GET /api/auth/me`
- `POST /api/auth/verify-email`
- `POST /api/auth/request-otp`
- `POST /api/auth/verify-otp`
- `POST /api/auth/forgot-password`
- `POST /api/auth/reset-password`
- `GET /api/projects?search=mern&category=Full Stack&page=1&limit=6`
- `POST /api/projects` admin only
- `POST /api/uploads/file`
- `POST /api/uploads/image`
- `POST /api/payments/checkout-session`

## Frontend Pages

- `/` portfolio, production features, searchable/filterable project list, resume, contact form, roadmap
- `/login` JWT login
- `/register` account creation with demo email OTP response
- `/admin` admin dashboard for protected project creation, upload testing, and Stripe checkout testing

## Blueprint Projects

- Full Stack E-Commerce Platform
- Job Portal Application
- Real-Time Chat Application
- Full Stack Blog Platform
- Task Management System

## Contact

- LinkedIn: `https://www.linkedin.com/in/uditjoshi/`
- GitHub: `https://github.com/`
- Facebook: `https://www.facebook.com/uditjoshi`
- Instagram: `https://www.instagram.com/uditjoshi/`
- X / Twitter: `https://x.com/uditjoshi`

## ATS-ready Description

Built a production-ready MERN stack application with JWT authentication, role-based authorization, OTP verification, Socket.io realtime communication, Cloudinary uploads, Docker containerization, GitHub Actions CI/CD pipeline, and responsive modern UI.

## Best Deployment Stack

- Frontend: Vercel
- Backend: Render or Railway
- Database: MongoDB Atlas
- Storage: Cloudinary
- CI/CD: GitHub Actions
- Monitoring: Sentry
- Analytics: Google Analytics

## Permanent Deployment Guide

Use this free MERN deployment architecture:

```text
User
  ↓
Frontend: Vercel
  ↓
Backend API: Render
  ↓
Database: MongoDB Atlas
```

### 1. Push Code to GitHub

You can keep this as one repo or split into two repos:

- `portfolio-frontend`
- `portfolio-backend`

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin YOUR_GITHUB_REPO_URL
git push -u origin main
```

### 2. Deploy Frontend on Vercel

Vercel settings:

- Root Directory: `frontend`
- Build Command: `npm run build`
- Output Directory: `dist`
- Environment Variable: `VITE_API_URL=https://your-api.onrender.com/api`

This project includes `frontend/vercel.json`.

### 3. Deploy Backend on Render

Render settings:

- Root Directory: `backend`
- Build Command: `npm install`
- Start Command: `npm start`
- Health Check Path: `/api/health`

Environment variables:

```bash
NODE_ENV=production
CLIENT_URL=https://your-frontend.vercel.app
MONGO_URI=your_mongodb_atlas_uri
DB_NAME=udit_joshi
JWT_SECRET=your_long_random_secret
JWT_EXPIRES_IN=7d
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret
STRIPE_SECRET_KEY=your_stripe_secret_key
```

This project includes `render.yaml`.

### 4. Setup MongoDB Atlas

- Create free cluster
- Create database user
- Add IP access: `0.0.0.0/0`
- Copy connection string into Render as `MONGO_URI`
- Use database name `udit_joshi` for the UDIT JOSHI portfolio

### 5. CORS Setup

The backend reads `CLIENT_URL`. For multiple URLs, use comma-separated values:

```bash
CLIENT_URL=http://localhost:5173,https://your-frontend.vercel.app
```

### 6. Deployment Checklist

Frontend:

- Responsive on mobile, tablet, desktop
- `npm run build` passes
- `VITE_API_URL` points to Render API
- No `localhost` URL in production

Backend:

- `npm start` works
- MongoDB Atlas connected
- Environment variables added on Render
- CORS allows Vercel frontend

Database:

- Atlas cluster active
- Database user created
- Network access configured

Recruiter buttons:

- Live Demo button
- Source Code button
