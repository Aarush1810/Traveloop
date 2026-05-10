# ✈️ Traveloop — Personalized Travel Planning App

A full-stack **MERN** (MongoDB, Express, React, Node.js) travel planning application.

---

## 📁 Project Structure

```
Traveloop/
├── frontend/                   # React + Vite frontend
│   ├── public/
│   │   └── favicon.svg
│   ├── src/
│   │   ├── App.jsx             # All 14 screens (single-file React app)
│   │   ├── main.jsx            # React entry point
│   │   └── index.css           # Global reset styles
│   ├── index.html
│   ├── vite.config.js          # Vite config + API proxy
│   └── package.json
│
├── backend/                    # Node.js + Express REST API
│   ├── config/
│   │   └── db.js               # MongoDB connection
│   ├── controllers/
│   │   ├── authController.js   # Register, login, profile
│   │   ├── tripController.js   # Trips, stops, notes, checklist, sharing
│   │   ├── cityActivityController.js
│   │   └── adminController.js
│   ├── middleware/
│   │   ├── auth.js             # JWT protect + adminOnly
│   │   └── errorHandler.js
│   ├── models/
│   │   ├── User.js
│   │   ├── Trip.js             # Embedded stops / notes / checklist
│   │   ├── City.js
│   │   └── Activity.js
│   ├── routes/
│   │   ├── auth.js
│   │   ├── trips.js
│   │   ├── catalog.js
│   │   ├── admin.js
│   │   └── shared.js           # Public share links (no auth)
│   ├── server.js               # Express app entry point
│   ├── seed.js                 # Seed DB with cities & activities
│   ├── .env.example            # Environment variable template
│   └── package.json
│
├── package.json                # Root: runs both apps with concurrently
└── README.md
```

---

## 🚀 Getting Started

### Prerequisites
- **Node.js** v18+
- **MongoDB** (local or [Atlas](https://www.mongodb.com/atlas))

---

### 1. Clone & Install

```bash
# Install root dev tools
npm install

# Install backend + frontend dependencies
npm run install:all
```

---

### 2. Configure Environment

```bash
cd backend
cp .env.example .env
```

Edit `backend/.env`:
```env
MONGO_URI=mongodb://localhost:27017/traveloop
JWT_SECRET=your_super_secret_key_here
JWT_EXPIRES_IN=7d
PORT=5000
NODE_ENV=development
ALLOWED_ORIGINS=http://localhost:5173
```

> **MongoDB Atlas?** Replace `MONGO_URI` with your Atlas connection string.

---

### 3. Seed the Database

```bash
npm run seed
```

This populates:
- **15 cities** (Paris, Tokyo, Bali, NYC, Barcelona…)
- **15 activities** (Food Tour, Museum, Hiking, Spa…)
- **Admin account**: `admin@traveloop.com` / `admin123`

---

### 4. Run the App

```bash
# Start both frontend + backend simultaneously
npm run dev
```

| Service | URL |
|---------|-----|
| Frontend | http://localhost:5173 |
| Backend API | http://localhost:5000/api |
| Health check | http://localhost:5000/api/health |

> The navbar shows **"Live DB"** when the frontend successfully connects to the backend. Otherwise it falls back to **"Mock Data"** and still works offline.

---

## 🌐 API Endpoints

All protected routes require `Authorization: Bearer <token>`.

### Auth
| Method | Endpoint | Auth |
|--------|----------|------|
| POST | `/api/auth/register` | ❌ |
| POST | `/api/auth/login` | ❌ |
| GET | `/api/auth/me` | ✅ |
| PUT | `/api/auth/profile` | ✅ |
| PUT | `/api/auth/change-password` | ✅ |
| DELETE | `/api/auth/account` | ✅ |

### Trips
| Method | Endpoint | Auth |
|--------|----------|------|
| GET/POST | `/api/trips` | ✅ |
| GET/PUT/DELETE | `/api/trips/:id` | ✅ |
| POST | `/api/trips/:id/stops` | ✅ |
| PUT/DELETE | `/api/trips/:id/stops/:stopId` | ✅ |
| GET/POST | `/api/trips/:id/notes` | ✅ |
| PUT/DELETE | `/api/trips/:id/notes/:noteId` | ✅ |
| GET/POST | `/api/trips/:id/checklist` | ✅ |
| PUT/DELETE | `/api/trips/:id/checklist/:itemId` | ✅ |
| PUT | `/api/trips/:id/checklist/reset` | ✅ |
| POST | `/api/trips/:id/share` | ✅ |
| POST | `/api/trips/:id/unshare` | ✅ |

### Catalog
| Method | Endpoint | Auth |
|--------|----------|------|
| GET | `/api/cities?search=&country=&pop=` | ✅ |
| GET | `/api/activities?type=&minCost=&maxCost=` | ✅ |

### Shared (public)
| Method | Endpoint | Auth |
|--------|----------|------|
| GET | `/api/shared/:slug` | ❌ |

### Admin
| Method | Endpoint | Auth |
|--------|----------|------|
| GET | `/api/admin/stats` | ✅ Admin |
| GET | `/api/admin/users` | ✅ Admin |
| DELETE | `/api/admin/users/:id` | ✅ Admin |

---

## 🖥️ App Screens

| # | Screen | Description |
|---|--------|-------------|
| 1 | Login / Signup | JWT authentication |
| 2 | Dashboard | Upcoming trips + inspiration |
| 3 | Create Trip | New trip form |
| 4 | My Trips | Trip list with CRUD |
| 5 | Itinerary Builder | Add cities, days, activities |
| 6 | Itinerary View | Day-wise timeline |
| 7 | City Search | Browse & filter cities |
| 8 | Activity Search | Browse & filter activities |
| 9 | Budget Breakdown | Cost charts by category |
| 10 | Packing Checklist | Categorized packing list |
| 11 | Shared Itinerary | Public read-only view |
| 12 | User Profile | Edit name, photo, language |
| 13 | Trip Notes | Journal / reminders |
| 14 | Admin Dashboard | Platform analytics |

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | React 18, Vite |
| Backend | Node.js, Express 4 |
| Database | MongoDB, Mongoose |
| Auth | JWT, bcryptjs |
| Dev tooling | nodemon, concurrently |
