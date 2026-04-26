# Redes Telefonicas Publicas Conmutadas (RTPC)
La estructura general de la Red Telefónica Pública Conmutada (RTPC o PSTN por sus siglas en inglés) está diseñada históricamente para interconectar usuarios y transmitir la voz, aunque posteriormente se adaptó para el tráfico de datos. 

Según los materiales, sus principales componentes se dividen en tres partes fundamentales :

**1. El Bucle Local (Local Loop):**
* Es el enlace de cableado físico (tradicionalmente un par trenzado de cobre analógico) que conecta el equipo del usuario directamente con las instalaciones de la compañía telefónica.
* Comúnmente se le conoce como la "última milla", aunque su distancia real puede ser de varios kilómetros.
* En este nivel es donde operaban los **módems telefónicos** tradicionales, encargados de disfrazar los datos digitales de los ordenadores convirtiéndolos en ondas analógicas para que pudieran viajar por estos cables de voz.

**2. Las Oficinas de Conmutación (Switching Offices / End Offices):**
* Son las centrales telefónicas donde terminan los bucles locales provenientes de las casas de los abonados.
* Su función principal es enrutar y "mover" las llamadas hacia el camino correcto para llegar a su destino.
* En estas oficinas se encuentran los **códecs**, dispositivos críticos que toman la señal analógica que llega por el bucle local y la digitalizan (usando modulación PCM), preparándola para viajar a alta velocidad por el resto de la red.

**3. Las Troncales (Trunks):**
* Son los enlaces digitales de alta velocidad y capacidad que interconectan las distintas oficinas de conmutación entre sí.
* Estas líneas agrupan (multiplexan) cientos o miles de llamadas digitalizadas simultáneamente.
* Utilizan tecnologías de transporte jerárquico que mencionamos anteriormente, como los portadores de cobre **T1/E1** o las redes masivas de fibra óptica **SONET/SDH**.
  
## Local Loop
En la arquitectura de la Red Telefónica Pública Conmutada (RTPC), se utilizan tanto transmisiones digitales como analógicas. Para poder cruzar entre estos dos mundos, se utilizan módems y códecs, los cuales realizan funciones de conversión exactamente opuestas:

### Modems y Codecs
* **Módem (Modulador-Demodulador):**
    * **Conversión:** De **Digital a Analógico** (y viceversa en el receptor).
    * **Para qué sirve:** Toma los datos digitales puros (ceros y unos) generados por un equipo informático y los convierte (modula) en una onda analógica. 
    * **Uso en la red:** Históricamente, los módems telefónicos se usaban para enviar datos digitales de ordenadores a través del "bucle local" de cobre, el cual era un canal que la red telefónica proporcionaba exclusivamente para señales de voz analógicas.

* **Códec (Codificador-Decodificador):**
    * **Conversión:** De **Analógico a Digital** (y viceversa en el receptor).
    * **Para qué sirve:** Toma una señal analógica natural y continua (como la voz humana) y la digitaliza tomando múltiples "muestras" por segundo (mediante técnicas como PCM y PAM) para convertirla en un flujo de bits. En el extremo de destino, el códec recrea la señal analógica original a partir de esas muestras cuantizadas para que el oído humano pueda escucharla.
    * **Uso en la red:** Se utiliza en las centrales telefónicas para digitalizar tu voz analógica, permitiendo que esta viaje empaquetada como datos por las troncales digitales de alta velocidad (como la portadora T1 o E1).

**Resumen rápido de la diferencia:**
| Dispositivo | Entrada (Origen)               | Salida (Para el cable)      | Propósito principal                                    |
| :---------- | :----------------------------- | :-------------------------- | :----------------------------------------------------- |
| **Módem**   | Datos de computadora (Digital) | Ondas continuas (Analógico) | "Disfrazar" datos para que viajen por líneas de voz.   |
| **Códec**   | Voz humana (Analógico)         | Ceros y unos (Digital)      | "Disfrazar" la voz para que viaje por líneas de datos. |

### PCM (Modulación por Impulsos Codificados): El bloque de construcción
* **Concepto:** PCM es la técnica (realizada por el códec en la central telefónica) que convierte tu voz analógica en datos digitales puros (ceros y unos).
* **El estándar de los 64 kbps:** PCM toma la onda de voz, la "muestrea" 8,000 veces cada segundo, y a cada muestra le asigna un valor de 8 bits. 
* **El resultado:** 8,000 muestras × 8 bits = **64 kbps**. Este flujo de 64 kbps se conoce como canal **DS0**. Todo el sistema mundial de telecomunicaciones está construido matemáticamente alrededor de este pequeño canal base de 64 kbps.

### DSL (Línea de Abonado Digital)
* **Concepto general:** DSL (o xDSL como término genérico para todas sus variantes) es una tecnología diseñada para enviar datos digitales desde el cliente hasta la oficina central de la compañía telefónica (y de ahí a Internet) reutilizando el "bucle local" de cobre existente.
* **Equipamiento:** En el extremo del usuario se instala un módem DSL, mientras que en el lado del proveedor (la central) se utiliza un dispositivo multiplexor llamado DSLAM (*DSL Access Multiplexer*). 

**DMT (Modulación Multitono Discreta)**
* **¿Qué es?** DMT es simplemente el nombre comercial y técnico que recibe la técnica de multiplexación OFDM (Multiplexación por División de Frecuencia Ortogonal) cuando se aplica específicamente al contexto de las redes ADSL.
* **División del Espectro:** Para superar las limitaciones del cable, DMT toma el espectro disponible de 1,1 MHz del bucle local y lo divide matemáticamente en 256 canales independientes, cada uno con un ancho de 4.312,5 Hz (a menudo redondeado a 4 kHz). 
* **Asignación de Canales:**
    * El **Canal 0** se reserva exclusivamente para el servicio telefónico tradicional de voz (POTS).
    * Los **Canales 1 al 5** se dejan vacíos deliberadamente para actuar como banda de guarda y evitar que los datos interfieran con la voz.
    * De los 250 canales restantes, uno se usa para el control de subida, otro para el control de bajada, y el resto queda disponible para el tráfico de datos del usuario.

**ADSL (DSL Asimétrico)**
* **La variante dominante:** ADSL se convirtió en el servicio de línea de abonado digital más popular.
* **¿Por qué es "Asimétrico"?** Aunque técnicamente es posible asignar los canales de datos mitad para subida y mitad para bajada, los proveedores asignan típicamente entre el 80% y el 90% del ancho de banda al canal descendente (de bajada). Esta decisión, que le da la "A" al nombre ADSL, se debe a que la mayoría de los usuarios domésticos descargan mucha más información de la que envían. Una configuración muy común es dedicar 32 canales para la subida y dejar el resto para la bajada.

**FTTx (Fiber to the x - Fibra hasta la "x")** es un término general utilizado en telecomunicaciones para describir cualquier arquitectura de red de banda ancha que utilice **fibra óptica** para reemplazar total o parcialmente el tradicional cableado de cobre en el "bucle local" (la última milla que llega al usuario).

La letra **"x"** representa el punto físico exacto donde termina la fibra óptica y donde la señal óptica se convierte en una señal eléctrica para recorrer el último tramo a través de cables de cobre o coaxiales. 

* **FTTN (Fiber to the Node - Fibra hasta el Nodo):** La fibra óptica llega hasta un nodo central del vecindario (a varios kilómetros de distancia del usuario). Desde allí, el resto del viaje hasta las casas se hace usando la red de cobre existente.
* **FTTC (Fiber to the Curb / Cabinet - Fibra hasta la Acera o Armario):** La fibra llega mucho más cerca, típicamente a un armario de telecomunicaciones en la calle del usuario (a unos 300 metros o menos). El último tramo corto hacia la casa sigue siendo de cobre.
* **FTTB (Fiber to the Building - Fibra hasta el Edificio):** La fibra llega hasta el cuarto de equipos en el sótano de un edificio de apartamentos o complejo de oficinas. Luego, se distribuye a cada apartamento individual mediante cables Ethernet (LAN) o cobre tradicional.
* **FTTH / FTTP (Fiber to the Home / Premises - Fibra hasta el Hogar / Local):** Es la conexión definitiva. La fibra óptica entra físicamente dentro de la casa o negocio del abonado. No hay cable de cobre en el medio. Requiere que el usuario tenga un equipo terminal óptico (ONT/ONU) en su casa para convertir los pulsos de luz en conexión Ethernet o Wi-Fi.

Mientras que el ADSL intentaba exprimir al máximo los viejos cables telefónicos, FTTx representa la actualización física de la red. Al acercar la fibra óptica cada vez más al usuario (especialmente con FTTH), se eliminan los cuellos de botella de velocidad, la atenuación por distancia y la interferencia electromagnética, permitiendo velocidades de Gigabit simétricas (misma velocidad de subida y de bajada).

## Troncales

### T1 y E1: Las Troncales de Cobre (TDM Síncrono)
Una vez que tienes miles de llamadas convertidas en flujos PCM de 64 kbps, necesitas empaquetarlas juntas para enviarlas por el cable de cobre de la troncal. Para esto se crearon los sistemas T-Carrier y E-Carrier .
* **T1 (El estándar de EE. UU. y Japón):** * Toma **24** de esos canales PCM (24 canales de voz).
    * Los empaqueta por división de tiempo (TDM) junto con un bit extra de control.
    * Su velocidad fija en la troncal es de **1.544 Mbps**.
* **E1 (El estándar Europeo y resto del mundo):**
    * Toma **32** canales en total: 30 dedicados a flujos PCM (voz) y 2 canales enteros dedicados exclusivamente a señalización y sincronización.
    * Es más ordenado y eficiente que el T1. Su velocidad fija es de **2.048 Mbps**.

### SONET (Red Óptica Síncrona): El "Troncal de Troncales"
Cuando el tráfico de Internet explotó y las troncales de cobre T1 y E1 ya no daban abasto, la industria tuvo que saltar a la fibra óptica .
* **El Concepto:** SONET (y su equivalente europeo SDH) no reemplaza a los bloques anteriores; los absorbe. Un equipo SONET es capaz de tomar múltiples líneas T1, T3 o E1 completas y meterlas dentro de contenedores matemáticos gigantes (llamados SPE).
* **Sincronización:** Su gran ventaja es que utiliza relojes atómicos extremadamente precisos. Esto permite que la red sepa exactamente dónde está cada bit sin necesidad de desarmar toda la trama.
* **Velocidad:** En lugar de hablar de un par de Megabits como en T1/E1, las troncales SONET emiten la información en forma de luz (portadoras ópticas o niveles OC). Comienzan en **51.84 Mbps** (OC-1) y escalan rápidamente a **2.5 Gbps** (OC-48), **10 Gbps** (OC-192) y velocidades de **40 Gbps** (OC-768).



## Conmutacion de circuitos y de paquetes

De acuerdo con las fuentes proporcionadas, a continuación se presenta un cuadro comparativo con las características de la conmutación de circuitos y la conmutación de paquetes:

| Característica                | Conmutación de Circuitos                                                                                                           | Conmutación de Paquetes                                                                                 |
| :---------------------------- | :--------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------ |
| **Origen**                    | Proviene de las compañías telefónicas.                                                                                             | Proviene de la comunidad de Internet.                                                                   |
| **Tipo de conexión**          | Se trata de redes orientadas a la conexión.                                                                                        | Son redes sin conexión o redes de datagramas.                                                           |
| **Método de enrutamiento**    | Cada mensaje posee un "número de circuito virtual" que los dispositivos intermedios (enrutadores) utilizan para realizar el ruteo. | Cada mensaje es ruteado de manera independiente utilizando los campos de dirección de origen y destino. |
| **Orden de llegada**          | Los mensajes llegan a su destino exactamente en el mismo orden en el que salieron de su origen.                                    | Los mensajes pueden llegar al destino en un orden distinto al que salieron originalmente.               |
| **Calidad de Servicio (QoS)** | Es fácil de implementar.                                                                                                           | Resulta difícil de implementar.                                                                         |
| **Recuperación ante fallas**  | Presenta una difícil recuperación ante fallas de enlace.                                                                           | Tiene una fácil recuperación ante fallas de enlace.                                                     |

