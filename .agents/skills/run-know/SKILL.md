---
name: run-know
description: >-
  Instructions to run, verify, and manage the Know application stack
  (Vue 3 web client, Spring Boot 3 API, PostgreSQL 16 database, and Caddy proxy)
  for local development and remote testing.
---

# Run Know Application

## 1. Prerequisites & Environment

Required environment variables for compose and backend execution:
- `JWT_SECRET`: Random string with at least 32 characters.
- `POSTGRES_PASSWORD`: Database password for local PostgreSQL.
- Database volume `know-db` persists PostgreSQL data across restarts. Do NOT pass `-v` to `docker compose down` unless resetting database state.

## 2. Launch Full Stack (Docker Compose)

Start all services (Database, API, Web, Caddy Proxy on port 3000):

```bash
JWT_SECRET='development-jwt-secret-at-least-32-chars-long' \
POSTGRES_PASSWORD='dev-postgres-password' \
docker compose up -d --build
```

Verify service health:

```bash
JWT_SECRET='development-jwt-secret-at-least-32-chars-long' \
POSTGRES_PASSWORD='dev-postgres-password' \
docker compose ps
```

Expected output: `db` (healthy), `api` (healthy), `web` (running), `proxy` (healthy).

## 3. Application Access Endpoints

- **Web Application:** `http://localhost:3000` (or `http://127.0.0.1:3000`)
- **API Base:** `http://localhost:3000/api/v1`
- **Actuator Health:** `http://localhost:3000/actuator/health`

### SSH Port Forwarding (Remote Access)
When accessing from a remote computer:
1. Establish SSH tunnel: `ssh -L 3000:localhost:3000 user@<host-ip>`
2. Open in remote browser: `http://localhost:3000` or `http://127.0.0.1:3000`
3. Caddy serves the localhost fallback as plain HTTP on port 3000; configured non-local domains redirect HTTP to HTTPS.

## 4. Frontend Hot-Reload Development (Alternative)

To run the Vue frontend with Vite dev server:

```bash
# 1. Run database and backend only
JWT_SECRET='dev-secret-32-chars' POSTGRES_PASSWORD='dev-password' docker compose up -d db api

# 2. Start Vite dev server on the memorable hot-reload port 5177
(cd frontend && npm install && npm run dev)

Vite binds to `0.0.0.0:5177`, prints `http://localhost:5177` when it starts, and proxies `/api` to the API’s loopback development port 8080. From another machine, use `ssh -L 5177:localhost:5177 user@<host-ip>` and open `http://localhost:5177`.
```

## 5. Teardown & Management

- **Stop containers (preserve data):** `docker compose stop`
- **Restart specific service:** `docker compose restart proxy`
- **Tear down containers (preserve data):** `docker compose down`
- **Tear down with database wipe:** `docker compose down -v`
