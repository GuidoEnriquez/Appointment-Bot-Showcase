# 🤖 Turno-Bot: Ecosistema de Reservas para WhatsApp

Este proyecto es un sistema dual e inteligente para la gestión de turnos ("SaaS Conserje"). Consta de un Bot automático de WhatsApp (desarrollado en Node.js) que atiende a los pacientes usando menús interactivos, y un Panel de Administración (Dashboard) construido en React + Tailwind + Vite para gestionar toda la clínica en tiempo real.

## ✨ Características Principales

### 📱 1. Asistente Virtual (Bot WhatsApp)

- **Menú Interactivo sin Texto Libre:** Usa encuestas nativas de WhatsApp para ofrecer opciones claras (Pedir Turno, Mis Turnos, Contacto).
- **Flujo Multi-Médico:** El paciente selecciona qué especialidad necesita y a qué especialista desea ver (si hay más de uno).
- **Control Inteligente de Agenda:** Conoce exactamente el horario base del doctor seleccionado, horas de almuerzo, turnos pre-reservados de otros pacientes y salta automáticamente los "Días Bloqueados" (Feriados y vacaciones).
- **Stateful Memoria Temporal:** Recuerda la conversación del paciente durante 10 minutos (estado `WAITING_DNI` o `DATE_SELECTION`) evitando confusión.
- **Auto-cancelación Segura:** Los pacientes pueden ver una lista de sus propios turnos pendientes y cancelarlos sin intervención humana.

### 💻 2. Panel Administrativo (React Dashboard)

Un completo panel web moderno vinculado a Supabase (PostgreSQL) para controlar al bot en caliente:

- **Vista Hogar Diario:** Tablero de control y métricas para la secretaria sobre los turnos confirmados del día actual.
- **Gestión Visual de Agenda:** Permite marcar en clics qué días trabaja un médico, qué descanso tiene y qué feriados se bloquearán en el calendario. Todo se reporta al instante al bot.
- **Gestión de Personal:** Altas y bajas de servicios (con valores en minutos para bloquear slots) y perfiles médicos.
- **Comandos de Cerebro Dinámicos (Settings):** Una pestaña donde la secretaria puede cambiar los textos que escribe el bot (mensajes de bienvenida, despedida, dirección) en milisegundos sin tocar ni una línea de código ni reiniciar el servidor.

## 🛠️ Requisitos Previos

- Node.js (v16+) y npm/yarn instalados.
- Cuenta habilitada en [Supabase](https://supabase.com/).
- Un número de WhatsApp disponible en un celular (se usará como el bot).
- La base de datos SQL de Supabase importada con las tablas `turnos`, `servicios`, `medicos`, `horarios`, `bloqueos`, `configuracion`.

## 🚀 Instalación y Despliegue

> **[INFO SAAS]:** Si deseas desplegar este bot en un servidor de Producción (Nube) para comercializarlo a nuevos clientes, por favor lee el manual avanzado: [Manual de Despliegue SaaS (README_SAAS.md)](README_SAAS.md). Las instrucciones a continuación son para entorno de desarrollo local.

### 🔙 Configuración del Bot (Backend)

1. Instalar las dependencias de Node.
   ```bash
   cd turno-bot
   npm install
   ```
2. Renombra/crea el archivo `.env` en la raíz de la carpeta `turno-bot` colocando la cadena de conexión de Supabase.
   ```env
   DB_USER=tu_usuario_postgres
   DB_PASSWORD=tu_contraseña_aqui
   DB_HOST=aws-0-xx-xxxx-x.pooler.supabase.com
   DB_PORT=6543
   DB_NAME=postgres
   ```
3. Ejecutar el asistente:
   ```bash
   npm start
   ```
   > Aparecerá un QR en la terminal. Escanéalo usando Dispositivos Vinculados en WhatsApp para conectar la sesión (usa la librería `whatsapp-web.js` y `puppeteer-core`).

### 🖥️ Configuración del Panel Web (Dashboard)

1. Abre una nueva ventana de terminal y dirígete al frontend.
   ```bash
   cd dashboard
   npm install
   ```
2. Crea tu archivo `.env` allí mismo colocando las variables públicas de Supabase para la autenticación:
   ```env
   VITE_SUPABASE_URL=https://xxxxxxxxxxxx.supabase.co
   VITE_SUPABASE_ANON_KEY=eyJhbG...
   ```
3. Lanza el servidor de desarrollo:
   ```bash
   npm run dev
   ```
   > Visita `http://localhost:5173`. Ingresa con tu cuenta administradora. Todo cambio (fechas, médicos nuevos, textos en Settings) afectará al bot de forma instantánea.

## 🤝 Contribución

¡Si deseas mejorar el motor de renderizado de horas o agilizar el bot envíame tu Pull Request! Validar el linter interno corriendo `npm run lint` sobre la carpeta `dashboard` antes.
