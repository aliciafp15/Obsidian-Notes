♻️ Primera parte -> [[SO Primera Parte 💻]]
# 17 Marzo 2022 🧨
---
- El mapa del proceso se crea en el disco. Se usa asignación no contigua.
---
### Principio de localidad de referencias
- **Temporal:** es bastante probable que una referencia se repita. Contribuyen mucho los bucles.
- **Espacial:** si accedo a una posición de memoria, en un futuro es posible que acceda a posiciones cercanas a esta.
---
### Ventajas de la Memoria Virtual
1. El tamaño del proceso puede ser mayor que el de la propia memoria.
2. Aumenta el grado de multiprogramación.
3. La gestión corre a cargo del procesador.
---
- **Paginación:** se siguen criterios físicos (se divide el proceso en trozos de igual tamaño).
- **Segmentación:** se siguen criterios lógicos (se tiene en cuenta el contenido del proceso).
---
### Memoria virtual, paginación
![[paginacion.png]]

---
---
# 22 Marzo 2022 🌽
---

### Memoria virtual, segmentación
---
2. *Mediante segmentación:*
	- Se divide el proceso siguiendo procesos lógicos, agrupando en cada segmento datos relacionados entre sí. 
	- Tendremos una tabla de segmentos que tendrá información sobre cada segmento.
	- La memoria se divide en trozos de distinto tamaño.
	- Es más compleja.
	- Ahora tenemos la dirección de comienzo del segmento.
	- Ahora se hace una suma, mientras que antes se concatenaba.
	
	**Ventajas**
	- Aumenta la multiprogramación.
	- Contempla la gestión de regiones, un segmento puede ser compartido por varios procesos.
	
	**Desventajas**
	- Problemas de gestión de almacenamiento real.
	- Es más complejo
3. *Segmentación+paginación*
	- Necesitamos una tabla de segmento por proceso.
	- La traducción es más complicada.
	- Requiere dos accesos adicionales, por tanto el tiempo de traducción es mayor que en paginación, ya que requiere un acceso más.
	
	Ventajas
	- Multiprogramación, protección de procesos,...
	Inconvenientes
	- Más lento, complicado,...
---
### Decisiones de diseño
1. Dependientes del Hardware
	- Paginación, segmentación, segmentación con paginación.
2. Dependientes del Software
	- Qué hacer cuando se produce un fallo de página, mediante el **sistema operativo**.
	- Un **fallo de página** es una excepción que e genera cuando la página buscada no está en memoria.
---
##  Administración del almacenamiento virtual 🥪

### Política de lectura
Determina cuando se debe cargar un programa en memoria.
- **Paginación por demanda:** se traen a memoria cuando se produce el fallo.
- **Prepaginación:** se traen a memoria varias páginas contiguas. Mayor eficiencia de carga. Es más eficiente leer un bloque grande una vez que 4 veces bloques pequeños.
Generalmente se suele usar prepaginación.
---
### Política de reemplazo
Determina qué página se reemplaza eb memoria principal cuando se debe cargar otra y no hay espacio para ella.
- **Alcance global:** se reemplaza una página de cualquier proceso en memoria.
- **Alcance local:** una página del proceso que la necesita.
---
### Política de asignación
Determina cuántos marcos se asignan a un proceso.
Busca el número ideal (Equilibrio):
- Pocas para que quepan más procesos en memoria.
- Suficientes para que no se produzca hiperpaginación.
```
hiperpaginación: se generan continuamente fallos de página.
```
Estrategias de asignación:

- **Fija:** con reemplazo local. No se adapta a las necesidades de memoria del proceso.
- **Dinámica:** con reemplazo global o local.
---
## Algoritmos de reemplazo básicos 🥗, asignación estática
- Óptimo
- LRU
- FIFO
- Reloj
---
### Óptimo ❌
- Genera el mínimo número de fallos de página.
- Reemplaza la página que tardará más tiempo en volver a usarse.
- Es imposible de implementar.
---
### FIFO (first in first out)
- Reemplaza la página que más tiempo lleva en memoria.
- Sencillo de implementar.
- Pésimo rendimiento.
- Sufre la anomalía de Belady, si un proceso tiene más marcos de página asignados, más fallos se generan.
---
### LRU ✅
- Reemplaza la página que más tiempo hace que no se utiliza.
- Se aproxima bastante bien al algoritmo óptimo.
- Es difícil de implementar.
---
### Reloj o FIFO segunda oportunidad
- Se implementa como una cola circular.
- Cada página tiene un bit de uso, cuando se accede a la página se pone a 1. Cuano hay que reemplazar una página miramos si el bit está a 1, si lo está se pone a 0 y se avanza.
- Comportamiento similar al FIFO.
---
# 29 Marzo 2022 🚎
---
- **Políticas de lectura:** cuando leer las páginas
- **Política de asignación:** es la más importante. Interesa asignar el número justo de marcos a un proceso, porque si asignamos demasiado ese proceso ocupa mucha memoria que no está siendo usada, y si está ocupando demasiado poco puede generar muchos fallos de página dando lugar a la hiperpaginación.
---
### Estrategia del conjunto de trabajo
---
- **Conjunto residente:** conjunto de páginas que tiene el proceso cargado en memoria en cada momento. Su tamaño es el número de marcos que tiene asignado ese proceso.
- **Conjunto de trabajo:** se calcula en un instante T y para un tamaño de ventana lambda(⍙). Es el conjunto de páginas a las que el proceso ha hecho referencia últimamente. Representa las páginas que hacían falta para ejecutar el proceso en ese intervalo de tiempo. Aproxima el comportamiento futuro a través del comportamiento pasado.

NOTAS:
- Si el proceso tiene en memoria el conjunto de trabajo se produce una baja tasa de fallos de página.
1. Una página debería ejeutarse sólo si su conjunto de trabajo se encuentra en memoria.
2. Una página no debería ser retirada de memoria si es miembro del conjunto de trabajo de un proceso.

- Si el proceso falla a menudo, no tiene su conjunto de trabajo cargado. 
- Si hay muchos fallos de página el proceso tiene pocos marcos.
---
### Buffering de páginas
---
- Técnica que almacena cosas que nos vayan a hacer falta (que sean referenciadas) en un futuro (Ej, la caché del procesador).
- En todo momento se mantiene una lista de marcos de página libres en el sistema.
---
# TEMA 5, Gestión de entrada salida 🚨
---
- Es importante que el sistema operativo generalice la aceptación de dispositivos (diversidad).
- Partes de los dispositivos:
![[partes dispositivos.png | 500]]

- Un controlador tiene las siguientes partes:
	- Registro de control
	- Registro de estado
	- Registro de dirección
	- Registro de datos
- Cada registro tiene asignado un puerto
---
# 31 Marzo 2022 🛩
---
- Cómo podría planificarse un sistema de entrada salida:
![[funcionamiento Entrada salida.png]]
- **IORB**-> Input Output Request Block, forma de funcionar el manejador independiente de dispositivo.
- **Manejador independiente:**: verifica los parámetros, crea el IORB y avisa al manejador dependiente del dispositivo (hay uno en el sistema).
- **Manejador dependiente del dispositivo (driver):** Hay uno por cada dispositivo o tipo de dispositivo. Es el driver del dispositivo. Da las órdenes para cumplir la petición (hay uno por cada dispositivo).
---
- **Buffering:** mecanismo acelerador que aparece por ejemplo en la caché, que almacena los últimos bloques de discos accedidos.
- **Spooling:** mecanismo por el cual no hay interbloqueo en los sistemas operativos.
---