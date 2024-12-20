# MONITORIZACIÓN PROCESOS

## ps
El comando `ps` muestra información sobre los procesos en ejecución.

Con la opción `a` se muestran todos los procesos de todos los usuarios.
```bash	
ps a
```
![psa](img/img2.png)

Con `ps au` se muestra información sobre todos los procesos de todos los usuarios en formato largo.
```bash	
ps au
```
![psau](img/img3.png)

Con `ps aux` se muestra información sobre todos los procesos de todos los usuarios en formato largo y con información adicional.
```bash
ps aux
```
![psaux](img/img4.png)

> [!TIP]
> Si quieres info sobre un proceso en concreto, puedes usar `ps -C <nombre>`
> ```bash
> ps -C nano
> ```
> ![psnano](img/img5.png)
> Parámetros interesantes: vsz (memoria virtual), rss (memoria física)

> [!NOTE]
> Si quieres ver los procesos que mas ocupen, por ejemplo, los 5 que mas ocupan memoria, puedes usar `ps -eo user,pid,%cpu,%mem,time --sort=-%cpu | head -n 6`
> 
> ![psmem](img/img6.png)

# Comando `top` y sus opciones en Linux

El comando `top` permite monitorear en tiempo real el uso de recursos del sistema, como CPU, memoria y procesos en ejecución.

## Opciones y atajos dentro de `top`

### `T` - Tiempo acumulado de los procesos
- Ordena los procesos según el **tiempo total de CPU acumulado** que han utilizado.
- Útil para identificar procesos que han consumido mucho tiempo de CPU durante su ejecución.

### `M` - Uso de memoria
- Ordena los procesos por la cantidad de **memoria RAM** que están utilizando.
- Ideal para localizar procesos que consumen demasiada RAM.

### `U` - Filtrar por usuario
- Permite mostrar los procesos de un **usuario específico**.
- Tras presionar `U`, se solicita el nombre de usuario.

### `p` - Ordenar por PID
- Ordena los procesos por su **ID de proceso** (PID).
- Es útil para localizar un proceso específico si conoces su PID.

### `P` - Uso de CPU
- Ordena los procesos por el **uso de la CPU** (de mayor a menor).
- Ayuda a identificar qué procesos están consumiendo más recursos de CPU.

### `N` - Orden por PID
- Igual que `p`, ordena los procesos por el **PID** en orden ascendente.

### `R` - Invertir el orden
- **Invierte el orden** de la columna seleccionada para ordenar.
- Por ejemplo, si los procesos están ordenados por PID, los muestra en orden descendente.

---

## Personalización en `top`
- Puedes usar estas teclas para ajustar el formato de la visualización según tus necesidades.
- Para guardar la configuración personalizada, presiona `W` (creará un archivo `.toprc` en tu directorio personal).

> [!NOTE]
>  `top -b -n 1 > top.txt`
> Genera una captura de top y guardar la informacion en un archivo

![top](img/img7.png)


> [!TIP]
> `top -b -n 3 -o +%CPU | head -n 17`
> 10 procesos que más CPU consumen por periodos de 3 segundos

![topa](img/img8.png)


# `htop`: Características y Opciones Interesantes

```bash
# Instalar htop
sudo apt install htop
```

`htop` es una herramienta interactiva y visual para monitorizar y gestionar procesos en Linux, con una interfaz amigable y opciones avanzadas.

## Características Principales
- **Interfaz visual amigable**:
  - Barras gráficas para el uso de CPU, memoria y swap.
  - Colores codificados para diferentes métricas.
- **Gestión de procesos**:
  - Navegación con teclado o mouse.
  - Posibilidad de enviar señales directamente a los procesos (`SIGKILL`, `SIGTERM`, etc.).
- **Configuración personalizable**:
  - Cambia columnas, colores y el comportamiento de la herramienta.

---

## Atajos de Teclado Más Interesantes

### `F2 (Setup)` - Configuración
- Cambia el aspecto y las métricas mostradas:
  - Añadir o quitar columnas (PID, usuario, CPU, memoria, etc.).
  - Ocultar procesos de usuarios no privilegiados.
  - Personalizar colores.

### `F3 (Search)` - Búsqueda
- Busca un proceso por nombre o ID.
- Ideal para localizar procesos en sistemas con muchas tareas.

### `F4 (Filter)` - Filtro
- Filtra los procesos mostrados por un criterio específico (nombre, tipo, etc.).

### `F5 (Tree)` - Vista en árbol
- Muestra los procesos en una estructura jerárquica:
  - Identifica relaciones entre procesos padre e hijo.

### `F6 (Sort)` - Ordenar
- Cambia el criterio de ordenación:
  - **CPU%**: Uso de CPU.
  - **MEM%**: Uso de memoria.
  - **TIME+**: Tiempo acumulado de CPU.
  - **PID**: ID del proceso.

### `F9 (Kill)` - Terminar un Proceso
- Enviar señales para finalizar procesos directamente desde la interfaz.

---

## Opciones de Línea de Comandos

- **`htop -u <usuario>`**: Muestra solo los procesos de un usuario específico.
- **`htop --tree`**: Inicia `htop` directamente en modo árbol.
- **`htop -p <PID1,PID2>`**: Muestra información solo de los procesos con los PIDs especificados.

---

## Ventajas de `htop` Frente a `top`
1. Interfaz visual con barras gráficas y colores.
2. Navegación y selección de procesos con teclado o mouse.
3. Configuración más sencilla y flexible.
4. Visualización jerárquica de los procesos.



![htop](img/img9.png)


# ATOP

`atop` es una herramienta de monitorización avanzada para sistemas Linux, que proporciona información detallada sobre el uso de recursos y procesos.

![atop](img/img10.png)

---

Modificar para que lo haga cada 60 segundos
```bash
sudo nano /etc/default/atop
```
Cambiar la linea `INTERVAL=60` y guardar

![atop2](img/img11.png)

Logs de atop
```bash
sudo cd /var/log/atop
# listar
ls
# para ver el log
atop -r nombre_log
```