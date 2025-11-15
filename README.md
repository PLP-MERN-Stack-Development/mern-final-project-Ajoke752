# Ecobarter

A MERN-stack application for community waste reporting and rewards, designed to help farmers and communities exchange or reward responsible waste management. This repository contains a split workspace with a `backend/` Express API and a `frontend/` Vite-powered client.

> Note: This README was generated from the repository structure and file names. A few small assumptions are listed in the "Assumptions" section — please adjust any environment variable names, script commands or endpoint paths to match your actual implementation if they differ.

## Table of contents

- [Project snapshot](#project-snapshot)
- [Features](#features)
- [Tech stack](#tech-stack)
- [Repository layout](#repository-layout)
- [Quick start](#quick-start)
  - [Prerequisites](#prerequisites)
  - [Backend setup](#backend-setup)
  - [Frontend setup](#frontend-setup)
- [Environment variables](#environment-variables)
- [API overview](#api-overview)
- [Running locally (development)](#running-locally-development)
- [Deployment notes](#deployment-notes)
- [Testing](#testing)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

## Project snapshot

Ecobarter helps users (farmers and community members) report waste, participate in reward schemes, and interact with the platform via web and (inferred) USSD endpoints. The backend provides REST APIs under `src/routes/` and services under `src/services/`.

## Features

- User authentication and authorization (`src/controllers/authController.js`)
- Farmer-specific functionality (`src/controllers/farmersController.js`)
- Waste reporting endpoints (`src/controllers/wasteReportController.js` and `src/services/wasteService.js`)
- Reward management (`src/controllers/rewardsController.js` and `src/services/rewardsService.js`)
- USSD-related routes for non-smartphone access (`src/routes/ussdRoutes.js`)
- Centralized error handling middleware (`src/middleware/errorHandler.js`)

## Tech stack

- Backend: Node.js, Express
- Database: MongoDB (inferred from typical MERN layout)
- Frontend: Vite (likely React + TypeScript given `tsconfig` and `vite.config.ts`)
- Deployment examples: Render (there is a `render.yaml` in `backend/`)

## Repository layout

- `backend/` - Express API
  - `src/` - application source
    - `app.js`, `server.js` - entrypoints
    - `config/db.js` - DB connection
    - `controllers/` - route handlers
    - `routes/` - route definitions
    - `models/` - Mongoose models (e.g. `User.js`, `WasteReport.js`, `Reward.js`)
    - `services/` - business logic helpers
    - `middleware/` - middleware (auth, error handling)
- `frontend/` - client app (Vite + TS configs present)

## Quick start

### Prerequisites

- Node.js (16+ recommended)
- npm or yarn
- MongoDB instance (local or cloud e.g., MongoDB Atlas)

### Backend setup

1. Open a terminal in `backend/`:

```powershell
cd "c:\Users\USER\Documents\MERN stack specialization\Final project\Ecobarter\backend"
```

2. Install dependencies:

```powershell
npm install
```

3. Create a `.env` file based on the `Environment variables` section below.

4. Start the server (two common options; check `package.json`):

```powershell
# Option A: if a dev script exists (recommended for local dev)
npm run dev

# Option B: start the production server
npm start
# or
node src/server.js
```

### Frontend setup

1. Open a terminal in `frontend/`:

```powershell
cd "c:\Users\USER\Documents\MERN stack specialization\Final project\Ecobarter\frontend"
```

2. Install dependencies and start the dev server:

```powershell
npm install
npm run dev
```

3. The dev server typically runs on `http://localhost:5173` (Vite default) — check the terminal output.

## Environment variables

Create a `.env` in `backend/` with variables similar to the following. Update names if your code uses different variables.

- `PORT` - port for the backend server (e.g., 5000)
- `MONGO_URI` or `DB_URI` - connection string for MongoDB
- `JWT_SECRET` - secret used to sign JWT tokens
- `NODE_ENV` - `development` or `production`

Example `.env` (do NOT commit to VCS):

```
PORT=5000
MONGO_URI=mongodb+srv://<user>:<password>@cluster0.mongodb.net/ecobarter?retryWrites=true&w=majority
JWT_SECRET=your_jwt_secret_here
NODE_ENV=development
```

If your project uses different names (for example `DATABASE_URL`), adapt accordingly.

## API overview

Routes are organized in `src/routes/`. Based on the file names, expect endpoints similar to:

- `POST /api/auth/register` - register a new user
- `POST /api/auth/login` - login and receive a JWT
- `GET/PUT /api/farmers` - farmer-specific endpoints
- `POST /api/waste-reports` - create a waste report
- `GET /api/waste-reports` - list reports
- `GET/POST /api/rewards` - create/list rewards
- `/api/ussd` - USSD entrypoint for non-web access

Example cURL (login) — adapt paths and payloads to your implementation:

```bash
curl -X POST http://localhost:5000/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{"phone": "+2348000000000", "password": "password"}'
```

Example cURL (create waste report):

```bash
curl -X POST http://localhost:5000/api/waste-reports \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer <JWT>" \
  -d '{"type": "organic", "quantity": 12, "location": "Village A"}'
```

Note: The exact request fields and auth method depend on your controller implementations in `src/controllers/`.

## Running locally (development)

- Start a local MongoDB or point `MONGO_URI` to a test cluster.
- Start the backend with `npm run dev` (or the script your `package.json` defines).
- Start the frontend with `npm run dev` inside `frontend/`.
- Use tools like Postman or the browser to test endpoints and the client app.

## Deployment notes

- There is a `backend/render.yaml` in the repository which suggests deployment to Render. Typical steps for Render:

  - Create a Render Web Service pointing to the `backend/` directory
  - Set environment variables (`MONGO_URI`, `JWT_SECRET`, `PORT`)
  - For the frontend, consider deploying to Vercel, Netlify, or another static host. Vite builds a static `/dist`.

- If you use Docker, add a `Dockerfile` in each service and use a multi-service setup.

## Testing

- Add unit and integration tests under `backend/tests` or with your chosen test runner (Jest, Mocha + Chai, etc.).
- For quick API testing, use Postman / Insomnia and the example requests above.

## Contributing

- Fork the repo and create a feature branch for any new work.
- Keep commits small and focused. Provide clear PR descriptions and reference any related issues.
- If you add breaking environment changes, update this `README.md` with the new env var names and examples.

## Assumptions

I inferred a few details from the repository structure and file names. Please confirm or update the following:

- The backend uses MongoDB (`MONGO_URI`) and JWT for auth (`JWT_SECRET`).
- Backend dev script is `npm run dev` or you'll run `node src/server.js` directly.
- The API base path is `/api/*` (common convention). If your code uses a different base, adjust the examples above.

If any of the above are different, tell me which values or script names to use and I'll update this README accordingly.

## License

Add your preferred license in the repository (for example, `MIT`). If you already have a `LICENSE` file, link to it here.

## Contact

Project owner / maintainer: (update with your name/email/links)

---

If you want, I can:

- update examples to match exact `package.json` scripts if you want me to read them,
- add badges (build, coverage),
- or generate a short `CONTRIBUTING.md` and sample `.env.example` file.

Tell me which of the above you'd like next and I will update the README or add files accordingly.

## Deployment 
https://vercel.com/ajokes-projects-9fdf3b7e/eco-barter/2tUALBeTvvvk8EUCmJ5LPVujSnp4

