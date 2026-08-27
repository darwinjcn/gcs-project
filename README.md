<p align="center">
  <img src="https://raw.githubusercontent.com/darwinjcn/gcs-project/blob/main/captures/vistas-sistema/Ilustración%2034%20-%20Vista%20GCS%20Login.jpg" alt="GCS Login" width="600"/>
</p>

<h1 align="center">Sistema GCS — Gestión de Contingencias Satelitales</h1>
<p align="center">
  <strong>Plataforma Web Centralizada para la Gerencia de Programa Plataforma Satelital de CANTV</strong><br>
  <em>Trabajo Especial de Grado — Certificado de Desarrollador de Software</em><br>
  <sub>UNETI · Programa Nacional de Formación en Informática · Julio 2026</sub>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Stack-Laravel%20%7C%20React%20%7C%20PostgreSQL-4A90E2?style=flat-square"/>
  <img src="https://img.shields.io/badge/Metodología-SCRUM-6DB33F?style=flat-square"/>
  <img src="https://img.shields.io/badge/Estado-MVP%20Completado%20%7C%20En%20Homologación-brightgreen?style=flat-square"/>
</p>

---

## 📋 Índice
- [Equipo de Desarrollo](#-equipo-de-desarrollo)
- [Contexto y Problemática](#-contexto-y-problemática)
- [Objetivos](#-objetivos)
- [Arquitectura y Tecnologías](#-arquitectura-y-tecnologías)
- [Módulos del Sistema](#-módulos-del-sistema)
- [Metodología de Trabajo](#-metodología-de-trabajo)
- [Estructura del Repositorio](#-estructura-del-repositorio)
- [Instalación y Configuración](#-instalación-y-configuración)
- [Artefactos y Documentación](#-artefactos-y-documentación)
- [Pruebas y Validación](#-pruebas-y-validación)
- [Lecciones Aprendidas](#-lecciones-aprendidas)
- [Recomendaciones](#-recomendaciones)
- [Agradecimientos](#-agradecimientos)

---

## 👥 Equipo de Desarrollo

Este proyecto fue concebido, diseñado e implementado por un equipo multifuncional de tres estudiantes del **Programa Nacional de Formación en Informática (PNFI)** de la **Universidad Nacional Experimental de Telecomunicaciones e Informática (UNETI)**, bajo el marco de trabajo ágil **SCRUM**.

| Rol | Nombre | Responsabilidad Principal |
|:---|:---|:---|
| **Product Owner (PO)** | Diana Sierra | Voz del cliente, definición de prioridades, validación de requisitos y aceptación de entregables. |
| **Scrum Master (SM)** | Ana Contreras | Facilitación del equipo, eliminación de impedimentos, gestión de la métrica de velocidad y transparencia del proceso. |
| **Development Team** | Diana Sierra, Ana Contreras, Darwin Colmenares | Diseño de arquitectura, modelado de datos, desarrollo full-stack (Laravel + React), pruebas y despliegue. |

**Tutoría Académica:** Msc. María Herrera (Docente Asesora UNETI)  
**Tutoría Empresarial:** Ing. Rodolfo José Pacheco Hellal (Gerencia General de Proyectos Mayores — CANTV)

---

## 🌍 Contexto y Problemática

La **Gerencia Programa Plataforma Satelital** de **CANTV** opera tres unidades críticas —**Caracas, Camatagua y Baemari**— encargadas de la continuidad de la infraestructura satelital nacional. Durante la fase de diagnóstico participativo (entrevistas, observación directa y revisión documental), el equipo identificó cinco necesidades críticas:

| ID | Necesidad | Impacto Operativo |
|:---|:---|:---|
| **N1** | Falta de un Repositorio Documental centralizado | Información técnica fragmentada en Excel y carpetas compartidas sin control de versiones. |
| **N2** | Falta de un Panel de Alertas en Tiempo Real | Tiempos de comunicación de 30-90 minutos entre sedes, dependiendo de WhatsApp o llamadas. |
| **N3** | Inexistencia de un Foro de Discusión Técnica | Pérdida de conocimiento tácito; soluciones a fallas recurrentes no quedan documentadas. |
| **N4** | Descentralización del Calendario de Eventos | Cada jefe de turno maneja su propio calendario en Outlook; no existe visibilidad única. |
| **N5** | Falta de trazabilidad en la Gestión de Usuarios | Imposible auditar quién modificó un reporte y cuándo; en 2023 se perdió trazabilidad por sobrescritura. |

> *"El MTTR debe bajar a <15 min"* — Prioridad 5/5 del personal técnico encuestado.

---

## 🎯 Objetivos

### Objetivo General
> Desarrollar una plataforma web centralizada para la gestión y trazabilidad de contingencias, enfocada en la optimización de los tiempos de respuesta en la Gerencia de Programa Plataforma Satelital de CANTV.

### Objetivos Específicos
1. **Diagnosticar** la situación actual y cuellos de botella de los procesos de registro y seguimiento de contingencias.
2. **Diseñar** mediante el marco de trabajo Scrum y criterios de seguridad de la información, la arquitectura lógica, el modelo de datos y la interfaz de usuario.
3. **Desarrollar** los módulos funcionales bajo el stack tecnológico PHP/Laravel y PostgreSQL, incluyendo herramientas de logging, gestión de roles y repositorios documentales.
4. **Validar** el rendimiento y la usabilidad de la plataforma mediante pruebas de aceptación de usuario (UAT) y simulacros de contingencias.

---

## 🏗️ Arquitectura y Tecnologías

El sistema implementa una **arquitectura desacoplada (Full-Stack)** optimizada para operar dentro de la **Intranet Corporativa de CANTV**, garantizando baja latencia y cumplimiento de protocolos de seguridad.

| Capa | Tecnología | Justificación Técnica |
|:---|:---|:---|
| **Frontend** | React 19 + Vite | SPA dinámica, consumo asíncrono de API REST, renderizado eficiente de componentes. |
| **Backend** | Laravel 11 (PHP 8.2) | API RESTful robusta, gestión de autenticación con Laravel Sanctum, lógica de negocio modular. |
| **Base de Datos** | PostgreSQL 14+ | Integridad referencial, trazabilidad audit-safe y manejo de datos técnicos satelitales estructurados. |
| **Autenticación** | OAuth 2.0 / Laravel Sanctum | Tokens seguros, control de acceso basado en roles (RBAC), cifrado bcrypt. |
| **Reportes** | jsPDF + jspdf-autotable | Generación de reportes PDF con encabezado institucional, ejecutada en el cliente. |
| **UI/UX** | SweetAlert2, Styled Components | Feedback inmediato al usuario, diseño responsive y adaptado a entornos de misión crítica. |

### Diagrama de Secuencia — Autenticación

```
Usuario → Frontend(React) → Backend(API Laravel) → PostgreSQL
   │            │                      │                  │
   │  Credenciales    POST /login (Payload cifrado)     │
   │            │                      │  Consulta hash  │
   │            │                      │◄────────────────►│
   │            │◄──── 200 OK + Token Sanctum + Rol ────┤
   │◄── Dashboard según Rol ──────────│                  │
```

---

## 🧩 Módulos del Sistema

La plataforma consolidó **cinco módulos críticos** más los subsistemas de seguridad y administración:

| Módulo | Descripción | Roles con Acceso |
|:---|:---|:---|
| 🔐 **Seguridad y Autenticación** | Login, recuperación de contraseña por correo (SMTP), bloqueo tras 3 intentos fallidos, cifrado SSL/TLS. | Todos |
| ⚠️ **Gestión de Contingencias** | Registro de fallas satelitales con nivel de criticidad (Baja/Media/Alta), seguimiento de estado (Abierta/En Progreso/Cerrada), filtrado por sede y fecha. | Admin, Supervisor, Operador (lectura/escritura según permisos) |
| 📁 **Repositorio Documental** | Carga, consulta, descarga y eliminación de manuales técnicos (PDF, max 10MB). Control de versiones y registro de auditoría por descarga. | Admin, Supervisor (CRUD); Operador, Visitante (lectura) |
| 💬 **Foro Técnico** | Hilos de discusión temática, respuestas anidadas, marcado de temas como "Resuelto/Cerrado", búsqueda por autor o palabra clave. | Todos (según permisos de escritura) |
| 📅 **Calendario de Eventos** | Visualización mensual de mantenimientos preventivos y ventanas de trabajo. Sincronización con zona horaria de Venezuela. | Admin, Supervisor (CRUD); Operador, Visitante (lectura) |
| 📊 **Reportes** | Generación de reportes PDF consolidados por módulo (Contingencias, Foro, Calendario, Histórico). | Usuarios registrados |
| 🛡️ **Histórico y Auditoría** | Logs inalterables de accesos, cargas, modificaciones y eliminaciones. Resaltado en rojo para accesos fallidos. | Solo Administrador |

### Matriz de Roles (RBAC)

| Función | Visitante | Operador | Supervisor | Administrador |
|:---|:---:|:---:|:---:|:---:|
| Ver contingencias | ✅ | ✅ | ✅ | ✅ |
| Crear/editar contingencias | ❌ | ✅ (propias) | ✅ (propias) | ✅ (todas) |
| Eliminar contingencias | ❌ | ❌ | ✅ (con justificación) | ✅ |
| Gestionar documentos | Ver | Ver | CRUD | CRUD |
| Gestionar foro | Ver | CRUD (propios) | CRUD (propios) | CRUD (todos) |
| Gestionar calendario | Ver | Ver | CRUD | CRUD |
| Ver histórico/auditoría | ❌ | ❌ | ❌ | ✅ |
| Gestionar usuarios | ❌ | ❌ | ❌ | ✅ |

---

## 📊 Metodología de Trabajo

El equipo adoptó **SCRUM** como marco de trabajo ágil, con Sprints de 2 semanas, una velocidad asumida inicial de 20 puntos de historia y un Product Backlog de 33 Historias de Usuario (134 PH totales).

### Planificación de Sprints

| Sprint | Periodo | Objetivo | Historias de Usuario | Puntos | Estado |
|:---|:---|:---|:---|:---:|:---:|
| **Sprint 0** | 3-11-25 al 22-11-25 | Definición, alcance y preparación | Diagnóstico, levantamiento de 24 RF, 33 HU, estimación Planning Poker | — | ✅ Completado |
| **Sprint 1** | 23-11-25 al 6-12-25 | Fundación y Seguridad Inicial | Autenticación, roles, gestión de usuarios, histórico de accesos | 23 | ✅ Completado |
| **Sprint 2** | 7-12-25 al 20-12-25 | Core de Contenido y Trazabilidad | Contingencias (ver/cargar), repositorio documental, logs de auditoría | 20 | ✅ Completado |
| **Sprint 3** | 4-1-26 al 17-1-26 | Foro, Reportes de Seguridad y Usabilidad | Foro técnico (ver/crear/reportar), búsqueda de documentos | 21 | ✅ Completado |
| **Sprint 4** | 18-1-26 al 31-1-26 | Reportes Finales y Usabilidad | Reportes de histórico, filtros de contingencias y foro, calendario | 23 | ✅ Completado |

### Métricas de Rendimiento

- **Velocity Promedio:** ~22 puntos de historia por sprint.
- **Burndown General:** Pendiente inicial de 134 PH → 0 PH al cierre del Sprint 4.
- **Deuda Técnica:** 3 PH arrastrados del Sprint 2 al 3 (generación de reportes PDF), compensados exitosamente.
- **Cobertura MVP:** 100% de requisitos "Must Have" (MoSCoW) entregados.

> 📈 Los gráficos de Burndown y Velocity están disponibles en [`/docs/`](./docs) y en [`/captures/modelado-casos-de-uso-secuencia/`](./captures/modelado-casos-de-uso-secuencia/).

---

## 📁 Estructura del Repositorio

```
gcs-project/
├── 📂 BACKEND/                 # API RESTful — Laravel 11
│   ├── app/
│   │   ├── Http/Controllers/   # Controladores por módulo
│   │   ├── Models/             # Modelos Eloquent (PostgreSQL)
│   │   └── ...                 # Middleware, Requests, Policies
│   ├── config/                 # Configuración de Sanctum, DB, Mail
│   ├── database/
│   │   ├── migrations/         # Esquema relacional completo
│   │   └── seeders/            # Datos iniciales de prueba
│   ├── routes/
│   │   └── api.php             # Endpoints REST protegidos
│   └── storage/
│       └── app/public/         # Almacenamiento de documentos técnicos
│
├── 📂 FRONTEND/                # Aplicación SPA — React 19 + Vite
│   ├── src/
│   │   ├── components/         # Componentes reutilizables (UI)
│   │   ├── pages/              # Vistas por módulo
│   │   ├── services/           # Consumo de API (Axios/Fetch)
│   │   ├── context/            # Gestión de estado global (Auth)
│   │   └── assets/             # Imágenes, logos CANTV/UNETI
│   └── ...                     # Configuración ESLint, Vite
│
├── 📂 captures/                # Evidencias gráficas del proyecto
│   ├── modelado-casos-de-uso-secuencia/  # Diagramas UML (Ilust. 7-33)
│   └── vistas-sistema/         # Screenshots de la interfaz (Ilust. 34-43)
│
├── 📂 docs/                    # Documentación académica y técnica
│   ├── 01.informe-final.pdf    # Informe completo del proyecto
│   ├── Recuperación de Contraseña en Laravel.pdf
│   ├── Correcciones GCS.txt    # Pendientes y mejoras identificadas
│   └── comandos.txt            # Dependencias npm instaladas
│
└── README.md                   # Este archivo
```

---

## ⚙️ Instalación y Configuración

### Requisitos Previos
- PHP >= 8.2
- Composer >= 2.0
- Node.js >= 20 & npm
- PostgreSQL >= 14

### 🔧 Backend (Laravel)

```bash
cd BACKEND

# 1. Instalar dependencias de PHP
composer install

# 2. Configurar variables de entorno
cp .env.example .env
# Editar .env con credenciales de PostgreSQL y configuración SMTP

# 3. Generar clave de aplicación
php artisan key:generate

# 4. Ejecutar migraciones y seeders (opcional)
php artisan migrate --seed

# 5. Crear enlace simbólico para almacenamiento de documentos
php artisan storage:link

# 6. Iniciar servidor de desarrollo
php artisan serve
```

### 💻 Frontend (React + Vite)

```bash
cd FRONTEND

# 1. Instalar dependencias
npm install

# 2. Dependencias adicionales utilizadas en el proyecto
npm i react-router-dom
npm install sweetalert2
npm install jspdf jspdf-autotable
npm install styled-components

# 3. Configurar variable de entorno apuntando al backend
# VITE_API_URL=http://localhost:8000/api

# 4. Iniciar servidor de desarrollo
npm run dev
```

### 🐘 Notas sobre PostgreSQL
Asegúrate de crear la base de datos `gcs_cantv` con codificación `UTF8` y configurar el acceso en el `.env` del backend. El esquema incluye tablas para usuarios, roles, contingencias, documentos, foros, comentarios, eventos de calendario y logs de auditoría con integridad referencial completa.

---

## 📚 Artefactos y Documentación

### Modelado UML
Los diagramas de casos de uso y secuencia se encuentran en [`captures/modelado-casos-de-uso-secuencia/`](./captures/modelado-casos-de-uso-secuencia/):

- **Casos de Uso:** Acceso al sistema, Recuperación de contraseña, Gestión de Contingencias, Documentación, Foro Técnico, Calendario, Reportes, Histórico y Usuarios — modelados por rol (Admin, Supervisor, Operador, Visitante).
- **Diagramas de Secuencia:** Autenticación y seguridad (Ilust. 31), Reporte de contingencia satelital (Ilust. 32), Gestión documental — carga de archivos (Ilust. 33).

### Vistas del Sistema
Screenshots funcionales disponibles en [`captures/vistas-sistema/`](./captures/vistas-sistema/):

| Vista | Descripción |
|:---|:---|
| Login | Pantalla de acceso con validación de dominio `@cantv.com.ve` |
| Recuperación de contraseña | Modal de envío de clave temporal por correo |
| Dashboard | Panel panorámico con alertas activas, documentos, hilos y eventos |
| Contingencias | Tabla cronológica con filtros de prioridad, estado y sede |
| Foro Técnico | Listado de temas abiertos/cerrados con acciones CRUD |
| Documentación | Gestor de archivos técnicos con paginación y búsqueda |
| Calendario | Vista mensual de mantenimientos programados |
| Perfil de usuario | Gestión de contraseña y datos personales |

### Documentación Académica
- **[`docs/01.informe-final.pdf`](./docs/01.informe-final.pdf)** — Informe técnico completo: marco teórico, metodológico, resultados, conclusiones y recomendaciones.
- **[`docs/Recuperación de Contraseña en Laravel.pdf`](./docs/Recuperación%20de%20Contraseña%20en%20Laravel.pdf)** — Especificación técnica del módulo de recuperación de credenciales.

---

## ✅ Pruebas y Validación

### Pruebas de Aceptación del Usuario (UAT)
Ejecutadas en conjunto con el **Product Owner** y el tutor empresarial **Ing. Rodolfo Pacheco**:

| ID | Módulo Evaluado | Criterio de Aceptación | Estado |
|:---|:---|:---|:---:|
| UAT-01 | Seguridad — Autenticación | Denegación con datos erróneos; token válido con Sanctum | ✅ Aprobado |
| UAT-02 | Gestión de Contingencias | Sincronización inmediata API-panel; registro de nodos afectados | ✅ Aprobado |
| UAT-03 | Repositorio Documental | Carga de PDF; restricción de lectura por rol; almacenamiento local funcional | ✅ Aprobado |
| UAT-04 | Foro Técnico | Apertura de hilos y actualización interactiva sin demoras | ✅ Aprobado |

### Plan de Capacitación
Se dictaron **dos sesiones intensivas** de entrenamiento práctico al personal técnico de CANTV bajo la metodología **"Aprender Haciendo"**:

1. **Nivel Operativo** (Ingenieros y Técnicos de Campo): Registro rápido de contingencias, asignación de criticidad, interacción en foro y consulta de calendario.
2. **Nivel Administrativo** (Supervisores e IT): Gestión de roles (RBAC), análisis de logs de auditoría, generación de reportes mensuales.

**Resultado del simulacro crítico:** El 100% del personal participante interactuó de forma autónoma con el sistema, registrando incidencias y localizando manuales en un tiempo promedio **inferior a 2 minutos**.

---

## 🎓 Lecciones Aprendidas

> *"La ingeniería de software está incompleta si no se acompaña de una estrategia de capacitación humana cercana."*

- **Arquitectura Desacoplada:** La separación Laravel/React demostró alta eficiencia en la intranet corporativa, reduciendo el consumo de ancho de banda entre sedes.
- **Gobernanza Digital:** Configurar un entorno de homologación local aislado fue clave para respetar las políticas de seguridad de CANTV y preparar el software para auditorías de código estrictas.
- **Adopción Humana:** Diseñar interfaces limpias y centradas en el usuario venció la resistencia al cambio del personal operativo, validando que la UX es tan crítica como la robustez de PostgreSQL.
- **Dinámica Ágil:** La gestión por Sprints permitió absorber deuda técnica (Sprint 2→3) sin comprometer la entrega del MVP ni la calidad del producto.

---

## 🔮 Recomendaciones

- **A la Gerencia de Sistemas de CANTV:** Agilizar la auditoría técnica de la plataforma provisional para proceder con la migración definitiva a servidores de producción corporativos.
- **Al Personal Operativo:** Mantener la rigurosidad en el registro inmediato de contingencias y alimentar activamente el foro técnico para consolidar una base de conocimientos robusta.
- **Mantenimiento de Datos:** Implementar política automatizada de backups semanales en PostgreSQL y plan de mantenimiento preventivo para el storage de manuales técnicos.
- **Líneas Futuras:** Planificar módulos de analítica predictiva aprovechando el histórico de fallas acumulado para generar alertas tempranas de hardware recurrente.

---

## 🙏 Agradecimientos

Agradecemos primeramente a **Dios** por la sabiduría y fortaleza en cada etapa del proyecto. A nuestras familias por su apoyo incondicional. A la **profesora María Herrera** por guiarnos con dedicación y exigencia académica. A la empresa **CANTV** y a la **Gerencia Programa Plataforma Satelital** por abrirnos sus puertas y confiarnos un problema real. De manera especial, al **Ingeniero Rodolfo Pacheco Hellal** por su paciencia, su know-how operacional y su respaldo continuo como tutor empresarial.

---

<p align="center">
  <sub>🇻🇪 <strong>Soberanía Tecnológica</strong> — Desarrollado con software libre (Laravel, React, PostgreSQL) bajo los mandatos del Decreto N° 3.390 y la Ley de Infogobierno.</sub><br>
  <sub>© 2026 — Ana Contreras, Diana Sierra, Darwin Colmenares. Todos los derechos reservados.</sub>
</p>