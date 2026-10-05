<div align="center">

<img src="assets/banner.png" width="100%" alt="Banner del bot de campaña navideña para iVentas">

# Bot de campaña navideña para iVentas

![Privado](https://img.shields.io/badge/C%C3%B3digo-Privado%20%C2%B7%20Proyecto%20Cliente-red?style=flat)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat&logo=nodedotjs&logoColor=white)
![Puppeteer](https://img.shields.io/badge/Puppeteer-40B5A4?style=flat&logo=puppeteer&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)
![node-cron](https://img.shields.io/badge/node--cron-programaci%C3%B3n-555555?style=flat)

**Bot de automatización que inicia sesión en el portal iVentas, recorre todas las conversaciones abiertas y envía un mensaje navideño a cada cliente en la fecha programada, con reintentos y registro de progreso.**

</div>

> Este es un **portafolio showcase**: el código fuente es propietario y no está incluido.

---

## Contenido

- [El Problema](#el-problema)
- [La Solución](#la-solución)
- [Funcionalidades](#funcionalidades)
- [Vista Previa](#vista-previa)
- [Arquitectura](#arquitectura)
- [Stack Tecnológico](#stack-tecnológico)
- [Instalación local](#instalación-local)
- [Roadmap](#roadmap)
- [Contacto](#contacto)

---

## El Problema

Enviar un saludo de temporada a cientos de clientes por un portal de chat es un trabajo manual y propenso a errores:

- Hay que abrir una por una cada conversación y escribir el mensaje.
- La lista de conversaciones carga por partes, y es fácil olvidar contactos.
- El envío debe ocurrir a una hora precisa, aunque nadie esté frente a la computadora.
- Si algo falla a mitad de camino, no se sabe a quién ya se le envió.

---

## La Solución

Un bot en Node.js con Puppeteer que automatiza el navegador: inicia sesión, desplaza la lista de forma incremental hasta cargar todas las conversaciones, abre cada una y envía el mensaje con una pausa configurable entre envíos. Se programa con una expresión cron (por defecto, el 25 de diciembre a medianoche), reintenta los envíos fallidos y guarda el progreso para poder retomar la campaña sin repetir mensajes.

---

## Funcionalidades

| Funcionalidad | Descripción |
|---------------|-------------|
| Inicio de sesión automático | Entra al portal con las credenciales definidas en variables de entorno |
| Desplazamiento inteligente | Scroll incremental con seguimiento del progreso para cargar todas las conversaciones |
| Programación con cron | Ejecución en la fecha y hora configuradas, o inmediata en modo de prueba |
| Reintentos | Hasta 3 intentos por mensaje antes de marcarlo como fallido |
| Progreso reanudable | Registro de contactos enviados y fallidos para no repetir envíos y reintentar los fallidos |
| Selectores con alternativas | Sistema de selectores con opciones de respaldo y herramienta de mapeo del portal |
| Pausa entre mensajes | Retraso configurable para evitar bloqueos |
| Registros detallados | Logs de color con progreso, estimación de tiempo y resumen final |

---

## Vista Previa

<table>
  <tr>
    <td width="50%">
      <img src="assets/cards/01-inicio-de-sesion-automatico.png" width="100%" alt="Tarjeta sobre el inicio de sesión automático en el portal">
      <br><b>Inicio de sesión automático</b>: el bot entra al portal y carga todas las conversaciones.
    </td>
    <td width="50%">
      <img src="assets/cards/02-programacion-con-cron.png" width="100%" alt="Tarjeta sobre la programación con cron">
      <br><b>Programación con cron</b>: el envío ocurre en la fecha y hora configuradas.
    </td>
  </tr>
  <tr>
    <td width="50%">
      <img src="assets/cards/03-reintentos-y-registros.png" width="100%" alt="Tarjeta sobre reintentos y registros">
      <br><b>Reintentos y registros</b>: reintenta los fallos y guarda el progreso de la campaña.
    </td>
    <td width="50%"></td>
  </tr>
</table>

---

## Arquitectura

```mermaid
graph LR
    CRON["Programador<br/>node-cron"]
    BOT["Bot<br/>Node.js · Puppeteer"]
    PORTAL["Portal iVentas<br/>conversaciones abiertas"]
    PROG[("Progreso<br/>enviados y fallidos")]
    LOGS["Registros<br/>consola y archivos"]

    CRON -->|"Dispara la campaña"| BOT
    BOT -->|"Login, scroll y envío"| PORTAL
    BOT -->|"Guarda el avance"| PROG
    BOT -->|"Progreso y resumen"| LOGS
```

El bot incluye un mapeador del portal que genera archivos de selectores recomendados, y un modo de prueba (`--now`) para ejecutar la campaña de inmediato antes de programarla.

---

## Stack Tecnológico

| Capa | Tecnología |
|------|-----------|
| Entorno | Node.js (módulos ES) |
| Automatización del navegador | Puppeteer |
| Programación | node-cron |
| Configuración | dotenv |
| Registros y progreso | Logger propio · archivo de progreso en JSON |

---

## Instalación local

> **Aviso:** el código es privado y propietario. Estos pasos son solo para colaboradores autorizados con acceso al repositorio.

1. Instala Node.js.
2. Instala las dependencias:
   ```bash
   npm install
   ```
3. Crea un archivo `.env` con tus propias credenciales, el mensaje y la expresión cron.
4. Mapea el portal la primera vez para identificar los selectores:
   ```bash
   npm run map
   ```
5. Prueba la campaña de inmediato o déjala programada:
   ```bash
   npm start -- --now
   npm start -- --schedule
   ```

---

## Roadmap

- [ ] Plantillas de mensaje personalizadas por cliente.
- [ ] Reporte final de la campaña en un archivo descargable.

---

## Contacto

El código fuente es propietario. Para consultas o propuestas, escríbeme:

[![Email](https://img.shields.io/badge/Email-pablozam1931%40gmail.com-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:pablozam1931@gmail.com)
[![WhatsApp](https://img.shields.io/badge/WhatsApp-(507)%206517--1870-25D366?style=for-the-badge&logo=whatsapp&logoColor=white)](https://wa.me/50765171870)
[![GitHub](https://img.shields.io/badge/GitHub-deadlyrat-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/deadlyrat)

- Correo: [pablozam1931@gmail.com](mailto:pablozam1931@gmail.com)
- WhatsApp: [(507) 6517-1870](https://wa.me/50765171870)
- GitHub: [github.com/deadlyrat](https://github.com/deadlyrat)

---

*Parte del portafolio de [deadlyrat](https://github.com/deadlyrat)*
