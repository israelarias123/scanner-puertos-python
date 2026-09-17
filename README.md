# Escáner de Puertos de Red en Python

Programa de consola que permite verificar qué puertos TCP se encuentran abiertos
en un equipo, dentro de un rango definido por el usuario.

Proyecto académico — Universidad Estatal de Milagro (UNEMI).

---

## Aviso de uso responsable

Este programa es exclusivamente educativo. El escaneo debe realizarse **únicamente** sobre:

- El equipo propio (`127.0.0.1` / `localhost`).
- Máquinas virtuales bajo control del usuario.
- Laboratorios o redes con autorización expresa.

Escanear equipos ajenos sin permiso puede constituir una infracción legal.

---

## Características

- Ingreso de dirección IP o nombre de host (con validación).
- Selección de puerto inicial y puerto final.
- Escaneo concurrente (más rápido que el recorrido secuencial).
- Listado de puertos abiertos con el servicio asociado.
- Resumen con puertos analizados, abiertos, cerrados y tiempo empleado.
- Opción de guardar el resultado en un archivo `.txt`.

---

## Requisitos

| Elemento | Detalle |
|---|---|
| Sistema operativo | Windows, Linux o macOS |
| Python | Versión 3.8 o superior |
| Bibliotecas | `socket`, `sys`, `ipaddress`, `datetime`, `concurrent.futures` (todas incluidas en Python) |
| Editor sugerido | Visual Studio Code |

No se requiere instalar paquetes externos con `pip`.

---

## Instalación

```bash
git clone https://github.com/USUARIO/scanner-puertos-python.git
cd scanner-puertos-python
```

También puede descargarse el archivo `scanner_puertos.py` directamente.

---

## Uso

Modo interactivo:

```bash
python scanner_puertos.py
```

Modo directo (IP, puerto inicial, puerto final):

```bash
python scanner_puertos.py 127.0.0.1 1 100
```

En Linux o macOS puede ser necesario usar `python3` en lugar de `python`.

---

## Ejemplo de ejecución

```
====================================================
                 ESCÁNER DE PUERTOS
====================================================
Uso académico. Escanee solamente equipos propios,
máquinas virtuales o redes autorizadas.
¿Cuenta con autorización para escanear? (s/n): s
----------------------------------------------------
IP: 192.168.1.10
Desde: 1
Hasta: 100
----------------------------------------------------
Escaneando... 100/100 (100.0%)
----------------------------------------------------
Puerto 22 - ABIERTO   (ssh)
Puerto 80 - ABIERTO   (http)
----------------------------------------------------
RESUMEN DEL ESCANEO
Equipo analizado : 192.168.1.10
Rango de puertos : 1 - 100
Puertos analizados: 100
Puertos abiertos  : 2
Puertos cerrados  : 98
Tiempo empleado   : 1.24 segundos
====================================================
```

---

## Estructura del repositorio

```
scanner-puertos-python/
├── scanner_puertos.py
├── README.md
└── MANUAL_USO.md
```

---

## Manual de uso

El manual detallado, con capturas de pantalla, se encuentra en
[MANUAL_USO.md](MANUAL_USO.md).

---

## Integrantes del grupo

| N.° | Nombre completo | Aporte |
|---|---|---|
| 1 | | |
| 2 | | |
| 3 | | |
| 4 | | |

Carrera: _____________  Asignatura: _____________  Docente: _____________
