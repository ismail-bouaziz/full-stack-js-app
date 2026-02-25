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

---

## Networks

### frontend network

Contains:
- Nginx
- Authelia
- Redis
- UI

Handles:
- HTTPS traffic
- Authentication
- Session management

---

### backend network

Contains:
- Nginx
- API
- MySQL

Handles:
- Business logic
- Database access

---

## Security Model

- HTTPS enforced (port 443)
- HTTP automatically redirected to HTTPS
- Authentication required before accessing:
  - UI
  - API
- Database is not exposed externally
- UI does NOT communicate directly with MySQL
- Only API communicates with MySQL
- Network isolation enforced via frontend/backend separation

---

## Network Isolation Summary

- Database is only reachable from the backend network
- UI has no direct access to MySQL
- Redis is only used by Authelia
- Nginx is the only public entry point
