# OverBooke - MVP P0

Implementation MVP P0 based on `docs/backlog.md` and `docs/architecture.md`.

## Stack
- Front: Next.js 15 + TypeScript (`apps/web`)
- Back: NestJS + Prisma (`apps/api`)
- DB: PostgreSQL
- Cache: Redis (prepared in `docker-compose.yml`)

## P0 implemented
- Authentification: inscription + connexion + refresh token
- Onboarding: bankroll initiale, objectif, persona
- Dashboard bankroll: solde, palier, mise max, compteur de paris/jour
- Regles de discipline:
  - 2 paris max/jour
  - mise max calculee par palier
- Analyse pre-match structuree
- Preview de pari (checks limite + mise)
- Validation de pari (avec acknowledgement responsable)
- Historique des paris + ROI simple
- Tracking analytics minimal (onboarding, first_bet, bet_created)

## Prerequisites
- Node.js 20+
- npm 11+
- Docker + Docker Compose

## Setup
1. Install dependencies:
```bash
npm install
```

2. Start Postgres and Redis:
```bash
docker compose up -d
```

3. Configure env files:
```bash
copy apps\\api\\.env.example apps\\api\\.env
copy apps\\web\\.env.example apps\\web\\.env.local
```

4. Generate Prisma client and push schema:
```bash
npm run prisma:generate -w apps/api
npm run prisma:push -w apps/api
```

5. Seed match + analysis sample data:
```bash
npm run seed -w apps/api
```

## Run
Terminal 1 (API):
```bash
npm run dev:api
```

Terminal 2 (Web):
```bash
npm run dev:web
```

- API: `http://localhost:4000/api/v1`
- Web: `http://localhost:3000`

## Tests and build
```bash
npm run test -w apps/api
npm run build -w apps/api
npm run build -w apps/web
```

## Project structure
- `apps/api`: API NestJS + Prisma
- `apps/web`: interface web Next.js
- `docs`: B-MAD deliverables

## Notes
- MVP scope is strictly P0.
- P1/P2 features (comparatif cotes multi-sources, export CSV, live, IA, premium) are not implemented in this iteration.
- `next build` may show transient SWC lock warnings on Windows when another process keeps a file handle; re-running the command resolves it.
# overbooke
