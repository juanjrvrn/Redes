# **Generaciones IEEE 802.11**

La subcapa **MAC** (*Medium Access Control* - Control de Acceso al Medio) se mantiene uniforme, pero la capa física ha evolucionado drásticamente para aumentar las tasas de transmisión. Las tarjetas de red (**NIC** - *Network Interface Cards*) modernas suelen implementar múltiples estándares (ej. 802.11a/b/g) y utilizan *Rate Adaptation* (Adaptación de tasa) para ajustar la velocidad a las condiciones del medio y evitar errores.

## **IEEE 802.11 (Legacy / Original)**
*   **Fecha de lanzamiento:** 1997 - 1999.
*   **Técnica de Capa Física:** Espectro ensanchado por salto de frecuencias (*Frequency Hopping*) e Infrarrojos.
*   **Desventaja:** Tecnologías obsoletas que ya han desaparecido de la práctica comercial.

## **IEEE 802.11b**
*   **Fecha de lanzamiento:** 1999.
*   **Frecuencia:** Banda **ISM** (*Industrial, Scientific and Medical*) de **2.4 GHz**.
*   **Tasa de Datos:** 11 Mbps máximo (típicamente 1, 2, 5.5, y 6.5 Mbps).
*   **Técnica de Transmisión:** **DSSS** (*Direct Sequence Spread Spectrum* - Espectro Ensanchado por Secuencia Directa).
*   **Detalles Técnicos y Modulaciones:**
    *   Utiliza una tasa de "chipping" de 11 MHz (*11 Mchips/seg*).
    *   Para 1 o 2 Mbps, utiliza una **Secuencia de Barker** combinada con modulación **BPSK** (*Binary Phase Shift Keying* - Modulación por Desplazamiento de Fase Binaria) o **QPSK** (*Quadrature Phase Shift Keying* - Modulación por Desplazamiento de Fase en Cuadratura).
    *   Para tasas más altas (5.5 y 11 Mbps), implementa la modulación **CCK** (*Complementary Code Keying* - Modulación por Código Complementario), la cual permite enviar más bits (4 u 8 bits por cada código de 8 chips) utilizando el mismo ancho de banda.
*   **Ventajas:** Tiene un alcance geográfico excelente (aproximadamente siete veces mayor que 802.11a).
*   **Desventajas:** La banda de 2.4 GHz está muy abarrotada, sufriendo interferencias de hornos microondas, teléfonos inalámbricos y abridores de garaje.

## **IEEE 802.11a**
*   **Fecha de lanzamiento:** 1999.
*   **Frecuencia:** Banda de **5 GHz**.
*   **Tasa de Datos:** 54 Mbps máximo (típicamente 25 Mbps).
*   **Técnica de Transmisión:** **OFDM** (*Orthogonal Frequency Division Multiplexing* - Multiplexación por División de Frecuencias Ortogonales).
*   **Detalles Técnicos y Modulaciones:**
    *   Transmite señales divididas en **52 subportadoras** (*subcarriers*) en paralelo: 48 transportan datos y 4 se usan para sincronización. Cada símbolo dura $4 \mu s$.
    *   **Clasificación de Modulaciones:** Soporta **BPSK**, **QPSK**, **16-QAM** (*Quadrature Amplitude Modulation* - Modulación de Amplitud en Cuadratura), y **64-QAM**.
    *   **Código de Detección/Corrección de Errores:** Utiliza un código convolucional binario a tasas de redundancia de 1/2, 2/3, o 3/4.
    *   **Regla de Tasa:** La combinación exacta de la técnica de modulación y la tasa de codificación es lo que determina la tasa de bits final (permitiendo 8 velocidades distintas desde 6 hasta 54 Mbps).
*   **Ventaja:** Resiste muy bien las interferencias y el ruido por trayectos múltiples (*multipath*) gracias a OFDM, y la banda de 5 GHz está menos congestionada.
*   **Desventaja:** Las ondas de radio más cortas de 5 GHz no penetran las paredes tan bien como las de 2.4 GHz, lo que reduce severamente su alcance.

## **IEEE 802.11g**
*   **Fecha de lanzamiento:** 2003.
*   **Frecuencia:** Banda de **2.4 GHz**.
*   **Tasa de Datos:** 54 Mbps máximo (típicamente 25 Mbps).
*   **Técnica de Transmisión:** **OFDM** de alta velocidad.
*   **Detalles Técnicos y Modulaciones:** Combina las técnicas físicas de 802.11a y 802.11b.
    *   Usa **ERP-OFDM** (*Extended Rate PHY OFDM*) para lograr tasas de 6, 9, 12, 18, 24, 36, 48 y 54 Mbps.
    *   Usa **ERP-PBCC** (*Packet Binary Convolutional Coding*) para tasas de 22 y 33 Mbps.
*   **Ventaja:** Es totalmente retrocompatible con dispositivos 802.11b, ofreciendo las altas velocidades de la versión "a" pero con el gran alcance de la versión "b".

## **IEEE 802.11n (Wi-Fi 4)**
*   **Fecha de lanzamiento:** 2009.
*   **Frecuencias:** **2.4 GHz y 5 GHz**.
*   **Tasa de Datos:** 600 Mbps máximo (típicamente 200 Mbps).
*   **Técnica de Transmisión:** **MIMO OFDM** (*Multiple Input, Multiple Output* - Múltiples Entradas y Múltiples Salidas).
*   **Detalles Técnicos y Modulaciones:**
    *   Utiliza múltiples antenas para transmitir hasta **4 flujos o cadenas de transmisión** simultáneamente.
    *   **Característica (Channel Bonding):** Permite la "unión de canales", tomando dos canales separados de 20 MHz que no se solapan para formar un canal ancho de **40 MHz**.
    *   Modulación máxima soportada: **64-QAM**.
    *   Reduce los gastos generales (*overhead*) permitiendo el envío conjunto de un grupo de tramas.
*   **Ventaja:** Multiplica la velocidad bruta, mejora el alcance y la fiabilidad de la señal, y es retrocompatible con 802.11a/b/g.

## **IEEE 802.11ac (Wi-Fi 5 / Gigabit Wi-Fi)**
*   **Fecha de lanzamiento:** 2013.
*   **Frecuencia:** Exclusivo en la banda de **5 GHz**.
*   **Tasa de Datos:** **6.933 Gbps** máximo teórico.
*   **Técnica de Transmisión:** **MU-MIMO OFDM** (*Multi-User MIMO* - MIMO Multiusuario). En esta versión, se aplica estrictamente en enlace descendente (*downlink*).
*   **Detalles Técnicos y Modulaciones:**
    *   Escala drásticamente los anchos de canal permitiendo **20, 40, 80 o 160 MHz**.
    *   Soporta hasta **8 cadenas de transmisión** (*streams*) y permite enviar datos a hasta 4 clientes distintos simultáneamente.
    *   Implementa una modulación de alta densidad: **256-QAM**, que permite que cada símbolo codifique **8 bits**.
*   **Desventaja:** Los dispositivos antiguos que solo poseen radios de 2.4 GHz no pueden ver ni utilizar esta red.

## **IEEE 802.11ad (Tecnología Direccional)**
*(Nota del profesor: Aunque no aparece en la tabla principal de la diapositiva 9, el estándar técnico lo clasifica como una adición crucial para entornos específicos)*.
*   **Frecuencia:** Banda de **60 GHz** (57-71 GHz).
*   **Ventajas/Características:** Al operar a frecuencias tan altas, las ondas de radio miden apenas 5 milímetros. Permite un ancho de banda masivo ideal para transmitir películas en resolución 4K u 8K sin comprimir.
*   **Desventajas:** Las ondas son tan cortas que no pueden penetrar paredes en absoluto. Su cobertura está estrictamente confinada a los límites de una sola habitación. 

## **IEEE 802.11ax (Wi-Fi 6 / High Efficiency Wireless)**
*   **Fecha de lanzamiento:** 2019.
*   **Frecuencias:** **2.4 GHz y 5 GHz**.
*   **Tasa de Datos:** **9.607 Gbps** máximo teórico (aunque puede operar en espectros futuros de hasta 7 GHz para alcanzar 11 Gbps).
*   **Técnica de Transmisión:** **MU-MIMO OFDMA** (*Orthogonal Frequency Division Multiple Access* - Acceso Múltiple por División de Frecuencias Ortogonales).
*   **Detalles Técnicos y Modulaciones:**
    *   Aplica **MU-MIMO** en ambas direcciones (subida y bajada).
    *   Utiliza anchos de canal de **20, 40, 80 o 160 MHz** con hasta **8 cadenas** de transmisión.
    *   Implementa modulación extrema: **1024-QAM**, que permite que cada símbolo codifique **10 bits** (superando los 8 bits de la versión *ac*).
    *   **Característica (Target Wake Time / Tiempo de Activación Objetivo):** Permite al enrutador programar matemáticamente la transmisión de los dispositivos conectados (especialmente dispositivos de hogares inteligentes o IoT - Internet de las Cosas) para enviar "latidos" periódicos, minimizando las colisiones drásticamente.
    *   Introduce dos **NAV** (*Network Allocation Vector*) paralelos: uno para la red asociada y otro para redes solapadas, mitigando caídas de rendimiento en entornos muy densos.
*   **Compatibilidad:** Es totalmente retrocompatible con 802.11a/b/g/n/ac.

Siguiente: [CSMA/CA](csmaca.md)