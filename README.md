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
<img width="1345" height="633" alt="Screenshot 2026-09-01 080953" src="https://github.com/user-attachments/assets/3b4a66bb-d6b2-4f5c-9dc9-04734918455d" />

</p>

---

## El Origen de Mi Proyecto

FVS Monitor nació como la idea de remplazar un antiguo monitor que teniamos hecho en Visual Basic (de origen chino) funcionada, pero se sentia algo obsoleto, con opciones súper limitadas y ninguna capacidad de personalización. 

Al principio, mi intención era simplemente modificar esa aplicación original para darle un refresh y hacer una traduccion bien (porque tenia caracteres chinos ahaha), pero al encontrarme con tantos bloqueos y problemas para manipularla, decidí mejor crear algo nuevo. Creé una primera versión de escritorio en Python que copiaba exactamente la misma funcionalidad. pero para evitar los problemas de cyberseguridad de tener que distribuir e instalar un `.exe` máquina por máquina dentro de un entorno empresarial, decidí dar un paso más y migrar el proyecto a una aplicación web para que cualquier persona pudiera utilizarla en cualquier lugar usando la intranet con solo entrar a una URL.

Lo que empezó como intentar actualizar una aplicacion se fue convirtiendo en nuestro HUB central para todos los técnicos e ingenieros, sustituyendo por completo a la antigua aplicación china. 

FVS Monitor a seguido evolucionando: se agregaron integraciones con otras aplicaciones web existentes (como Shopfloor, Testpoint y Toolpoint) y se volvió más inteligente, llevando el control de activaciones de los equipos, enviando notificaciones a los usuarios para realizar sus mantenimientos, ayudando a llenar los diversos checklist diarios en linea con la informacion recopilada en FVS MONITOR etc. Al final, el objetivo de mi herramienta es optimizar y facilitarnos "la vida" en el trabajo, evitando tener que navegar entre un montón de carpetas, servidores o páginas web distintas, y concentrando todo lo que necesitamos saber en una sola pantalla, al alcance de un click.

FVS MONITOR comenzo a construirse el 24 de octubre de 2025. Constantemente recibe actualizaciones y es nuestra herramienta del dia a dia junto a sus apps hermanas `SerialInsight` y `LogFinder`.

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
