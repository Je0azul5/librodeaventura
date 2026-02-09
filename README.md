# Libro de Aventuras

Monorepo with a React + Vite frontend and an Express + Prisma API for tracking shared adventures.

**Project Layout**
- `apps/web` React app (Vite)
- `apps/api` Express API + Prisma (PostgreSQL)
- `apps/api/prisma/schema.prisma` data model

**Requirements**
- Node.js + npm
- PostgreSQL database

**Setup**
1. Install dependencies.
```bash
npm install
```
2. Create API environment config.
Create `apps/api/.env` with:
```dotenv
DATABASE_URL="postgresql://USER:PASSWORD@HOST:PORT/DB?sslmode=require"
PORT=8080
DEFAULT_USER_ID="Nosotros"
```
3. (Optional) Create web environment config.
Create `apps/web/.env` with:
```dotenv
VITE_API_URL="http://localhost:8080"
VITE_DEFAULT_USER_ID="Nosotros"
```
4. Generate Prisma Client and sync schema.
```bash
npm run prisma:generate -w apps/api
npm run prisma:push -w apps/api
```
5. Start both apps.
```bash
npm run dev
```

**Scripts**
- `npm run dev` starts API + Web together
- `npm run build` builds Web then API
- `npm run dev -w apps/api` starts only the API
- `npm run dev -w apps/web` starts only the Web app

**API Endpoints**
- `GET /health` health check
- `GET /api/entries` list entries
- `POST /api/entries` create entry
  Body: `{ "title": string, "note"?: string, "date"?: string, "userId"?: string }`
- `PUT /api/entries/:id` update entry
  Body: `{ "title": string, "note"?: string }`
- `PATCH /api/entries/:id/done` toggle completion
  Body: `{ "done": boolean }`
- `DELETE /api/entries/:id` delete entry

**Data Model**
`Entry`: `id`, `userId`, `title`, `note`, `date`, `done`, `createdAt`

**Notes**
- The API serves static files from `apps/api/public` when `NODE_ENV` is not `development`.
