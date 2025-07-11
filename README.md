# chat-kash

A chat-kash for starting up app with react, tailwind, postgres, docker, fastify

## Prerequisites

- Node.js (>=16.0.0)
- pnpm
- Docker & Docker Compose
- Git

## Initial Setup

1. Clone the repository:
```bash
git clone <your-repo-url>
cd chat-kash
```

2. Install dependencies:
```bash
pnpm install
```

3. Start the PostgreSQL database:
```bash
docker-compose up -d
```

4. Set up the environment variables:
```bash
# Copy the example env file in the server directory
cp server/.env.example server/.env
```

5. Initialize the database with Prisma:
```bash
cd server
npx prisma generate  # Generate Prisma Client
npx prisma migrate dev  # Create and apply migrations
```

## Development

Start both client and server in development mode:
```bash
# From the root directory
pnpm dev
```

Or start them separately:
```bash
# Start client only
pnpm dev:client

# Start server only
pnpm dev:server
```

The application will be available at:
- Client: http://localhost:5173
- Server: http://localhost:3000

## Database Management with Prisma

### Common Prisma Commands

Create a new migration:
```bash
cd server
npx prisma migrate dev --name <migration-name>
```

Reset the database:
```bash
npx prisma migrate reset
```

View the database in Prisma Studio:
```bash
npx prisma studio
```

Generate Prisma Client after schema changes:
```bash
npx prisma generate
```

Apply migrations in production:
```bash
npx prisma migrate deploy
```

### Example Migration

To add a new table, modify `server/prisma/schema.prisma`:
```prisma
model Update {
  id        Int      @id @default(autoincrement())
  title     String
  content   String
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
}
```

Then run:
```bash
npx prisma migrate dev --name add_updates_table
```

## Building for Production

Build both client and server:
```bash
pnpm build
```

Start the production server:
```bash
pnpm start
```

## Project Structure

```
chat-kash/
├── client/               # React TypeScript frontend
│   ├── src/             # Source files
│   └── package.json     # Client dependencies
├── server/              # Fastify TypeScript backend
│   ├── src/            # Source files
│   ├── prisma/         # Database schema and migrations
│   └── package.json    # Server dependencies
├── docker-compose.yml   # Docker configuration
└── package.json        # Root package.json for running both services
```