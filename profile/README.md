# FamilyTree

FamilyTree is a web application by GTA for building, exploring and sharing family trees.
Families record their members, link generations together and keep their history in one place, from any device.

**Live app:** [familytree.gta-it.com](https://familytree.gta-it.com)

## What the app does

- Build several family trees per account, each in its own interactive canvas.
- Add members with photos, birth and death dates, and personal notes.
- Link parents and children (biological or adoptive) and couples (with marriage and divorce dates).
- Generations and layout are computed automatically, with manual drag and drop on top.
- Share a tree by invitation or by link, with viewer or editor roles.
- Export a tree to PDF or image.
- Available in French, English and German, with light and dark themes.
- Free plan plus paid plans (Premium monthly, Premium yearly, Family Pack), paid by mobile money through Smobilpay.

## Repositories

| Repository | Content |
|---|---|
| `Genealogy-tree` | The application: `genealogy-backend` (API, workers, database migrations) and `genealogy-frontend` (web app) |

## Tech stack

**Backend**

- Python, FastAPI, SQLAlchemy
- PostgreSQL with Alembic migrations
- Redis and Celery for background jobs (exports, payment checks)
- Transactional emails rendered with Jinja

**Frontend**

- React 19, Vite, React Router
- React Flow with dagre and ELK for tree layout
- i18next for translations

**Platform**

- Docker images, deployed with Docker Compose
- GitHub Actions for lint, type checks, tests, security scans (Bandit, Semgrep, pip-audit, npm audit, Trivy) and deployment

## Architecture

- The browser only talks to the backend API, through the frontend's web server.
- The database and Redis live on a private Docker network and are reachable only by the backend.
- Each environment (staging, production) runs as its own isolated stack: separate containers, network and database.

## Environments and releases

| Environment | Deployed when |
|---|---|
| Staging | Every push to `main` |
| Production | Manual run of the deploy workflow on `main` with `deploy_prod` checked |

Pull requests run the full check suite (lint, tests, build) without deploying.

## Contributing

1. Branch from `main`.
2. Open a pull request to `main` and get the checks green.
3. Database changes ship with an Alembic migration.
4. Secrets never go in the repository: environment files live on the servers and in GitHub environment secrets.

---

Built and maintained by [GTA](https://gta-it.com).
