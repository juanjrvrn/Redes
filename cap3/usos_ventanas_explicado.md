## **PPP (Protocolo Punto a Punto)**

Imagina el PPP como un servicio de mensajería muy estricto y exclusivo que solo viaja entre dos puntos directos (por ejemplo, tu router y el equipo de tu proveedor de Internet). Su trabajo es tomar un paquete de datos, meterlo en un sobre seguro (la trama), y asegurarse de que llegue al otro lado entendiendo las reglas del canal físico.


### 1. ¿Qué es y cuáles son sus Características Principales?
El PPP define un tipo de trama (el "sobre") y establece las reglas exactas de cómo dos dispositivos se comunican directamente a través de un enlace, multiplexando (combinando) protocolos de red y de enlace de datos.

**Lista exhaustiva de sus funciones y capacidades:**
* **Configuración dinámica de enlaces:** Negocia cómo se va a comunicar antes de empezar a hablar.
* **Autenticación:** Puede pedir usuario y contraseña (usando protocolos como PAP o CHAP) antes de dejar pasar los datos.
* **Compresión de encabezados:** Achica la cabecera de los paquetes para no desperdiciar ancho de banda.
* **Verificación de calidad del enlace:** Monitorea si el cable o la conexión está teniendo demasiados errores.
* **Control de errores:** Detecta si los datos llegaron corruptos.
* **Multilink:** Tiene la capacidad de agrupar varias conexiones físicas para que funcionen como un solo "tubo" más grande y rápido.
* **Scrambling (Revuelto de datos):** Antes de enviar los datos sobre ciertas redes de fibra (como SONET), los datos son "revueltos" utilizando una función matemática **XOR** para evitar largas secuencias de ceros o unos que puedan desincronizar los relojes del hardware.

### 2. El "Cerebro" dividido: Los Sub-protocolos
El PPP no hace todo el trabajo solo; delega las tareas de negociación en dos ayudantes clave:

* **LCP (Link Control Protocol - Protocolo de Control de Enlace):** Es el arquitecto de la capa de enlace. Se encarga de negociar las opciones físicas, establecer la conexión, probarla y desconectarla.
* **NCP (Network Control Protocol - Protocolo de Control de Red):** Es el traductor de la capa de red. Una vez que el LCP armó el enlace, el NCP negocia cómo se van a enviar los paquetes de red (por ejemplo, le asigna una dirección IP a tu computadora). Existe un NCP distinto por cada protocolo de red soportado.

### 3. La Anatomía: Formato de la Trama PPP

El PPP es un protocolo **orientado a bytes**. Todo se mide en bloques de 8 bits. Su estructura es estrictamente la siguiente:

* **Flag (Bandera):** 1 byte. Marca el inicio y el fin de la trama. Su valor hexadecimal es estricto: **`0x7E`** (en binario: `01111110`).
* **Address (Dirección):** 1 byte. Usualmente configurado en `11111111` (todos a 1), que es una dirección de difusión estándar, ya que al ser "punto a punto" no hay necesidad de buscar a quién enviarlo.
* **Control:** 1 byte. Su valor estándar es **`00000011`**, lo que indica que se usa en modo "no numerado" (no se usan ventanas corredizas para retransmisión de control de flujo a este nivel por defecto).
    * *Detalle técnico vital:* Los campos de *Address* y *Control* **pueden ser omitidos** (comprimidos) para ahorrar espacio, si ambos extremos lo negocian previamente a través de una opción en el LCP.
* **Protocolo:** 1 o 2 bytes. Indica qué tipo de carga útil viene adentro (¿Es un paquete IP? ¿Es un mensaje LCP? ¿Es un mensaje NCP?).
* **Carga útil (Payload):** El paquete de datos en sí (variable en tamaño).
* **Checksum (FCS):** 2 o 4 bytes. Utiliza comprobación de redundancia cíclica para la detección de errores.

### 4. El Mecanismo de Entramado: "Byte Stuffing" (Relleno de Bytes)
Aquí viene un problema lógico que el PPP resuelve brillantemente: Si la bandera de inicio/fin es `0x7E`... ¿Qué pasa si dentro de la "Carga útil" (una foto que estás enviando) hay un byte que casualmente es `0x7E`? El receptor creería erróneamente que la trama terminó a la mitad.

**La solución técnica:**
* Se utiliza una **secuencia de escape**, cuyo valor estricto es **`0x7D`** (en binario: `01111101`).
* **Regla:** Cada vez que el emisor ve un `0x7E` dentro de los datos reales, inserta justo antes un `0x7D` y modifica el dato original (haciendo un XOR con `0x20`). Cuando el receptor ve el `0x7D`, sabe que debe ignorarlo, "des-modificar" el siguiente byte, y entender que es parte del mensaje y no una bandera de fin.

### 5. El Ciclo de Vida: Diagrama de Estados de PPP

El PPP es como una llamada telefónica; pasa por fases estrictas. Extraído textualmente de tus diapositivas, las transiciones principales son:

1.  **Dead (Muerto):** No hay señal física. El cable está desconectado o el módem apagado.
2.  **Establish (Establecer):** La señal física llega. El LCP comienza a negociar las opciones básicas del enlace (como si omitirán los campos Address y Control).
3.  **Authenticate (Autenticar):** (Opcional pero común). Se comprueba quién eres (usuario y contraseña). Si fallas, te devuelve al estado Dead.
4.  **Network (Red):** Si te autenticaste, el NCP entra a jugar y negocia las direcciones IP.
5.  **Open (Abierto):** ¡Éxito! Los datos del usuario (la carga útil) están fluyendo libremente por la conexión. Cuando terminas, se cierra el enlace y vuelve a Dead.


## **Packet over SONET (POS)** 

Imagina que el Internet es un sistema de transporte masivo. Los paquetes IP son las cajas de mercancía. El protocolo **PPP** (que acabamos de estudiar) es el contenedor de acero estandarizado donde metemos esas cajas. Y **SONET** es un tren bala de levitación magnética ultra rápido que viaja sobre rieles de luz (fibra óptica). 

**POS** es simplemente la técnica exacta de cómo subimos esos contenedores PPP directamente a ese tren bala óptico, sin intermediarios innecesarios.

### 1. ¿Qué es y cuál es su Arquitectura (Pila de Protocolos)?

Packet over SONET es una tecnología de red de área amplia (WAN) utilizada para el transporte de altísima velocidad sobre medios puramente ópticos. En lugar de usar protocolos pesados en el medio (como ATM, que fragmenta todo), POS simplifica el viaje.

* **La Pila de Encapsulamiento estricta:** El viaje de los datos sigue exactamente este orden lógico: **IP $\rightarrow$ PPP $\rightarrow$ SONET $\rightarrow$ Fibra**.
    * **Capa de Red:** El router genera un paquete **IP**.
    * **Capa de Enlace:** Ese paquete se encapsula dentro de una trama **PPP**.
    * **Capa Física:** Esa trama PPP se mapea (se inserta) directamente en la carga útil de la trama **SONET** (llamada *Synchronous Payload Envelope* o SPE), la cual se convierte en pulsos de luz enviados a través de la **Fibra Óptica**.

### 2. El Mecanismo: Entramado PPP sobre SONET
SONET por sí solo es un protocolo de capa física que transmite un flujo constante y síncrono de bits (una tubería continua de luz). No tiene forma de saber dónde empieza o termina un paquete IP. Por eso necesita a PPP.

* **El uso de las Banderas:** Se utiliza el entramado de bytes de PPP. Las tramas se separan usando la bandera estándar **`0x7E`**. 
* **El detalle técnico del "Byte Stuffing":** Como SONET transmite todo lo que le llega, si la carga útil del usuario casualmente incluye bytes que coinciden con las banderas o escapes, el hardware de la interfaz POS debe intervenir usando las reglas de PPP.
    * *Ejemplo estricto del documento:* Si en el flujo de datos de la red aparece la secuencia maliciosa o accidental **"ESC FLAG FLAG ESC"**, el hardware inyectará (rellenará) bytes adicionales basándose en los bits definidos por el protocolo PPP para enmascararlos. De esta forma, no se confunde al hardware SONET subyacente haciéndole creer que la trama terminó.

### 3. El Reto de la Capa Física y la Solución (Scrambling)
Aquí es donde entra un detalle técnico fascinante y vital de POS. Los equipos receptores de fibra óptica sincronizan sus relojes internos leyendo las transiciones de luz (los cambios de $0$ a $1$ y de $1$ a $0$).

* **El Problema:** Si un usuario envía un paquete IP que consiste únicamente en una cadena larguísima de ceros (o unos), el rayo de luz se mantendría estático. El reloj del receptor se desincronizaría y el enlace se caería. (Esto es un riesgo de seguridad, ya que un atacante podría botar el enlace enviando este tipo de paquetes a propósito).
* **La Solución Matemática (Aleatorización):** Antes de inyectar la trama PPP en SONET, el hardware realiza un **"Scrambling"** (revuelto de datos). Se pasa toda la trama de datos por un circuito matemático que aplica una función $\text{XOR}$ utilizando un polinomio pseudoaleatorio (comúnmente $x^{43} + 1$). 
* **El Resultado:** Esto convierte cualquier secuencia larga de ceros en una mezcla aparentemente caótica de unos y ceros, garantizando que el hardware óptico siempre vea parpadeos suficientes para mantener el reloj sincronizado. Al llegar al destino, se aplica la función $\text{XOR}$ inversa para recuperar el dato original.

### 4. Ventajas de POS (Comparado con tecnologías como ATM/ADSL)
* **Menor "Overhead" (Sobrecarga):** A diferencia de ATM (que vimos en ADSL, el cual roba 5 bytes de encabezado por cada 48 bytes de datos, perdiendo casi un 10% del ancho de banda solo en control), POS es extremadamente ligero.
* **Alta Eficiencia del Canal:** Casi todo el ancho de banda del láser de fibra óptica se utiliza para transportar datos IP reales y útiles, lo que lo hace el estándar preferido para las "columnas vertebrales" (Backbones) del Internet mundial moderno.

## **ADSL (Asymmetric Digital Subscriber Line)** o Línea de Abonado Digital Asimétrica.

Imagina que la línea telefónica de cobre de tu casa es una tubería por la que originalmente solo pasaba un hilo de agua (tu voz en una llamada telefónica). La genialidad de ADSL es que logra enviar, por ese mismo cable viejo de cobre, grandes autopistas de datos digitales de Internet sin interferir con el teléfono. 

### 1. La Arquitectura Física (El Viaje del Dato)

La estructura de red ADSL tiene puntos de control muy específicos. El viaje de la información ocurre en este orden estricto:
* **PC del usuario:** Genera el tráfico de Internet.
* **Módem DSL (Router):** Es el equipo en tu casa que modula la señal digital a analógica.
* **Bucle Local (Local Loop):** Es el par de cables de cobre trenzado tradicionales que conectan tu casa con el proveedor.
* **DSLAM (Digital Subscriber Line Access Multiplexer):** Es el equipo gigante ubicado en la central telefónica del Proveedor de Internet (ISP). Su trabajo es recibir miles de cables de cobre de distintos hogares, separar las frecuencias de voz de las de datos, y canalizar el Internet hacia la red troncal (Backbone) del proveedor.

### 2. Clasificación de Modulación: OFDM y Multitono Discreto
¿Cómo logra meter tanta información en un cable telefónico? 
* **Multitono Discreto (DMT) / Modulación OFDM:** ADSL no envía un solo flujo de datos enorme. Utiliza la Multiplexación por División de Frecuencia Ortogonal (**OFDM**). Lo que hace es dividir la capacidad eléctrica del cable en múltiples canales (o subportadoras) de frecuencia más pequeños (usualmente 256 canales separados por 4.3125 kHz). 
* **La Asimetría:** Se le llama "Asimétrica" porque asigna matemáticamente muchos más canales de frecuencia para la descarga (Download) que para la subida (Upload). El proveedor asume que los usuarios en casa consumen más contenido del que envían.

### 3. La Pila de Protocolos Estricta: PPPoA
ADSL utiliza una pila de encapsulamiento muy particular, montando capas sobre capas para que la comunicación sea compatible con infraestructuras antiguas de telecomunicaciones. Funciona así:
1. **IP (Capa de Red):** El paquete de datos original.
2. **PPP (Capa de Enlace):** El paquete se encapsula en una trama PPP (para control de errores, autenticación de usuario/contraseña, etc., tal como vimos antes).
3. **PPPoA (PPP over ATM):** A diferencia de las redes modernas que inyectan el PPP directamente en fibra, el módem ADSL encapsula el PPP sobre una red heredada llamada **ATM** (Asynchronous Transfer Mode).

### 4. El Mecanismo de Fragmentación: AAL5 y ATM

Aquí es donde entra el nivel de detalle técnico crítico que se suele preguntar en los exámenes de redes:

* **Capa de Adaptación AAL5:** La red ATM no entiende paquetes gigantes, solo pequeñas porciones. Por lo tanto, se utiliza un protocolo intermediario llamado **AAL5** (ATM Adaptation Layer 5). AAL5 toma la trama PPP que le manda tu computadora, le añade información de control y la "trocea" o fragmenta en piezas muy pequeñas.
* **La Red ATM (Modo de Transferencia Asíncrono):** Es un protocolo de capa de enlace orientado a la conexión, donde los datos fluyen a través de un identificador de circuito virtual.
* **Estructura Estricta de la Celda ATM (Fórmula matemática de tamaño):** ATM no utiliza "tramas" de tamaño variable. Utiliza **celdas** de un tamaño absolutamente fijo y rígido.
    * **Tamaño total de la celda:** **53 bytes** exactos.
    * **Carga útil (Payload):** **48 bytes** (el trocito de tu dato de Internet).
    * **Encabezado (Header):** **5 bytes** (información de ruteo y control).

![partes de la trama adsl](assets\trama_adsl.png)

*Nota técnica:* Esta obligación de usar celdas fijas de 53 bytes genera lo que se conoce como el "Impuesto ATM". Por cada 48 bytes de datos útiles, siempre tienes que desperdiciar 5 bytes en control, lo que hace que ADSL tenga una sobrecarga (overhead) notablemente mayor en comparación con redes de fibra pura (POS) o redes Ethernet.

## **DOCSIS (Data Over Cable Service Interface Specification)**

Para entenderlo con una analogía simple: Imagina que la red de televisión por cable de tu ciudad es un sistema de tuberías gigante que llega a todas las casas. Originalmente, por ahí solo fluía "agua" (canales de TV). DOCSIS es la ingeniería que permite inyectar "gas" (Internet de alta velocidad) por esas mismas tuberías al mismo tiempo, sin que el agua y el gas se mezclen, y controlando exactamente cuánta presión de gas recibe cada vecino.

Aquí tienes el análisis exhaustivo y técnico, aplicando nuestra **Regla de Oro** para tu guía de estudio:

### 1. ¿Qué es y cuál es su Arquitectura Principal?
DOCSIS es el estándar internacional que permite a los proveedores de televisión por cable (redes HFC - Híbrido Fibra Coaxial) ofrecer servicios de Internet de banda ancha. A diferencia de ADSL (que es una línea dedicada para ti), el cable es un medio compartido; tú y tus vecinos comparten el mismo cable físico que pasa por la calle.

**Los Dos Actores Principales:**
* **CM (Cable Módem):** El equipo que está en tu casa.
* **CMTS (Cable Modem Termination System):** El equipo "jefe" o enrutador gigante ubicado en las oficinas del proveedor de cable. Es el director de orquesta absoluto de la red.

### 2. Los Dos Componentes Estructurales del Estándar
Para organizar el caos de miles de módems hablando por un mismo cable, el estándar DOCSIS se divide estrictamente en dos capas operativas:
* **Capa Física (PHY):** Se encarga de la modulación de las señales eléctricas y de radiofrecuencia (cómo se convierten los unos y ceros en ondas de radio que viajan por el cable coaxial).
* **Media Access Control (MAC):** Es la capa lógica que decide "quién habla, cuándo habla y por cuánto tiempo". Como el cable es un medio compartido, si todos los módems transmiten a la vez, ocurre una colisión. La capa MAC previene esto.

### 3. Mecanismos de Control: Los Flujos de Servicio (Service Flows)
Como el CMTS es el jefe, necesita una forma de controlar el ancho de banda y priorizar el tráfico (por ejemplo, darle prioridad a una llamada de voz sobre la descarga de un archivo). Esto lo hace mediante los **Flujos de servicio**.

**Características de los Flujos de Servicio:**
* **Identificador Único:** Cada flujo de servicio tiene un ID propio.
* **Parámetros de Calidad de Servicio (QoS):** Se le asigna una velocidad máxima, mínima y una prioridad estricta.
* **El Flujo de Servicio Primario:** Es un canal de control exclusivo. El CMTS lo utiliza para comunicarse internamente con cada módem. A través de este flujo, el CMTS le indica al CM qué canales de frecuencia específicos debe utilizar para transmitir datos y le entrega las **claves de cifrado** (vitales para que tu vecino no pueda "escuchar" tus datos, al ser un cable compartido).

### 4. Nivel Técnico Avanzado: Modulación y Corrección de Errores
A nivel de la capa física, DOCSIS utiliza técnicas muy agresivas para exprimir al máximo la capacidad del cable y evitar el ruido eléctrico. 

**Clasificación de Modulación y Entramado:**
* **Perfiles de Modulación Avanzados:** Utiliza **OFDM** (Multiplexación por División de Frecuencia Ortogonal) para los canales modernos de alta capacidad y **SC-QAM** para canales heredados.
* **Asignación de Tramas (Codewords):** Los paquetes de datos (tramas DOCSIS) no se envían sueltos. Se alinean y se mapean dentro de una estructura matemática compleja llamada **"Palabra de código" (Codeword)**.
* **Esquemas FEC (Corrección de Errores Hacia Adelante):** Como el cable coaxial es propenso a interferencias (ruido de motores, radios, estática), a la carga útil se le inyectan bits redundantes de paridad muy avanzados para curar los datos corruptos sin tener que pedir retransmisiones. Utiliza combinaciones estrictas de:
    * **BCH (Bose-Chaudhuri-Hocquenghem):** Código polinómico para corregir pequeños errores.
    * **LDPC (Comprobación de Paridad de Baja Densidad):** Un código de corrección de última generación que permite recuperar información incluso en canales extremadamente ruidosos.