# **Protocolo CSMA/CA (Carrier Sense, Multiple Access / Collision Avoidance)**

## **Los Problemas Fundamentales de la Topología Inalámbrica**

A diferencia de las redes cableadas, las redes inalámbricas no pueden detectar colisiones simultáneas mediante señales eléctricas.
### **El Problema del Terminal Oculto (*Hidden Terminal*):** 
*   **Características:** Ocurre cuando dos emisores (por ejemplo, A y C) están fuera del rango de escucha mutuo, pero ambos quieren transmitir a un receptor central (B) que está al alcance de ambos. 
*   **Desventaja:** Si A transmite, C no escucha la señal, concluye erróneamente que el canal está libre y decide transmitir. Las señales de A y C colisionan y se destruyen en la antena de B, desperdiciando ancho de banda.
*   SOLUCION: CTS.

### **El Problema del Terminal Expuesto (*Exposed Terminal*):** 
*   **Características:** Ocurre cuando una estación (B) está transmitiendo a (A), y una tercera estación (C), dentro del rango de (B), quiere transmitir a un cuarto nodo (D).
*   **Desventaja:** Al escuchar la transmisión de B, la estación C asume falsamente que el medio está ocupado y decide no enviar su trama a D. Sin embargo, su transmisión no interferiría con la recepción de A, lo que resulta en un desperdicio injustificado de oportunidades de transmisión.
*   SOLUCION: RTS/CTS.

## **La Solución MAC: Protocolo CSMA/CA**

Para superar estas barreras, el estándar **IEEE 802.11** implementa el protocolo **CSMA/CA (*Carrier Sense, Multiple Access / Collision Avoidance* - Acceso Múltiple por Detección de Portadora con Prevención de Colisiones)**. 

Este protocolo se clasifica rígidamente en dos modos de operación:

#### **A. Modo PCF (*Point Coordination Function* - Función de Coordinación Puntual)**
*   **Características:** Es un método centralizado donde el **AP (*Access Point* - Punto de Acceso)** otorga el canal basado en prioridades mediante sondeos (*polling*) a las estaciones.
*   **Desventaja:** No forma parte del estándar obligatorio de interoperabilidad de la organización *Wi-Fi Alliance*, por lo que su uso es extremadamente raro en la práctica comercial.

#### **B. Modo DCF (*Distributed Coordination Function* - Función de Coordinación Distribuida)**
*   **Características:** Es el mecanismo de acceso múltiple predeterminado y obligatorio. A diferencia de Ethernet, se asume la pérdida física de detección de colisiones durante la transmisión.
*   **Trama ACK (*Acknowledgment* - Acuse de Recibo):** Como no se pueden detectar choques en el aire, se vuelve imperativo el uso de una trama explícita de ACK. Si el emisor no recibe este ACK, deduce que hubo una colisión y debe retransmitir.
*   **Retroceso Exponencial Binario (*Binary Exponential Backoff*):** 
    *   **Fórmula / Rango:** El intervalo de espera aleatorio se encuentra en el rango $[1, CW]$, donde **CW** es la *Contention Window* (Ventana de Contención). 
    *   **Parámetros:** Se inicia con $CW_{min} = 15$ slots y llega hasta $CW_{max} = 1023$ slots. Un slot de tiempo dura típicamente entre $9$ y $20 \mu s$.
    *   **Regla Matemática:** El límite superior de CW se multiplica por 2 tras cada intento fallido (colisión).

### **Clasificación Exhaustiva de Detección del Canal en DCF**

Para que el CSMA/CA evite colisiones eficazmente, las estaciones evalúan el canal de dos maneras concurrentes:

*   **Detección Física:** El circuito de radio directamente escucha la energía en la frecuencia para verificar si alguien más está transmitiendo.
*   **Detección Virtual (El temporizador NAV):** 
    *   **Características:** Se basa en el **NAV (*Network Allocation Vector* - Vector de Asignación de Red)**, un timer interno a cada estación. Las estaciones leen el campo "Duración" (*duration*, medido en microsegundos) de los encabezados de las tramas 802.11. 
    *   **Protocolo Opcional MACA (Mecanismo RTS/CTS):** Para solucionar a las terminales ocultas, el emisor envía primero una pequeña trama **RTS (*Request To Send* - Petición para Enviar)** de 30 bytes detallando la duración del envío. Si el receptor está libre, responde con un **CTS (*Clear To Send* - Listo para Enviar)**. 
    *   **Ventajas de la Detección Virtual:** Cualquier estación que escuche el RTS o el CTS actualiza inmediatamente su NAV interno y se impone un estado de silencio. Esto evita terminales ocultos y expuestos, y ahorra enormemente el consumo de batería de los dispositivos.

### **Clasificación de Tiempos de Separación: Los Intervalos IFS (*Inter Frame Space*)**

Para asegurar prioridades estrictas en el canal, los diagramas de tiempo dividen las esperas en diferentes intervalos (IFS):

*   **SIFS (*Short InterFrame Spacing*):** Es el más corto (típicamente $10 \mu s$). Se usa para respuestas inmediatas de la misma conversación (como CTS, ACKs, o fragmentos consecutivos) para evitar que cualquier otra estación robe el canal.
*   **PIFS (*PCF InterFrame Spacing*):** (Típicamente $30 \mu s$). Lo utilizan los AP para tomar control absoluto del medio en modo PCF.
*   **DIFS (*DCF InterFrame Spacing*):** (Típicamente $50 \mu s$). Es el tiempo de espera predeterminado. Cualquier estación común debe encontrar el canal libre durante un tiempo DIFS antes de poder siquiera empezar a descontar su tiempo de *backoff* aleatorio para enviar tramas de datos regulares.
*   **EIFS (Extended InterFrame Spacing):** Se usa únicamente por una estación que acaba de recibir una trama mala/corrupta para informar del problema o esperar sin interferir.
*   **AIFS (*Arbitration InterFrame Space* - IEEE 802.11e):** Sustituye al DIFS cuando se aplican reglas de Calidad de Servicio (QoS). *AIFS1* es muy corto para dar prioridad al tráfico de voz en tiempo real, mientras que *AIFS4* es más largo, relegando las descargas de fondo al último lugar.

### **Funcionamiento IFS + Backoff (Algoritmo Exponencial Binario)**
La regla matemática del estándar es simple: El algoritmo de retroceso (Backoff) SOLO se aplica si tu tarjeta de red tuvo que esperar (diferir) porque el canal estaba ocupado cuando intentó hablar por primera vez. Si tuviste la suerte de encontrar el canal libre desde el segundo cero, te ganas el derecho a usar la "vía rápida".

El estándar IEEE 802.11 es muy inteligente y distingue entre dos escenarios completamente diferentes cuando a tu tarjeta de red le llega un paquete listo para enviar.

#### **Escenario A: El Aula Vacía**
Imagina que entras a un aula y no hay nadie hablando. Hay un silencio total. Tienes una pregunta para el profesor.

"Medium idle? -> Yes": Escuchas el aire y confirmas que hay silencio absoluto.

"Wait IFS": Por cortesía, esperas el tiempo DIFS (50 μs) solo para asegurarte de que nadie estaba tomando un respiro rápido entre frases.

"Still idle? -> Yes": El aula sigue en absoluto silencio.

"Transmit Frame": ¡Hablas directamente! ¿Por qué no hay Backoff aquí? Porque si la red está tranquila y tú eres el único que quiere hablar en ese preciso instante, obligarte a tirar un dado y esperar tiempos aleatorios adicionales sería un desperdicio absoluto de tiempo (aumentaría la latencia de la red sin ninguna razón). No hay nadie con quien desempatar, ¡estás solo!

#### **Escenario B: El "Choque de Trenes" evitado**
Ahora imagina que entras al aula, pero alguien más ya está hablando. Tienes una pregunta urgente.

"Medium idle? -> No": Escuchas el aire y detectas energía. El canal está ocupado.

"Wait until current transmission ends": Te callas pacientemente hasta que esa persona termine de hablar.

El peligro oculto: El problema es que, mientras esa persona hablaba, otros tres alumnos también llegaron al aula con preguntas. Ahora hay cuatro personas esperando en silencio a que termine la transmisión actual.

"Wait IFS": La persona termina. Todos esperan los 50 μs reglamentarios de cortesía.

"Still idle? -> Yes": Aquí es donde la historia cambia. El estándar sabe que este silencio post-transmisión es "peligroso" porque probablemente haya varios acumulados esperando.

"Exponential backoff": ¡Obligatorio sacar los dados! Todos los que estaban esperando tiran su dado. El que saque el número menor, habla. Los demás congelan sus relojes.

### **Confiabilidad**
Para mejorar la confiabilidad se puede disminuir la tasa de bits (rate adaptation) o fragmentar las tramas.

Siguiente [Tramas 802.11 (tramas80211.md)](tramas80211.md)
