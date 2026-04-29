# **Evolución a Alta Velocidad (Fast y Gigabit Ethernet)**

## **Fast Ethernet (Estándar IEEE 802.3u)**

La primera gran evolución, denominada **Fast Ethernet** (estandarizada por el **IEEE**, *Institute of Electrical and Electronics Engineers*, bajo la norma **802.3u**), tuvo como objetivo multiplicar por 10 la tasa de bits, manteniendo un nivel de compatibilidad con los sistemas preexistentes.

**Características y Clasificación de Implementaciones (Capa Física):**
El estándar definió variantes específicas de cableado para garantizar su viabilidad comercial, ilustradas en las tablas del material:

*   **100Base-T4:**
    *   **Cable:** Par trenzado (*Twisted pair*).
    *   **Segmento máximo:** 100 metros.
    *   **Ventajas (*Advantages*):** Utiliza UTP (*Unshielded Twisted Pair*) de Categoría 3.
*   **100Base-TX:**
    *   **Cable:** Par trenzado (*Twisted pair*).
    *   **Segmento máximo:** 100 metros.
    *   **Ventajas (*Advantages*):** Permite comunicación *Full duplex* a 100 Mbps.
*   **100Base-FX:**
    *   **Cable:** Fibra óptica (*Fiber optics*).
    *   **Segmento máximo:** 2000 metros.
    *   **Ventajas (*Advantages*):** *Full duplex* a 100 Mbps; ideal para tramos largos (*long runs*).

**Aspectos Técnicos Adicionales de Fast Ethernet:**
*   **Codificación:** Abandona la ineficiente codificación Manchester de la versión clásica e introduce la codificación **4B/5B** acoplada con modulación **NRZI** (*Non-Return-to-Zero Inverted*).
*   **Compatibilidad (Autonegociación / *Autonegotiation*):** Todos los equipos Fast Ethernet son compatibles hacia atrás con el Ethernet clásico de 10 Mbps gracias a esta función, la cual permite a los dispositivos acordar la mejor velocidad y modo (Half o Full Duplex) antes de transmitir.

---

## **Gigabit Ethernet (Estándares IEEE 802.3z y IEEE 802.3ab)**

El siguiente salto tecnológico fue el **Gigabit Ethernet** (1000 Mbps o 1 Gbps), pensado inicialmente para enlaces troncales de fibra y luego adaptado al cableado de oficinas. 

**Evolución Normativa:**
1.  **IEEE 802.3z (Año 1997):** Estándar original diseñado exclusivamente para fibra óptica.
2.  **IEEE 802.3ab (Año 1999):** Estándar que logró llevar 1 Gbps a través de cables de cobre (1000Base-T), utilizando 4 pares de cable UTP Categoría 5e operando a 125 MHz en modo *Full Duplex (FDX) dual*. 

**Características y Clasificación de Implementaciones (Capa Física):**
La tabla técnica proporcionada en el apunte clasifica las opciones de la siguiente manera:

*   **1000Base-SX:**
    *   **Cable:** Fibra óptica (*Fiber optics*).
    *   **Segmento máximo:** 550 metros.
    *   **Ventajas (*Advantages*):** Fibra multimodo (*Multimode fiber* de 50 o 62.5 micrones). Utiliza emisores **LED** (*Light-Emitting Diode*), lo que la hace una opción más barata.
*   **1000Base-LX:**
    *   **Cable:** Fibra óptica (*Fiber optics*).
    *   **Segmento máximo:** 5000 metros.
    *   **Ventajas (*Advantages*):** Soporta fibra monomodo (*Single*, 10 $\mu$) o multimodo (50, 62.5 $\mu$).
*   **1000Base-CX:**
    *   **Cable:** 2 pares de **STP** (*Shielded twisted pair* - Par trenzado blindado).
    *   **Segmento máximo:** 25 metros.
    *   **Ventajas (*Advantages*):** Par trenzado blindado.
*   **1000Base-T:**
    *   **Cable:** 4 pares de **UTP**.
    *   **Segmento máximo:** 100 metros.
    *   **Ventajas (*Advantages*):** Utiliza UTP de categoría 5 estándar.

**Análisis Visual y Codificación (Apoyado en los diagramas de la fuente):**
*   Para las versiones de fibra óptica, se utilizan decodificadores **8B/10B** (esquema heredado de *Fibre Channel*) que codifican 8 bits de datos en palabras de 10 bits equilibradas (igual número de ceros y unos), enviadas al medio mediante señalización **NRZ** (*Non-Return-to-Zero*).
*   Para el cobre (1000Base-T), se aplica un procesamiento digital de señales (**DSP**, *Digital Signal Processing*) y una modulación con cinco niveles de voltaje para transmitir simultáneamente de forma bidireccional sobre los 4 pares trenzados. 
*   **Diagramas "Standard Frame" vs "Jumbo Frame":** Como lo marca el esquema visual, a estas inmensas velocidades surge la opción de usar *Jumbo Frames* (tramas gigantes no estándar de hasta 9000 bytes) en lugar de la trama estándar de ~1518 bytes. Esto incrementa drásticamente la eficiencia al reducir la sobrecarga de procesador en los equipos.



## **Gigabit Ethernet en Redes No Conmutadas (Fórmulas y Desafíos)**

Aunque la inmensa mayoría del Gigabit Ethernet actual utiliza *Switches* en modo *Full Duplex*, el estándar original permitía explícitamente el uso de concentradores (*Hubs*) basados en el protocolo de contención **CSMA/CD** (*Carrier Sense Multiple Access with Collision Detection*). 

Aquí se presentó un grave obstáculo físico y matemático: a 1000 Mbps, el tamaño mínimo clásico de trama de Ethernet (64 bytes) se transmite de manera tan efímera que una estación terminaría de hablar antes de que la señal viaje y vuelva en caso de colisión. Para evitar esto, las diapositivas detallan las siguientes **fórmulas matemáticas inquebrantables**:

1.  **Fórmula general de longitud mínima:**
    $$l_{trama\_min} = 2 \cdot \tau \cdot V_{transm.}$$
    $$l_{trama\_min} = 2 \cdot (d_{max} / V_{propag.}) \cdot V_{transm.}$$
2.  **Cálculo en Ethernet clásico (10 Mbps):**
    $$64 \text{ bytes} = 2 \cdot (2500 \text{ m} / V_{propag.}) \cdot 10 \text{ Mbps}$$
3.  **Cálculo equivalente para Gigabit Ethernet (1 Gbps):**
    $$l_{trama\_min} = 2 \cdot (200 \text{ m} / V_{propag.}) \cdot 1 \text{ Gbps} = 512 \text{ bytes}$$

Para poder mantener el **tamaño de trama mínimo estándar de 64 bytes por motivos de compatibilidad**, y al mismo tiempo simular los 512 bytes requeridos en redes no conmutadas para detectar colisiones, el estándar introdujo **dos mecanismos exclusivos** detallados en la presentación:

*   **A) Ráfaga de tramas (*Fragment burst* o *Frame burst*):** Se envían juntas más de una trama consecutiva en el canal hasta sumar el mínimo estricto de 512 bytes entre todas ellas.
*   **B) Extensión de portadora (*Carrier extension*):** Si se desea enviar una sola trama pequeña, el equipo emisor aumenta artificialmente el tamaño del campo de "Relleno" (*Pad*) mediante señales especiales hasta que la transmisión alcance los 512 bytes requeridos, asegurando que escuche lo suficiente como para detectar un posible choque.