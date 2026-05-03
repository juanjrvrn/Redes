# **Redes PAN Inalámbricas Bluetooth**

## **Características Generales**

Bluetooth fue concebido para crear una **PAN (*Personal Area Network* - Red de Área Personal)**. Su objetivo fundamental es conectar dispositivos cercanos (teléfonos, periféricos, etc.) mediante enlaces inalámbricos de bajo costo y bajo consumo de energía.

*   **Creadores:** Fue desarrollado inicialmente por un **SIG (*Special Interest Group* - Grupo de Interés Especial)** formado por Ericsson, IBM, Intel, Nokia y Toshiba, lanzando su primera versión en 1998.
*   **Nombre:** Se llama así en honor al rey vikingo Harald Blaatand (Bluetooth II), quien unificó Dinamarca y Noruega de forma "inalámbrica".


## **Clasificación de la Capa de Radio y Clases de Potencia**

La capa física de Bluetooth, conocida como capa de radio, opera en un entorno complejo y ruidoso. Para asegurar la transmisión, implementa las siguientes características técnicas y clasificaciones estrictas:

*   **Frecuencia:** Opera en la banda **ISM (*Industrial, Scientific and Medical*) de 2.4 GHz**.
*   **Canalización:** Divide la banda en **79 canales de 1 MHz** cada uno.
*   **Técnica de Transmisión:** Utiliza **Espectro Disperso por Salto de Frecuencia** (*Frequency Hopping Spread Spectrum*) realizando hasta **1600 saltos por segundo**.
    *   **Salto de Frecuencia Adaptativo:** Para coexistir con redes como IEEE 802.11 (Wi-Fi) sin colisionar, Bluetooth adapta su secuencia de saltos excluyendo los canales donde detecta interferencias de otras señales de radiofrecuencia.
*   **Técnicas de Modulación:**
    *   **Tasa Básica (1 Mbps):** Utiliza modulación por desplazamiento de frecuencia, enviando 1 bit cada microsegundo.
    *   **Tasas Mejoradas (2 o 3 Mbps):** Introducidas en la versión 2.0, utilizan modulación por desplazamiento de fase para enviar 2 o 3 bits por símbolo.

### **Clasificación Exhaustiva de Clases de Potencia Bluetooth**
Basándonos en la tabla explícita de sus diapositivas, los dispositivos se clasifican según su potencia máxima y alcance aproximado:

1.  **Clase 1:**
    *   Potencia de salida máxima: **100 mW (20 dBm)**.
    *   Rango aproximado: **~100 metros**.
2.  **Clase 2:**
    *   Potencia de salida máxima: **2.5 mW (4 dBm)**.
    *   Rango aproximado: **~10 metros**.
3.  **Clase 3:**
    *   Potencia de salida máxima: **1 mW (0 dBm)**.
    *   Rango aproximado: **~1 metro**.
4.  **Clase 4:**
    *   Potencia de salida máxima: **0.5 mW (-3 dBm)**.
    *   Rango aproximado: **~0.5 metro**.

## **Evolución y Clasificación de las Versiones de Bluetooth**

De acuerdo con la tabla de "Especificaciones de Versiones de Bluetooth" proporcionada en las imágenes de la presentación, la evolución técnica de este estándar no ha omitido detalles para ir abarcando nuevas necesidades del mercado:

*   **Versión 2.1 + EDR (*Enhanced Data Rate*):**
    *   **Año de Lanzamiento:** 2007.
    *   **Velocidad de transmisión:** 3 Mbit/s.
    *   **Alcance PAN estándar:** $\approx$ 10 m.
    *   **Mejoras principales:** Seguridad, EIR (*Extended Inquiry Response*), Consumo.
*   **Versión 3.0 + HS (*High Speed*):**
    *   **Año de Lanzamiento:** 2009.
    *   **Velocidad de transmisión:** 24 Mbit/s.
    *   **Alcance PAN estándar:** $\approx$ 10 m.
    *   **Mejoras principales:** Incremento exponencial de la velocidad (usando 802.11 en combinación para transferencias de datos), incremento de perfiles, MAC/PHY alternativo.
*   **Versión 4.0 + LE (*Low Energy*):**
    *   **Año de Lanzamiento:** 2010.
    *   **Velocidad de transmisión:** 32 Mbit/s.
    *   **Alcance PAN estándar:** $\approx$ 10 m.
    *   **Mejoras principales:** Mantiene la velocidad de 32 Mbit/s, pero con un diseño enfocado en la reducción del consumo energético y de menor coste de implementación.
*   **Versión 4.1:**
    *   **Año de Lanzamiento:** 2013.
    *   **Velocidad de transmisión:** 32 Mbit/s.
    *   **Alcance PAN estándar:** $\approx$ 10 m.
    *   **Mejoras principales:** Actualización de software para mejorar usabilidad.
*   **Versión 4.2:**
    *   **Año de Lanzamiento:** 2014.
    *   **Velocidad de transmisión:** 32 Mbit/s.
    *   **Alcance PAN estándar:** $\approx$ 10 m.
    *   **Mejoras principales:** *Data Length Extension* (Extensión de longitud de datos) y mejoras sustanciales en seguridad.
*   **Versión 5:**
    *   **Año de Lanzamiento:** 2017.
    *   **Velocidad de transmisión:** $\approx$ 50 Mbit/s.
    *   **Alcance PAN estándar:** $\approx$ 40 m (incremento significativo de alcance en interiores).
    *   **Mejoras principales:** Mayor velocidad, mayor alcance, diseñado específicamente como capaz de habilitar entornos masivos de **IoT (*Internet of Things* - Internet de las cosas)**.


## **Clasificación de la Arquitectura Topológica**

Las redes Bluetooth se organizan de forma jerárquica estricta para simplificar la electrónica de los chips y bajar sus costos de fabricación.

*   **La Piconet (Red Básica):** Es la unidad fundamental de comunicación y funciona bajo un sistema centralizado **TDM (*Time Division Multiplexing* - Multiplexación por División de Tiempo)**. Las ranuras de tiempo duran **625 $\mu s$**. Se compone rígidamente de:
    *   **1 Controlador o Maestro (*Master/C*):** Define el reloj y la secuencia de los saltos de frecuencia de toda la piconet.
    *   **Hasta 7 Trabajadores o Esclavos Activos (*Slaves/Worker/W*):** Pueden transmitir y recibir simultáneamente.
    *   **Hasta 255 Trabajadores Aparcados (*Parked workers*):** Nodos en estado de muy bajo consumo que solo despiertan para responder a balizas del controlador. También existen estados de energía intermedios menores denominados **hold** y **sniff**.
    *   **Regla MAC estricta:** Toda comunicación obligatoriamente pasa por el controlador. No es posible la comunicación directa "trabajador a trabajador".

*   **La Scatternet (Red Dispersa):**
    *   **Características:** Es la interconexión lógica de múltiples *Piconets* contiguas (por ejemplo, en un auditorio grande). Se logra utilizando un nodo "trabajador puente" (Bridge) que pertenece simultáneamente a dos Piconets, pasando tramas de un maestro a otro.


## **La Pila de Protocolos Bluetooth (Arquitectura Lógica)**

A diferencia de otras redes, el estándar Bluetooth no sigue el modelo clásico OSI (*Open Systems Interconnection*), el modelo TCP/IP, ni el modelo IEEE 802 convencional. Agrupa sus protocolos de manera específica, divididos lógicamente por una **Interfaz host-controlador**, la cual separa las funciones implementadas en el hardware (chip Bluetooth) de las implementadas en el dispositivo anfitrión (el teléfono o computadora).

La clasificación exhaustiva de sus capas, de abajo hacia arriba, es la siguiente:

*   **Capa Física de Radio:** 
    *   **Características:** Es la capa inferior y se ocupa de la transmisión de radio y la modulación electromagnética en la banda ISM de 2.4 GHz. 
    *   **Ventaja:** Su diseño principal está enfocado en mantener el sistema muy barato para ser viable en el mercado masivo.
*   **Capa de Control de Enlace (Banda Base):** 
    *   **Características:** Es la capa más parecida a la subcapa **MAC (*Medium Access Control*)** convencional. 
    *   **Funciones:** Convierte el flujo de bits en tramas físicas de 1, 3 o 5 ranuras de tiempo (*slots*), donde cada ranura dura $625 \mu s$. Se encarga del control **TDM (*Time Division Multiplexing* - Multiplexación por División de Tiempo)** centralizado, donde el controlador (Maestro) dicta los tiempos de las transmisiones.
*   **Administrador de Enlaces (*Link Manager*):** 
    *   **Características:** Ubicada justo debajo de la interfaz host-controlador.
    *   **Funciones:** Maneja la gestión de la alimentación, la calidad del servicio (QoS) y establece los canales lógicos (enlaces) entre dispositivos que se han descubierto.
    *   **Tipos de Enlaces Establecidos:** Permite crear enlaces **SCO (*Synchronous Connection Oriented* - Orientado a Conexión Síncrona)**, usados para datos en tiempo real como la voz (ej. auriculares manos libres), y enlaces **ACL (*Asynchronous Connection-Less* - Sin Conexión Asíncrona)** para tráfico de datos regulares.
    *   **Mecanismos de Emparejamiento:** Históricamente usaba el método de **NIP (*Número de Identificación Personal* - PIN)** (ej. "0000" o "1234"), pero por seguridad evolucionó al **Emparejamiento Simple Seguro**, donde los usuarios confirman contraseñas generadas dinámicamente.
*   **Capa L2CAP (*Logical Link Control and Adaptation Protocol* - Protocolo de Adaptación y Control de Enlace Lógico):** 
    *   **Características:** Situada por encima de la interfaz hardware/software.
    *   **Funciones:** Acepta mensajes de longitud variable de las capas superiores, los enmarca, proporciona fiabilidad (si es requerida) y determina el protocolo de origen.
*   **Protocolos de Utilidad (Sobre L2CAP):**
    *   **Descubrimiento de Servicios:** Se utiliza para localizar qué servicios están disponibles en la red Bluetooth.
    *   **RFcomm (*Radio Frequency communication* - Comunicación por Radiofrecuencia):** Emula los puertos serie estándar de un PC (necesario para conectar ratones, teclados o módems heredados).
*   **Capa de Aplicaciones y Perfiles (*Profiles*):** 
    *   **Características:** Bluetooth no deja las aplicaciones al azar; el **SIG (*Special Interest Group*)** estandarizó usos específicos llamados "perfiles". Un perfil es un recorte que contiene *solo* la pila de protocolos exacta necesaria para esa tarea.
    *   **Clasificación de los Perfiles (Más de 25 en total):**
        *   **Audio y video:** Intercomunicador (tipo walkie-talkie), Auriculares, Manos libres, transmisión estéreo a parlantes.
        *   **Interfaz humana:** Conexión de ratones, teclados, consolas de videojuegos.
        *   **Control remoto:** Para usar un celular como control de TV u otros dispositivos.
        *   **Red de área personal (PAN):** Permite formar una red *Ad hoc* o acceder a Internet.
        *   **Red de acceso telefónico (Marcación telefónica):** Usar el teléfono celular como módem desde una PC.
        *   **Sincronización:** Carga e intercambio de objetos/datos como libretas de contactos.
    *   **Ventaja:** Permite implementaciones de software altamente optimizadas para cada dispositivo.
    *   **Desventaja:** Añade una complejidad enorme al estándar general.

---

## **Formato Exhaustivo de la Trama Bluetooth**

Debido a que Bluetooth opera en un entorno muy ruidoso (banda de 2.4 GHz compartida con hornos microondas y Wi-Fi) usando dispositivos de muy baja potencia (ej. dispositivos Clase 2 de $2.5 mW$), el diseño de sus tramas prioriza fuertemente la redundancia matemática sobre la eficiencia bruta. 

Las tramas se dividen en dos formatos principales:

#### **A. Trama de Datos de Tasa Básica (1X - 1 Mbps)**
Este es el formato estándar, compuesto por tres partes:

1.  **Código de Acceso (*Access Code*) - 72 bits:** 
    *   **Función:** Identifica al controlador (*Master*) de la *Piconet* para que los trabajadores sepan si el tráfico está dirigido a su red y no a otra red cercana.
2.  **Cabecera (*Header*) - 54 bits:** 
    *   **Detalle Técnico Matemático:** Aunque la cabecera real es de **18 bits**, el estándar obliga a repetirla **3 veces** idénticas ($18 \times 3 = 54$ bits). El circuito receptor examina las tres copias; si difieren, aplica la "opinión mayoritaria" para corregir errores. Es muy ineficiente pero altamente robusto.
    *   **Desglose de los 18 bits lógicos de la cabecera:**
        *   **Addr (Dirección) - 3 bits:** Identifica a cuál de los trabajadores activos se dirige el mensaje. *Matemáticamente, $2^3 = 8$, lo que explica la limitación arquitectónica de Bluetooth de tener exactamente 1 Controlador y solo hasta 7 Trabajadores activos por Piconet*.
        *   **Type (Tipo) - 4 bits:** Identifica el tipo de trama (ACL, SCO, sondeo o nula), el tipo de corrección de errores y si la trama ocupa 1, 3 o 5 ranuras.
        *   **F (Flujo / *Flow*) - 1 bit:** Implementa control de flujo primitivo. Un trabajador lo activa (1) cuando su búfer está lleno y no puede recibir más datos.
        *   **A (Acuse de recibo / *ACK*) - 1 bit:** Se usa para adjuntar una confirmación de recepción (*piggybacking*).
        *   **S (Secuencia / *Sequence*) - 1 bit:** Numera las tramas. Dado que el protocolo es de "parada y espera" (*stop-and-wait*), un solo bit (0 o 1) es suficiente para detectar retransmisiones duplicadas.
        *   **CRC (*Cyclic Redundancy Check*) - 8 bits:** Suma de comprobación para detectar errores exclusivamente en la cabecera.
3.  **Datos (*Data*):** 
    *   Para una transmisión corta de 1 sola ranura (*slot*), el máximo es **240 bits**.
    *   Para una trama larga de 5 ranuras, el máximo de carga útil sube a **2744 bits**.

#### **B. Trama de Datos de Tasa Mejorada (2X o 3X - 2 o 3 Mbps)**
Introducido a partir de Bluetooth 2.0. Cuando se requieren transferencias más rápidas, la cabecera se mantiene igual (modulada a 1 Mbps para garantizar compatibilidad y robustez), pero la carga útil cambia:
1.  **Código de Acceso:** 72 bits.
2.  **Cabecera (*Header*):** 54 bits.
3.  **Guard/Sync (Guarda / Sincronización) - 16 bits:** Se insertan antes de los datos para sincronizar el cambio de modulación de desplazamiento de frecuencia (1 Mbps) a modulación de desplazamiento de fase (2 o 3 Mbps).
4.  **Datos (*Data*):** La capacidad se incrementa enormemente, permitiendo hasta **8184 bits** de carga útil en una trama de múltiples ranuras.
5.  **Trailer (Remolque) - 2 bits:** Marca el final de la carga de datos a alta velocidad.

Siguiente [RFID](rfid.md)