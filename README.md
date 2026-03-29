# GearGuard

A full-stack equipment maintenance tracker built with Flask, MySQL, React, and TypeScript.

GearGuard helps teams manage equipment, monitor maintenance status, and organize operational workflows from a single dashboard-style interface.

## Table of Contents

- Overview
- Tech Stack
- Current Status
- Project Structure
- Prerequisites
- Quick Start
- Environment Variables
- API Reference
- Frontend Features
- Database
- Testing
- Deployment Notes
- Security Notes
- Contributing
- License

## Overview

This repository contains two primary applications:

- backend: A Flask API connected to MySQL
- frontend: A React + TypeScript UI (Vite)

The frontend currently provides rich UI flows and module screens. The backend currently exposes foundational endpoints and database connectivity through a demo status-check resource.

## Tech Stack

Backend:

- Python 3.11+
- Flask 3.1.2
- Flask-CORS 6.0.2
- PyMySQL 1.1.2
- python-dotenv

Frontend:

- React 18
- TypeScript
- Vite 6
- Radix UI components
- Tailwind CSS utilities
- Recharts

Database:

- MySQL 8+ (MariaDB compatible)

## Current Status

Implemented:

- Flask API service is running and connected to MySQL
- CORS is configured for API routes
- CRUD-style demo endpoints for status checks
- React frontend with multi-module equipment maintenance UI

In progress / planned:

- Full domain API implementation (equipment, maintenance, team, categories)
- Authentication and authorization
- Replacing frontend static/demo state with live API integration

## Project Structure

```text
hackathon/
|-- README.md
|-- INTEGRATION_SUMMARY.md
|-- test_result.md
|-- backend/
|   |-- requirements.txt
|   `-- server.py
|-- frontend/
|   |-- package.json
|   |-- vite.config.ts
|   |-- index.html
|   |-- build/
|   `-- src/
|       |-- App.tsx
|       |-- main.tsx
|       |-- index.css
|       `-- components/
|-- frontend_old_backup/
`-- tests/
```

## Prerequisites

- Python 3.11 or newer
- Node.js 18 or newer (Node.js 20 recommended)
- npm
- MySQL 8+ (or compatible MariaDB)

## Quick Start

### 1) Clone and enter the project

```bash
git clone <your-repo-url>
cd hackathon
```

### 2) Start the backend

```bash
cd backend
pip install -r requirements.txt
python server.py
```

Backend default URL:

- http://localhost:8001
- API base: http://localhost:8001/api

### 3) Start the frontend

In a new terminal:

```bash
cd frontend
npm install
npm run dev
```

Frontend default dev URL (Vite):

- http://localhost:5173

### 4) Build frontend for production

```bash
cd frontend
npm run build
```

## Environment Variables

Create backend environment variables (for local development) in backend/.env:

```env
MYSQL_HOST=localhost
MYSQL_USER=root
MYSQL_PASSWORD=root123
DB_NAME=test_database
CORS_ORIGINS=*
```

Optional frontend environment variables in frontend/.env:

```env
VITE_API_URL=http://localhost:8001/api
VITE_BACKEND_URL=http://localhost:8001
```

## API Reference

Base URL:

- http://localhost:8001/api

### Health Check

- Method: GET
- Endpoint: /api/
- Response:

```json
{
  "message": "Hello World"
}
```

### Create Status Check

- Method: POST
- Endpoint: /api/status
- Body:

```json
{
  "client_name": "Acme Corp"
}
```

- Success response (201):

```json
{
  "id": "uuid",
  "client_name": "Acme Corp",
  "timestamp": "2026-03-29T10:00:00"
}
```

### List Status Checks

- Method: GET
- Endpoint: /api/status

### Delete Status Check

- Method: DELETE
- Endpoint: /api/status/{status_id}

## Frontend Features

The frontend includes screens and flows for:

- Authentication (login/register UI)
- Dashboard and KPI-style overview
- Equipment management
- Maintenance tracking and details
- Team management
- Calendar view
- Kanban board
- Analytics dashboard
- Categories and settings

Note: Most screens are currently UI-driven and still need full backend binding.

## Database

Current required demo table:

```sql
CREATE TABLE IF NOT EXISTS status_checks (
  id VARCHAR(36) PRIMARY KEY,
  client_name VARCHAR(255) NOT NULL,
  timestamp DATETIME NOT NULL
);
```

You can create the database and table with:

```sql
CREATE DATABASE IF NOT EXISTS test_database;
USE test_database;

CREATE TABLE IF NOT EXISTS status_checks (
  id VARCHAR(36) PRIMARY KEY,
  client_name VARCHAR(255) NOT NULL,
  timestamp DATETIME NOT NULL
);
```

## Testing

Backend smoke tests with curl:

```bash
curl http://localhost:8001/api/

curl -X POST http://localhost:8001/api/status \
  -H "Content-Type: application/json" \
  -d '{"client_name":"Test Client"}'

curl http://localhost:8001/api/status
```

Project also includes a tests folder for expanding automated tests.

## Deployment Notes

- frontend/build contains a production bundle artifact
- backend/server.py runs on port 8001 by default
- Use a production WSGI server (for example Gunicorn) and managed process runner for production environments

## Security Notes

Before production use:

- Replace default database credentials
- Restrict CORS to trusted frontend origins
- Add authentication and role-based authorization
- Add request validation and rate limiting
- Store secrets securely (not in source control)

## Contributing

1. Create a feature branch
2. Make focused changes
3. Run local checks and smoke tests
4. Open a pull request with a clear description

## License

This project is currently provided for development and hackathon/demo purposes.
