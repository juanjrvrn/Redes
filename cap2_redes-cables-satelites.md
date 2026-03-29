## Redes de telefonia conmutadas
hice a mano en la tablet jeje...
[Ver anotaciones](redes_telefonicas.pdf)
## Redes de cables
Las redes de cable representan en la actualidad una de las infraestructuras más importantes para el acceso a Internet de banda ancha a nivel mundial. Originalmente diseñadas exclusivamente para la transmisión de televisión, han sufrido una evolución tecnológica profunda para soportar el tráfico de datos bidireccional y de alta velocidad.

Basado en las imágenes de las diapositivas y el texto proporcionado, a continuación se presenta un análisis exhaustivo de todas sus características, topología, uso del espectro y funcionamiento lógico:

### 1. Historia y Evolución a HFC (Híbrido Fibra-Coaxial)
*   **Orígenes (CATV):** La televisión por cable nació a fines de los años 40 para llevar señal a zonas rurales o montañosas. Como ilustra el diagrama histórico de las diapositivas (Fig. 2-44), el sistema original consistía en una gran antena comunitaria en una colina, un amplificador (llamado **cabecera** o *headend*) y un único cable coaxial que se iba derivando (haciendo "taps") hacia las casas. La transmisión era estrictamente unidireccional.
*   **Arquitectura HFC:** Para poder ofrecer acceso a Internet y telefonía, el sistema fue modernizado hacia una arquitectura de **Híbrido Fibra-Coaxial (HFC)**. Según los esquemas visuales de las diapositivas (Fig. 2-45a), en lugar de tender cables coaxiales desde la cabecera central hasta el destino final, se utilizan **troncales de fibra óptica de gran ancho de banda** para cubrir las distancias largas. Esta fibra llega hasta un convertidor electro-óptico en el vecindario llamado **nodo de fibra**. Desde este nodo salen los cables coaxiales tradicionales que finalmente alimentan a los hogares.
*   Para lograr la bidireccionalidad, todos los antiguos amplificadores unidireccionales del cableado tuvieron que ser reemplazados por amplificadores bidireccionales. Además, la cabecera se transformó en un enrutador digital inteligente conocido como **CMTS (Cable Modem Termination System)**, que sirve de interfaz con la red del Proveedor de Servicios de Internet (ISP).
*   La principal diferencia arquitectónica entre la red de cable y la telefónica (ADSL) se evidencia al comparar los diagramas de las diapositivas: el bucle telefónico es un hilo dedicado y exclusivo para cada usuario, mientras que **el cable coaxial es un medio físico compartido por decenas o cientos de casas** conectadas al mismo nodo. 
*   **Impacto en el rendimiento:** Si un usuario del barrio decide descargar un archivo gigante, ese ancho de banda físico dejará de estar disponible para sus vecinos. Debido a esto, el rendimiento máximo real está limitado por lo que hacen los demás, obligando a las empresas a hacer "sobreaprovisionamiento" o a aplicar la **"división de nodos" (node splitting)**, que consiste en acercar aún más la fibra a las casas para reducir la cantidad de personas compartiendo el mismo coaxial.

### 2. Uso del Espectro y Multiplexación FDM
El cable coaxial tiene una capacidad de ancho de banda inmensa, y para organizar el tráfico se recurre a la Multiplexación por División de Frecuencia (FDM). La diapositiva con la gráfica del espectro (Fig. 2-46) detalla exactamente cómo se distribuyen estas frecuencias en un sistema típico (valores de Norteamérica):
*   **Canal Ascendente (Upstream / Subida de datos):** Se ubica en la parte más baja del espectro, típicamente en la banda de **5 a 42 MHz**.
*   **Canales de TV y FM:** Ocupan el rango a partir de los 54 MHz hasta los 550 MHz (con la radio FM ocupando el espacio de 88 a 108 MHz).
*   **Canal Descendente (Downstream / Bajada de datos):** Se ubica en las frecuencias más altas, operando desde los **550 MHz hasta los 750 MHz** o más.
*   **Asimetría:** Esta asignación de espectro es asimétrica por naturaleza, otorgando mucho más espectro (y por ende velocidad) para la descarga que para la subida de datos, lo cual se alinea con las preferencias de la mayoría de los usuarios domésticos.

### 3. El Estándar DOCSIS
El funcionamiento lógico de estas redes está dictado por el estándar **DOCSIS (Data Over Cable Service Interface Specification)**, cuyas versiones han escalado masivamente el rendimiento:
*   **Evolución:** Las versiones 1.0 y 1.1 tenían un límite de 38 Mbps de bajada y 9 Mbps de subida. DOCSIS 2.0 triplicó la subida, y DOCSIS 3.0 introdujo la "unión de canales" (channel bonding) para alcanzar cientos de megabits e IPv6.
*   **DOCSIS 3.1 y futuro:** La versión 3.1 introdujo OFDM (Multiplexación por división de frecuencias ortogonales), lo que permite superar **1 Gbps de capacidad de bajada por casa**. Actualizaciones recientes incorporan operaciones *Full Duplex* (simetría en la velocidad de subida/bajada) y Baja Latencia.
*   **Modulación:** Típicamente, el canal de bajada (de 6 a 8 MHz de ancho) se modula utilizando la técnica **QAM-64** (generando unos 27 Mbps netos) o, si el cable está en óptimas condiciones, **QAM-256** (logrando unos 39 Mbps netos por canal).
*   Dado que múltiples usuarios pueden intentar enviar datos a la vez, el tiempo en la frecuencia de subida (que usa modulaciones como QPSK) se divide rígidamente en **mini-ranuras o *minislots*** (típicamente de 8 bytes).

## Redes Satelitales

Un satélite de comunicaciones funciona esencialmente como un gran repetidor de microondas en el cielo. Estos satélites contienen dispositivos llamados **transpondedores**, los cuales escuchan una porción específica del espectro, amplifican la débil señal entrante y la retransmiten de vuelta a la Tierra en una frecuencia diferente para evitar interferencias. A este esquema tradicional se le conoce como satélite de **tubo doblado (bent-pipe)**, aunque las unidades modernas poseen capacidad de procesamiento digital para manipular los flujos de datos y no amplificar el ruido.

Para comprender exhaustivamente estas redes, el material y las diapositivas dividen su análisis en la altura de las órbitas, las bandas de frecuencia utilizadas, la arquitectura de conmutación y su contraste con las redes terrestres.

### 1. Clasificación según la Altitud de la Órbita
La posición de los satélites está estrictamente limitada por los **cinturones de Van Allen**, capas protectoras de partículas altamente cargadas por el campo magnético de la Tierra que destruirían cualquier equipo que vuele en su interior. Las diapositivas presentan una tabla comparativa fundamental que clasifica a los satélites en tres zonas de operación seguras:

**A) Satélites GEO (Órbita Terrestre Geoestacionaria)**
*   **Características:** Orbitan a una inmensa altitud de aproximadamente **35.000 a 35.800 km** sobre el ecuador. A esta altura, el satélite viaja a la misma velocidad de rotación de la Tierra, por lo que parece permanecer completamente inmóvil en el cielo.
*   **Métricas (según las diapositivas):** Solo se necesitan **3 satélites** para brindar cobertura a nivel global. Sin embargo, la gran desventaja es su enorme latencia, introduciendo un retardo típico de **270 milisegundos** de ida y vuelta. 
*   **Gestión del espacio:** Para evitar interferencias, estos satélites deben estar espaciados unos 2 grados entre sí, lo que limita la órbita ecuatorial a un máximo de 180 satélites comerciales activos. Además, requieren ajustes continuos de posición mediante motores, lo que se conoce como *mantenimiento de estación*.
*   **Redes VSAT:** Una aplicación destacada en GEO son los **VSAT (Terminales de Apertura Muy Pequeña)**, sistemas de bajo costo con antenas de 1 metro y solo 1 vatio de potencia de emisión. Las imágenes de las diapositivas muestran que los VSAT no tienen la fuerza para comunicarse directamente entre ellos a través del satélite. En su lugar, utilizan una topología de estrella: la señal viaja al satélite, rebota hacia un **Concentrador (Hub)** terrestre provisto de una enorme antena de alta ganancia, y este Hub retransmite la información de nuevo al satélite hacia el VSAT destino.

**B) Satélites MEO (Órbita Terrestre Media)**
*   **Características:** Se ubican en el espacio libre entre el cinturón de Van Allen inferior y el superior, a una altitud de **10.000 a 20.000 km**. Tardan unas 6 horas en dar una vuelta a la Tierra, por lo que las antenas terrestres deben rastrearlos mientras se mueven por el cielo. 
*   **Métricas:** Requieren unos **10 satélites** para cobertura global y ofrecen una latencia moderada de **35 a 85 ms**.
*   **El Sistema GPS:** Las diapositivas indican que el uso principal de MEO no es la telecomunicación directa, sino los **sistemas de navegación como el GPS**. Un esquema visual detalla su funcionamiento: una constelación de unos 30 satélites a 20.200 km de altura transmite de forma incesante el *almanaque* y las *efemérides* (datos de fecha, hora exacta y ubicación espacial). La imagen de la diapositiva ilustra cómo un receptor en tierra (un barco o un usuario con un dispositivo) capta señales distintas de **al menos tres satélites** simultáneamente para calcular y triangular su latitud y longitud. Para mitigar las interferencias, el GPS utiliza el esquema de multiplexación de espectro ensanchado **DSSS**.

**C) Satélites LEO (Órbita Terrestre Baja)**
*   **Características:** Orbitan por debajo del cinturón inferior de Van Allen, a altitudes que van desde el nivel del suelo hasta los **5.000 km** (típicamente entre 670 y 750 km).
*   **Métricas:** Al estar tan cerca de la Tierra, ofrecen un tiempo de retardo teóricamente minúsculo de **1 a 7 ms** (y en la práctica de 40 a 150 ms), pero el área que cubren es tan pequeña que requieren enjambres de **50 o más satélites** para cubrir el planeta. Son mucho más baratos de lanzar e incluyen tecnologías como los **Cubesats**, minisatélites en forma de cubo de 10 cm que se lanzan con resortes.

### 2. Arquitecturas de Enrutamiento (Ejemplos LEO)
Las diapositivas dedican gráficos específicos para contrastar cómo se enrutan los datos entre satélites de órbita baja para llevar una llamada desde el Polo Norte hasta el Polo Sur:
*   **Retransmisión en el Espacio (El caso Iridium):** Un gráfico de la Tierra muestra cómo la red Iridium opera con 66 satélites dispuestos en **seis collares** orbitales norte-sur. El diagrama detalla que la comunicación viaja **físicamente en el espacio exterior** saltando de un satélite a otro vecino. Esto exige que los propios satélites realicen tareas de conmutación complejas a bordo.
*   **Retransmisión en Tierra (El caso Globalstar):** Otro diagrama muestra un modelo alternativo. Aquí, el satélite simplemente capta la señal del usuario en el Polo Norte y, operando como un "tubo doblado", la baja de inmediato a una gran estación terrestre. El gráfico ilustra que **la conmutación ocurre a nivel del suelo** utilizando la red terrestre de fibra o cables, la cual transporta la señal hasta la estación terrestre más cercana al receptor y la sube al satélite correspondiente. Al delegar la complejidad a tierra y usar grandes antenas receptoras, los teléfonos de los usuarios pueden ser más baratos y de menor potencia.

### 3. Las Bandas de Frecuencia Satelital
La UIT coordina el uso del espectro electromagnético satelital. Las diapositivas presentan una tabla que resume las cinco bandas principales:
1.  **Banda L:** (Bajada a 1.5 GHz / Subida a 1.6 GHz). Provee un escaso ancho de banda de 15 MHz. Su problema principal es la **congestión**.
2.  **Banda S:** (1.9 GHz / 2.2 GHz). Ancho de banda de 70 MHz. También sufre de bajo ancho de banda y saturación.
3.  **Banda C:** (4.0 GHz / 6.0 GHz). Fue la primera en usarse comercialmente. Brinda 500 MHz de ancho de banda. Su problema crítico es la **interferencia terrestre**, ya que comparte frecuencias con enlaces comunes de microondas en la superficie terrestre.
4.  **Banda Ku:** (11 GHz / 14 GHz). Brinda 500 MHz de capacidad y permite espaciar satélites a solo 1 grado. Su debilidad principal es la **lluvia**, ya que el agua absorbe drásticamente la energía de estas microondas más cortas.
5.  **Banda Ka:** (20 GHz / 30 GHz). Entrega un enorme ancho de banda de 3500 MHz. Sus problemas son una severa sensibilidad a la absorción por la **lluvia** y el altísimo **costo del equipo** requerido para procesar señales a esas frecuencias.

### 4. Propiedades y Comparativa con Redes Terrestres (Fibra y Cable)
El material compara de forma exhaustiva los satélites frente a la fibra óptica y el ADSL:
*   **Independencia de la distancia:** En las redes terrestres, el costo aumenta por cada kilómetro de cable tendido. En las redes satelitales, el costo de transmisión de un mensaje es idéntico ya sea que viaje a la casa del vecino o al otro lado del océano.
*   **Medio de Difusión (Broadcasting):** Las redes de fibra son conexiones punto a punto, lo cual garantiza privacidad nativa. Un satélite, en cambio, tiene una "huella" gigante (en GEO, un tercio de la superficie terrestre). No cuesta más dinero transmitir un programa a un millón de receptores que a uno solo. Por esto, es la opción primordial para transmitir televisión digital, radio y flujos de datos financieros masivos. El reverso es la total falta de seguridad: cualquiera con una antena puede captar la señal, haciendo que el **cifrado sea obligatorio** para los servicios bidireccionales.
*   **Nichos de Mercado (Diapositivas y texto):** Aunque la fibra ofrece anchos de banda muy superiores (terabits frente a unos 50 Mbps de los satélites comerciales comunes) y menor latencia, las diapositivas enumeran áreas donde los satélites son imbatibles:
    1.  **Despliegues ultrarrápidos:** En zonas de guerra o desastres naturales (como tsunamis), un enlace satelital con paneles solares puede levantarse y dar comunicación global en menos de 24 horas.
    2.  **Infraestructuras terrestres deficientes:** Llevar fibra a miles de islas (como en el archipiélago de Indonesia) o a través del desierto es financieramente inviable. Las redes LEO como Iridium brindan acceso de voz en cualquier parte del globo, incluso en el Polo Sur.
    3.  **Movilidad absoluta (Internet satelital):** Existe un creciente mercado impulsado por empresas como SpaceX (Starlink) o OneWeb para brindar servicio de banda ancha allí donde no llegan las redes celulares terrestres, siendo el ejemplo más claro proveer **acceso a Internet en pleno vuelo para aviones comerciales** sobre los océanos.