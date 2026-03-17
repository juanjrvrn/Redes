## Medios de transmisión no guiados

### Conceptos Fundamentales
Las ondas electromagnéticas se generan a partir del movimiento de los electrones y las variaciones que estos producen en los campos electromagnéticos. Para comprender su comportamiento, es indispensable manejar los siguientes conceptos:
*   **Frecuencia ($f$):** Es el número de oscilaciones que la onda realiza en un segundo. Su unidad de medida es el Hertz (Hz).
*   **Longitud de onda ($\lambda$):** Es la distancia física que ocupa un ciclo completo de la onda (la distancia entre dos puntos con la misma fase, como dos crestas consecutivas).
*   **Fase ($\phi$):** Indica la posición relativa de la onda en el tiempo, usualmente medida en ángulos.
*   **Periodo ($T$):** Es el tiempo que tarda la onda en completar un ciclo.
*   **Velocidad de propagación ($v_p$) y su relación con la luz ($c$):** En el vacío, todas las ondas electromagnéticas viajan a la velocidad de la luz ($c \approx 3 \times 10^8$ m/s), independientemente de su frecuencia. Existe una relación matemática inquebrantable entre la velocidad, la longitud de onda y la frecuencia: $c = \lambda \cdot f$. Dado que $c$ es constante, a mayor frecuencia, menor longitud de onda, y viceversa. En medios guiados como el cobre o la fibra óptica, esta velocidad disminuye a aproximadamente dos tercios de la velocidad de la luz.

### Escalas del Espectro Electromagnético (Frecuencias y Longitudes de Onda)
Las diapositivas y los textos muestran el espectro en una escala logarítmica que abarca desde $10^0$ Hz hasta $10^{24}$ Hz. A continuación se detallan las escalas combinando sus rangos de frecuencia, sus longitudes de onda y la analogía de su tamaño físico:

*   **Ondas de Radio:**
    *   **Frecuencia:** Generalmente desde los $10^4$ Hz hasta los $10^9$ Hz (teóricamente la banda de radiofrecuencia abarca de 3 kHz a 3 GHz).
    *   **Longitud de onda:** Alrededor de $10^3$ metros. Son tan inmensas que se comparan con el **tamaño de un edificio**. Logran penetrar la atmósfera terrestre.
*   **Microondas:**
    *   **Frecuencia:** De $10^9$ Hz a $10^{11}$ Hz en la escala gráfica (oficialmente de 3 GHz a 300 GHz).
    *   **Longitud de onda:** Alrededor de $10^{-2}$ metros. Físicamente comparables al **tamaño de un humano o de una abeja**.
*   **Infrarrojos:**
    *   **Frecuencia:** De $10^{12}$ Hz a $10^{14}$ Hz (de 300 GHz a 400 THz).
    *   **Longitud de onda:** Alrededor de $10^{-5}$ metros. Su tamaño es similar al de la **punta de un alfiler**.
*   **Luz Visible:**
    *   **Frecuencia:** Alrededor de $10^{15}$ Hz.
    *   **Longitud de onda:** Aprox. $0.5 \times 10^{-6}$ metros (entre 0.4 y 0.7 micras o 400 a 700 nanómetros). Es tan diminuta que se compara con el tamaño de un **protozoo**. Es la otra gran franja, junto con la radio, que logra penetrar la atmósfera de la Tierra.
*   **Ultravioleta (UV):**
    *   **Frecuencia:** Entre $10^{15}$ Hz y $10^{16}$ Hz.
    *   **Longitud de onda:** Alrededor de $10^{-8}$ metros, comparable al tamaño de una **molécula**.
*   **Rayos X:**
    *   **Frecuencia:** De $10^{17}$ Hz a $10^{19}$ Hz.
    *   **Longitud de onda:** Alrededor de $10^{-10}$ metros, el equivalente al tamaño de un **átomo**.
*   **Rayos Gamma:**
    *   **Frecuencia:** De $10^{20}$ Hz hasta $10^{24}$ Hz.
    *   **Longitud de onda:** Alrededor de $10^{-12}$ metros, tan increíblemente minúsculas que se asimilan al tamaño de un **núcleo atómico**. Las ondas desde el espectro UV hasta los rayos gamma son bloqueadas por la atmósfera terrestre y son peligrosas para los seres vivos.

### Bandas ITU: Frecuencias, Propagación y Aplicaciones
El uso práctico para telecomunicaciones se concentra en las bandas de radio y microondas reguladas por la UIT (Unión Internacional de Telecomunicaciones):

*   **VLF (3-30 kHz) y LF (30-300 kHz):**
    *   **Propagación:** Superficial (ground-wave). Siguen la curvatura de la Tierra (hasta 1.000 km).
    *   **Aplicaciones:** Radionavegación de largo alcance, comunicaciones con submarinos, radiofaros y señal horaria.
*   **MF (300 kHz - 3 MHz):**
    *   **Propagación:** Aérea y superficial. Atraviesan edificios fácilmente.
    *   **Aplicaciones:** Radio AM (onda media).
*   **HF (3 - 30 MHz):**
    *   **Propagación:** Aérea (sky-wave). Rebotan en la ionosfera, logrando alcances globales.
    *   **Aplicaciones:** Banda ciudadana (CB), radioafición, comunicación de barcos y aviones (onda corta).
*   **VHF (30 - 300 MHz) y UHF (300 MHz - 3 GHz):**
    *   **Propagación:** Aérea y línea de vista (line-of-sight). Las UHF no atraviesan bien los obstáculos y viajan en línea recta.
    *   **Aplicaciones:** Radio FM, Televisión VHF/UHF, telefonía móvil (celular), buscapersonas, GPS y Bluetooth.
*   **SHF (3 - 30 GHz) y EHF (30 - 300 GHz):**
    *   **Propagación:** Estrictamente línea de vista. Al ser microondas, se enfocan en haces estrechos con antenas parabólicas. Sufren atenuación por lluvia y no atraviesan objetos sólidos.
    *   **Aplicaciones:** Comunicación por satélite, radioastronomía, radares, WiFi y enlaces terrestres de microondas.

### Propiedades Físicas según el Tipo de Onda
*   **Radiofrecuencias (3 kHz a 3 GHz):** Son omnidireccionales, penetran edificios y obstáculos con facilidad. Sin embargo, su potencia disminuye bruscamente con la distancia (pérdida de trayecto), requiriendo estricta regulación gubernamental para evitar interferencias.
*   **Microondas (3 GHz a 300 GHz):** Son altamente direccionales, permitiendo comunicación punto a punto sin interferir con otros enlaces paralelos, pero están sujetas al *desvanecimiento multitrayecto* (señales que rebotan y se anulan entre sí) y a la absorción por la lluvia en frecuencias altas (ej. 4 GHz o bandas Ku/Ka en satélites).
*   **Infrarrojos (300 GHz a 400 THz):** Muy direccionales. Su incapacidad para atravesar objetos sólidos les otorga una ventaja natural de seguridad; por ello, no requieren licencias y son ideales para redes de corto alcance o controles remotos dentro de una misma habitación.

### Técnicas de espectro expandido
El **espectro expandido o ensanchado** es un método de codificación fundamental para las comunicaciones inalámbricas, el cual distribuye o "ensancha" los datos sobre todo el ancho de banda disponible [1]. Sus principales ventajas radican en que proporciona una gran inmunidad al ruido y a la distorsión por trayectorias múltiples (multipath), permite ocultar o encriptar las señales dificultando su intercepción, y hace posible que varios usuarios compartan el mismo ancho de banda con muy poca interferencia [1, 2].

**Espectro Ensanchado por Salto de Frecuencia (FHSS)**
En esta técnica, co-inventada y patentada por la actriz Hedy Lamarr en 1942, la señal se envía a través de una serie pseudoaleatoria de frecuencias [1-3]. El transmisor "salta" de una frecuencia a otra cientos de veces por segundo, y el receptor debe realizar estos mismos saltos en estricto sincronismo con el transmisor para poder recuperar la información [1, 4]. Como ilustran los diagramas de las diapositivas, la energía de la señal no permanece en una única frecuencia, sino que el uso del canal se desplaza de manera aleatoria en el tiempo a través de diferentes frecuencias preasignadas en el espectro [1].

Esta tecnología es muy resistente a las interferencias de banda estrecha y a la atenuación, ya que la transmisión no se queda bloqueada en una frecuencia deficiente el tiempo suficiente para que la comunicación se interrumpa [4]. El FHSS se divide en dos categorías según la relación entre el tiempo que dura cada salto de frecuencia ($T_c$, ranuras) y la duración del elemento de señal o bit ($T_s$, datos) [1]:
*   **Slow FHSS (Salto lento):** Ocurre cuando $T_c (ranuras) \ge T_s$ (datos). En este caso, se transmiten uno o varios bits completos durante el tiempo que la señal permanece en una sola frecuencia [1].
![slow fhss](assets/slow_fhss.png)
*   **Fast FHSS (Salto rápido):** Ocurre cuando $T_c (ranuras) \le T_s$ (datos). En este escenario, la frecuencia cambia varias veces durante la transmisión de un solo bit [1]. Esta modalidad ofrece un mejor rendimiento y hace que la señal sea excepcionalmente resistente al ruido [1].
![fast fhss](assets/fast_fhss.png)

**Espectro Ensanchado de Secuencia Directa (DSSS)**
A diferencia del salto de frecuencias, el DSSS utiliza una secuencia de códigos pseudoaleatorios, como una máscara, para expandir la señal de datos a lo largo de una banda de frecuencias más amplia [5]. En este esquema, cada bit de datos original es representado por múltiples bits.

![dsss](assets/dsss.png)
Las imágenes de las diapositivas muestran visualmente cómo funciona este proceso en el transmisor y el receptor mediante una función XOR lógica: la entrada de datos original (señal A) se combina con un flujo de bits pseudoaleatorio generado localmente (señal B), el cual oscila a una velocidad mucho mayor ($T_c$) [6]. El resultado es la señal transmitida (señal C), que ahora posee un espectro ensanchado [6]. En el lado del receptor, se requiere utilizar exactamente la misma secuencia pseudoaleatoria (B) para combinarla con la señal recibida (C) y así recuperar con éxito la salida de datos original (A) [6].

El DSSS ofrece un rendimiento y tolerancia a las interferencias muy similar al FHSS, ya que ante una distorsión solo se pierde una fracción de la señal deseada [5, 6]. Su uso comercial es sumamente amplio porque permite a múltiples señales compartir la misma banda de frecuencia codificando a los usuarios con secuencias diferentes (base de la tecnología CDMA), aplicándose intensivamente en redes celulares 3G y en el sistema GPS [5].

**Comunicación por Banda Ultraancha (Ultra Wideband Communication - UWB)**
La comunicación UWB, regulada bajo el estándar IEEE 802.15.4a, opera en un rango de frecuencias extremadamente extenso, desde los 3.1 hasta los 10.6 GHz [6]. Envía rápidos pulsos de muy baja energía variando continuamente sus frecuencias [6, 7]. Estas transiciones ultrarrápidas generan una señal que abarca un ancho de banda gigantesco (al menos 500 MHz o el 20% de su frecuencia central) [7].

El diagrama de la diapositiva ilustra la señal UWB como una capa subyacente ("underlay") muy amplia horizontalmente a lo largo del eje de las frecuencias, pero con una amplitud de alimentación muy baja en el eje vertical, operando prácticamente por debajo del espectro de ruido en comparación con los picos angostos y potentes de las señales originales o las de DSSS/FHSS [6].

Gracias a esta extensa distribución de baja energía, la UWB ofrece características operativas distintivas:
*   Posee el potencial de transmitir datos a velocidades muy altas, del orden de varios cientos de Mbps [6, 7].
*   Tolera niveles considerables de interferencia externa de banda estrecha [6, 7].
*   Al concentrar tan poca energía en una frecuencia específica, no causa interferencias perjudiciales a otros dispositivos que operen en bandas estrechas compartiendo el mismo espacio radioeléctrico [6, 7].
*   Sus aplicaciones típicas se centran en comunicaciones de corta distancia en interiores, funcionamiento de radares de precisión, obtención de imágenes a través de objetos sólidos y tecnología de localización [7, 8].

### Utilización del espectro electromagnético para la transmisión 

El espectro electromagnético se divide y su uso está estrictamente regulado mediante licencias gubernamentales para evitar interferencias. Sin embargo, existen excepciones conocidas como **bandas libres (ISM y U-NII)**, que permiten a los dispositivos de baja potencia operar sin licencia gestionando ellos mismos la interferencia. Según los esquemas visuales, estas bandas libres operan en frecuencias como 900 MHz, 2.4 GHz y 5 GHz, y son ampliamente utilizadas para tecnologías de uso cotidiano como **Wi-Fi (estándares 802.11 a/b/g/n), Bluetooth y Zigbee**.

De acuerdo con la clasificación y los diagramas presentes en el material, la utilización del espectro para la transmisión no guiada se divide en cuatro grandes categorías principales:

**1. Transmisión por Radiofrecuencias (3 KHz a 3 GHz)**
Las ondas de radio son omnidireccionales, fáciles de generar, pueden recorrer grandes distancias y atraviesan fácilmente los muros y edificios. Las imágenes y gráficos detallan tres tipos de propagación dependiendo de la banda utilizada:
*   **Propagación superficial (Ground-wave):** Presente en las bandas VLF, LF y MF. Las ondas siguen la curvatura de la Tierra. Se utilizan para la comunicación de submarinos, radiofaros y la radio AM.
![ground wave](assets/ground_wave.png)
*   **Propagación aérea (Sky-wave):** Característica de la banda HF. Las ondas rebotan en la ionosfera, lo que permite comunicaciones a gran distancia, siendo la opción preferida por la radioafición.
![sky wave](assets/sky_wave.png)
*   **Propagación por línea de vista (Line-of-sight):** Utilizada en bandas VHF y UHF. Las ondas viajan directo entre antenas y se emplean para radio FM, televisión local, telefonía móvil y sistemas GPS.
![line of sight](assets/line_of_sight.png)

**2. Transmisión por Microondas (3 GHz a 300 GHz)**
Las microondas viajan en línea recta y, por lo tanto, son altamente direccionales (requiriendo línea de vista). Difícilmente logran atravesar objetos opacos. Concentran su energía usando antenas parabólicas y se emplean principalmente en telecomunicaciones de larga distancia, satélites, telefonía celular y Wi-Fi. 
Al analizar su rendimiento, los esquemas indican que están sujetas a dos problemas importantes:
*   **Atenuación:** Principal fuente de pérdida de la señal debido a la distancia o a la lluvia, ya que las gotas de agua absorben la energía de las microondas, particularmente alrededor y por encima de los 4 GHz.
*   **Interferencia por múltiples trayectorias (Desvanecimiento multitrayecto):** Las ilustraciones de las diapositivas muestran cómo la señal originada en una antena puede rebotar contra edificios u otros objetos físicos (como vehículos) antes de llegar al receptor. Estas ondas retrasadas pueden llegar desfasadas respecto a la onda directa y terminar anulando la señal.

El Sistema de Posicionamiento Global (GPS) es una tecnología de gran importancia que opera dentro de la categoría de las **microondas**, específicamente en la banda **UHF (Frecuencia Ultra Alta)** que comprende el rango de los 300 MHz a los 3 GHz. Por operar en estas frecuencias, su transmisión requiere una propagación de ondas por línea de vista (line-of-sight).

El funcionamiento del GPS y su uso del espectro electromagnético se basan en las siguientes características detalladas en los esquemas y textos:

*   **Constelación de satélites:** El sistema se apoya en una red de aproximadamente 30 satélites de órbita terrestre media (conocidos como satélites MEO), los cuales orbitan a una altitud de unos 20.200 km de la Tierra.
*   **Gestión de la interferencia:** Para evitar problemas de interferencia y mejorar la robustez de la comunicación, el GPS utiliza la técnica de modulación conocida como **Espectro Ensanchado de Secuencia Directa (DSSS)**. Esta técnica reparte la señal en una banda de frecuencia más amplia utilizando una secuencia de códigos, lo que le permite tolerar interferencias y desvanecimientos de forma muy efectiva.
*   **Transmisión de datos:** Las imágenes muestran que cada satélite envía una señal distinta al receptor GPS. En esta señal, el satélite transmite dos series de datos fundamentales: el **almanaque** y las **efemérides**. Con esta información, el receptor puede descifrar la ubicación espacial del satélite, además de la fecha y la hora exactas de la transmisión.
*   **Cálculo de la posición:** Para que un receptor GPS pueda localizar al usuario (es decir, calcular la longitud y la latitud exactas en el mapa), es requisito indispensable obtener y triangular las señales de **al menos tres satélites** simultáneamente.


**3. Transmisión por Infrarrojos (300 GHz a 400 THz)**
Se emplean ondas no guiadas, altamente direccionales y de bajo costo para la comunicación de corto alcance. No pueden atravesar objetos sólidos, lo que desde una perspectiva de redes es una ventaja: la incapacidad de cruzar paredes impide la interferencia con sistemas de habitaciones adyacentes y provee una alta seguridad contra el robo de información. Por ello, los infrarrojos no requieren licencia de uso y son comunes en controles remotos de TV, reproductores Blu-ray y para interconectar laptops usando el estándar IrDA.

**4. Transmisión por Ondas de Luz (Luz Visible y Láseres)**
La transmisión óptica aprovecha el altísimo ancho de banda disponible a bajo costo.
*   **Óptica de espacio libre (Láser):** Consiste en colocar láseres direccionales (por ejemplo, interconectando edificios). Los esquemas muestran una gran limitante ilustrando dos edificios: el sol calienta los techos generando **corrientes de convección y regiones de aire turbulento** que desvían y hacen "bailar" el rayo láser de su trayectoria, impidiendo que golpee el fotodetector receptor. Además, factores como la lluvia y la niebla también bloquean estos haces.
*   **Li-Fi (Wireless LAN mediante luz visible):** Las diapositivas ilustran esta tecnología moderna utilizando el espectro de luz visible emitido por las bombillas de las habitaciones. La luz de las bombillas parpadea en periodos de nanosegundos (totalmente imperceptibles para el ojo humano) transmitiendo datos directamente a los dispositivos de los usuarios que se encuentran bajo ellas, brindando gran seguridad por su corto alcance.

