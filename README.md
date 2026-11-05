# 🏡 APP Vesta

Plataforma web de alquileres temporarios y residenciales que conecta a usuarios con propiedades mediante búsqueda avanzada, gestión de reservas e integración de pagos online.

## 🌐 Demo en vivo

| Servicio | URL |
|---|---|
| Frontend (Vercel) | https://proyecto-final-grupo-2.vercel.app/ |
| Backend API (Render) | 	https://proyecto-final-grupo-2.onrender.com |
| Documentación Swagger | https://proyecto-final-grupo-2.onrender.com/api |

> ⏳ El backend corre en el plan gratuito de Render: la primera petición después de un rato de inactividad puede tardar ~50 segundos en responder.

## ✨ Funcionalidades

- 🔎 Búsqueda de propiedades con filtros por ubicación, precio, capacidad y tipo de alquiler.
- 📅 Gestión de reservas y disponibilidad de propiedades.
- 💳 Integración con Mercado Pago para pagos online.
- ❤️ Sistema de favoritos para usuarios registrados.
- 🔐 Autenticación con JWT y Google OAuth.
- 🗺️ Visualización de ubicaciones mediante Mapbox.
- 🤖 Chatbot con inteligencia artificial para consultas y búsqueda de propiedades.

## 🛠️ Tecnologías

| Capa | Stack |
|---|---|
| Frontend | Next.js, React, TypeScript, Zustand, React Hook Form + Zod |
| Backend | NestJS, Node.js, TypeScript, Swagger |
| Base de datos | PostgreSQL, TypeORM (migraciones) |
| Integraciones | Mercado Pago, Google OAuth, Mapbox, Cloudinary, SendGrid, Groq (IA) |
| Deploy | Vercel (frontend), Render (backend), Neon (PostgreSQL) |

## 📁 Estructura del repositorio

```
.
├── back/            # API REST en NestJS
│   └── src/
│       ├── config/      # DataSource de TypeORM
│       ├── migrations/  # Migraciones de la base de datos
│       ├── modules/     # auth, users, properties, reservations, payments,
│       │                # appointments, chatbot, cloudinary, mail, support
│       └── seed/        # Datos iniciales y creación de admin
├── front/           # Aplicación Next.js
│   └── src/         # app, components, services, store, hooks, schemas...
└── Vesta DER.pdf    # Diagrama entidad-relación
```

## ⚙️ Instalación local

### Requisitos previos

- Node.js 20 o superior y npm
- PostgreSQL (local o una base en [Neon](https://neon.tech))
- Cuentas/credenciales de: Google Cloud (OAuth), Mercado Pago, Mapbox, Cloudinary, SendGrid y Groq

### 1. Clonar el repositorio

```bash
git clone https://github.com/appvestapf/Proyecto-Final-Grupo-2.git
cd Proyecto-Final-Grupo-2
```

### 2. Backend

```bash
cd back
npm install
```

Crear un archivo `back/.env`:

```env
# Servidor
PORT=3001
FRONTEND_URL=http://localhost:3000

# Base de datos
DATABASE_URL=postgresql://usuario:password@localhost:5432/vesta

# Auth
JWT_SECRET=una_clave_secreta_larga
GOOGLE_CLIENT_ID=
GOOGLE_CLIENT_SECRET=
GOOGLE_CALLBACK_URL=http://localhost:3001/auth/google/callback

# Mercado Pago
MERCADOPAGO_ACCESS_TOKEN=

# Cloudinary
CLOUDINARY_CLOUD_NAME=
CLOUDINARY_API_KEY=
CLOUDINARY_API_SECRET=

# Mails (SendGrid)
SENDGRID_API_KEY=
MAIL_FROM_EMAIL=
MAIL_FROM_NAME=Vesta
SUPPORT_INBOX_EMAIL=

# Chatbot IA (Groq)
GROQ_API_KEY=
```

Correr las migraciones, cargar datos de prueba y levantar el servidor:

```bash
npm run migration:run   # crea las tablas (synchronize está desactivado)
npm run seed            # opcional: carga propiedades de ejemplo
npm run make-admin      # opcional: crea un usuario administrador
npm run start:dev
```

La API queda en `http://localhost:3001` y la documentación Swagger en `http://localhost:3001/api`.

### 3. Frontend

En otra terminal:

```bash
cd front
npm install
```

Crear un archivo `front/.env.local`:

```env
NEXT_PUBLIC_API_URL=http://localhost:3001
NEXT_PUBLIC_MAPBOX_TOKEN=
```

```bash
npm run dev
```

La app queda disponible en `http://localhost:3000`.

## 📜 Scripts útiles

**Backend (`back/`)**

| Script | Descripción |
|---|---|
| `npm run start:dev` | Servidor en modo desarrollo con recarga |
| `npm run build` / `npm run start:prod` | Compilar y correr en producción |
| `npm run migration:generate -- src/migrations/Nombre` | Generar una migración a partir de las entidades |
| `npm run migration:run` / `migration:revert` | Aplicar o revertir migraciones |
| `npm run seed` | Cargar datos de ejemplo |
| `npm run make-admin` | Crear un usuario administrador |
| `npm test` / `npm run test:e2e` | Tests unitarios / end-to-end |
| `npm run lint` | Linter (oxlint) |

**Frontend (`front/`)**

| Script | Descripción |
|---|---|
| `npm run dev` | Servidor de desarrollo de Next.js |
| `npm run build` / `npm start` | Build y servidor de producción |
| `npm test` | Tests con Jest |
| `npm run lint` | ESLint |

## 🚀 Deploy

- **Frontend → Vercel:** root directory `front`, con las variables `NEXT_PUBLIC_API_URL` (URL de Render) y `NEXT_PUBLIC_MAPBOX_TOKEN`.
- **Backend → Render:** root directory `back`, build `npm install && npm run build`, start `npm run start:prod`. Cargar todas las variables del `.env`, usando la URL de Vercel en `FRONTEND_URL` y `https://TU-API.onrender.com/auth/google/callback` en `GOOGLE_CALLBACK_URL`.
- **Base de datos → Neon:** usar el connection string de Neon como `DATABASE_URL` y correr `npm run migration:run` contra esa base.

## 🎯 Objetivo del proyecto

Desarrollado como proyecto final grupal (Grupo 2) de Henry, APP Vesta busca ofrecer una experiencia de alquiler digital intuitiva, segura y accesible, integrando herramientas modernas de desarrollo web y automatización.
