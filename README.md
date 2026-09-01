<h1 align="center">FVS Monitor 2.0</h1>

<p align="center">
  Una actualización para la herramienta de monitoreo en tiempo real de estaciones de prueba industriales, procesando logs concurrentemente y generando estadísticas de calidad en una interfaz web moderna.
</p>

<p align="center">
  <a href="#quick-start">Quick Start</a> ·
  <a href="Funcionalidades.md">Interfaz y funcionalidades</a> ·
  <a href="#estructura-del-proyecto">Estructura</a> ·
  <a href="https://github.com/MrAleex3/Dashboard-FVS">Versión Anterior</a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.9%2B-blue" alt="Python">
  <img src="https://img.shields.io/badge/Framework-Flask-green" alt="Flask">
  <img src="https://img.shields.io/badge/Server-Waitress-red" alt="Server">
  <img src="https://img.shields.io/badge/Status-Production-success" alt="Status">
</p>

<p align="center">
  <img width="1354" height="682" alt="Screenshot 2026-09-01 080913" src="https://github.com/user-attachments/assets/57ccf23d-263d-4ad7-a4d9-5b4726499c0c" />

</p>

---

## Quick Start

> Asegúrate de estar en un entorno Windows 10 o superior y contar con acceso a las rutas de red compartidas de las estaciones.

Configura las rutas de red a monitorear y ejecuta el servidor compilado:

```bash
# 1. Define las carpetas en tu archivo de configuración
# Editar rutas.ini

# 2. Ejecuta el servidor y worker
./server.exe
```

## Features
-   **Monitoreo en Tiempo Real:** — Actualiza la informacion automaticamente cada 3 segundos.
-   **Alto Rendimiento (Multi-Hilo):** — Utiliza `ThreadPoolExecutor` (actualmente 20 hilos) y servidor WSGI `Waitress` para manejar multiples rutas de logs y usuarios simultaneos.
-   **Lectura "Snapshot" Segura:** — Cuenta con un sistema de copias temporales para leer archivos que estan siendo escritos activamente y evitar interferir en el proceso.
-   **Trazabilidad Historica:** — Buscador integrado para rastrear el historial de un numero de serie en los ultimos 7 días.
-   
-   **Estadísticas de Calidad:**
    -   Calculo automatico de Yield (Pass/Fail).
    -   Top 10 de fallas mas recurrentes.
    -   Deteccion de "Racha de Fallas" consecutivas.
-   **Interfaz** Tema oscuro y notificaciones "Toast" para alertas.
