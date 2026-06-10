# Amber Quiz

A full-stack quiz platform with real-time capabilities, built with modern web technologies.

## Tech Stack

| Layer | Technology |
|-------|------------|
| Frontend | React 18, Vite, Tailwind CSS, Zustand, Socket.io-client |
| Backend | Express.js, Prisma, Socket.io, PostgreSQL |
| Validation | Zod |
| Testing | Vitest |

## Project Structure

```
amber-quiz/
├── frontend/          # React SPA (Vite + Tailwind)
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── stores/
│   │   ├── lib/
│   │   └── hooks/
│   └── tests/
├── backend/           # Express API server
│   ├── src/
│   ├── prisma/
│   └── tests/
└── README.md
```

## Getting Started

### Prerequisites

- Node.js >= 18
- PostgreSQL
- npm >= 9

### Setup

1. **Install all dependencies (workspace-aware):**

   ```bash
   npm install
   ```

2. **Configure environment variables:**

   ```bash
   # Backend: create backend/.env
   DATABASE_URL="postgresql://user:password@localhost:5432/quiz_db"
   JWT_SECRET="your_jwt_secret_here"
   JWT_EXPIRES_IN="7d"
   PORT=3000
   CORS_ORIGIN="http://localhost:5173"
   UPLOAD_DIR="uploads"

   # Frontend: create frontend/.env
   VITE_API_URL="http://localhost:3000"
   VITE_SOCKET_URL="http://localhost:3000"
   ```

3. **Set up the database:**

   ```bash
   npm run db:push    # Development
   # or
   npm run db:migrate # Production
   ```

4. **Start development servers:**

   ```bash
   # Both at once
   npm run dev

   # Or individually
   npm run dev:backend
   npm run dev:frontend
   ```

## Development

| Command | Description |
|---------|-------------|
| `npm run dev` | Start both frontend and backend |
| `npm run dev:frontend` | Start frontend only (port 5173) |
| `npm run dev:backend` | Start backend only (port 3000) |
| `npm run build` | Build both packages |
| `npm run test` | Run all tests |
| `npm run lint` | Lint all packages |
| `npm run db:studio` | Open Prisma Studio |

## API Endpoints

| Route | Description |
|-------|-------------|
| `/api/auth` | Register, Login, Me |
| `/api/quizzes` | Quiz CRUD, List |
| `/api/quizzes/:quizId/questions` | Question CRUD |
| `/api/quizzes/:quizId/attempts` | Take/Submit quizzes |
| `/api/quizzes/:quizId/leaderboard` | Live/Historical leaderboard |
| `/api/upload` | Image upload |

## Architecture

- **Real-time**: Socket.io for live quiz sessions and leaderboard updates
- **Auth**: JWT-based with role-based access (Teacher/Student)
- **State**: Zustand stores for auth, quizzes, and socket connections
- **Validation**: Zod schemas shared between endpoints
