# S.A.M. — Stakeholder Analysis & Mapping

A full-stack Dockerized app for managing stakeholders across projects.

## Features

- **Power/Interest Matrix** — Visualize stakeholders by influence and interest level
- **Relationship Network** — Map connections between stakeholders (reports to, influences, collaborates, etc.)
- **Stakeholder List** — Table view with filterable columns
- **Detail Panel** — Click any stakeholder for full profile
- **Multi-project** — Manage multiple projects independently

## Quick Start

```bash
# Clone / place project, then:
cd sam
docker compose up --build
```

Open **http://localhost:5173** in your browser.

## Architecture

```
sam/
├── docker-compose.yml
├── backend/          # Express REST API (port 4000)
│   ├── Dockerfile
│   └── src/server.js
└── frontend/         # React + Vite (port 5173)
    ├── Dockerfile
    ├── vite.config.js
    └── src/
        ├── App.jsx
        ├── api.js
        ├── constants.js
        ├── styles.css
        └── components/
            ├── Matrix.jsx
            ├── Network.jsx
            ├── StakeholderModal.jsx
            ├── StakeholderDetail.jsx
            ├── RelationshipModal.jsx
            └── ProjectModal.jsx
```

## API Endpoints

| Method | Path | Description |
|--------|------|-------------|
| GET    | /api/projects | List all projects |
| POST   | /api/projects | Create project |
| PUT    | /api/projects/:id | Update project |
| DELETE | /api/projects/:id | Delete project + stakeholders |
| GET    | /api/projects/:pid/stakeholders | List stakeholders |
| POST   | /api/projects/:pid/stakeholders | Add stakeholder |
| PUT    | /api/stakeholders/:id | Update stakeholder |
| DELETE | /api/stakeholders/:id | Remove stakeholder |
| GET    | /api/projects/:pid/relationships | List relationships |
| POST   | /api/projects/:pid/relationships | Add relationship |
| DELETE | /api/projects/:pid/relationships/:rid | Remove relationship |

> **Note:** Data is stored in-memory. For persistent storage, replace the in-memory store with a database (SQLite, Postgres, etc.).

## Stakeholder Fields

- **Name, Role, Organization, Email**
- **Category**: Internal · External · Government · Customer · Supplier · Partner · Community · Media · Investor · Other
- **Interest** (1–5): How much they care about the project
- **Influence** (1–5): How much power they have to affect outcomes
- **Stance**: Champion · Supporter · Neutral · Skeptic · Blocker
- **Notes**: Free-text for engagement strategy, concerns, motivations

## Relationship Types

`reports_to` · `influences` · `collaborates` · `opposes` · `funds` · `approves`
