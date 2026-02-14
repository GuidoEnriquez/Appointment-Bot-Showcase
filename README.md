# 🤖 Appointment Management Bot (WhatsApp) 📅

Este repositorio contiene la documentación y arquitectura de un sistema de gestión de turnos automatizado vía WhatsApp, diseñado específicamente para optimizar la agenda de profesionales independientes y clínicas odontológicas.

> **Nota:** El código fuente de este proyecto es privado. Este repositorio sirve como demostración técnica de la arquitectura y funcionalidades implementadas.

## 🚀 Funcionalidades Principales

- **Agendamiento Automático:** Interfaz conversacional 100% automatizada para consultar servicios, fechas y horarios disponibles sin intervención humana.
- **Encuestas Nativas:** Uso de **WhatsApp Polls** para una experiencia de usuario (UX) fluida y sin errores de tipeo.
- **Sincronización en Tiempo Real:** Validación instantánea contra base de datos para evitar _overbooking_ o solapamientos.
- **Recordatorios Inteligentes:** Sistema de notificaciones cronometradas (24hs y 2hs antes) para reducir el ausentismo de pacientes.
- **Panel de Administración:** Comandos específicos y acceso a dashboard de base de datos para gestión total de la agenda.

## 🛠️ Stack Técnico

El proyecto ha sido construido utilizando tecnologías robustas y escalables:

- **Engine:** [Node.js](https://nodejs.org/) (Entorno de ejecución de alto rendimiento).
- **Librería de WhatsApp:** `whatsapp-web.js` (Automatización basada en Puppeteer/Chrome Headless).
- **Base de Datos:** [PostgreSQL](https://www.postgresql.org/) (Persistencia de datos relacional robusta).
- **Orquestación:** [Docker](https://www.docker.com/) & Docker Compose (Despliegue contenerizado de la App y BD).
- **Programación de Tareas:** `node-cron` (Gestión precisa de recordatorios background).

## 🏗️ Arquitectura y Despliegue

El sistema sigue una arquitectura modular y está contenerizado para garantizar consistencia entre entornos de desarrollo y producción.

### Diagrama de Flujo Simplificado

1.  **Usuario** inicia conversación ("Hola").
2.  **Bot** responde con Menú Interactivo (Poll).
3.  **Usuario** selecciona servicio/fecha.
4.  **Bot** consulta disponibilidad en **PostgreSQL**.
5.  **Bot** confirma turno y agenda recordatorios automáticos.

### Despliegue con Docker

El proyecto se levanta con un solo comando gracias a la orquestación de servicios:

```bash
# Inicia la App y la Base de Datos PostgreSQL
docker-compose up -d
```

## 📸 Capturas de Pantalla (Demo)



---

### ¿Te interesa implementar algo similar?

📩 Contáctame para discutir sobre automatización y bots a medida.
