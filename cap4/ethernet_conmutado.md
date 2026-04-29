# **Aislamiento de Dominios: Hubs vs. Switches**

El concepto fundamental del Ethernet conmutado es la eliminación de la competencia por el medio físico. Las imágenes y esquemas de las diapositivas contrastan visualmente dos eras tecnológicas:

*   **Los Concentradores (Hubs):** 
    *   **Características:** Funcionan en la capa 1 (Física). Engloban todas las líneas en un único "dominio de colisión".
    *   **Desventajas:** Obligan a utilizar el protocolo **CSMA/CD** (*Carrier Sense Multiple Access with Collision Detection*, estandarizado bajo **IEEE 802.3**) y restringen a las estaciones a operar en modo *Half-Duplex* (solo pueden enviar o recibir, no ambas a la vez).
*   **Los Conmutadores (Switches):** 
    *   **Características:** Aíslan cada puerto en un "dominio de colisión" separado. Operan en la capa 2 (Enlace de Datos).
    *   **Ventajas:** Al aislar los dominios, **ya no se usa CSMA/CD** en esos enlaces y las líneas pasan a ser *Full-Duplex* (transmisión y recepción simultánea sin colisiones).
    *   **Análisis de la imagen:** Una imagen clave muestra un Switch con nubes rosadas independientes por cada puerto, etiquetadas como "Domain". Otra imagen ilustra el interior de un Switch como una **matriz de conmutación** (una cuadrícula de nodos interconectados) frente al modelo de Hub, que es un simple punto central donde todo choca. Además, se muestra que los switches pueden conectarse a estaciones de trabajo, a otros conmutadores o incluso a concentradores antiguos.


### **La Tabla CAM**

Para que el Switch pueda enviar las tramas Ethernet (*Frames*) al puerto correcto, lee los encabezados de las mismas y construye una base de datos interna conocida como **Tabla CAM** (*Content Addressable Memory* o Memoria Direccionable por Contenido).

Para llenar esta tabla dinámicamente, el equipo ejecuta el **Algoritmo de Aprendizaje (hacia atrás)**:
1.  **Leer dirección MAC de origen:** Al ingresar una trama por un puerto, el Switch extrae la MAC de quien la envía.
2.  **¿Dirección de origen encontrada en tabla CAM?**
    *   **NO:** Añade la dirección de origen a la tabla CAM, registrando el Número de Puerto por donde ingresó y un *Timer* (temporizador de envejecimiento).
    *   **SÍ:** Actualiza el puerto (de ser necesario, por si la máquina se movió) y reinicia el *Timer* para mantener la entrada activa.
3.  **Terminar:** El proceso de aprendizaje de esa trama concluye.

Una vez que el Switch aprende de dónde viene la trama, utiliza el **Algoritmo de Retransmisión (Forwarding)** para decidir hacia dónde retransmitirla basándose en la **Dirección MAC de destino**:

1.  **Trama recibida en el puerto "x":** Se lee la Dirección MAC de destino.
2.  **¿Dirección de destino = FF.FF.FF.FF.FF.FF (Broadcast)?**
    *   **SÍ:** El Switch reenvía la trama por **todos los puertos excepto "x"** (el puerto de entrada).
    *   **NO:** Se pasa a la siguiente condición.
3.  **¿Dirección de destino encontrada en tabla CAM?**
    *   **NO (Inundación):** Si el Switch no sabe dónde está el destino, reenvía la trama por **todos los puertos excepto "x"** para asegurar que llegue.
    *   **SÍ:** Se pasa a la última condición.
4.  **¿Puerto de salida = "x"?**
    *   **SÍ (Terminar):** Si el destino se encuentra en el mismo segmento físico del que provino la trama (común si hay un Hub conectado al puerto), el Switch **descarta** la trama porque el destinatario ya la escuchó.
    *   **NO:** El Switch **reenvía la trama exclusivamente por el puerto de salida** indicado en su tabla.

### **Clasificación de los Modos de Trabajo del Switch**

La presentación lista de forma explícita que los switches poseen distintos modos operativos para dictaminar en qué momento exacto comienzan a reenviar la trama. Estos definen un equilibrio entre velocidad y fiabilidad:

1.  **Store and Forward (Almacenamiento y reenvío):**
    *   **Características:** El switch recibe y almacena la trama completa en su memoria (*buffer*) antes de enviarla. Realiza un cálculo matemático mediante el **CRC** (*Cyclic Redundancy Check*).
    *   **Ventajas:** Ofrece la más alta confiabilidad, ya que detecta y descarta tramas corruptas, evitando desperdiciar ancho de banda.
    *   **Desventajas:** Posee la mayor latencia (retraso), ya que debe esperar el último bit de la trama para procesarla.
2.  **Cut-through (Envío directo):**
    *   **Características:** El switch lee únicamente los primeros 6 bytes (la dirección MAC de destino) y comienza a emitir los datos de forma inmediata.
    *   **Ventajas:** Es el método más rápido, asegurando la latencia más baja posible.
    *   **Desventajas:** Tiene cero tolerancia a errores. Reenviará colisiones y tramas completamente corruptas a la red.
3.  **Free of segments / Fragment-free (Libre de fragmentos):**
    *   **Características:** El switch lee únicamente los primeros **64 bytes** de la trama antes de reenviarla. Esto se debe a que 64 bytes (512 bits) es la longitud mínima de trama en Ethernet, ventana donde ocurren todas las colisiones típicas.
    *   **Ventajas:** Logra un equilibrio inteligente: filtra de manera efectiva los fragmentos de colisiones sin sufrir el gran retraso del método *Store and Forward*.
    *   **Desventajas:** Tiene una latencia intermedia y no filtra errores que ocurran en los datos después del byte 64.

Siguiente [Evolucion de Ethernet](evolucion_ethernet.md)