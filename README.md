# FVS Monitor 2.0

Actualización de la herramienta de monitoreo en tiempo real para estaciones de prueba industriales. Procesa los logs de forma concurrente y genera estadísticas de calidad en una interfaz web.

![Python](https://img.shields.io/badge/Python-3.9%2B-blue)
![Flask](https://img.shields.io/badge/Framework-Flask-green)
![Server](https://img.shields.io/badge/Server-Waitress-red)
![Status](https://img.shields.io/badge/Status-Production-success)

- [Interfaz y funcionalidades](Funcionalidades.md)
- [Versión anterior (FVS Monitor)](https://github.com/MrAleex3/Dashboard-FVS)

![Vista principal](https://github.com/user-attachments/assets/3b4a66bb-d6b2-4f5c-9dc9-04734918455d)

## Origen del proyecto

FVS Monitor nació como reemplazo del monitor anterior, hecho en Visual Basic (de origen chino): funcionaba, pero se sentía obsoleto, con opciones muy limitadas y sin capacidad de personalización.

Al principio mi intención era modificar esa aplicación original para darle un refresco y traducirla bien, porque tenía caracteres en chino. Pero al encontrar tantos bloqueos y problemas para manipularla, decidí crear algo nuevo. Hice una primera versión de escritorio en Python que copiaba exactamente la misma funcionalidad. Para evitar los problemas de ciberseguridad de tener que distribuir e instalar un `.exe` máquina por máquina dentro de un entorno empresarial, decidí dar un paso más y migrar el proyecto a una aplicación web, para que cualquiera pudiera usarla desde la intranet con solo entrar a una URL.

Lo que empezó como intentar actualizar una aplicación se fue convirtiendo en el HUB central de todos los técnicos e ingenieros, sustituyendo por completo a la aplicación anterior. FVS Monitor ha seguido evolucionando: se agregaron integraciones con otras aplicaciones web (como Shopfloor, Testpoint y Toolpoint), empezó a llevar el control de activaciones de los equipos, a enviar notificaciones a los usuarios para sus mantenimientos y a ayudar a llenar los checklists diarios en línea con la información recopilada. El objetivo es optimizar el trabajo diario, evitando navegar entre un montón de carpetas, servidores o páginas web distintas y concentrando en una sola pantalla todo lo que necesitamos saber.

FVS Monitor se empezó a construir el 24 de octubre de 2025. Recibe actualizaciones constantes y es la herramienta del día a día, junto a sus aplicaciones hermanas SerialInsight y LogFinder.

## Puesta en marcha

FVS Monitor lee los logs directamente desde las carpetas de red donde las estaciones de prueba suben sus archivos. Solo hay que dar acceso a esas rutas y levantar la aplicación.

**1. Mapear las rutas de red**

El equipo donde correrá el sistema debe tener conexión y permisos de lectura hacia las unidades de red o servidores de las estaciones de prueba.

**2. Configurar las rutas**

En el archivo `rutas.ini` se definen las direcciones a monitorear. Se pueden agregar tantas rutas como se necesiten y activarlas o desactivarlas con el parámetro `Enabled`.

La aplicación se abre en el puerto 10000.

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

## Características

- Monitoreo en tiempo real: la información se actualiza automáticamente cada 3 segundos.
- Alto rendimiento: usa `ThreadPoolExecutor` (actualmente 20 hilos) y el servidor WSGI Waitress para atender varias rutas de logs y usuarios simultáneos.
- Lectura por copia temporal ("snapshot") para leer archivos que se están escribiendo de forma activa sin interferir con el proceso.
- Trazabilidad histórica: buscador para rastrear el historial de un serial en los últimos 7 días.
- Estadísticas de calidad: cálculo automático de yield (Pass/Fail), top 10 de fallas más recurrentes y detección de rachas de fallas consecutivas.
- Interfaz con tema oscuro y notificaciones tipo toast para las alertas.

## Autor

Alejandro Espinoza
Foxconn México
