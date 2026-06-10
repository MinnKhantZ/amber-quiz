# Backend

Express.js API server with Prisma ORM and Socket.io.

## Quick Start

```bash
npm install
npm run db:push
npm run dev
```

## Environment Variables

Create `.env`:

```env
DATABASE_URL="postgresql://user:password@localhost:5432/quiz_db"
JWT_SECRET="your_jwt_secret_here"
JWT_EXPIRES_IN="7d"
PORT=3000
CORS_ORIGIN="http://localhost:5173"
UPLOAD_DIR="uploads"
```

## Scripts

| Command | Description |
|---------|-------------|
| `npm run dev` | Start with nodemon |
| `npm start` | Production server |
| `npm run db:push` | Push schema (dev) |
| `npm run db:migrate` | Run migrations |
| `npm run db:seed` | Seed database |
| `npm run db:studio` | Prisma Studio |
| `npm test` | Run tests |

## Project Structure

```
src/
├── routes/      # Express route handlers
├── middleware/   # Auth, error handling
├── services/    # Business logic
└── utils/       # Helpers
prisma/
├── schema.prisma
└── seed.js
```
