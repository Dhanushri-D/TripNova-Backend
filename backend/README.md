# TripNova — Backend

The engine behind TripNova. A REST API built with Node.js, Express, and MongoDB that powers everything — authentication, destinations, bookings, trip planning, reviews, and more.

---

## Tech Stack

- **Node.js + Express 5** — server and routing
- **MongoDB + Mongoose** — database and ODM
- **JWT (jsonwebtoken)** — stateless auth
- **bcryptjs** — password hashing
- **dotenv** — environment variable management
- **cors** — cross-origin requests
- **nodemon** — dev auto-restart

---

## Project Structure

```
backend/
├── config/
│   └── db.js              # MongoDB connection
├── controllers/           # Business logic for each resource
│   ├── authController.js
│   ├── bookingController.js
│   ├── budgetPlanController.js
│   ├── destinationController.js
│   ├── enquiryController.js
│   ├── galleryController.js
│   ├── hotelController.js
│   ├── packageController.js
│   ├── reviewController.js
│   ├── tripPlanController.js
│   ├── userController.js
│   └── wishlistController.js
├── middleware/
│   └── auth.js            # JWT protect + adminOnly guards
├── models/                # Mongoose schemas
│   ├── Booking.js
│   ├── BudgetPlan.js
│   ├── Destination.js
│   ├── Enquiry.js
│   ├── Gallery.js
│   ├── Hotel.js
│   ├── Package.js
│   ├── Review.js
│   ├── TripPlan.js
│   ├── User.js
│   └── Wishlist.js
├── routers/               # Express routers for each resource
├── .env                   # Environment variables (never commit this)
├── migrate.js             # DB migration script
├── seed.js                # DB seed script
└── server.js              # App entry point
```

---

## API Endpoints

| Prefix | Resource |
|--------|----------|
| `/api/auth` | Register, login, get/update profile, reset password |
| `/api/destinations` | CRUD for destinations |
| `/api/packages` | CRUD for travel packages |
| `/api/hotels` | CRUD for hotels |
| `/api/bookings` | Create, view, cancel, complete bookings |
| `/api/reviews` | Create and delete reviews |
| `/api/enquiries` | Submit and manage enquiries |
| `/api/gallery` | Gallery image management |
| `/api/users` | Admin: list and delete users |
| `/api/trip-plans` | User trip planning |
| `/api/budget-plans` | User budget tracking |
| `/api/wishlist` | Add/remove wishlist items |

---

## Auth & Roles

- JWT tokens expire in **7 days**
- Every protected route uses the `protect` middleware — it reads the `Authorization: Bearer <token>` header, verifies the token, and attaches the user to `req.user`
- Admin-only routes additionally use the `adminOnly` middleware which checks `req.user.role === 'admin'`

---

## Getting Started

### Prerequisites
- Node.js v16+
- MongoDB Atlas account (or local MongoDB)

### Install & Run

```bash
cd Backend/backend
npm install
```

Create a `.env` file (see below), then:

```bash
# Development (with auto-restart)
npm run dev

# Production
npm start
```

Server runs at `http://localhost:5000`

---

## Environment Variables

Create a `.env` file in `Backend/backend/`:

```env
PORT=5000
MONGO_URI=<your_mongodb_connection_string>
JWT_SECRET=<your_jwt_secret>
JWT_EXPIRE=7d
FRONTEND_URL=http://localhost:3000
```

Never commit your `.env` file — it's already in `.gitignore`.

---

## Seeding the Database

If you want to pre-populate the DB with sample data:

```bash
node seed.js
```

---

## Deployment

The backend is deployed on **Render**.

Live URL: `https://tripnova-backend-tdec.onrender.com`

Allowed CORS origins:
- `http://localhost:3000` (local dev)
- `https://trip-nova-frontend.vercel.app` (production frontend)
