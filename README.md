# 🤖 Proyecto RobotStudio – Robot ABB IRB140

Este proyecto corresponde a la práctica de laboratorio en el entorno **RobotStudio** con el robot **ABB IRB140**, desarrollada en el marco del curso de **Robótica Industrial**.  
El sistema combina control digital, simulación y programación en lenguaje **RAPID**, integrando movimiento coordinado con un **conveyor** y rutinas de dibujo automático sobre una superficie de trabajo.

---

## 📘 Descripción detallada de la solución planteada

El proyecto tiene como objetivo **automatizar la ejecución de un dibujo sobre un objeto transportado por una banda (conveyor)**, realizando un acercamiento con limitaciones a lo que podria ser la automatización de procesos como el decorado de tortas.  
El robot ABB IRB140 se encarga de detectar la llegada de la pieza mediante señales digitales, detener el conveyor en la posición de trabajo, y posteriormente ejecutar una secuencia de movimientos para dibujar figuras predefinidas (como el ícono de Batman y nombres personalizados).

El sistema está compuesto por los siguientes elementos:

- **Robot ABB IRB140**: encargado de la manipulación y trazado.
- **Conveyor**: controlado mediante señales digitales de salida (DO) para desplazamiento hacia adelante y en reversa.
- **Herramienta “Marker”**: un plumón o marcador diseñado en CAD y calibrado en RobotStudio.
- **WorkObject “Cake”**: define el sistema de coordenadas del objeto sobre el cual se realizan los trazos.

La lógica de control principal se encuentra en el módulo RAPID `Module1`, que gestiona los eventos de entrada, salidas digitales y subrutinas de dibujo, garantizando seguridad y repetibilidad durante todo el proceso.

---

## 🔁 Diagrama de flujo de acciones del robot

El diagrama de flujo completo del funcionamiento del robot está disponible en la carpeta [`Diagrams`](./Diagrams/), en formato `.mmd` (Mermaid), compatible para ser visualizado en GitHub con Markdown.



---

## 🧭 Plano de planta

El plano de planta con la ubicación del robot, conveyor, herramienta y sensores se encuentra en la carpeta [`Layouts`](./Layouts/).

---

## ⚙️ Descripción de las funciones utilizadas

El módulo RAPID está estructurado en **subrutinas** que organizan la secuencia lógica y los movimientos del robot, además del control de entradas y salidas digitales.  
Esto permite que el programa sea modular, legible y fácil de mantener.

### 🔸 Subrutinas principales

| Subrutina | Función principal |
|------------|-------------------|
| `main()` | Rutina principal: gestiona el flujo completo del proceso y evalúa las señales de entrada (`DI_01`, `DI_02`, `DI_03`). Coordina el control del conveyor y las llamadas a las rutinas de dibujo. |
| `P_Home()` | Envía al robot a la posición inicial segura usando un **movimiento articular (MoveJ)**. |
| `P_Local_Home()` | Lleva al robot a una posición de referencia local (dentro del área de trabajo) mediante un **movimiento lineal (MoveL)**. |
| `P_Bat()` | Ejecuta la trayectoria que dibuja el ícono principal, combinando movimientos **lineales (MoveL)** y **circulares (MoveC)** para lograr curvas suaves y precisas. |
| `P_Names()` | Realiza el trazo de nombres o etiquetas personalizadas sobre la superficie, utilizando **MoveL** para garantizar precisión en líneas rectas. |
| `P_Maintenance()` | Posiciona el robot en una ubicación de mantenimiento para inspección o ajustes. |

---

### 🔹 Comandos de movimiento utilizados

En el programa se emplean tres tipos de instrucciones de movimiento fundamentales del lenguaje **RAPID**:

| Comando | Tipo de movimiento | Descripción |
|----------|--------------------|--------------|
| `MoveJ` | **Articular (Joint)** | El robot se desplaza de un punto a otro siguiendo el camino más corto posible según sus ejes. Se usa principalmente para ir a posiciones seguras o iniciales. |
| `MoveL` | **Lineal (Linear)** | El robot se mueve en línea recta desde el punto actual hasta el destino, manteniendo la orientación de la herramienta. Ideal para trazos o movimientos de precisión. |
| `MoveC` | **Circular (Circular)** | Realiza un movimiento en arco entre dos puntos, útil para crear trayectorias curvas o segmentos suaves en dibujos. |

Cada uno de estos movimientos se ejecuta especificando **velocidad (`vXXX`)**, **zona de aproximación (`zX`)**, y la **herramienta (`tooldata`)** y **objeto de trabajo (`wobjdata`)** activos, garantizando control y repetibilidad.

---

## 🛠️ Diseño de la herramienta

El diseño CAD de la herramienta “Marker” y su montaje se encuentra en la carpeta [`Design`](./Design/), donde se incluyen los modelos 3d de cada elemento y el ensamble realizado en FUSION 360.  
Se incluye tambien los archivos `.MOD` utilizados para la calibración de la herramienta realizada en el laboratorio, los cuales se encuentran en la carpeta [`ABB-Calibration`](./ABB-Calibration/).

---

## 💻 Código RAPID

El código fuente completo se encuentra en la carpeta [`RS/robotic-ABB-Cake/`](./RS/robotic-ABB-Cake).

> Incluye la configuración del objeto de trabajo (`wobjdata`) y la herramienta (`tooldata`) empleadas en la simulación.

---

## 🎥 Video de simulación e implementación

El video de la práctica (simulación y prueba real) se encuentra disponible en la carpeta [`Video`](./Video/).  
Debe comenzar con la introducción oficial del laboratorio **LabSIR** según las indicaciones institucionales.




