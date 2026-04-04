El protocolo **CSMA** (del inglés *Carrier Sense Multiple Access*, que se traduce como **Acceso Múltiple por Detección de Portadora**) es un conjunto de reglas de comunicación utilizado en las redes de computadoras para controlar cómo los dispositivos acceden a un medio de transmisión compartido (como un cable o el aire en las redes inalámbricas).

La regla fundamental del CSMA se puede resumir en la frase: **"Escuchar antes de hablar"**. Antes de que un dispositivo envíe datos, primero "escucha" el canal de comunicación (detecta la portadora) para verificar si algún otro dispositivo ya está transmitiendo. Si el canal está libre, transmite; si está ocupado, espera.



Sin embargo, incluso si dos dispositivos escuchan que el canal está libre y deciden transmitir exactamente al mismo tiempo, sus señales chocarán y se arruinarán. A esto se le llama **colisión**. Para lidiar con cuándo transmitir y cómo manejar las colisiones, CSMA se clasifica de diferentes maneras.

A continuación, te explico sus clasificaciones principales:

### 1. Clasificación según la "Persistencia" (Cómo esperan)
Esta clasificación define qué hace un dispositivo cuando detecta que el canal está ocupado:

* **CSMA 1-persistente:** El dispositivo escucha el canal. Si está ocupado, se queda escuchando continuamente sin pausas. En el instante exacto en que el canal se libera, transmite inmediatamente (con una probabilidad de 1, es decir, 100%).
    * *Problema:* Si dos o más dispositivos estaban esperando a que el canal se liberara, ambos transmitirán al mismo tiempo en cuanto se libere, garantizando una colisión.
* **CSMA No persistente:** El dispositivo escucha el canal. Si está ocupado, no se queda esperando continuamente. En su lugar, se "va", espera un tiempo aleatorio y vuelve a escuchar el canal más tarde.
    * *Ventaja/Desventaja:* Reduce drásticamente las colisiones, pero la red se vuelve menos eficiente porque el canal puede quedarse vacío por momentos mientras todos los dispositivos están en su tiempo de espera.
* **CSMA p-persistente:** Se aplica en canales divididos en ranuras de tiempo. Si el canal está libre, el dispositivo transmite con una probabilidad *p* (por ejemplo, 10%). Con una probabilidad *q = 1-p* (90%), decide esperar a la siguiente ranura de tiempo y volver a verificar. Combina las ventajas de los dos anteriores para equilibrar colisiones y eficiencia.

---

### 2. Clasificación según el "Manejo de Colisiones" (Protocolos Avanzados)
Como las colisiones son inevitables, CSMA evolucionó en dos grandes protocolos prácticos que se usan en la vida real:



* **CSMA/CD (Collision Detection - Detección de Colisiones):**
    * **¿Dónde se usa?** Es el estándar clásico de las redes cableadas como **Ethernet** (los cables de red que conectas a tu PC).
    * **¿Cómo funciona?** El dispositivo transmite y, *mientras* transmite, sigue escuchando el cable. Si detecta que la señal eléctrica en el cable es más fuerte de lo normal (lo que indica que su mensaje chocó con el de otro), detiene la transmisión inmediatamente, envía una señal de atasco para avisar a los demás y espera un tiempo aleatorio antes de volver a intentarlo.
    * *Analogía:* Dos personas empiezan a hablar al mismo tiempo, se dan cuenta de que se interrumpieron, ambas se callan y esperan un instante antes de volver a hablar.

* **CSMA/CA (Collision Avoidance - Prevención de Colisiones):**
    * **¿Dónde se usa?** Es el estándar de las redes inalámbricas como **Wi-Fi** (IEEE 802.11).
    * **¿Cómo funciona?** En el aire (Wi-Fi), un dispositivo no puede escuchar y transmitir al mismo tiempo fácilmente, por lo que no puede *detectar* colisiones. Por lo tanto, intenta *evitarlas*. Para ello, cuando el canal está libre, el dispositivo espera un pequeño tiempo extra antes de transmitir. Además, utiliza un sistema de acuses de recibo (ACK): si el emisor no recibe una confirmación del receptor, asume que hubo una colisión y retransmite. A veces también usa mensajes previos pidiendo permiso para transmitir (RTS/CTS).
    * *Analogía:* En una sala de conferencias oscura (donde no ves si alguien más está a punto de hablar), levantas la mano o pides la palabra antes de empezar a hablar para asegurarte de que nadie más lo haga al mismo tiempo.