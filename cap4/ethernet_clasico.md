# **Redes Ethernet Clásico (10 Mbps)**

## **La Capa Física y las Implementaciones de Ethernet**

El estándar Ethernet clásico opera de forma estandarizada a una tasa de bits de **10 Mbps** y utiliza la **Codificación Manchester** en su capa física. Esta codificación es un método que garantiza una transición de voltaje en el medio de cada bit, permitiendo sincronizar los relojes del emisor y receptor.

### **Clasificación de las Implementaciones de Cableado Ethernet (Estándar IEEE 802.3):**
La evolución del medio físico nos dejó cuatro implementaciones históricas exactas que no debemos olvidar:
*   **10Base5:** 
    *   **Cable:** Cable coaxial grueso (*Thick coax*).
    *   **Segmento máximo:** 500 metros.
    *   **Nodos por segmento:** 100.
    *   **Ventajas:** Fue el cable original; actualmente se encuentra obsoleto.
*   **10Base2:**
    *   **Cable:** Cable coaxial delgado (*Thin coax*).
    *   **Segmento máximo:** 185 metros.
    *   **Nodos por segmento:** 30.
    *   **Ventajas:** No requiere el uso de un concentrador (*Hub*).
*   **10Base-T (La más extendida en su época):**
    *   **Cable:** Par trenzado (*Twisted pair*), específicamente **UTP** (*Unshielded Twisted Pair*) de Categoría 3 como mínimo.
    *   **Segmento máximo:** 100 metros.
    *   **Nodos por segmento:** 1024.
    *   **Ventajas:** Es el sistema más económico (*Cheapest system*).
*   **10Base-F:**
    *   **Cable:** Fibra óptica (*Fiber optics*).
    *   **Segmento máximo:** 2000 metros.
    *   **Nodos por segmento:** 1024.
    *   **Ventajas:** Es el mejor sistema para conexiones entre edificios (*Best between buildings*).

**Análisis de las imágenes de la Capa Física:**
El material ilustra la implementación **10Base-T** con un esquema de una red LAN en **topología de estrella**, donde varias computadoras ("Terminales") se conectan mediante cables **UTP** (con conectores RJ-45) a un dispositivo central llamado **Hub** (concentrador).
*   **Detalle técnico del Hub:** Otra imagen ilustra una explosión visual con la palabra **"CRASH!"** cuando dos terminales (H1 y H2) envían una trama a la vez. Esto demuestra que **el Hub es un dispositivo analógico de capa 1** (física) que actúa como un bus de datos: repite ciegamente la señal eléctrica por todos sus puertos, creando un único y frágil **dominio de colisión**. Debido a esto, las estaciones están obligadas a operar en modo **Half-Duplex** (no pueden enviar y recibir al mismo tiempo).

## **Subcapa MAC y el Protocolo CSMA/CD**

Para gestionar este dominio de colisión único, la subcapa **MAC** (*Multiple Access Control*, parte del estándar **IEEE 802.3**) utiliza un protocolo específico de contención. 

**Características del Algoritmo CSMA/CD (*Carrier Sense Multiple Access with Collision Detection* - IEEE 802.3) 1-persistente:**
El comportamiento estricto de las estaciones bajo este protocolo incluye los siguientes pasos exactos:
*   Antes de transmitir, la estación **escucha el canal** (detección de portadora).
*   Si el canal está libre, **transmite la trama** inmediatamente (de ahí el "1-persistente").
*   Si está ocupado, **espera** a que esté libre y luego transmite.
*   Mientras transmite, la estación **sigue escuchando el canal**. 
*   Si detecta una colisión, **interrumpe la transmisión** inmediatamente para ahorrar tiempo y ancho de banda, y emite una ráfaga de ruido.
*   Tras la interrupción, la estación **espera un tiempo aleatorio** computado mediante el **Algoritmo Exponencial Binario** y luego repite el proceso.
*   **Límite técnico:** Todas las colisiones en este estándar ocurren exclusivamente entre el **byte 1 y el byte 64** de la trama.

## **Formato de las Tramas Ethernet DIX e IEEE 802.3**

El empaquetamiento de los datos exige una estructura muy rígida. La diapositiva muestra los diagramas de bloques rectangulares contrastando la trama original **Ethernet DIX** (*Digital, Intel, Xerox*) con la estandarizada **IEEE 802.3**. 

**Características y Campos de la Trama (Estructura Completa):**
*   **Preámbulo (Preamble):** 8 bytes. Sirve para sincronizar los relojes. En el estándar 802.3, el último byte termina en `11` y se denomina "Delimitador de inicio de trama".
*   **Dirección MAC de Destino:** 6 bytes.
*   **Dirección MAC de Origen:** 6 bytes.
*   **Campo Longitud / Tipo (Length / Type):** 2 bytes. Aquí radica la diferencia clave:
    *   Si el valor es **$\ge 1536$ (0x0600)**: Se interpreta como "Ethertype" (Trama DIX), indicando qué protocolo de la capa de red viaja dentro (ej. IPv4).
    *   Si el valor es **$< 1536$**: Se interpreta como "Longitud" de los datos (Trama IEEE 802.3). En este caso, el "Ethertype" va oculto más adelante dentro de una cabecera adicional llamada **LLC/SNAP** (*Logical Link Control / Subnetwork Access Protocol* - **IEEE 802.2**) que ocupa 8 bytes y queda incrustado en los datos de la trama.
*   **Datos (Data):** De 0 a 1500 bytes de carga útil (1492 si se usa LLC/SNAP, Ethernet DIX).
*   **Relleno (Pad):** De 0 a 46 bytes. Se utiliza si los datos son muy pequeños, para forzar que la trama entera alcance el **mínimo estricto de 64 bytes** (512 bits). Este tamaño mínimo garantiza que la transmisión dure más tiempo que el viaje de ida y vuelta de la señal en el cable ($L_{trama\_minima} = V_t \cdot 2 \cdot \tau$), asegurando que el emisor detecte la colisión antes de terminar de hablar.
*   **Suma de Comprobación (Checksum/CRC - *Cyclic Redundancy Check*):** 4 bytes finales (32 bits) calculados matemáticamente para detectar si la trama sufrió alteraciones eléctricas en el camino.


## **Estructura de las Direcciones MAC (MAC Address)**

La dirección consta exactamente de **6 bytes, lo que equivale a 12 dígitos hexadecimales o 48 bits**. Se divide en dos partes fundamentales:
*   **Parte asignada al fabricante (OUI - *Organizationally Unique Identifier*):** Los primeros 3 bytes. Son asignados globalmente por la IEEE.
*   **Parte específica del equipo (Número de serie):** Los últimos 3 bytes. Asignados por el fabricante en la tarjeta de red (NIC).

**Reglas a nivel de Bits (Primer Byte):**
El documento hace un desglose vital de los bits menos significativos del primer byte de la dirección:
*   **Bit de tipo de comunicación:** 
    *   `0` = Dirección Individual (**Unicast**).
    *   `1` = Dirección de Grupo (**Multicast**).
*   **Bit de administración:**
    *   `0` = Dirección Global (administrada globalmente desde fábrica).
    *   `1` = Dirección Local (administrada o alterada localmente por el administrador).
*   **Dirección de Broadcast (Difusión):** Compuesta enteramente por unos (1). Se representa en hexadecimal como **FF:FF:FF:FF:FF:FF** y es aceptada por todas las estaciones de la red.

Siguiente [Ethernet conmutado](ethernet_conmutado.md)

