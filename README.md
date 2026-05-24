# DataLearn - Aprende Bases de Datos

Plataforma educativa interactiva para aprender fundamentos de bases de datos.

## Stack Tecnológico

### Backend
- **Java 21** + **Spring Boot 3.4**
- **Spring Data JPA** + **Hibernate**
- **Spring Security** + **JWT** (autenticación)
- **Flyway** (migraciones de base de datos)
- **PostgreSQL**
- **Swagger/OpenAPI** (documentación de API)

### Frontend
- **React 19** + **TypeScript**
- **Vite 7** (build tool)
- **Tailwind CSS 3.4** + **shadcn/ui** - estilos
- **React Router v7** - enrutamiento
- **TanStack Query** - estado de servidor
- **Zustand** - estado global (auth)
- **Axios** - HTTP client
- **React Hook Form** + **Zod** - formularios y validación

---

## Requisitos

- **Java 21+**
- **Maven** (o usar `mvnw` incluido)
- **Node.js 18+**
- **Docker Desktop** (para PostgreSQL)

---

## Cómo ejecutar

### 1. Base de datos (PostgreSQL)

```bash
# Iniciar PostgreSQL + pgAdmin
docker compose -f backend/docker-compose.yml up -d
```

- PostgreSQL: `localhost:5432` - user: `datalearn` / pass: `datalearn123`
- pgAdmin: `http://localhost:5050` - email: `admin@datalearn.com` / pass: `admin123`

### 2. Backend (Spring Boot)

```bash
cd backend
mvn spring-boot:run
```

La API arranca en `http://localhost:8080`

- Swagger UI: `http://localhost:8080/swagger-ui.html`
- API Docs: `http://localhost:8080/v3/api-docs`

### 3. Frontend (React)

```bash
cd frontend
npm install
npm run dev
```

La app arranca en `http://localhost:5173`

---

## Usuarios precargados (seed data)

| Email | Contraseña | Rol |
|---|---|---|
| `demo@datalearn.com` | `demo123` | USER |
| `admin@datalearn.com` | `admin123` | ADMIN |

---

## Contenido educativo (8 módulos)

| # | Módulo | Lecciones |
|---|---|---|
| 1 | Introducción a las Bases de Datos | ¿Qué es una BD?, Tipos de BD, DBMS |
| 2 | Modelo Entidad-Relación | Entidades/Atributos, Relaciones/Cardinalidad, DER |
| 3 | SQL - Fundamentos | SELECT/WHERE/ORDER BY, INSERT/UPDATE/DELETE, LIMIT/DISTINCT |
| 4 | SQL - Joins y Relaciones | INNER JOIN, LEFT/RIGHT JOIN, Llaves foráneas |
| 5 | SQL - Funciones y Agrupación | COUNT/SUM/AVG, GROUP BY/HAVING, Fecha/Texto |
| 6 | Normalización | 1FN, 2FN/3FN, FNBC |
| 7 | Índices y Optimización | Tipos de índices, EXPLAIN |
| 8 | Transacciones y Concurrencia | ACID, COMMIT/ROLLBACK, Niveles de aislamiento |

Cada lección incluye: contenido teórico (Markdown) + 3-5 preguntas de evaluación.

---

## Estructura del proyecto

```
├── backend/                     # Spring Boot API
│   ├── pom.xml
│   ├── docker-compose.yml       # PostgreSQL + pgAdmin
│   └── src/
│       ├── main/java/com/datalearn/
│       │   ├── config/          # Security, CORS, OpenAPI
│       │   ├── controller/      # REST endpoints
│       │   ├── dto/             # Request/Response DTOs
│       │   ├── exception/       # Global error handling
│       │   ├── model/           # JPA entities
│       │   ├── repository/      # Spring Data JPA
│       │   ├── security/        # JWT provider + filters
│       │   └── service/         # Business logic
│       └── main/resources/
│           └── db/migration/    # Flyway SQL migrations
│
├── frontend/                    # React + Vite
│   ├── package.json
│   ├── vite.config.ts
│   ├── tailwind.config.js
│   └── src/
│       ├── components/ui/       # shadcn-style components
│       ├── hooks/               # Custom React hooks
│       ├── layouts/             # MainLayout, AuthLayout
│       ├── lib/                 # API client, utils
│       ├── pages/               # Route pages
│       ├── stores/              # Zustand stores
│       └── types/               # TypeScript interfaces
│
└── README.md
```

---

## API Endpoints

| Método | Ruta | Auth | Descripción |
|---|---|---|---|
| POST | `/api/auth/register` | No | Registro de usuario |
| POST | `/api/auth/login` | No | Login → JWT |
| GET | `/api/auth/me` | Sí | Perfil del usuario |
| GET | `/api/modules` | No | Listar módulos publicados |
| GET | `/api/modules/{slug}` | Sí | Módulo con progreso del usuario |
| GET | `/api/modules/{slug}/lessons/{lessonSlug}` | No | Lección + assessments |
| POST | `/api/progress` | Sí | Guardar progreso |
| GET | `/api/progress` | Sí | Progreso del usuario |
| GET | `/api/progress/stats` | Sí | Estadísticas de progreso |

---

## Mejoras realizadas vs el export original

| Aspecto | Original (Mocha) | Nueva versión |
|---|---|---|
| Backend | Hono (scaffold vacío) | Spring Boot completo |
| Base de datos | D1 (vacío) | PostgreSQL + Flyway |
| Autenticación | Servicio externo Mocha | JWT propio + Spring Security |
| Frontend | Esqueleto sin código | App funcional con 7 páginas |
| Contenido | No existía | 8 módulos, 24 lecciones, 60+ assessments |
| UI | Solo configuración | Sistema de componentes shadcn-style |
| API Docs | No existía | Swagger/OpenAPI |
| Despliegue local | No configurado | Docker Compose |
