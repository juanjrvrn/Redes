# Capa de enlace
La capa de enlace de datos es un componente fundamental en el modelo de red, situada exactamente entre la capa de red (superior) y la capa física (inferior), como se ilustra en el diagrama de la pila de protocolos de las diapositivas, donde aparece resaltada en color rosa. Su responsabilidad principal es tomar los datos en bruto y enviarlos de forma fiable a través de un enlace físico simple (el siguiente salto). 

A continuación, se presenta un análisis exhaustivo de sus funciones, apoyado en los conceptos y elementos visuales de las fuentes:

## **1. Cuestiones de Diseño de la Capa de Enlace**
Para lograr una comunicación eficiente, esta capa debe resolver varios problemas fundamentales de diseño:
*   **Proporcionar una interfaz de servicio bien definida:** Entregar de forma eficiente los datos a la capa de red.
*   **Entramado (Framing):** Identificar secuencias de bytes y agruparlas en segmentos autocontenidos (tramas).
*   **Detección y Corrección de errores:** Manejar las perturbaciones de la transmisión física para que el receptor reciba datos limpios.
*   **Control de flujo:** Regular la transmisión para no permitir que transmisores muy rápidos saturen o sobrepasen a receptores más lentos.
*   **Direccionamiento físico:** Identificar el inicio y fin del enlace de datos a nivel local.

## **2. Las Tramas (Frames)**
La unidad fundamental de información en esta capa es la **trama**. (Las diapositivas incluyen una imagen humorística del personaje Fry de Futurama con el texto "Que es lo que tramas", haciendo un juego de palabras con esta unidad de datos).
*   **Encapsulación:** Un diagrama ilustra claramente este proceso: la máquina emisora toma un **Paquete** de la capa de red y la capa de enlace lo encapsula añadiéndole una **Cabecera (Header)** al inicio, ubicando el paquete en el **Campo de carga útil (Payload field)**, y colocando un **Remolque (Trailer)** al final.
*   **Rutas de comunicación:** Otra imagen muestra cómo, conceptualmente, existe una "ruta de datos virtual" directa entre la capa de enlace del Host 1 y el Host 2, aunque la "ruta de datos real" implica que la trama baje a la capa física para viajar por el medio físico.

## **Métodos de identificación de inicio y fin de tramas (Entramado):**

### a) Conteo de caracteres o Bytes
En este método, el primer campo del encabezado de la trama especifica el número total de caracteres (o bytes) que contiene esa misma trama, incluyéndose a sí mismo.

* **Estructura base:** `[ Número Total | Datos ]`
* **Ejemplo simbólico:** Supongamos que queremos enviar los caracteres `A`, `B`, `C` y `D`. 
    * La trama sería: `[ 5 | A | B | C | D ]`
* **El problema:** Si un error de transmisión altera el número `5` (por ejemplo, lo cambia a un `8`), el receptor perderá la sincronización. Intentará leer 8 caracteres para esa trama y, a partir de ahí, no sabrá dónde empiezan las tramas siguientes.

### b) Bytes de “Bandera” de inicio y fin, con relleno de bytes (Byte Stuffing)
Para evitar la pérdida de sincronización del conteo, aquí cada trama empieza y termina con un byte especial reservado llamado "Bandera" (Flag). Representémoslo con el símbolo **`[F]`**.

* **Estructura base:** `[F] | Datos | [F]`
* **El problema:** ¿Qué pasa si el archivo (los datos) que estás enviando contiene casualmente un byte idéntico a la bandera `[F]` o al escape `[E]`? El receptor pensaría que la trama terminó antes de tiempo.
* **La solución (Relleno):** Se introduce un byte de "Escape", representado como **`[E]`**, justo antes de cualquier dato que se parezca a una bandera o al escape. El receptor sabe que debe ignorar el byte `[E]` y procesar el siguiente como datos normales.
* **Ejemplo simbólico:** * Datos a enviar: `[ A ] | [ F ] | [ B ]`
    * Trama transmitida: `[F] | [ A ] | [E] | [ F ] | [ B ] | [F]`


### c) Bits de “Bandera” de inicio y fin, con relleno de bits (Bit Stuffing)
Este método es la misma lógica que el anterior, pero aplicado a nivel de bits. Se usa un patrón de bits específico como bandera, casi siempre **`01111110`** (seis unos consecutivos flanqueados por ceros).

* **Estructura base:** `01111110 | Datos en bits | 01111110`
* **La solución (Relleno):** El hardware del emisor monitorea los datos. Si detecta cinco `1`s consecutivos en la carga útil de los datos (`11111`), automáticamente inserta un `0` extra. Así se asegura de que nunca aparezcan seis `1`s por accidente. El receptor hace lo inverso: si ve cinco `1`s seguidos de un `0`, asume que es relleno y quita el `0`.
* **Ejemplo:**
    * Datos originales: `0 1 1 1 1 1 1 0` (Se parece a la bandera)
    * Trama transmitida: `0 1 1 1 1 1` **`0`** `1 0` (El cero en negrita es el relleno)


### d) Violación de la codificación en la capa física
Este método se apoya directamente en la capa inferior (la física). Muchos códigos de línea en telecomunicaciones (como la codificación Manchester, o esquemas similares a los usados en portadoras T1) dictan reglas estrictas sobre cómo debe ser la señal eléctrica. Por ejemplo, exigir siempre una transición de voltaje en medio de un bit.
* **El concepto:** Una "violación" ocurre cuando el emisor envía deliberadamente una señal eléctrica que es *inválida* o ilegal según las reglas de ese código de línea. 
* **Por qué funciona:** Como ese patrón "ilegal" es imposible que se genere en los datos normales del usuario, se convierte en el delimitador perfecto para marcar el inicio o el fin de una trama, sin necesidad de insertar bytes de escape ni rellenar bits.


## **3. Servicios proporcionados a la Capa de Red**
El objetivo primordial es transferir datos desde la capa de red del emisor a la del receptor. Se ofrecen tres tipos principales de servicios:
*   **Servicio sin conexión, sin confirmación de recepción:** La máquina origen envía tramas sin que el destino las confirme. Es apropiado cuando la tasa de errores es muy baja (como en las redes Ethernet por cable) o cuando el tráfico es en tiempo real y no se puede permitir el retardo de una retransmisión.
*   **Servicio sin conexión, con confirmación de recepción:** Aún sin establecer conexiones lógicas, cada trama es reconocida individualmente. Es vital cuando la tasa de errores es alta o en canales inestables (como las redes inalámbricas Wi-Fi).
*   **Servicio orientado a la conexión con confirmación:** Las máquinas establecen una conexión antes de transferir. Cada trama está numerada, y la capa de enlace garantiza el orden y que cada trama sea recibida exactamente una vez. Es el servicio más sofisticado, ideal para redes largas o poco fiables como las Redes WAN.

## **4. Control de Flujo y Estrategias ARQ**
El control de flujo evita que un emisor rápido inunde a un receptor más lento, sobrepasando sus memorias intermedias. Se maneja principalmente mediante dos enfoques:
*   **Basado en retroalimentación:** El receptor envía información al emisor otorgándole permiso explícito para enviar más datos.
*   **Basado en tasas de bits:** El protocolo tiene mecanismos para limitar la velocidad de transmisión sin necesidad de recibir retroalimentación constante.
Para optimizar el flujo y permitir que haya múltiples tramas en tránsito, se utilizan protocolos de **ventanas deslizantes** (sliding windows).

## **5. Corrección y Detección de Errores**
El control de errores maneja las fallas causadas por ruido térmico, distorsión y atenuación. *En las diapositivas, las perturbaciones y fallos se ilustran de forma humorística con el personaje de Homero Simpson exclamando "D'OH!"*. Se emplea redundancia estructurada con dos propósitos distintos:
*   **Códigos de detección de errores:** Añaden poca redundancia, solo la suficiente para **detectar** que ocurrió un error y solicitar una retransmisión. Es más eficiente en canales altamente fiables como la fibra óptica.
*   **Códigos de corrección de errores (FEC - Forward Error Correction):** Añaden suficiente redundancia para que el receptor pueda deducir y reconstruir el mensaje original correcto. Es ideal para canales muy ruidosos e inestables (como los inalámbricos) donde las retransmisiones probablemente volverían a fallar.

### **Códigos de Corrección de Errores**
*   **Distancia de Hamming:** Es la cantidad mínima de bits que deben cambiar para pasar de una palabra codificada válida a otra,. Para detectar $s$ errores se necesita una distancia de $d_{min} > s$, y para corregir $t$ errores se requiere $d_{min} > 2t$,. *Visualmente, este concepto se ilustra con dos siluetas humanas separadas por un letrero de "2 METROS"*, *y mediante diagramas de círculos de radio $s$ y $t$ rodeados de puntos fucsias que representan palabras corruptas*.
*   **Código de Hamming:** Método que inserta bits de control en posiciones que son potencias de 2 y permite corregir errores simples. Requiere cumplir la inecuación $m+r+1 \le 2^r$. *En las diapositivas se acompaña curiosamente con la imagen del reverso del billete de un dólar (la pirámide con el ojo Illuminati)*. *Técnicamente, se ilustra con un diagrama donde un "Síndrome 0101" señala con flechas curvas el bit 5, indicando que debe ser volteado para reparar el mensaje*.
[Ver conversacion con gemini](hamming.md)   

*   **Códigos Convolucionales:** Operan sobre una cadena continua de bits, manteniendo un estado interno. La salida depende de los bits actuales y de los anteriores, y se decodifican utilizando el **Algoritmo de Viterbi**. El estándar IEEE 802.11 emplea el código convolucional de la NASA. *Para ilustrarlo, las diapositivas muestran a un astronauta flotando en el espacio* *y a un hombre sosteniendo una laptop mientras analiza una red de nodos, representando los complejos diagramas de estados y Trellis que usa Viterbi*,.
*   **Otros códigos:** Se mencionan los códigos **Reed-Solomon** (excelentes para corregir errores de ráfaga basándose en polinomios) y los **LDPC** (códigos de comprobación de paridad de baja densidad, utilizados para bloques grandes).

### **Códigos de Detección de Errores**
*   **Bits de Paridad:** Consiste en agregar un solo bit para que la suma de bits "1" sea par o impar. Detecta errores que afecten a un número impar de bits. *Visualmente, para combatir las ráfagas de error (ilustradas como bloques de bits corruptos marcados en azul), se muestra una matriz amarilla bidimensional; intercalar la paridad por columnas permite distribuir los errores y detectarlos*.
*   **Checksums (Sumas de comprobación):** Trata los datos como palabras de $N$ bits y añade redundancia igual a la suma módulo $2^N$. *Se representa conceptualmente con una libreta y un bolígrafo marcando verificaciones*. *Técnicamente, se muestran columnas de sumas en formato hexadecimal y binario calculando los acarreos ("carries")*. Su debilidad es que es vulnerable a errores sistemáticos, como la adición de ceros.
*   **CRC (Comprobación de Redundancia Cíclica):** Relaciona los mensajes con polinomios. El algoritmo anexa ceros al mensaje y realiza una división larga módulo 2 usando un "polinomio generador" $G(x)$. Si el receptor obtiene un residuo distinto de cero al dividir los datos recibidos, se detecta un error. Es extremadamente eficaz para detectar ráfagas de error. *Conceptualmente, se ilustra con un sobre de mensaje pasando por una caja de CRC y saliendo con un candado adjunto*. *También se incluye una operación matemática detallada de división binaria larga*, *y dramáticas imágenes de palmeras siendo azotadas por un huracán para metaforizar la furia de las "ráfagas de errores"*. *Para los errores matemáticos indetectables que causan frustración, se incluye el dibujo de un oficinista estresado frente a su computadora*.