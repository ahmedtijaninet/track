# TRACKAPP — React Native + Node.js/Express + SQLite

A full-stack trucking management application with:
- **React Native (Expo)** mobile app for truck drivers
- **Node.js/Express** backend API with **SQLite** database
- **Offline-first GPS tracking**, trip logging, working hours, and reporting
- **Minimal black & white design with colored status icons** (green active, blue completed, red alert)

---

## Features

### Mobile App (React Native + Expo)
- Email/password authentication (JWT)
- Start/end trip with destination, cargo, commission type
- Background GPS location tracking (Expo Location + TaskManager)
- Offline mode with local SQLite caching and sync
- View active and completed trips
- Log working hours (start/stop shift)
- Minimal design: black & white with colored status icons

### Backend API (Node.js/Express + SQLite)
- REST API with Prisma ORM (SQLite provider)
- JWT authentication and password hashing (bcrypt)
- CRUD endpoints for drivers, trips, GPS pings, work logs
- Zod validation and rate limiting
- OpenAPI 3.1 (Swagger UI) + Postman collection
- Seed data and migrations included

---

## Tech Stack

- **Mobile:** React Native (Expo), TypeScript, React Navigation, react-hook-form, zod, Zustand, Axios
- **Backend:** Node.js (TypeScript), Express, Prisma ORM (SQLite), JWT, bcrypt, Zod
- **Database:** SQLite (file-based), Prisma migrations
- **Testing:** Vitest (backend), Jest/RTL (mobile)
- **Docs:** Swagger/OpenAPI + Postman collection
- **Dev Tools:** ESLint, Prettier, pino logger

---

## Project Structure

```
/backend
  /src
    /config
    /middlewares
    /modules/{auth,drivers,trips,gps,worklogs,reports}
    /routes
    server.ts
  prisma/schema.prisma
  .env.example
  package.json
  openapi.yaml (generated or static)
  postman/collection.json
  data/trackapp.db (gitignored)

/mobile
  App.tsx
  /src
    /screens/{Dashboard,Trips,TripDetails,StartTrip,WorkHours,Profile}
    /components/{Card,StatusIcon,Button,TextField,Badge}
    /navigation
    /api/client.ts
    /state/{authStore,networkStore}
    /services/{gpsTask.ts,sync.ts}
    /theme
    /hooks
  app.json
  package.json
  README.md
```

---

## Setup

### 1. Clone the Repository
```bash
git clone https://github.com/your-org/trackapp.git
cd trackapp
```

### 2. Configure Backend

1. Navigate to backend folder:
   ```bash
   cd backend
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Create `.env` file from example:
   ```bash
   cp .env.example .env
   ```
   Update values:
   ```
   JWT_SECRET=your_jwt_secret_here
   DB_FILE=./data/trackapp.db
   PORT=4000
   ```

4. Run Prisma migrations and seed data:
   ```bash
   npx prisma migrate dev
   npm run seed   # if seed script exists
   ```

5. Start backend:
   ```bash
   npm run dev
   ```
   API available at: `http://localhost:4000/api/v1`  
   Swagger docs: `http://localhost:4000/docs`

---

### 3. Configure Mobile App

1. Navigate to mobile folder:
   ```bash
   cd ../mobile
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Update API base URL in `/src/api/client.ts`:
   ```ts
   export const API_BASE_URL = "http://<your-computer-ip>:4000/api/v1";
   ```

4. Start Expo development server:
   ```bash
   npx expo start
   ```
   - Press `a` to run on Android emulator or device
   - Press `i` to run on iOS simulator (macOS only)
   - Scan QR code in Expo Go app to run on a physical device

---

## Seed Data

After running migrations and seed:
- **Driver login:**  
  Email: `admin@example.com`  
  Password: `Pass1234!`

This account has sample trips and GPS data.

---

## Available Scripts

### Backend
- `npm run dev` — start server in dev mode (nodemon)
- `npm run build` — build TypeScript to JavaScript
- `npm run start` — run compiled server
- `npm run lint` — check linting
- `npm run test` — run backend tests
- `npx prisma migrate dev` — apply schema changes

### Mobile
- `npx expo start` — run app in dev mode
- `npm run lint` — check linting
- `npm run test` — run mobile tests

---

## API Documentation

- Swagger UI available at: `http://localhost:4000/docs`
- Postman collection: `/backend/postman/collection.json`

Main endpoints:
- `POST /auth/register` — register driver
- `POST /auth/login` — login and get token
- `GET /auth/me` — validate session
- `POST /trips` — start trip
- `PATCH /trips/:id/end` — end trip
- `POST /trips/:id/gps` — send GPS ping
- `GET /trips/:id/gps` — list GPS pings
- `POST /worklogs` — log work hours
- `GET /worklogs` — list work logs

---

## Screens

- **Login** — email/password
- **Dashboard** — active trips + summary
- **Trips List** — filter by active/completed
- **Trip Details** — timeline + GPS mini map
- **Start Trip** — destination, cargo, commission type
- **Work Hours** — start/stop shift, weekly total
- **Profile** — driver info + logout

---

## Offline Mode

- Trips and GPS pings are cached in device SQLite
- Sync queue retries when connection is restored
- Visual indicator shows online/offline state

---

## License

This project is provided as-is under [MIT License](LICENSE).

---

## Authors

- **Your Name / Team** — [GitHub](https://github.com/your-org)  
