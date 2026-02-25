# Full Stack JS App — Secure Containerized Architecture

## Overview

Full-stack JavaScript application containerized with Docker / Podman Compose and secured with centralized authentication.

### Stack

- React (Frontend UI)
- Node.js + Express (API)
- MySQL (Database)
- Nginx (Reverse Proxy + SSL Termination)
- Authelia (SSO / MFA Authentication Gateway)
- Redis (Session Store for Authelia)

---

## Architecture

![Architecture Diagram](docs/archi_app.png)

---

## Containers

| Service   | Role | Port | Network |
|------------|------|------|----------|
| **Nginx** | Reverse proxy / SSL termination / Auth gateway | 443 (public) | frontend + backend |
| **Authelia** | Authentication (SSO / MFA) | 9091 (internal) | frontend |
| **Redis** | Session store for Authelia | 6379 (internal) | frontend |
| **UI** | React frontend | 3000 (internal) | frontend |
| **API** | Backend REST service | 5050 (internal) | backend |
| **MySQL** | Database | 3306 (internal) | backend |

## Networks

**frontend**
- Nginx
- Authelia
- Redis
- UI

**backend**
- Nginx
- API
- MySQL

---

## Request Flow

Client → Nginx (443)
→ Authelia (9091) → Redis (6379)
→ UI (3000)
→ API (5050)
→ MySQL (3306)


---

## Security

- HTTPS enforced
- Authentication required (UI + API)
- UI does NOT access MySQL directly
- Only API communicates with MySQL
- Database not exposed externally