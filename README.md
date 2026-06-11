# Amber Quiz - Real-Time Quiz Platform 🎓⚡

A full-stack, real-time quiz platform with teacher/student roles, live quiz sessions, and analytics. Teachers can create quizzes, host live sessions with real-time answer tracking, and view detailed analytics. Students take quizzes, join live sessions via join codes, and track their performance on leaderboards.

![React](https://img.shields.io/badge/React-18-61DAFB)
![Node.js](https://img.shields.io/badge/Node.js-18+-339933)
![TypeScript](https://img.shields.io/badge/TypeScript-6-3178C6)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Database-4169E1)
![Prisma](https://img.shields.io/badge/Prisma-ORM-2D3748)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-4-06B6D4)

## ✨ Features

### 👩‍🏫 Teacher Features
- **Quiz Management**: Create, edit, and delete quizzes with MCQ, True/False, and Fill-in-the-blank questions
- **Quiz Creation Wizard**: 2-step guided flow — define details, then add questions with image upload
- **Live Quiz Sessions**: Host real-time sessions with unique 6-char join codes
- **Real-Time Tracking**: Monitor student answers live with answer distribution bars
- **Student Roster**: See who's online/offline with presence indicators
- **Session Controls**: Toggle result/leaderboard visibility, advance questions, terminate sessions
- **Analytics Dashboard**: Score distribution charts, per-question accuracy, recent attempts

### 👨‍🎓 Student Features
- **Quiz Browsing**: Paginated quiz library with search and filtering
- **Quiz Taking**: Instant per-question feedback with correct/incorrect flash, countdown timers
- **Live Sessions**: Join by code, receive questions in real-time, submit answers instantly
- **Session Resume**: Reconnect and resume live sessions after disconnects
- **Results Review**: Detailed breakdown of each attempt with score and time
- **Leaderboards**: Ranked performance per quiz
- **Attempt History**: Paginated history of all past attempts

### 🔧 Technical Features
- **Real-Time Communication**: Socket.io for live quiz sessions with event-driven architecture
- **JWT Authentication**: Secure token-based auth with role-based access control (Teacher/Student)
- **Rate Limiting**: Configurable rate limiters for API, auth, and upload endpoints
- **Zod Validation**: Request body and query parameter validation with detailed error messages
- **Stale-While-Revalidate Cache**: Client-side caching with subscription-based reactivity
- **Session Snapshot Hydration**: Full state recovery on reconnect for live sessions
- **Dark/Light Theme**: System-aware theme toggle with flash-free initialization

## 🛠️ Tech Stack

### Backend
- **Runtime**: Node.js 18+ (ESM)
- **Framework**: Express.js 4.21
- **ORM**: Prisma 6.6
- **Database**: PostgreSQL
- **Real-Time**: Socket.io 4.8
- **Auth**: JWT (jsonwebtoken) + bcrypt
- **Validation**: Zod 3.24
- **Logging**: Pino 9
- **File Uploads**: Multer 1.4
- **Security**: Helmet, CORS, express-rate-limit
- **Dev Runner**: tsx watch

### Frontend
- **Framework**: React 18 with Vite 6
- **Styling**: Tailwind CSS 4
- **Routing**: React Router DOM 7
- **State**: Zustand 5
- **Real-Time**: socket.io-client 4.8
- **UI Primitives**: Radix UI (dialog, dropdown, tabs, toast, progress, etc.)
- **Design Utilities**: class-variance-authority, clsx, tailwind-merge
- **Icons**: Lucide React
- **Testing**: Vitest 3, @testing-library/react

## 📋 Prerequisites

Before you begin, ensure you have:

- **Node.js** 18 or higher
- **npm** or **yarn**
- **PostgreSQL** database (local or cloud)
- **Git**

## 🚀 Quick Start

### 1. Clone Repository

```bash
git clone <your-repo-url>
cd amber-quiz
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Environment Setup

**Backend** (`backend/.env`):

```env
DATABASE_URL="postgresql://postgres:yourpassword@localhost:5432/quizapp?schema=public"
JWT_SECRET="change-this-to-a-long-random-string"
JWT_EXPIRES_IN="7d"
PORT=3001
CORS_ORIGIN="http://localhost:5173"
UPLOAD_DIR="uploads"
```

**Frontend** (`frontend/.env`):

```env
# Leave empty in dev — Vite proxies /api and /socket.io to backend
# In production, set to deployed backend URL:
# VITE_API_URL=https://your-backend.railway.app
```

### 4. Database Setup

```bash
cd backend
npx prisma db push
npx prisma db seed
cd ..
```

### 5. Start Development

```bash
# Start both frontend and backend
npm run dev

# Or start individually
npm run dev:backend    # Backend on port 3001
npm run dev:frontend   # Frontend on port 5173
```

## 📁 Project Structure

```
amber-quiz/
├── package.json                    # Root workspace config
├── .gitignore
├── README.md
│
├── backend/
│   ├── package.json
│   ├── prisma/
│   │   ├── schema.prisma           # Database schema (8 models)
│   │   └── migrations/
│   ├── src/
│   │   ├── app.ts                  # Entry point
│   │   ├── config/
│   │   │   ├── env.ts              # Zod-validated env config
│   │   │   └── db.ts               # Prisma client singleton
│   │   ├── socket/
│   │   │   └── index.ts            # Socket.io event handlers
│   │   ├── middleware/
│   │   │   ├── auth.ts             # JWT auth + RBAC
│   │   │   ├── errorHandler.ts     # Centralized error handler
│   │   │   ├── rateLimit.ts        # Rate limiters
│   │   │   ├── validate.ts         # Zod validation
│   │   │   └── requestContext.ts   # Request ID tracking
│   │   ├── routes/
│   │   ├── controllers/
│   │   ├── services/
│   │   └── utils/
│   └── tests/
│
└── frontend/
    ├── package.json
    ├── index.html
    ├── vite.config.ts
    ├── vercel.json
    └── src/
        ├── main.tsx
        ├── App.tsx
        ├── stores/
        ├── components/
        ├── pages/
        └── lib/
```

## 🗄️ Database Schema

| Model | Description |
|-------|-------------|
| **User** | Teachers and students with email/password/role |
| **Quiz** | Title, description, category, timer settings, publish status |
| **Question** | MCQ, True/False, Fill-in-blank with options and correct answers |
| **Attempt** | Student quiz attempt with score, time, completion status |
| **Answer** | Individual question answers linked to attempts |
| **LiveSession** | Real-time session with join code, status, visibility flags |
| **LiveParticipant** | Students in a live session with online/offline status |
| **LiveAnswer** | Answers submitted during live sessions |

## 🔐 API Endpoints

### Authentication
| Method | Endpoint | Auth | Description |
|--------|----------|------|-------------|
| POST | `/api/auth/register` | No | Register with email/password/role |
| POST | `/api/auth/login` | No | Login, returns JWT |
| GET | `/api/auth/me` | Yes | Get current user |

### Quizzes
| Method | Endpoint | Auth | Role | Description |
|--------|----------|------|------|-------------|
| GET | `/api/quizzes` | Yes | Any | List quizzes (paginated) |
| POST | `/api/quizzes` | Yes | Teacher | Create quiz |
| GET | `/api/quizzes/:id` | Yes | Any | Get quiz details |
| PUT | `/api/quizzes/:id` | Yes | Teacher | Update quiz |
| DELETE | `/api/quizzes/:id` | Yes | Teacher | Delete quiz |

### Questions
| Method | Endpoint | Auth | Role | Description |
|--------|----------|------|------|-------------|
| POST | `/api/:quizId/questions` | Yes | Teacher | Add question |
| PUT | `/api/questions/:id` | Yes | Teacher | Update question |
| DELETE | `/api/questions/:id` | Yes | Teacher | Delete question |
| PATCH | `/api/:quizId/questions/reorder` | Yes | Teacher | Reorder questions |

### Attempts
| Method | Endpoint | Auth | Role | Description |
|--------|----------|------|------|-------------|
| POST | `/api/quizzes/:quizId/start` | Yes | Student | Start attempt |
| POST | `/api/attempts/:id/submit` | Yes | Student | Submit answers |
| GET | `/api/attempts/:id` | Yes | Any | Get attempt detail |
| GET | `/api/me/attempts` | Yes | Student | Attempt history |

### Analytics & Leaderboard
| Method | Endpoint | Auth | Role | Description |
|--------|----------|------|------|-------------|
| GET | `/api/quizzes/:quizId/analytics` | Yes | Teacher | Quiz analytics |
| GET | `/api/quizzes/:quizId/leaderboard` | Yes | Any | Quiz leaderboard |

### Upload
| Method | Endpoint | Auth | Role | Description |
|--------|----------|------|------|-------------|
| POST | `/api/upload` | Yes | Teacher | Upload image (5MB max) |

## 🔄 Real-Time Events (Socket.io)

| Event | Direction | Description |
|-------|-----------|-------------|
| `create-session` | Teacher → Server | Create session, get join code |
| `join-session` | Student → Server | Join by 6-char code |
| `resume-session` | Both → Server | Resume after reconnect |
| `start-session` | Teacher → Server | Begin session |
| `next-question` | Teacher → Server | Advance to next question |
| `live-answer` | Student → Server | Submit answer |
| `end-session` | Teacher → Server | Terminate session |

## 🚀 Deployment

### Frontend (Vercel)

```bash
npx vercel
```

Set `VITE_API_URL` to your deployed backend URL.

### Backend (Railway/Render)

Set environment variables:

```env
DATABASE_URL=your_production_db
JWT_SECRET=your_secure_secret
CORS_ORIGIN=your_frontend_url
PORT=3001
```

### Database

Use any PostgreSQL provider (Neon, Supabase, Railway, etc.).

## 🧪 Development

### Available Scripts

| Command | Description |
|---------|-------------|
| `npm run dev` | Start both frontend and backend |
| `npm run dev:backend` | Backend only (tsx watch) |
| `npm run dev:frontend` | Frontend only (Vite) |
| `npm run build` | Build both packages |
| `npm run test` | Run all tests |
| `npm run lint` | Lint all packages |
| `npm run db:push` | Push Prisma schema |
| `npm run db:migrate` | Run Prisma migrations |
| `npm run db:seed` | Seed database |

### Testing

```bash
# Backend tests
cd backend && npm test

# Frontend tests
cd frontend && npm test
```

## 🐛 Troubleshooting

**Database connection failed:**
- Ensure PostgreSQL is running
- Check `DATABASE_URL` in `backend/.env`
- Run `npx prisma db push` to sync schema

**Frontend can't reach backend:**
- Check `VITE_API_URL` is empty in dev (Vite proxy)
- Verify backend is running on port 3001
- Check CORS_ORIGIN matches frontend URL

**Live session issues:**
- Ensure Socket.io is not blocked by firewall
- Check for proxy/WebSocket upgrade issues
- Session resumes within 6 hours via localStorage hint

**Build failures:**
```bash
rm -rf node_modules package-lock.json
npm install
```

## 🤝 Contributing

1. Fork the repository
2. Create feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add AmazingFeature'`)
4. Push to branch (`git push origin feature/AmazingFeature`)
5. Open Pull Request

## 📝 License

This project is licensed under the MIT License.

## 🙏 Acknowledgments

- **Prisma Team** for the excellent ORM
- **Socket.io** for real-time capabilities
- **Radix UI** for accessible UI primitives
- **Tailwind CSS** for utility-first styling
- **Vercel** for frontend deployment
- **Vitest** for fast testing

---

**Built with ❤️ for interactive learning**
