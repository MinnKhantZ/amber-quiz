# Frontend

React SPA built with Vite, Tailwind CSS, and Socket.io.

## Quick Start

```bash
npm install
npm run dev
```

## Environment Variables

Create `.env`:

```env
VITE_API_URL="http://localhost:3000"
VITE_SOCKET_URL="http://localhost:3000"
```

## Scripts

| Command | Description |
|---------|-------------|
| `npm run dev` | Dev server with HMR |
| `npm run build` | Production build |
| `npm run preview` | Preview production build |
| `npm run lint` | Lint code |
| `npm run test` | Run tests |
| `npm run test:watch` | Tests in watch mode |

## Project Structure

```
src/
├── components/  # Reusable UI components
├── pages/       # Route-level views
├── stores/      # Zustand state stores
├── lib/         # API services, Socket.io config
└── hooks/       # Custom React hooks
tests/           # Test suite
```
