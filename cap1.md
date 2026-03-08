# Fundamentals of Computer Networks and Physical Layer Technologies

- Notebook ID: a66715a2-791e-4c6e-80f5-0a4f8c6e7514
- Exported at: 2026-03-08T19:38:26Z

## PRUEBA, ACA NO EMPIEZA
## [Note] Fundamentos y Arquitectura de las Redes de Computadoras

**1. Usos de las Redes de Computadoras** [1]
*   **Acceso a la información:** Uso del modelo cliente-servidor (peticiones y respuestas) y redes *peer-to-peer* (comunicación entre iguales sin servidores fijos) [3, 4].
*   **Comunicación de persona a persona:** Mensajería instantánea, redes sociales (flujo guiado por relaciones) y sitios colaborativos como wikis [5, 6].
*   **Comercio electrónico:** Modelos de interacción B2C, B2B, G2C, C2C y P2P [5, 7].
*   **Entretenimiento:** Sistemas IPTV, *streaming* de medios inalámbricos y juegos en línea [5, 8].
*   **Internet de las cosas (IoT):** Computación ubicua, uso de sensores inalámbricos, electrodomésticos inteligentes y conectividad de dispositivos cotidianos [8, 9].

**2. Tipos de Redes de Computadoras** [10]
*   **Redes de acceso de banda ancha:** Conexiones de alta velocidad a hogares mediante cable coaxial o fibra óptica [11].
*   **Redes de acceso móviles e inalámbricas:** Dispositivos como smartphones o redes basadas en el estándar 802.11 [11].
*   **Redes de proveedores de contenidos:** Infraestructura para el alojamiento masivo de información [10].
*   **Redes de tránsito:** Redes que conectan el acceso local con los centros de datos [10].
*   **Redes corporativas:** Uso de Redes Privadas Virtuales (VPN) para conectar distintas sedes y compartir recursos organizacionales [12].

**3. Tecnología de Redes (De lo Local a lo Global)** [12]
*   **Redes de Área Personal (PAN):** Comunicación de corto alcance, como el esquema maestro-esclavo de Bluetooth [12, 13].
*   **Redes de Área Local (LAN):** Conexiones dentro de un edificio o campus utilizando Ethernet conmutada o WiFi, incluyendo conceptos como VLANs [12, 14].
*   **Redes Domésticas:** Redes en el hogar [15].
*   **Redes de Área Metropolitana (MAN):** Redes del tamaño de una ciudad, implementadas mediante televisión por cable o WiMAX [12, 15].
*   **Redes de Área Extensa (WAN):** Conectan países o continentes mediante enrutadores y líneas de transmisión (ej. redes ISP) [12, 16].
*   **Inter-redes (Internetworks):** Conexión de redes incompatibles o independientes mediante *gateways* o pasarelas [17, 18].

**4. Ejemplos de Redes** [19, 20]
*   **La Internet:** Su historia desde ARPANET y NSFNET, hasta la arquitectura actual estructurada mediante Proveedores de Servicios (ISPs), datacenters y enrutadores [20-22].
*   **Redes Móviles:** Conceptos de celdas, traspasos (handoff), y la evolución de la tecnología celular desde voz analógica hasta la conmutación de paquetes (tecnologías 3G, 4G, 5G) [18, 19].
*   **Redes Inalámbricas (WiFi):** Implementación del estándar IEEE 802.11 [18, 19].

**5. Protocolos de Red** [2]
*   **Objetivos de diseño:** Confiabilidad (control y detección de errores), asignación de recursos (multiplexado, control de flujo), capacidad de evolución y seguridad [17, 23, 24].
*   **Estratificación (Layering):** Arquitectura de capas donde cada una añade un encabezado (*header*) a la carga útil y se comunica mediante procesos pares (*peers*) e interfaces [24, 25].
*   **Tipos de servicios:** Orientados a la conexión (con negociación de parámetros, análogo a una llamada telefónica) y sin conexión o datagramas (análogo a un telegrama) [26].
*   **Primitivas de servicio:** Comandos fundamentales en la programación de *sockets* (LISTEN, CONNECT, ACCEPT, RECEIVE, SEND, DISCONNECT) [27, 28].

**6. Modelos de Referencia** [28]
*   **Modelo OSI:** Arquitectura teórica de 7 capas creada por la ISO (Física, Enlace de datos, Red, Transporte, Sesión, Presentación, Aplicación) [29, 30].
*   **Modelo TCP/IP:** Arquitectura práctica impulsada por Internet con 4 capas (Enlace, Inter-red, Transporte, Aplicación) [31, 32].
*   **Críticas a los modelos:** El "apocalipsis de los dos elefantes" (mala sincronización para OSI) y las deficiencias arquitectónicas de TCP/IP, que mezcla capas físicas y de enlace [33, 34].
*   **Modelo de 5 capas:** El enfoque híbrido moderno que adopta el curso y el libro [34, 35].

**7. Estandarización de Redes** [34]
*   **Importancia:** Interoperabilidad de sistemas [34].
*   **Entidades:** La UIT en telecomunicaciones, la ISO y el comité IEEE 802 (para estándares como Ethernet y WiFi), y el IAB/IETF (que gestionan los RFCs en Internet) [36-38].

**8. Asuntos Políticos, Legales y Sociales** [39, 40]
*   **Desafíos contemporáneos:** Libertad de expresión, neutralidad de la red, robo de información, privacidad del usuario y el reto de gestionar la desinformación (*fake news*) [39-41].

**9. Unidades de Medida** [40]
*   **Diferenciación de sistemas:** Uso estricto de potencias de 10 para tasas de transmisión (bits por segundo) y potencias de 2 para almacenamiento de datos (Bytes) [40, 42].

---

## [Note] Fundamentos y Arquitectura de las Redes de Computadoras

**Las redes de computadoras** son conjuntos de dispositivos de computación autónomos interconectados, que intercambian información a través de diversos medios de transmisión como cables de cobre, fibra óptica u ondas electromagnéticas [1, 2]. 

El primer capítulo del libro de Tanenbaum y la primera parte de las diapositivas estructuran la introducción a estas redes en cuatro pilares fundamentales:

**1. Usos de las Redes de Computadoras**
Las redes modernas se utilizan en múltiples escenarios de la vida diaria y empresarial:
*   **Acceso a la información:** Se fundamenta principalmente en el **modelo cliente-servidor**, donde un cliente solicita datos (como al usar un navegador web) y un servidor centralizado responde [3, 4]. También destaca el modelo **peer-to-peer (P2P)**, donde no hay servidores fijos y las computadoras operan tanto como clientes y servidores para compartir recursos [5, 6].
*   **Comunicación persona a persona:** Incluye la mensajería instantánea, los correos electrónicos, los sitios wiki de contenido colaborativo y las plataformas de redes sociales [6-8].
*   **Comercio electrónico:** Abarca modelos de transacción categorizados con etiquetas como B2C (negocio a consumidor), B2B (negocio a negocio), G2C (gobierno a consumidor), C2C y P2P [9, 10].
*   **Entretenimiento:** Facilita el consumo de plataformas de IPTV, *media streaming* de audio/video y juegos en línea [11, 12].
*   **Internet de las Cosas (IoT):** Integra la computación ubicua en la vida diaria, conectando a la red elementos como sensores físicos, parquímetros, electrodomésticos y sistemas de seguridad [11, 13, 14].

**2. Tipos de Redes según su Función**
Dependiendo de su propósito y del proveedor, las redes se clasifican en:
*   **Redes de acceso de banda ancha y domésticas:** Proveen Internet de alta velocidad a los hogares usando fibra óptica o cable coaxial [15, 16].
*   **Redes de acceso móviles e inalámbricas:** Incluyen redes 802.11 (WiFi), telefonía celular para *m-commerce*, comunicación NFC y redes de sensores [14, 16, 17].
*   **Redes proveedoras de contenido:** Alojan servicios en la nube a través de masivos **centros de datos** y Redes de Distribución de Contenido (CDN) para acercar la información a los usuarios [18, 19].
*   **Redes de tránsito (Backbones):** Interconectan las redes de acceso con los centros de datos mediante los proveedores de servicios de Internet (ISP) [19, 20].
*   **Redes corporativas:** Operan en campus o empresas para compartir hardware e información, utilizando herramientas como **Redes Privadas Virtuales (VPN)** para enlazar sucursales distantes en una sola red lógica [21-23].

**3. Tecnologías de Redes por su Escala**
Las redes se categorizan según la distancia geográfica que cubren:
*   **PAN (Personal Area Network):** Redes de alcance personal (1 metro aprox.) que conectan periféricos o sensores alrededor de una persona, siendo **Bluetooth** y RFID los ejemplos principales [24-26].
*   **LAN (Local Area Network):** Redes privadas para un edificio o campus (ej. Ethernet conmutado y WiFi 802.11) [27-29].
*   **MAN (Metropolitan Area Network):** Abarcan una ciudad entera, como los sistemas de televisión por cable o la tecnología WiMAX [30-32].
*   **WAN (Wide Area Network):** Se extienden por países o continentes y están formadas por **líneas de transmisión y enrutadores (routers)** operados habitualmente por proveedores de telecomunicaciones [31, 33-35].
*   **Inter-redes (Internetworks):** Ocurren cuando múltiples redes diferentes se conectan a través de dispositivos de conmutación o *gateways*, formando redes masivas como la propia Internet [31, 36, 37].

**4. Ejemplos Históricos y Conceptos Clave de Redes**
*   **La Internet:** Comenzó en la Guerra Fría como **ARPANET** bajo el diseño distribuido de Paul Baran para sobrevivir a ataques nucleares [38-40]. Posteriormente integró NSFNET como columna vertebral (*backbone*) universitaria y evolucionó hacia una jerarquía comercial de ISPs y centros de datos que hoy componen la web [39, 41, 42].
*   **Redes móviles:** Basan su arquitectura en "celdas" espaciales servidas por estaciones base [43, 44]. Cuando un usuario se desplaza fuera del rango de una celda, la red redirige la señal a una nueva base en un proceso llamado **handover** (o traspaso) [43, 45].
*   **Conmutación de Paquetes vs. Circuitos:** Las redes informáticas actuales y la Internet favorecen la **conmutación de paquetes** (redes sin conexión donde los mensajes se enrutan de forma independiente y pueden llegar desordenados), lo cual provee tolerancia a fallos [46-48]. Por el contrario, las compañías telefónicas tradicionales utilizaban la **conmutación de circuitos** (redes orientadas a conexión con una ruta física reservada) [47, 49].

---
## ACA SI EMPIEZA
## [Note] 1. Aplicaciones y Usos de las Redes de Computadoras

Las redes de computadoras se definen como conjuntos de dispositivos de computación autónomos que están interconectados con el fin de intercambiar información a través de medios de transmisión, tales como cables de cobre, fibra óptica u ondas electromagnéticas [1-3]. La convergencia entre la industria de las computadoras y la de las comunicaciones ha reemplazado el concepto de computadoras centrales aisladas por sistemas distribuidos donde múltiples redes prestan diversos servicios [4-6]. 

A nivel universitario, los usos de las redes de computadoras se categorizan de la siguiente manera:

**1. Acceso a la información**
El acceso a la información se estructura fundamentalmente en dos grandes arquitecturas de comunicación:
*   **Modelo Cliente-Servidor:** Es la base operativa de gran parte de Internet, especialmente de la World Wide Web [7-9]. En este modelo, un proceso "cliente" envía una solicitud (petición) explícita a través de la red hacia un "servidor" remoto que aloja la información o la base de datos [8, 10, 11]. El servidor procesa el trabajo y devuelve una respuesta [10, 11]. Esta arquitectura es altamente escalable, permitiendo que un solo servidor gestione simultáneamente a cientos o miles de clientes [7, 8]. Se utiliza a diario mediante navegadores web y smartphones para acceder a sitios informativos, redes sociales y bibliotecas digitales [12-14].
*   **Modelo Peer-to-Peer (P2P) o Comunicación entre iguales:** A diferencia del modelo cliente-servidor, en el ecosistema P2P no existe una división fija entre clientes y servidores [15-17]. Los usuarios que forman el grupo se comunican directamente entre sí [15, 16]. En aplicaciones como BitTorrent, no hay una base de datos centralizada; cada nodo mantiene su propia base de datos local y un índice de otros miembros de la red, facilitando una búsqueda iterativa de contenidos que escala masivamente [18-20]. Este modelo se popularizó inicialmente con Napster para compartir música y hoy se usa para intercambio de archivos, chats y distribución de software [21-24].

**2. Comunicación de persona a persona**
Esta categoría representa la evolución del teléfono tradicional hacia las plataformas digitales del siglo XXI [25].
*   **Mensajería y Redes Sociales:** Incluye desde la mensajería instantánea hasta servicios de difusión uno-a-muchos (como Twitter) [26]. En las redes sociales, el flujo de la información está estructurado y dirigido estrictamente por el grafo de relaciones que los usuarios declaran entre ellos [26].
*   **Colaboración remota:** Permite la creación de sitios colaborativos (como las Wikis) [26], además de videoconferencias, escritorios compartidos para la edición simultánea de documentos y herramientas incipientes como la telemedicina para la coordinación a distancia [27].

**3. Comercio electrónico**
Las redes permiten operaciones financieras, compras en línea y subastas de manera sumamente eficiente, minimizando la necesidad de grandes inventarios mediante pedidos electrónicos just-in-time [26, 28, 29]. Estos flujos de transacción se catalogan mediante acrónimos específicos:
*   **B2C (Business-to-consumer):** Transacciones directas entre empresas y consumidores, como pedir libros o realizar compras en línea [30, 31].
*   **B2B (Business-to-business):** Comercio entre empresas, por ejemplo, un fabricante automotriz solicitando componentes a sus proveedores de forma automatizada [30, 31].
*   **G2C (Government-to-consumer):** Servicios estatales digitales, como la distribución electrónica de formularios de impuestos [30, 31].
*   **C2C (Consumer-to-consumer):** Interacción directa entre consumidores, como las subastas de productos de segunda mano en plataformas como eBay [30, 31].
*   **P2P (Peer-to-peer):** Intercambio directo de recursos, como compartir música o archivos [30, 31].

**4. Entretenimiento**
La distribución digital ha comenzado a reemplazar y rivalizar con los métodos tradicionales de radio, televisión y cine [30, 32].
*   **IPTV (Televisión IP):** Los programas de televisión ya no dependen de las transmisiones tradicionales por cable o radiofrecuencia de transmisión abierta, sino que se transmiten basándose completamente en la pila de protocolos IP [30, 32, 33].
*   **Streaming de medios:** Permite el consumo en tiempo real de radio por Internet, música, películas en alta definición y series a través de aplicaciones conectadas a menudo a redes inalámbricas [30, 32, 33]. 
*   **Juegos en línea:** Entornos de simulación interactiva multijugador dependientes de baja latencia y alta conectividad [33].

**5. Internet de las cosas (IoT)**
Este concepto engloba la "computación ubicua" (Ubiquitous computing), que integra tecnología de red en el entorno físico de la vida diaria [33].
*   **Dispositivos embebidos:** Los elementos tradicionales como electrodomésticos, cerraduras, televisores, termostatos y alarmas antirrobo ahora poseen capacidades computacionales y de interconexión IP [34-36].
*   **Sensores inalámbricos:** Nodos que reúnen información acerca de parámetros físicos, implementados desde parquímetros hasta monitores de consumo de agua o cámaras digitales de alta gama que envían fotografías a servidores de edición en tiempo real [37, 38].
*   **Redes Power-line:** Para soportar esta densidad de dispositivos sin saturar las frecuencias de radio, se utiliza el cableado eléctrico del hogar para difundir señales de red y datos de manera simultánea con la electricidad, operando ambas en bandas de frecuencia distintas [39-42].

---

## [Note] 2. Tipos y Arquitecturas de las Redes de Computadoras

**2. Tipos de Redes de Computadoras**

*   **Redes de Uso Doméstico y Acceso de Banda Ancha**
    *   Proporcionan conectividad a computadoras remotas para que los usuarios puedan acceder a música, fotos, videos, información y comprar productos [1, 2].
    *   **Ley de Metcalfe**: Formulada por Bob Metcalfe (inventor de Ethernet), esta ley postula que el valor de una red es proporcional al cuadrado del número de usuarios ($N^2$), ya que este valor representa aproximadamente el número de conexiones distintas que se pueden realizar [1-3]. Esto explica matemáticamente por qué la enorme popularidad de Internet se debe directamente a su tamaño [1, 3].
    *   Para el acceso, utilizan tecnologías de banda ancha basadas en cables coaxiales y fibra óptica, las cuales son capaces de entregar tasas de transferencia de gigabits por segundo a hogares individuales [2].

*   **Redes de Acceso Móviles e Inalámbricas**
    *   Surgieron de la necesidad de proveer conectividad en entornos donde el cableado es imposible, como automóviles, barcos o aviones [4].
    *   Se implementan principalmente a través de redes inalámbricas basadas en el estándar IEEE 802.11 (Wi-Fi) y redes celulares operadas por compañías telefónicas [2, 4].
    *   Los *smartphones* (teléfonos inteligentes) combinan características de telefonía tradicional y computación móvil [2, 5]. Estos dispositivos suelen integrar sistemas GPS o triangular posiciones mediante puntos Wi-Fi para determinar su ubicación exacta [6, 7].
    *   **Geoetiquetado (*Geo-tagging*)**: Es la función que permite registrar la ubicación del usuario para añadir anotaciones geográficas a fotos y videos con el lugar exacto en el que se crearon [2, 6, 7]. Esto también habilita servicios dependientes de la ubicación, como mapas móviles, búsqueda de restaurantes cercanos o pronósticos del clima local [6, 7].
    *   **M-commerce y NFC**: Las redes móviles impulsan el comercio móvil (*m-commerce*). Además, la tecnología NFC (*Near Field Communication*) permite que el dispositivo actúe como una tarjeta inteligente RFID, interactuando con lectores cercanos para realizar pagos [8].
    *   **Redes de sensores**: Utilizan nodos para recolectar y transmitir información sobre estados del mundo físico [8, 9]. Pueden estar integradas en objetos cotidianos (como sistemas de diagnóstico en autos para reportar velocidad, baches y consumo de combustible) o ser dispositivos independientes [9, 10]. 
    *   *Ejemplos de sensores:* Microcomputadoras de un milímetro cúbico para el rastreo de migración de cebras, aves e insectos, o parquímetros inteligentes que verifican la presencia de autos, aceptan tarjetas de crédito y alertan si el tiempo ha expirado [8, 11, 12].

*   **Redes Proveedoras de Contenido y de Centros de Datos**
    *   Soportan los servicios de Internet que operan desde "la nube", almacenando la información en granjas de servidores [13-15].
    *   Se encargan de mover cantidades masivas de datos tanto entre los propios servidores internos del *datacenter* como hacia el resto de Internet [14]. Sus principales desafíos técnicos son maximizar el *throughput* (ancho de banda transversal) y optimizar el uso de energía [13-15].
    *   **CDN (*Content Delivery Network* / Red de Entrega de Contenidos)**: Es un conjunto masivo de servidores replicados y distribuidos geográficamente [14, 16, 17]. Su propósito es situar el contenido lo más cerca posible del usuario para mejorar la velocidad. El sistema decide qué réplica usar evaluando la distancia al cliente, la carga de los servidores y la congestión de la red [18, 19].

*   **Redes de Tránsito (Redes Troncales o *Backbones*)**
    *   Transportan el tráfico entre el proveedor de contenido y la red del ISP (*Internet Service Provider*) de los clientes cuando estos no tienen una conexión directa [14, 18].
    *   Históricamente, dependían de acuerdos comerciales donde ambas partes pagaban por el uso del enlace [14, 20, 21].
    *   Actualmente, la jerarquía de Internet se ha "aplanado". El gran tamaño de los ISP de acceso y de los proveedores de contenido ha provocado que prefieran interconectarse directamente entre sí, utilizando las redes de tránsito casi exclusivamente como rutas de respaldo [20, 21].

*   **Redes Corporativas (De Empresa)**
    *   Su meta es compartir recursos físicos y lógicos (información) mediante el modelo cliente-servidor, donde equipos potentes alojan las bases de datos y equipos de escritorio (clientes) acceden a ellas [22-24].
    *   **SAN (*Storage Area Networks*)**: Mencionadas en el material como redes dedicadas específicamente a interconectar recursos de almacenamiento [23].
    *   **VPN (*Virtual Private Networks* / Redes Privadas Virtuales)**: Permiten conectar lógicamente redes individuales ubicadas en distintos sitios geográficos a través de Internet, operando como una sola red y acabando con la "tiranía de la geografía" [22, 23, 25].
    *   Estas redes facilitan la compartición de monitores (escritorios remotos), la telefonía IP (*Voice over IP*) y la comunicación B2B para negocios electrónicos, permitiendo hacer pedidos automáticamente y reducir inventarios [23, 26, 27].

---

## [Note] 3. Tecnologias de Redes: de lo Local a Global

### Evolución de la Tecnología de Redes
La arquitectura de redes ha evolucionado desde los Mainframes centralizados en 1971, pasando por la era de la Computadora Personal (1980), el modelo Cliente-Servidor en LAN (1990), los sistemas basados en Web en WAN (2000), hasta llegar a la Nube apoyada en enormes datacenters (2011 en adelante) [1].

Las tecnologías actuales se clasifican por su alcance físico y paradigma de conexión:

### 1. Redes de Área Personal (PAN)
Permiten la comunicación entre dispositivos cercanos a una persona (alcance de aprox. 1 metro) [2].
*   **Funcionamiento:** Estándares como Bluetooth operan bajo un paradigma maestro-esclavo, donde un nodo principal asigna direcciones y frecuencias a los periféricos para compartir datos a bajas tasas de bits [2, 3].

### 2. Redes de Área Local (LAN)
Conectan dispositivos dentro de un edificio o campus y pertenecen a una sola organización [4].
*   **Ethernet Conmutada:** Utiliza topologías punto a punto conectadas a un conmutador (*switch*) central. Los switches aíslan los dominios de colisión por puerto, eliminando la necesidad de compartir el medio como en la antigua Ethernet [5, 6]. Utilizan algoritmos de árbol de expansión (spanning tree) para evitar bucles [7].
*   **VLAN (Redes LAN Virtuales):** Permiten dividir lógicamente una red física mediante software, asignando "colores" o etiquetas a los puertos para aislar el tráfico (incluyendo el de difusión) por departamentos o funciones [8, 9].
*   **Redes Domésticas:** Son un subtipo de LAN diseñadas para conectar computadoras, televisores y electrodomésticos (Internet de las Cosas) de forma plug-and-play [10, 11]. 

### 3. Redes de Área Metropolitana (MAN)
Abarcan toda una ciudad [11].
*   **Ejemplos:** Las redes de televisión por cable, las cuales inyectan señales bidireccionales de Internet junto con la televisión para distribuirlas desde un amplificador de cabecera a los hogares [12, 13]. Otro ejemplo es WiMAX (IEEE 802.16) [13].

### 4. Redes de Área Amplia (WAN)
Cubren áreas geográficas extensas (países o continentes) y comúnmente son operadas por Proveedores de Servicios (ISP) [14].
*   **Componentes estructurales:** Se componen fundamentalmente de dos elementos: **líneas de transmisión** (cables de cobre, fibra óptica o radioenlaces que mueven los bits) y **elementos de conmutación** o enrutadores (equipos que deciden por qué línea saliente enviar los datos) [14-16].
*   **Redes Privadas Virtuales (VPN):** En lugar de alquilar costosas líneas dedicadas, las organizaciones conectan sus distintas sedes mediante enlaces virtuales que corren sobre Internet [17]. Las VPN unen estas redes geográficamente separadas en una sola red lógica, eliminando la "tiranía de la geografía" [18]. Su ventaja es la flexibilidad y el ahorro, aunque ceden el control del rendimiento de los recursos subyacentes físicos [17].
*   **Paradigmas de conmutación en la red central:**
    *   **Conmutación de Circuitos:** Heredada de las compañías telefónicas. Es orientada a la conexión. Requiere establecer una ruta física o virtual dedicada (y reservar ancho de banda, búferes y CPU) antes de poder transmitir los datos [19-21]. Esto garantiza la entrega en el mismo orden y facilita la Calidad de Servicio (QoS), pero es vulnerable a fallas de enrutadores, ocasiona bloqueos al inicio ("señal de ocupado") y desperdicia recursos si la conexión está inactiva [19, 22-24].
    *   **Conmutación de Paquetes:** Heredada de la comunidad de Internet. Es un servicio sin conexión (datagramas) [25, 26]. Los mensajes se dividen y se enrutan de manera independiente mediante el modelo *store-and-forward* (almacenamiento y reenvío) [27, 28]. No reserva ancho de banda, por lo que es altamente eficiente y tolerante a fallos (los paquetes pueden rodear un nodo caído) [24, 29]. Sin embargo, los paquetes pueden llegar en desorden, dificulta la implementación de QoS y puede sufrir de congestión o retardo si muchos paquetes llegan al mismo tiempo [19, 25, 28, 30].

### 5. Interredes (Internetworks)
Son colecciones de redes independientes o incompatibles conectadas entre sí [31, 32].
*   Para unirlas se emplean **pasarelas (gateways)** o enrutadores que operan en la capa de red, traduciendo formatos de hardware y software para permitir el paso de información (por ejemplo, entre una red inalámbrica y una alámbrica) [33].

---

## [Note] 4. Ejemplos de Redes: Evolución de Internet y Redes Inalámbricasnn

### 1. Línea de Tiempo de la Internet
*   **Fines de 1950s:** El Departamento de Defensa de EE. UU. busca crear una red de mando y control capaz de sobrevivir a un ataque nuclear [1].
*   **Octubre 1957:** La Unión Soviética lanza el Sputnik, motivando la creación de ARPA en EE. UU [2].
*   **1967:** Larry Roberts orienta a ARPA hacia las redes; Wesley Clark propone usar una subred de conmutación de paquetes con enrutadores independientes [1].
*   **Diciembre 1969:** ARPANET se lanza como red experimental con cuatro nodos iniciales (UCLA, UCSB, SRI y la Universidad de Utah) interconectados por líneas de 56 kbps [1, 2].
*   **Diciembre 1972:** AlohaNet se conecta a ARPANET, naciendo la primera red interconectada [2].
*   **Mayo 1974:** Vint Cerf y Bob Kahn inventan el protocolo TCP/IP [1, 3].
*   **1981:** La NSF financia la creación de CSNET [1].
*   **1 de enero de 1983:** ARPA adopta oficialmente TCP/IP como su protocolo estándar y se inventa el DNS [1, 2].
*   **1985 - 1995:** NSFNET actúa como red troncal abierta a universidades [1, 4].
*   **1989:** Tim Berners-Lee inventa la World Wide Web en el CERN [1, 2].
*   **1994 - 1995:** NSFNET transiciona hacia redes troncales comerciales operadas por proveedores [1].

### 2. Conmutación de Paquetes vs. Conmutación de Circuitos
Existen dos métodos fundamentales para enrutar la información:
*   **Conmutación de Circuitos (Modelo Telefónico):** Orientado a la conexión [5, 6]. Se establece una ruta física dedicada de extremo a extremo antes de enviar datos [6]. **Ventajas:** Garantiza la Calidad de Servicio (QoS) reservando ancho de banda y ciclos de CPU, y los paquetes llegan en orden [7, 8]. **Desventajas:** La configuración inicial toma tiempo, el ancho de banda se desperdicia si no hay tráfico, y si un enrutador falla, la llamada se cae por completo [7, 9-11].
*   **Conmutación de Paquetes (Modelo de Internet):** Diseño sin conexión (datagramas) basado en el almacenamiento y reenvío (store-and-forward) [5, 12]. Cada paquete se enruta independientemente [5, 12]. **Ventajas:** Altamente tolerante a fallos (rodea enrutadores caídos) y no desperdicia ancho de banda [10, 11]. **Desventajas:** Los paquetes pueden llegar desordenados y el tráfico excesivo causa retrasos en las colas (congestión), dificultando la QoS [5, 8, 9].

### 3. La Internet y su Arquitectura
La Internet es un conjunto de redes interconectadas que funciona como una subred de datagramas sin conexión [13, 14]. 
*   **Evolución:** En sus inicios, ARPANET utilizó minicomputadoras llamadas Procesadores de Mensajes de Interfaz (IMP) conectadas a los hosts [15]. El diseño dividía estrictamente los protocolos de subred y de host [15].
*   **Arquitectura Jerárquica vs. Plana:** Convencionalmente, Internet era jerárquica: operadores troncales nacionales (Nivel 1), proveedores regionales (ISP) y redes locales [16]. Sin embargo, en la última década, esta jerarquía se ha "aplanado" [16]. Los proveedores de contenido "hipergigantes" (Google, Netflix) y las Redes de Distribución de Contenido (CDN, como Akamai) ahora se interconectan directamente (peering) con los ISP locales en Puntos de Intercambio de Internet (IXP), entregando datos mucho más cerca del usuario final y saltándose las redes de tránsito tradicionales [16-18].
*   **Acceso de Última Milla:** Los usuarios se conectan mediante diversas tecnologías: módems de cable usando infraestructura coaxial (redes HFC con estándar DOCSIS y CMTS), DSL (cobre con multiplexores DSLAM), redes ópticas (FTTH) o redes móviles [19, 20].

### 4. Redes Móviles y Traspaso (Handoff)
Las redes móviles organizan su cobertura en "celdas", cada una con una estación base conectada a un Centro de Conmutación Móvil (MSC) [21-23]. 
Cuando un dispositivo se mueve de una celda a otra, ocurre el **traspaso o handoff**:
1.  **Traspaso Duro (Hard Handoff):** El móvil se desconecta de la estación antigua antes de conectarse a la nueva. Usado en diseños FDM antiguos, puede causar cortes de servicio [24, 25].
2.  **Traspaso Suave (Soft Handoff):** Posible en redes CDMA (3G). El dispositivo se conecta a la nueva estación antes de soltar la antigua, evitando interrupciones [24, 25].
3.  **MAHO (Mobile Assisted HandOff):** Usado en redes GSM. El móvil usa sus "ranuras de tiempo" inactivas para medir la señal de celdas vecinas y avisa a la red para coordinar el cambio [26].

**Evolución:**
*   **1G (AMPS):** Voz analógica [27].
*   **2G (GSM):** Voz digital, introduce SMS. Usa multiplexación FDM y TDM [27, 28].
*   **3G (UMTS):** Integra voz y datos digitales usando tecnología de espectro ensanchado (CDMA) [29, 30].
*   **4G (LTE):** Abandona la conmutación de circuitos. Usa un núcleo 100% de conmutación de paquetes llamado EPC (Evolved Packet Core) para la Voz sobre IP [21, 31]. Los nodos de radio se llaman eNodeB e interactúan con entidades como el MME y los gateways S-GW/P-GW [32-34].
*   **5G:** Despliegues más densos (picoceldas), ondas milimétricas, MIMO masivo (múltiples antenas) y fragmentación de red (network slicing) para alcanzar hasta 10 Gbps [35-38].

### 5. Redes Inalámbricas (WiFi - IEEE 802.11)
El estándar 802.11 opera en bandas sin licencia (2.4 GHz y 5 GHz) [39, 40]. Funciona en modo *Infraestructura* (con un Punto de Acceso o AP) o en modo *Ad Hoc* (conexión directa entre equipos) [41-43].
*   **Capa MAC y CSMA/CA:** Las radios WiFi son semidúplex, por lo que no pueden escuchar colisiones mientras transmiten (no pueden usar CSMA/CD) [39, 44]. En su lugar, usan CSMA/CA (Evitación de Colisiones) [39]. Las estaciones esperan un tiempo aleatorio tras detectar el canal inactivo; si el paquete llega, el receptor envía un acuse de recibo (ACK) [39, 45]. La falta de ACK implica colisión [45].
*   **Problemas Inalámbricos:** 
    *   *Terminal Oculta:* Dos nodos no se ven entre sí, pero transmiten al mismo AP al mismo tiempo, causando una colisión [39, 46].
    *   *Terminal Expuesta:* Un nodo escucha una transmisión cercana y asume erróneamente que no puede transmitir hacia un destino diferente [39, 47].
*   **Soluciones en 802.11:**
    *   *Detección Virtual (NAV):* Cada trama incluye un temporizador (Vector de Asignación de Red) que avisa a las estaciones vecinas cuánto tiempo estará ocupado el canal [39, 48].
    *   *Protocolo RTS/CTS:* El emisor manda Request To Send, el receptor responde Clear To Send, silenciando a los vecinos. Es opcional y rara vez se usa por su enorme sobrecarga [39, 46, 47].
    *   *Fragmentación:* Divide tramas largas en fragmentos pequeños con ACK individuales para mitigar altas tasas de error por interferencias [39, 49].
*   **Evolución Física:** Pasó de salto de frecuencias (802.11 original) a espectro ensanchado (802.11b), luego a modulación OFDM (802.11a/g) y finalmente a la tecnología de múltiples antenas MIMO/OFDMA (802.11n, ac, ax) para escalar de 11 Mbps hasta teóricos 11 Gbps [50-53].

***

---

## [Note] Génesis y Evolución de la Red Global

Aquí tienes el flujo cronológico exacto de cómo la tecnología de red evolucionó desde un experimento militar hasta la Internet actual:

*   **Finales de los 50 y 60s (El concepto):** En la Guerra Fría, el Pentágono necesitaba una red de control que sobreviviera a ataques nucleares [1]. Paul Baran propuso la **conmutación de paquetes**, pero AT&T lo rechazó por considerarlo imposible de construir [2]. La agencia gubernamental ARPA tomó el control de la idea [3].
*   **1969 (El primer hardware - ARPANET):** Arranca la primera red con solo 4 nodos universitarios [4]. El hardware central no eran enrutadores modernos, sino **IMPs** (minicomputadoras conectadas por líneas telefónicas de 56 kbps) [5].
*   **1974 (El nacimiento de TCP/IP):** Al intentar conectar ARPANET con redes de radio satelital en camiones, descubrieron que los protocolos originales no servían para cruzar redes distintas [6, 7]. Vint Cerf y Bob Kahn inventaron el **TCP/IP** específicamente para interconectar cualquier tipo de red sin problemas [7, 8].
*   **Años 80 (La apertura - NSFNET):** La Fundación Nacional de la Ciencia (NSF) creó su propia red troncal basada en TCP/IP (**NSFNET**) para conectar universidades que no tenían contratos militares [9, 10]. Esto masificó la red en el ámbito académico.
*   **Años 90 (Comercialización y la Web):** El gobierno se retiró y cedió la infraestructura a operadores comerciales de telecomunicaciones [11, 12]. A principios de la década nació la **World Wide Web (WWW)**, lo que hizo que el tamaño y uso de la red explotaran a nivel mundial [13].
*   **Actualidad (La Nube y CDNs):** La arquitectura jerárquica clásica se ha "aplanado" [14]. Hoy en día, la red está dominada por el contenido multimedia y las **granjas de servidores**; gigantes como Google o Netflix se conectan directamente con los proveedores de Internet locales para entregar datos de forma masiva y rápida [14, 15].

---

## [Note] Génesis de ARPANET y la Evolución del Internet Moderno

**1. El miedo nuclear y el rechazo de AT&T**
Todo comenzó en la Guerra Fría. El Departamento de Defensa de EE. UU. (DoD) necesitaba una red de mando y control que sobreviviera a un ataque nuclear [1]. La red telefónica de la época era vulnerable porque dependía de unas pocas oficinas centrales [1]. Paul Baran propuso un diseño tolerante a fallos usando **conmutación de paquetes**, pero cuando el Pentágono le pidió a AT&T (el monopolio telefónico) que construyera un prototipo, AT&T rechazó la idea rotundamente diciendo que era imposible de construir [2].

**2. El Hardware: Los IMPs sin discos duros**
Años después, la agencia ARPA revivió la idea y contrató a la empresa BBN para construir la subred [3, 4]. BBN construyó equipos llamados **IMP** (Procesadores de Mensajes de Interfaz), que actuaban como los enrutadores de la época [4]. Un dato técnico importante: los IMPs no tenían discos duros porque las piezas mecánicas móviles se consideraban demasiado propensas a fallar [4]. Estaban conectados mediante líneas telefónicas alquiladas de 56 kbps, lo más rápido de la época [4].

**3. El caos del software (Estudiantes al rescate)**
BBN diseñó la subred (los IMPs), pero consideró que su trabajo terminaba ahí, dejando a las computadoras de los usuarios (*hosts*) sin software para hablar entre sí [5]. Para resolverlo, ARPA reunió a un grupo de estudiantes de posgrado en Utah esperando que un experto les diera el diseño a programar [6]. Para su sorpresa, no había ningún experto ni diseño previo; los estudiantes tuvieron que inventar los protocolos de comunicación desde cero por sí mismos [6].

**4. El experimento del camión y el nacimiento de TCP/IP**
El mayor desafío llegó cuando ARPA intentó unir ARPANET con redes inalámbricas. En una demostración, usaron un camión en movimiento en California que enviaba datos por radio, los cuales pasaban a ARPANET y luego por satélite hasta Londres [7]. El experimento demostró que los protocolos originales de ARPANET no servían para cruzar redes de tecnologías distintas [8]. Este fracaso directo llevó a los investigadores Vint Cerf y Bob Kahn a inventar un protocolo universal para interconectar cualquier red: el **TCP/IP** [8].

---

## [Note] 5. Protocolos de Red

### **1. Definición y Análisis de Protocolos**
Un protocolo de red es un conjunto de reglas y normas que deben cumplir los dispositivos para establecer una comunicación de datos en una red [1, 2]. De manera específica, un protocolo es un acuerdo que rige el formato y el significado de los paquetes o mensajes que se intercambian las entidades homólogas (procesos iguales o *peers*) dentro de una sola capa [3, 4]. 

Para analizar correctamente un protocolo, las diapositivas establecen que se deben considerar tres cuestiones fundamentales [5, 6]:
*   **Sintaxis:** Define el formato estructural, incluyendo las longitudes de los encabezados, los campos del mensaje y las reglas de relleno [5, 6].
*   **Semántica:** Determina el significado específico de cada campo o encabezado dentro del mensaje [5, 6].
*   **Temporización:** Involucra el uso de temporizadores (*timers*) para sincronizar y gestionar los tiempos de la comunicación [5, 6].

### **2. Objetivos de Diseño**
Las redes y sus protocolos se diseñan persiguiendo cuatro metas fundamentales para resolver problemas transversales [7, 8]:
*   **Confiabilidad:** Consiste en lograr que la red opere correctamente a pesar de estar construida con componentes físicos y de software que no son del todo confiables y pueden perder datos [5, 9]. Esto abarca el **control de errores** para detectar o corregir fallos mediante campos con bits de redundancia, y el **enrutamiento** automático para encontrar rutas operativas cuando existan fallas en la red [5, 6].
*   **Asignación de recursos:** Aborda cómo la red escala al aumentar su tamaño [10, 11]. Utiliza el **multiplexado estadístico**, compartiendo el ancho de banda dinámicamente según las estadísticas de demanda a corto plazo [10, 12]. Incluye el **control de flujo** (para evitar que un emisor rápido sature a un receptor lento) y el **control de congestión** (cuando demasiados hosts intentan enviar demasiado tráfico y sobrecargan la red) [10, 12]. También gestiona la **calidad de servicio (QoS)**, conciliando demandas de aplicaciones de alto rendimiento con aplicaciones que requieren entregas en tiempo real [13, 14].
*   **Capacidad de evolución:** Asegura que nuevos diseños se puedan adaptar a la red existente [10, 13]. Emplea el **direccionamiento** para identificar emisores y receptores, e ***internetworking*** para solucionar incompatibilidades (como diferentes tamaños máximos de paquetes) entre redes distintas mediante fragmentación y reensamblado [10, 15].
*   **Seguridad:** Define los mecanismos para defender la red. Utiliza la confidencialidad para proteger contra intrusos (*eavesdropping*), mecanismos de autenticación para evitar suplantación de identidad, y controles de integridad para evitar cambios clandestinos en los mensajes [14, 16, 17].

### **3. Estratificación (Layering) y Aspectos de Diseño de Capas**
Para reducir la complejidad, la arquitectura de red se organiza en una pila de capas [18, 19].
*   Cada capa actúa como una máquina virtual que ofrece servicios específicos a la capa inmediatamente superior, ocultándole los detalles técnicos de su estado interno y algoritmos [3, 18].
*   La comunicación se logra mediante **procesos pares (*peers*)** que residen en la misma capa pero en máquinas distintas [20, 21]. El libro ilustra esto con la arquitectura "filósofo-traductor-secretaria", donde los pares se comunican lógicamente en su nivel, pero la información desciende físicamente por las capas [22-24].
*   **Encabezados (*Headers*) y Terminadores (*Trailers*):** Al descender por la pila, cada capa añade su propio encabezado con información de control al mensaje original (y en la capa de enlace se suele añadir un terminador); al llegar al destino, cada capa remueve y procesa su respectivo encabezado [25-27].

Los diseñadores deben resolver varios **aspectos operativos** en estas capas [25, 28-30]:
*   **Direccionamiento:** Usar campos de "dirección origen" y "dirección destino" para identificar los extremos [25, 29].
*   **Control de errores:** Utilizar campos con bits de "redundancia" [25, 29].
*   **Numeración:** Secuenciar los mensajes usando campos de "número de secuencia" para su ordenamiento [28, 30].
*   **Control de flujo:** Aplicar técnicas como la "ventana deslizante" [28, 30].
*   **Segmentación:** Dividir y reensamblar mensajes mediante campos de "más fragmentos" o "último fragmento" [28, 30].
*   **Multiplexado:** Compartir una misma conexión o medio para múltiples conversaciones [28, 30].
*   **Enrutamiento:** Dirigir paquetes a través de rutas en una red compleja [28, 30].

### **4. La Distinción Crítica: Servicio vs. Protocolo**
Es fundamental no confundir estos dos términos, ya que están completamente desacoplados [31, 32]:
*   **Servicio:** Es un conjunto de primitivas u operaciones que una capa proporciona a la capa superior a través de una interfaz [33, 34]. Define *qué* operaciones puede realizar, pero no *cómo* las implementa [33, 34].
*   **Protocolo:** Es el conjunto de reglas que rige el formato y significado de los mensajes que intercambian las entidades iguales (pares) dentro de una misma capa para implementar ese servicio [31, 35].

### **5. Tipos de Servicios y Métodos de Conmutación**
Las capas pueden ofrecer dos grandes categorías de servicio a las capas superiores:
*   **Orientados a la conexión:** Modelados según el sistema telefónico [36, 37]. Requieren tres pasos: establecer la conexión, transferir los datos y liberar la conexión [36, 37]. Actúan como un tubo donde los bits llegan en el mismo orden en que fueron enviados [37, 38]. Antes de la transmisión, los participantes realizan una negociación previa para determinar parámetros (tamaño máximo, calidad de servicio) y reservan recursos, formando lo que se conoce como un circuito [36, 39].
*   **Sin conexión (Datagramas):** Modelados según el sistema postal o telegráfico [36, 40]. No hay conexión previa; cada mensaje (datagrama) lleva incrustada la dirección completa y se enruta de forma independiente [36, 40]. Como no hay ruta fija, pueden llegar en desorden [40, 41]. 

En las redes sin conexión surgen dos técnicas de conmutación en los nodos [36, 40]:
1.  ***Store-and-forward* (Almacenamiento y reenvío):** El enrutador recibe el paquete completo, lo almacena, verifica errores y luego lo transmite [40, 41].
2.  ***Cut-through switching* (Conmutación al vuelo):** La transmisión de un mensaje hacia el siguiente nodo comienza antes de que se haya recibido por completo [36, 40].

### **6. Servicios Confiables y No Confiables**
Los servicios también se dividen por cómo manejan la pérdida de datos [42-44]:
*   **Servicios Confiables:** Análogos a una carta certificada [42, 45]. El receptor emite un mensaje de confirmación de recepción (**ACK**) o de confirmación negativa (**NAK**) [42, 46]. Requieren la numeración de mensajes y el uso de temporizadores (*timers*) [42, 47]. Tienen dos variantes: *flujos de bytes confiables* (sin límites de mensaje, ideal para descargas de películas) y *secuencias de mensajes confiables* (ideal para enviar páginas a una impresora) [46, 48]. 
*   **Servicios No Confiables:** Los mensajes no se confirman [46, 49]. Se utilizan donde la velocidad es prioritaria o la capa inferior ya es inherentemente propensa a errores, dejando la recuperación a capas superiores [43, 45]. Ejemplos incluyen el envío de correo electrónico basura (*datagramas no confiables*) o voz sobre IP (*conexión no confiable*) [43, 46].
*   Existen también servicios híbridos como el *datagrama confirmado* (ej. mensajes de texto SMS) y el *servicio de solicitud-respuesta* (modelo cliente-servidor) [45, 46, 50].

### **7. Primitivas de Servicio**
La interfaz de servicio se especifica formalmente a través de un conjunto de primitivas, a menudo implementadas como llamadas al sistema operativo (como la clásica interfaz de *sockets* de Berkeley) [51, 52]. Las operaciones fundamentales para un servicio orientado a la conexión son [52, 53]:
*   **LISTEN:** Bloquea el proceso del servidor en espera de una conexión entrante [52, 53].
*   **CONNECT:** El cliente establece de forma activa una conexión enviando un paquete de solicitud [52, 53].
*   **ACCEPT:** El servidor acepta formalmente la conexión entrante [52, 54].
*   **RECEIVE:** Bloquea la ejecución en espera de que llegue un mensaje con datos [52, 55].
*   **SEND:** Envía información a través de la conexión establecida [52, 55].
*   **DISCONNECT:** Solicita la liberación de la conexión [52, 55]. Esta desconexión puede ser *asimétrica* (cualquiera puede romper la conexión completa de una vez) o *simétrica* (cada dirección se cierra por separado y de forma independiente) [56].

---

## [Note] 6. Modelos de Referencia: Arquitecturas OSI y TCP/IP en Redes

### 6. Modelos de Referencia

El diseño de protocolos estructurados por capas es una de las abstracciones más importantes en las redes de computadoras, permitiendo dividir la inmanejable tarea de diseñar una red completa en problemas más pequeños y manejables [1, 2]. A continuación, se detallan los dos modelos predominantes, sus críticas y el modelo híbrido adoptado en el entorno académico y práctico [1].

#### El Modelo de Referencia OSI (Interconexión de Sistemas Abiertos)
Propuesto por la Organización Internacional de Normalización (ISO) en 1983 y revisado en 1995, es una arquitectura teórica de referencia [3-5]. No es una arquitectura de red en sí misma, ya que no especifica los protocolos exactos a utilizar, sino que define qué debe hacer cada capa [3, 6, 7]. Sus principios de diseño dictan que debe crearse una capa cuando se necesite una abstracción diferente, cada capa debe tener una función bien definida, el flujo de información a través de las interfaces debe minimizarse y la cantidad de capas debe ser manejable [7-9]. La mayor aportación de OSI es la clara distinción conceptual entre servicios, interfaces y protocolos [10-12]. 

OSI se compone de 7 capas, con sus respectivas unidades de información y funciones:
*   **1. Capa Física:** Se encarga de la transmisión de bits puros (unidad de información: **Bit**) a través de un canal de comunicación [8, 9, 13, 14]. Define especificaciones mecánicas y eléctricas, niveles de voltaje, conectores, funciones de pines, distancias y modulación/codificación de datos [6, 13, 15, 16].
*   **2. Capa de Enlace de Datos:** Transforma un medio de comunicación físico en una línea libre de errores para el dispositivo siguiente, logrando una entrega salto a salto [6, 13, 15, 16]. Fragmenta el flujo en **Tramas** (frames), realiza control de flujo, control de errores de transmisión e incluye direcciones físicas [8, 9, 13, 17, 18].
*   **3. Capa de Red:** Controla las operaciones de la subred y la interconexión de redes [6, 15, 17, 19]. Realiza el enrutamiento dinámico o estático de los **Paquetes** desde el origen hasta el destino final utilizando direccionamiento lógico [8, 9, 15, 17, 19].
*   **4. Capa de Transporte:** Es la primera capa de extremo a extremo [20]. Acepta datos de capas superiores, los divide en **Segmentos** (o TPDU) y asegura la entrega confiable de mensajes de proceso a proceso y la recuperación de errores [6, 8, 9, 14, 15]. Aísla a los hosts de los detalles técnicos de la red y maneja el multiplexado de conexiones y el ordenamiento secuencial [17, 19, 21, 22].
*   **5. Capa de Sesión:** Permite establecer, gestionar y terminar sesiones entre usuarios de distintas máquinas [6, 15, 23]. Gestiona el control de diálogo (tokens, full/half duplex), la sincronización y la definición de puntos de recuperación ante fallas mediante **SPDU** [8, 9, 21, 22]. Un ejemplo de protocolo es RPC [21, 22].
*   **6. Capa de Presentación:** Se ocupa de la sintaxis y semántica de la información transmitida a través de **PPDU** [8, 9, 21, 22]. Realiza funciones de traducción, codificación de caracteres (ej. ASCII), algoritmos de cifrado/descifrado y compresión de datos (ej. ZIP) [6, 15, 21, 22].
*   **7. Capa de Aplicación:** Interactúa directamente con la aplicación del usuario para permitir el acceso a los recursos de la red mediante **APDU** (ej. HTTP) [6, 8, 9, 14, 15, 24].

#### El Modelo TCP/IP
Este modelo tiene un origen completamente práctico, no teórico, y surgió como la arquitectura de referencia principal para la interconexión en Internet entre 1974 y 1988 a partir de ARPANET [25-28]. A diferencia de OSI, TCP/IP no incluye las capas de Presentación ni de Sesión [29-31]. Se compone de 4 capas:
*   **1. Capa de Enlace:** Define lo que los enlaces (como líneas seriales o Ethernet) deben hacer para satisfacer las necesidades de la capa superior [25, 26, 32, 33]. En la práctica es más una interfaz entre hosts y enlaces que una capa tradicional [32-34].
*   **2. Capa de Inter-red (Internet):** Es el eje que mantiene unida toda la arquitectura [35-37]. Implementa un servicio sin conexión que permite a los hosts inyectar paquetes que viajan de forma independiente hasta su destino, pudiendo llegar en desorden [25, 26, 35, 36]. Aquí operan los protocolos **IP**, **ICMP** e **IGMP**; su desafío principal es el enrutamiento y la congestión [25, 26, 38-41].
*   **3. Capa de Transporte:** Diseñada para permitir que las entidades pares mantengan una conversación de extremo a extremo [42, 43]. Aquí operan el **TCP** (confiable y orientado a la conexión) el **UDP** (no confiable y sin conexión), y el **SCTP** [39, 40, 42, 43].
*   **4. Capa de Aplicación:** Contiene los protocolos de alto nivel que utilizan las aplicaciones, tales como **HTTP, DNS, SMTP, FTP, TELNET** y **SNMP** [39, 40, 43-45].

#### Relación entre Capas, Protocolos y Direcciones
Un aspecto clave en la arquitectura es cómo cada capa maneja tipos específicos de protocolos y direccionamiento para comunicarse correctamente con su par [39, 40]:
*   **Capa de Aplicación:** Los procesos utilizan **direcciones específicas** [39, 40].
*   **Capa de Transporte:** Los protocolos como SCTP, TCP y UDP utilizan **direcciones de puerto** [39, 40].
*   **Capa de Red:** El protocolo IP y otros protocolos relacionados gestionan las **direcciones lógicas** (como las direcciones IPv4 o IPv6) [39, 40].
*   **Capa de Enlace de Datos y Física:** Las redes físicas subyacentes se comunican mediante **direcciones físicas** (ej. direcciones MAC), apoyándose en protocolos como ARP y RARP para la traducción de direcciones [39, 40].

#### Críticas a los Modelos
Ambos modelos tienen fortalezas y debilidades históricas y técnicas [46, 47]:
*   **Crítica a OSI:** Su principal fortaleza es que es un modelo de referencia excelente con conceptos muy claros (servicios, interfaces y protocolos) [11, 46-48]. Su gran falla fue el "apocalipsis de los dos elefantes" (una mala sincronización histórica donde la estandarización llegó demasiado tarde, cuando TCP/IP ya estaba establecido) [49]. Además, los protocolos y la adopción se estancaron por su extrema complejidad y por motivaciones políticas [46, 47].
*   **Crítica a TCP/IP:** Su mayor ventaja son sus protocolos inmensamente exitosos, probados en la práctica y en constante evolución [46-48]. Su debilidad radica en que el modelo conceptual es muy pobre, derivado directamente de los protocolos [46, 47]. No distingue claramente los conceptos de interfaz, servicio y protocolo, y falla al no separar la capa de Enlace de la capa Física, siendo que la capa de enlace en este modelo funciona realmente más como una interfaz que como una capa [33, 46, 47].

#### El Modelo Híbrido de 5 Capas
Debido a las deficiencias de ambos modelos de manera aislada, la academia moderna y la bibliografía utilizan un enfoque híbrido de **5 capas** (Física, Enlace, Red, Transporte y Aplicación) [46, 47, 49-51]. Este modelo retiene el gran valor teórico del modelo OSI para comprender las arquitecturas de red y la separación de funciones, pero se centra exclusivamente en estudiar los protocolos exitosos y prácticos derivados del ecosistema TCP/IP y de las tecnologías modernas de enlace [49, 52, 53].

---

## [Note] 7, 8, 9. Fundamentos de Redes: Estándares, Ética y Unidades de Medida

Aquí tienes el resumen universitario detallado y exhaustivo de los puntos 7, 8 y 9 de tu esquema, integrando la información técnica del libro de Tanenbaum y los conceptos de tus diapositivas:

### 7. Estandarización
La estandarización es un proceso fundamental en el diseño de redes. De acuerdo con las diapositivas, **los estándares definen qué se necesita para la interoperabilidad** [1, 2]. Sin coordinación, existiría un caos de hardware y software propietarios, lo que impediría la comunicación [3]. Los estándares no solo permiten que sistemas de distintos fabricantes se comuniquen, sino que aumentan el tamaño del mercado, lo que conduce a la producción en masa, economías de escala y una reducción de precios [3].

*   **Organizaciones de Estandarización (Quién es quién):** El mundo de los estándares se divide en varias organizaciones clave [4, 5]. En las telecomunicaciones destaca la **UIT (Unión Internacional de Telecomunicaciones)** [6]. Para los estándares internacionales existe la **ISO**, y en la industria eléctrica y electrónica el **IEEE** (responsable de los estándares LAN como el 802.3 para Ethernet y el 802.11 para WiFi) [6-8]. Los estándares de Internet son gestionados por la **IETF (Internet Engineering Task Force)**, que pública sus normativas en documentos técnicos llamados **RFCs (Request For Comments)** [6, 9].
*   **El "Apocalipsis de los dos elefantes" (Teoría de David Clark):** Este concepto ilustra la importancia de la *sincronización* al crear un estándar [10]. Se representa gráficamente en una curva de "Actividad" versus "Tiempo". El gráfico muestra dos grandes picos (los "elefantes"): el primero representa el auge de la **Investigación** (descubrimiento, discusiones, publicaciones) y el segundo representa la **Inversión de miles de millones de dólares** por parte de las corporaciones [11]. El estándar exitoso debe escribirse exactamente en el "valle" entre ambos elefantes [11, 12]. Si se escribe muy pronto, la tecnología no se comprende bien; si se escribe muy tarde, las empresas ya han invertido en soluciones propietarias incompatibles [12].

### 8. Asuntos políticos, legales y sociales
Las redes de computadoras, al igual que la imprenta en su momento, permiten distribuir y ver contenido de formas sin precedentes, pero esto viene acompañado de complejos problemas éticos y legales [13].
*   **Discurso en línea y Desinformación:** El auge de la desinformación y las "noticias falsas" impone grandes retos técnicos a los operadores de red y plataformas sobre cómo definir, detectar y mitigar estos flujos de datos sin violar la libertad de expresión [14, 15].
*   **Neutralidad de la red:** Las políticas de red enfrentan debates técnicos y legales sobre la priorización del tráfico y las disputas de interconexión (peering) [16].
*   **Privacidad, Seguridad y Censura:** La información personal y el rastreo de usuarios levantan preocupaciones globales [17]. Además, los usuarios y disidentes políticos en regímenes restrictivos buscan formas de eludir la censura. 
*   **Esteganografía (Ejemplo técnico de las imágenes):** El libro detalla cómo se usa la esteganografía para evadir la censura ocultando información en contenido aparentemente inocuo. El texto presenta un análisis de la imagen de "Tres cebras y un árbol de acacia" [18, 19]. En esta imagen a color de 1024x768 píxeles, se utilizan los bits de menor orden (1 bit) de los canales rojo, verde y azul (RGB) de cada píxel como canal secreto [20]. En este espacio (294,912 bytes ocultos), los autores comprimieron mediante algoritmos el texto íntegro de cinco obras de Shakespeare (reduciendo 734,891 bytes a unos 274 KB) y luego lo encriptaron usando el algoritmo simétrico **IDEA** antes de incrustarlo [21, 22]. Para el ojo humano (e incluso para la vigilancia automatizada sin la clave), la diferencia de color de 24 bits a 21 bits es imperceptible [21, 22].
*   **Derechos de autor (Copyright):** El intercambio de archivos P2P plantea dilemas técnicos frente a las leyes de propiedad intelectual y los avisos de eliminación del DMCA [23-25].

### 9. Unidades de medida
En ciencias computacionales y redes, es estrictamente necesario diferenciar los sistemas de medición para evitar ambigüedades en cálculos técnicos [26, 27].
*   **Tasas de transmisión (Velocidad de red / Ancho de banda):** Se utilizan potencias base 10 (Hertz o bits por segundo) [26, 28]. 
    *   **kbps:** $10^3$ bits/seg.
    *   **Mbps:** $10^6$ bits/seg.
    *   **Gbps:** $10^9$ bits/seg.
    *   **Tbps:** $10^{12}$ bits/seg [15, 27, 29].
*   **Almacenamiento (Memoria / Tamaños de archivo):** Se utilizan estrictamente potencias de base 2 [26].
    *   **KB:** $2^{10}$ bytes (1,024 bytes).
    *   **MB:** $2^{20}$ bytes (1,048,576 bytes).
    *   **GB:** $2^{30}$ bytes.
    *   **TB:** $2^{40}$ bytes [15, 27, 29, 30].
*   **Otras medidas temporales comunes en protocolos:** Milisegundos ($10^{-3}$ seg), microsegundos ($\mu sec$, $10^{-6}$ seg), nanosegundos ($10^{-9}$ seg) y picosegundos ($10^{-12}$ seg) [15].

***

---
