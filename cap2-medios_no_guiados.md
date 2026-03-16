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

Esta tecnología es muy resistente a las interferencias de banda estrecha y a la atenuación, ya que la transmisión no se queda bloqueada en una frecuencia deficiente el tiempo suficiente para que la comunicación se interrumpa [4]. El FHSS se divide en dos categorías según la relación entre el tiempo que dura cada salto de frecuencia ($T_c$) y la duración del elemento de señal o bit ($T_s$) [1]:
*   **Slow FHSS (Salto lento):** Ocurre cuando $T_c (ranuras) \ge T_s$ (datos). En este caso, se transmiten uno o varios bits completos durante el tiempo que la señal permanece en una sola frecuencia [1].
*   **Fast FHSS (Salto rápido):** Ocurre cuando $T_c (ranuras) \le T_s$ (datos). En este escenario, la frecuencia cambia varias veces durante la transmisión de un solo bit [1]. Esta modalidad ofrece un mejor rendimiento y hace que la señal sea excepcionalmente resistente al ruido [1].

**Espectro Ensanchado de Secuencia Directa (DSSS)**
A diferencia del salto de frecuencias, el DSSS utiliza una secuencia de códigos para expandir la señal de datos a lo largo de una banda de frecuencias más amplia [5]. En este esquema, cada bit de datos original es representado por múltiples bits utilizando un "código de expansión" (secuencia de chips) [5, 6]. 

Las imágenes de las diapositivas muestran visualmente cómo funciona este proceso en el transmisor y el receptor mediante una función XOR lógica: la entrada de datos original (señal A) se combina con un flujo de bits pseudoaleatorio generado localmente (señal B), el cual oscila a una velocidad mucho mayor ($T_c$) [6]. El resultado es la señal transmitida (señal C), que ahora posee un espectro ensanchado [6]. En el lado del receptor, se requiere utilizar exactamente la misma secuencia pseudoaleatoria (B) para combinarla con la señal recibida (C) y así recuperar con éxito la salida de datos original (A) [6].

El DSSS ofrece un rendimiento y tolerancia a las interferencias muy similar al FHSS, ya que ante una distorsión solo se pierde una fracción de la señal deseada [5, 6]. Su uso comercial es sumamente amplio porque permite a múltiples señales compartir la misma banda de frecuencia codificando a los usuarios con secuencias diferentes (base de la tecnología CDMA), aplicándose intensivamente en redes celulares 3G y en el sistema GPS [5].

**Comunicación por Banda Ultraancha (Ultra Wideband Communication - UWB)**
La comunicación UWB, regulada bajo el estándar IEEE 802.15.4a, opera en un rango de frecuencias extremadamente extenso, desde los 3.1 hasta los 10.6 GHz [6]. En lugar de alterar una portadora continua, la UWB envía rápidos pulsos de muy baja energía variando continuamente sus frecuencias [6, 7]. Estas transiciones ultrarrápidas generan una señal que abarca un ancho de banda gigantesco (al menos 500 MHz o el 20% de su frecuencia central) [7].

El diagrama de la diapositiva ilustra la señal UWB como una capa subyacente ("underlay") muy amplia horizontalmente a lo largo del eje de las frecuencias, pero con una amplitud de alimentación muy baja en el eje vertical, operando prácticamente por debajo del espectro de ruido en comparación con los picos angostos y potentes de las señales originales o las de DSSS/FHSS [6].

Gracias a esta extensa distribución de baja energía, la UWB ofrece características operativas distintivas:
*   Posee el potencial de transmitir datos a velocidades muy altas, del orden de varios cientos de Mbps [6, 7].
*   Tolera niveles considerables de interferencia externa de banda estrecha [6, 7].
*   Al concentrar tan poca energía en una frecuencia específica, no causa interferencias perjudiciales a otros dispositivos que operen en bandas estrechas compartiendo el mismo espacio radioeléctrico [6, 7].
*   Sus aplicaciones típicas se centran en comunicaciones de corta distancia en interiores, funcionamiento de radares de precisión, obtención de imágenes a través de objetos sólidos y tecnología de localización [7, 8].


