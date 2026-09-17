# Manual de Uso — Escáner de Puertos de Red

Universidad Estatal de Milagro (UNEMI)

Este manual explica, paso a paso, cómo instalar y utilizar el programa
`scanner_puertos.py`.

---

## Índice

1. [Requisitos](#1-requisitos)
2. [Instalación](#2-instalación)
3. [Cómo iniciar la aplicación](#3-cómo-iniciar-la-aplicación)
4. [Cómo ingresar la IP](#4-cómo-ingresar-la-ip)
5. [Cómo seleccionar el rango de puertos](#5-cómo-seleccionar-el-rango-de-puertos)
6. [Cómo ejecutar el escaneo](#6-cómo-ejecutar-el-escaneo)
7. [Cómo interpretar los resultados](#7-cómo-interpretar-los-resultados)
8. [Guardar el reporte](#8-guardar-el-reporte)
9. [Registro de la prueba experimental](#9-registro-de-la-prueba-experimental)
10. [Solución de problemas](#10-solución-de-problemas)
11. [Advertencia legal](#11-advertencia-legal)

---

## 1. Requisitos

Antes de ejecutar el programa se necesita:

| Requisito | Detalle |
|---|---|
| Computador | Windows, Linux o macOS |
| Python | Versión 3.8 o superior |
| Editor de código | Visual Studio Code (recomendado) |
| Conexión de red | Solo si se escanea otro equipo de la red local |
| Bibliotecas | Ninguna externa: `socket` viene incluida en Python |

Para comprobar si Python está instalado, abra la terminal y escriba:

```bash
python --version
```

Si el sistema responde con algo como `Python 3.12.1`, todo está listo. Si
aparece un error, descargue Python desde <https://www.python.org/downloads/>
y, durante la instalación en Windows, marque la casilla **Add Python to PATH**.

> **Captura 1:** verificación de la versión de Python.
> `![Versión de Python](capturas/01_version_python.png)`

---

## 2. Instalación

El programa consiste en un único archivo, por lo que no requiere instalación
formal.

**Opción A — Clonar el repositorio:**

```bash
git clone https://github.com/USUARIO/scanner-puertos-python.git
cd scanner-puertos-python
```

**Opción B — Descarga manual:**

1. Ingrese al repositorio en GitHub.
2. Presione el botón verde **Code** y elija **Download ZIP**.
3. Descomprima la carpeta en el escritorio.
4. Abra la carpeta con Visual Studio Code (**Archivo → Abrir carpeta**).

> **Captura 2:** carpeta del proyecto abierta en Visual Studio Code.
> `![Proyecto en VS Code](capturas/02_proyecto_vscode.png)`

---

## 3. Cómo iniciar la aplicación

1. Abra una terminal dentro de la carpeta del proyecto.
   En Visual Studio Code: menú **Terminal → Nueva terminal**.
2. Escriba el siguiente comando y presione Enter:

```bash
python scanner_puertos.py
```

En Linux o macOS use `python3 scanner_puertos.py`.

Al iniciar aparece el encabezado del programa y una pregunta de autorización:

```
====================================================
                 ESCÁNER DE PUERTOS
====================================================
Uso académico. Escanee solamente equipos propios,
máquinas virtuales o redes autorizadas.
¿Cuenta con autorización para escanear? (s/n):
```

Escriba `s` y presione Enter para continuar. Cualquier otra respuesta cierra
el programa.

> **Captura 3:** pantalla inicial del programa.
> `![Inicio del programa](capturas/03_inicio.png)`

---

## 4. Cómo ingresar la IP

El programa solicita la dirección del equipo a analizar:

```
IP:
```

Escriba la dirección y presione Enter. Valores admitidos:

| Valor | Significado |
|---|---|
| `127.0.0.1` | El propio computador (recomendado para las pruebas) |
| `localhost` | Equivalente a `127.0.0.1` |
| `192.168.1.10` | Otro equipo de la red local (por ejemplo, una máquina virtual) |

**¿Cómo conocer la IP de su equipo?**

- Windows: ejecute `ipconfig` y observe el valor de *Dirección IPv4*.
- Linux o macOS: ejecute `ip a` o `ifconfig`.

Si la dirección no es válida, el programa muestra un aviso y vuelve a
preguntar, sin cerrarse.

> **Captura 4:** obtención de la IP con `ipconfig` e ingreso en el programa.
> `![Ingreso de IP](capturas/04_ingreso_ip.png)`

---

## 5. Cómo seleccionar el rango de puertos

A continuación se piden dos valores:

```
Desde: 1
Hasta: 100
```

- **Desde:** primer puerto del rango.
- **Hasta:** último puerto del rango.

Reglas de validación:

- Ambos deben ser números enteros entre **1 y 65535**.
- El puerto final no puede ser menor que el inicial.

Rangos sugeridos:

| Rango | Descripción |
|---|---|
| 1 – 100 | Prueba rápida, ideal para la demostración |
| 1 – 1024 | Puertos bien conocidos (HTTP, FTP, SSH, etc.) |
| 1 – 65535 | Análisis completo (tarda considerablemente más) |

> **Captura 5:** ingreso del rango de puertos.
> `![Rango de puertos](capturas/05_rango_puertos.png)`

---

## 6. Cómo ejecutar el escaneo

El escaneo inicia automáticamente después de ingresar el puerto final. Se
muestra el avance en una sola línea:

```
Escaneando... 100/100 (100.0%)
```

El programa intenta abrir una conexión TCP con cada puerto del rango. Si la
conexión se establece, el puerto se considera **ABIERTO**.

Para interrumpir el proceso antes de que termine, presione **Ctrl + C**.

> **Captura 6:** escaneo en ejecución.
> `![Escaneo en proceso](capturas/06_escaneo.png)`

---

## 7. Cómo interpretar los resultados

Al finalizar se presentan dos bloques.

**Listado de puertos abiertos:**

```
Puerto 22 - ABIERTO   (ssh)
Puerto 80 - ABIERTO   (http)
```

Cada línea indica el número de puerto y, entre paréntesis, el servicio que
normalmente utiliza ese puerto. Si el sistema no reconoce el servicio, aparece
la palabra `desconocido`.

**Resumen:**

```
RESUMEN DEL ESCANEO
Equipo analizado : 192.168.1.10
Rango de puertos : 1 - 100
Puertos analizados: 100
Puertos abiertos  : 2
Puertos cerrados  : 98
Tiempo empleado   : 1.24 segundos
```

Significado de cada estado:

| Estado | Interpretación |
|---|---|
| **ABIERTO** | Hay un servicio escuchando y aceptando conexiones en ese puerto |
| **Cerrado** | No hay servicio, o un firewall bloqueó el intento de conexión |

Puertos comunes de referencia:

| Puerto | Servicio | Uso habitual |
|---|---|---|
| 21 | FTP | Transferencia de archivos |
| 22 | SSH | Acceso remoto seguro |
| 23 | Telnet | Acceso remoto sin cifrado |
| 25 | SMTP | Envío de correo |
| 53 | DNS | Resolución de nombres |
| 80 | HTTP | Páginas web |
| 443 | HTTPS | Páginas web cifradas |
| 3306 | MySQL | Base de datos |
| 3389 | RDP | Escritorio remoto de Windows |
| 8080 | HTTP alternativo | Servidores de desarrollo |

Si no se encuentra ningún puerto abierto, el programa lo indica con un
mensaje. Es un resultado normal cuando el equipo no tiene servicios activos o
el firewall bloquea las conexiones.

> **Captura 7:** resultados y resumen del escaneo.
> `![Resultados](capturas/07_resultados.png)`

---

## 8. Guardar el reporte

Al final el programa pregunta:

```
¿Desea guardar el reporte en un archivo? (s/n):
```

Si responde `s`, se crea un archivo de texto en la misma carpeta, con un
nombre como `reporte_192_168_1_10_20260916_143502.txt`, que contiene la fecha,
el equipo analizado, el rango y la lista de puertos abiertos.

> **Captura 8:** archivo de reporte generado.
> `![Reporte generado](capturas/08_reporte.png)`

---

## 9. Registro de la prueba experimental

Complete esta tabla con los datos de su propia ejecución:

| Elemento | Resultado |
|---|---|
| IP utilizada | |
| Rango de puertos | |
| Puertos abiertos | |
| Observaciones | |

---

## 10. Solución de problemas

| Problema | Causa probable | Solución |
|---|---|---|
| `python: command not found` | Python no instalado o fuera del PATH | Reinstale Python marcando *Add Python to PATH*; pruebe con `python3` |
| `No se pudo resolver '...'` | IP mal escrita o host inexistente | Verifique la dirección con `ipconfig` / `ip a` |
| El escaneo tarda demasiado | Rango muy amplio | Use un rango menor, por ejemplo 1–1024 |
| No aparece ningún puerto abierto | Firewall activo o sin servicios en ejecución | Pruebe con `127.0.0.1`, o levante un servicio de prueba |
| El programa se detiene solo | Se respondió `n` a la autorización | Vuelva a ejecutarlo y responda `s` |

Para generar un puerto abierto de prueba en su propio equipo, ejecute en otra
terminal:

```bash
python -m http.server 8080
```

Luego escanee `127.0.0.1` en el rango 8000–8100: el puerto 8080 debe aparecer
como abierto.

---

## 11. Advertencia legal

El escaneo de puertos sobre equipos o redes ajenas, sin autorización del
propietario, puede constituir una infracción penal en Ecuador y en la mayoría
de países. Este programa se entrega con fines estrictamente académicos; el uso
indebido es responsabilidad exclusiva de quien lo ejecuta.

Realice las pruebas únicamente sobre su propio equipo, una máquina virtual
propia o un laboratorio autorizado por el docente.
