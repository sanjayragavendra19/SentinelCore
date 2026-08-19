# SentinelCore

An intelligent, full-stack security monitoring system built with **Spring Boot** (backend) and **React + Vite** (frontend). SentinelCore provides real-time threat detection, asset management, vulnerability tracking, SIEM logging, automated playbook execution, and live dashboard monitoring.

---

## Tech Stack

| Layer | Technology |
|---|---|
| Backend | Java 17, Spring Boot 3.2.5 |
| Frontend | React 19, Vite 8, React Router 7 |
| Security | Spring Security, JWT (jjwt 0.11.5), BCrypt |
| Database | H2 (dev), MySQL / PostgreSQL (prod) |
| Real-time | WebSocket (STOMP) |
| API Docs | SpringDoc OpenAPI (Swagger UI) |
| Container | Docker |

---

## Features

- **Authentication** — JWT-based login/signup with role-based access control (RBAC)
- **Asset Management** — Register, track, and manage network assets with metrics, software, processes, and network interfaces
- **Vulnerability Tracking** — CVE-linked vulnerability records per asset
- **Alert System** — Real-time security alerts with severity classification
- **SIEM Logging** — Centralized security event and incident log management
- **Threat Intelligence** — Threat feed ingestion and intel correlation
- **Network Discovery** — Automated network scan and device discovery
- **FIM (File Integrity Monitoring)** — Track file changes across monitored assets
- **Process Monitoring** — Monitor running processes on registered assets
- **Incident Response** — Manage and respond to security incidents
- **Playbook Automation** — Create and execute multi-step automated response playbooks with actions: Block IP, Isolate Host, Disable User, Notify Analyst, Run Script, Call REST API, Generate Report, and more
- **Enterprise Reports** — Generate comprehensive security reports
- **WebSocket Dashboard** — Live broadcast of dashboard metrics to connected clients
- **Audit Logs** — Full audit trail of user and system actions

---

## Project Structure

```
sentinelcore/
├── src/
│   ├── main/java/com/example/myapp/
│   │   ├── config/          # Security, CORS, JWT filter, WebSocket, Swagger
│   │   ├── controller/      # REST API controllers
│   │   ├── service/         # Business logic (interfaces + impl)
│   │   ├── repository/      # Spring Data JPA repositories
│   │   ├── model/           # JPA entities
│   │   ├── dto/             # Request/Response DTOs
│   │   ├── enums/           # UserRole, AssetType, OrderStatus
│   │   ├── mapper/          # Entity ↔ DTO mappers
│   │   ├── exception/       # Global exception handling
│   │   ├── util/            # JWT utility, Date utility
│   │   ├── websocket/       # WebSocket handler & broadcaster
│   │   └── playbook/        # Playbook engine (entities, services, actions)
│   ├── main/resources/
│   │   ├── application.yml          # Base config (port: 5000)
│   │   ├── application-dev.yml      # H2 in-memory DB
│   │   └── application-prod.yml     # Production DB config
│   └── (React frontend)
│       ├── pages/           # Login, Signup, Dashboard
│       ├── components/      # Sidebar, Header, Cards, Charts, DeviceTable, RiskScore
│       └── Router/          # AppRouter (React Router)
├── Dockerfile
├── pom.xml
└── package.json
```

---

## Getting Started

### Prerequisites

- Java 17+
- Maven 3.8+
- Node.js 18+
- npm 9+

---

### 1. Clone the Repository

```bash
git clone https://github.com/sanjayragavendra19/SentinelCore.git
cd SentinelCore
```

---

### 2. Run the Backend

The backend runs on **port 5000** by default using an H2 in-memory database in dev mode.

```bash
./mvnw spring-boot:run
```

On Windows:

```bash
mvnw.cmd spring-boot:run
```

- API Base URL: `http://localhost:5000`
- Swagger UI: `http://localhost:5000/swagger-ui/index.html`
- H2 Console (dev only): `http://localhost:5000/h2-console`

---

### 3. Run the Frontend

```bash
npm install
npm run dev
```

- Frontend URL: `http://localhost:5173`

---

### 4. Environment Variables (Optional)

Override defaults using environment variables:

| Variable | Default | Description |
|---|---|---|
| `SPRING_PROFILES_ACTIVE` | `dev` | Active Spring profile (`dev` / `prod`) |
| `SPRING_DATASOURCE_URL` | H2 in-memory | JDBC URL for the database |
| `SPRING_DATASOURCE_DRIVER` | `org.h2.Driver` | JDBC driver class |
| `SPRING_DATASOURCE_USERNAME` | `sa` | Database username |
| `SPRING_DATASOURCE_PASSWORD` | `password` | Database password |

---

### 5. Run with Docker

Build and run the backend container:

```bash
docker build -t sentinelcore .
docker run -p 5000:5000 sentinelcore
```

To use MySQL or PostgreSQL in production, pass environment variables:

```bash
docker run -p 5000:5000 \
  -e SPRING_PROFILES_ACTIVE=prod \
  -e SPRING_DATASOURCE_URL=jdbc:postgresql://<host>:5432/<db> \
  -e SPRING_DATASOURCE_DRIVER=org.postgresql.Driver \
  -e SPRING_DATASOURCE_USERNAME=<user> \
  -e SPRING_DATASOURCE_PASSWORD=<password> \
  sentinelcore
```

---

## API Endpoints (Summary)

| Module | Base Path |
|---|---|
| Auth | `/api/auth` |
| Users | `/api/users` |
| Assets | `/api/assets` |
| Alerts | `/api/alerts` |
| Vulnerabilities | `/api/vulnerabilities` |
| SIEM Logs | `/api/siem-logs` |
| Threat Feeds | `/api/threat-feeds` |
| Threat Intel | `/api/threat-intel` |
| Network Discovery | `/api/network-discovery` |
| FIM | `/api/fim` |
| Process Monitoring | `/api/processes` |
| Metrics | `/api/metrics` |
| Incident Response | `/api/incidents` |
| Playbooks | `/api/playbooks` |
| Playbook Executions | `/api/executions` |
| Reports | `/api/reports` |
| Notifications | `/api/notifications` |
| System Health | `/api/health` |
| Agent | `/api/agent` |

Full interactive documentation available at `/swagger-ui/index.html`.

---

## Frontend Routes

| Path | Page |
|---|---|
| `/` | Login |
| `/signup` | Signup |
| `/dashboard` | Main Dashboard |

---

## Running Tests

```bash
./mvnw test
```

---

## License

This project is for educational and demonstration purposes.
