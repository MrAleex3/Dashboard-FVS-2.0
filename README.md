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

FVS Monitor funciona leyendo los logs directamente desde las carpetas de red donde las estaciones de pruebas suben sus archivos, solo necesitas darle acceso a esas rutas y levantar la app.

**1. Mapear las rutas de red**  
El equipo donde correra el sistema debe tener conexión y permisos de lectura hacia las unidades de red o servidores de las estaciones de prueba.

**2. Configurar las rutas**  
Abre el archivo `rutas.ini` y define las direcciones a monitorear. Puedes agregar tantas rutas como necesites, apagarlas o encenderlas usando el parametro `Enabled`.

```ini
[General]
Description = Lista de rutas FVS Monitor

[Route_1]
Path = \\RutaDeServidor\EquipoPruebas
Enabled = True

[Route_2]
Path = \\RutaDeServidor\EquipoPruebas
Enabled = True

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
