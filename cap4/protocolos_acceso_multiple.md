# **Protocolos de Acceso Múltiple**

Su objetivo principal dentro de la subcapa MAC es **decidir quién es el siguiente en transmitir** cuando varias computadoras o estaciones comparten un mismo medio (como un cable Ethernet clásico o el aire en las redes inalámbricas). 

A diferencia de la **asignación estática** (como FDM o TDM, donde el canal se divide en porciones fijas para cada usuario y se desperdicia si alguien no tiene nada que transmitir), la **asignación dinámica** otorga el canal a un usuario únicamente cuando realmente lo necesita. Esto hace que la red sea muchísimo más eficiente para manejar el tráfico impredecible o en "ráfagas" típico de las computadoras.

Todos los protocolos que mencionas son diferentes "estrategias" para realizar esta asignación dinámica, y se dividen en las tres grandes familias:

1. **Protocolos de contención (Competencia pura):** Los dispositivos intentan transmitir cuando lo necesitan. Si dos hablan a la vez, ocurre una colisión, se detienen y lo intentan de nuevo tras un tiempo aleatorio. Son excelentes cuando hay poco tráfico en la red.
   * *Aquí entran:* **ALOHA** y **CSMA/CD**.
2. **Protocolos libres de colisiones (Turnos estrictos):** Utilizan mecanismos para reservar el canal o ceder el turno de antemano, garantizando matemáticamente que nadie hable al mismo tiempo y eliminando los choques por completo. Son excelentes cuando la red está saturada y todos quieren hablar.
   * *Aquí entran:* **Mapeo de bits (Bitmap)**, **Token Ring** y **Cuenta atrás binaria (Binary Countdown)**.
3. **Protocolos de contención limitada (Híbridos):** Combinan lo mejor de ambos mundos. Permiten la competencia cuando hay poco tráfico (para no hacer esperar a los dispositivos), pero aplican reglas de turnos o agrupan a las estaciones para evitar el caos cuando la red está muy congestionada.
   * *Aquí entra:* El **Árbol adaptativo (Adaptive Tree-Walk)**.


Las reglas generales del juego siempre se dividen en estos tres momentos. 

1. **Período de Inactividad (El canal está ocioso):**
Es el momento de silencio en la red. Absolutamente nadie tiene datos listos para enviar en ese instante, o bien, el medio está libre pero los dispositivos están esperando su turno para hablar. **En forma general:** Durante este tiempo, el canal no se está aprovechando para enviar información útil. Es un recurso que temporalmente se está desperdiciando, pero es un estado natural y necesario (como el silencio entre las palabras en una conversación) para que alguien pueda empezar a hablar sin interrumpir a otro.

2. **Período de Contención (El conflicto y la resolución):**
Es la fase de "competencia". Ocurre cuando dos o más dispositivos deciden que quieren usar el medio libre *exactamente al mismo tiempo* o en un intervalo de tiempo tan cercano que sus intenciones se cruzan. **En forma general:** Este período es puramente sobrecarga temporal (overhead). El canal está ocupado, pero no se está transmitiendo ninguna información útil y válida porque las señales se están mezclando (colisión) o porque los dispositivos están intercambiando mensajes de control cortos para ponerse de acuerdo sobre quién va primero. El objetivo de este período es **resolver el conflicto** usando las reglas del protocolo (como tirar unos dados invisibles para ver quién espera menos tiempo) hasta que quede un único ganador claro.

3. **Período de Transmisión (El envío exitoso):**
El conflicto se resolvió y un dispositivo obtuvo el control exclusivo del canal. **En forma general:** Este es el único período verdaderamente productivo. El dispositivo ganador envía su paquete de datos de principio a fin. Mientras esto ocurre, el resto de los dispositivos en esa misma red aceptan su derrota temporal y se dedican a escuchar el medio o a recibir los datos en silencio. Saben que no pueden intentar hablar hasta que este período termine y el canal vuelva al estado de **Inactividad**.


## **ALOHA**
### ALOHA Puro
El concepto básico de ALOHA puro es que las estaciones operan en tiempo continuo y transmiten sus tramas en el instante exacto en que tienen datos para enviar. Si dos o más tramas intentan ocupar el canal al mismo tiempo, se superponen y se produce una colisión que destruye ambas tramas, obligando a los emisores a esperar un tiempo aleatorio antes de retransmitir.

*   **Tiempo de vulnerabilidad:** Matemáticamente, el periodo en el que una trama es vulnerable a colisiones es de **$2t$** (donde $t$ es el tiempo que toma transmitir la trama completa). Esto se demuestra en un esquema visual ("Vulnerable period") donde una trama sombreada que inicia en el tiempo $t_0$ colisionará si cualquier otra estación inició una transmisión entre $t_0 - t$ y $t_0$, o si inicia una entre $t_0$ y $t_0 + t$.
*   **Eficiencia:** Debido al amplio periodo de vulnerabilidad, el rendimiento es bastante bajo. La fórmula de eficiencia (Throughput, $S$) en función del tráfico ofrecido ($G$) es **$S = G \cdot e^{-2G}$**. Su punto de máxima eficiencia se alcanza cuando la carga es $G = 0.5$, logrando apenas un **18.4% (o $1/2e$)** de utilización del canal.

### ALOHA Ranurado (Slotted ALOHA)
 Esta variante elimina la naturaleza continua del tiempo y lo divide en **intervalos discretos o "ranuras" (slots)**. En este sistema, a una estación no se le permite transmitir en cualquier momento; debe esperar obligatoriamente al inicio de la siguiente ranura para enviar su trama.

*   **Tiempo de vulnerabilidad:** Al alinear todas las transmisiones con el inicio exacto de las ranuras, las tramas ya no pueden solaparse parcialmente. O colisionan de forma total dentro de la misma ranura, o no colisionan en absoluto. Esto **reduce el periodo de vulnerabilidad a la mitad, siendo ahora igual a $t$** (el tiempo de una sola ranura).
*   **Eficiencia:** La reducción del periodo de vulnerabilidad tiene un impacto directo y proporcional en el rendimiento, cuya fórmula pasa a ser **$S = G \cdot e^{-G}$**. Su máxima eficiencia se da con una carga de $G = 1$, logrando alcanzar el **36.8% (o $1/e$, aproximadamente un 37%)**. 

### El Gráfico Comparativo de Eficiencia vs. Carga
Ambas variantes se consolidan en el material mediante un **gráfico de curvas (Throughput $S$ vs. intentos por tiempo de paquete $G$)**. 
*   En la gráfica se observa visualmente cómo la curva inferior correspondiente al "Pure ALOHA" sube lentamente hasta un tope de $\sim 0.18$ y luego decae rápidamente ante el aumento de colisiones.
*   Por encima de esta, la curva del "Slotted ALOHA" alcanza un pico mucho más alto ($\sim 0.37$), demostrando gráficamente la afirmación de que **el ALOHA ranurado es exactamente el doble de eficiente que el ALOHA puro** gracias a la discretización del tiempo. Además, el gráfico evidencia que en ambos sistemas, mantener cargas demasiado bajas desperdicia tiempo del canal, pero imponer cargas muy altas provoca tantas colisiones que el rendimiento general de la red se desploma exponencialmente.
  


## **Protocolos CSMA (Carrier Sense Multiple Access)**

El protocolo CSMA supone una evolución fundamental frente a ALOHA al introducir la **detección de portadora** ("Carrier Sense"). La regla básica de este protocolo es que las estaciones "escuchan" el canal antes de transmitir; si detectan que el medio está ocupado por otra transmisión, no envían sus datos. 

La diapositiva detalla tres variaciones principales que definen qué hace la estación si encuentra el canal ocupado:
*   **1-persistente:** La estación escucha continuamente y transmite *inmediatamente* (con probabilidad 1) apenas detecta que el canal se libera. Tiene la desventaja de generar una mayor probabilidad de colisiones si varias estaciones estaban esperando el mismo turno.
*   **No-persistente:** En lugar de quedarse escuchando fijamente, la estación espera un tiempo aleatorio antes de volver a verificar el estado del canal. Esto mejora drásticamente la eficiencia al reducir colisiones, pero aumenta el retardo promedio.
*   **p-persistente:** Diseñado para canales ranurados. Si el canal está libre, transmite con una probabilidad matemática *p*; si no lo hace, espera a la siguiente ranura y repite el proceso.

**Análisis de la Imagen (Gráfico de Eficiencia vs. Carga):**
Para ilustrar el impacto de estas variaciones, el material presenta un gráfico de curvas que compara la eficiencia (*Throughput*, eje Y) frente a la carga de intentos de transmisión (eje X). 
*   Visualmente, se observa que el protocolo **1-persistente** tiene un pico de eficiencia moderado (alrededor de 0.5) y cae rápidamente a medida que aumenta el tráfico. 
*   Por el contrario, las curvas del **CSMA no-persistente** y del **CSMA 0.01-persistente** alcanzan la cima de la gráfica (acercándose al 1.0 o 100% de eficiencia), demostrando que introducir "paciencia" (esperas aleatorias o probabilidades bajas) permite a la red sobrevivir a cargas de tráfico muy pesadas.

### Protocolo CSMA/CD (Collision Detect)
CSMA/CD es el corazón de las redes Ethernet clásicas (no conmutadas). La mejora crítica que añade al CSMA básico es que la estación **sigue escuchando el canal mientras transmite**. 
*   Si la estación detecta una colisión al inicio de su transmisión (porque la señal que lee del cable se mezcla con otra), **interrumpe el envío inmediatamente**, lo que ahorra tiempo y ancho de banda.
*   Tras interrumpir y confirmar la colisión (mediante una señal de bloqueo), espera un tiempo aleatorio y vuelve a iniciar el proceso.

**Análisis de las Imágenes (Estado del canal y Backoff):**
*   **Diagrama de Períodos:** Se muestra un diagrama rectangular donde el tiempo del canal se divide en tres estados: un "Período de transmisión" (donde una trama viaja con éxito), un "Período de inactividad", y un **"Período de contención"** fragmentado en "ranuras" (slots). Este diagrama visualiza que las colisiones y la competencia por el canal solo ocurren en esas ranuras específicas antes de que alguien gane el medio.


### El Escenario de Colisión y la Fórmula de Longitud Mínima de Trama
El protocolo CSMA/CD *exige* que el emisor escuche el choque antes de terminar de enviar su trama. Si la trama es demasiado corta, terminará de emitirla y asumirá que llegó bien antes de que la señal de colisión tenga tiempo de regresar.

**Análisis de la Imagen (Escenario de Colisiones a tiempo $\tau$):**
El material expone un diagrama de 4 viñetas (a, b, c, d) con dos estaciones alejadas, A y B:
1.  La estación A inicia un paquete en el tiempo 0.
2.  La señal viaja y está a punto de llegar a B en el tiempo $\tau - \epsilon$ (donde $\tau$ es el tiempo de propagación de un extremo al otro).
3.  Justo antes de que llegue, B transmite, causando una **colisión en el tiempo $\tau$**.
4.  La "ráfaga de ruido" (noise burst) generada por la colisión tiene que viajar todo el camino de vuelta, **llegando a la estación A en el tiempo $2\tau$**.

**La Fórmula Matemática:**
A partir de este escenario visual, la diapositiva establece que el tiempo máximo para detectar una colisión es $2\tau$ (el tiempo de propagación de ida y vuelta). Por lo tanto, el tiempo que tarda en transmitirse la trama más corta debe ser *igual o mayor* a ese tiempo de ida y vuelta. 

La fórmula fundamental deducida en la presentación es:
**$L_{trama\_minima} = V_t \cdot 2 \cdot \tau$**
*(Longitud de trama mínima = Velocidad de transmisión multiplicada por el doble del tiempo de propagación)*.

Esta misma ecuación se desglosa más adelante para las distintas velocidades (como en Gigabit Ethernet) de la siguiente manera:
**$l_{trama\_min} = 2 \cdot (d_{max} / V_{propag.}) \cdot V_{transm.}$**


## **Protocolo de Mapeo de Bits (Bitmap)**
En este protocolo de reserva, el periodo de contención se divide exactamente en un número de ranuras discretas igual al número de estaciones. 
*   **Funcionamiento:** Cada estación tiene una ranura de tiempo preasignada. Si una estación tiene datos para enviar, transmite un bit "1" en su ranura correspondiente. Una vez que termina el periodo de contención y todas las estaciones tuvieron su turno para "anunciar" si tienen datos, las estaciones transmiten sus tramas en orden numérico secuencial, evitando así cualquier choque.
*   **Análisis de la imagen:** La diapositiva ilustra esto con un diagrama que muestra bloques de "Ranuras de contención" (numeradas del 0 al 7). 
    *   En el primer bloque, se observa un número "1" en las celdas **1, 3 y 7**. Inmediatamente después del bloque de contención, el diagrama muestra tres tramas de datos transmitiéndose organizadamente en ese exacto orden: trama 1, trama 3 y trama 7.
    *   En el siguiente ciclo de 8 ranuras, solo hay un "1" en las celdas **1 y 5**, seguido por las tramas 1 y 5, demostrando visualmente cómo las estaciones "piden turno" y luego envían sin interferirse.

## **Protocolo de Paso de Ficha (Token Ring) (Papa caliente)**
Este protocolo elimina la contención mediante el uso de un mensaje especial (la ficha o *token*) que va rotando entre las máquinas.
*   **Funcionamiento:** Las estaciones se organizan en un orden lógico o físico. El *Token* circula constantemente por el anillo y representa el permiso exclusivo para transmitir. Una estación solo puede enviar una trama de datos si está en posesión de la ficha; al terminar, debe pasar su turno enviando el *token* a la siguiente estación.
*   **Análisis de la imagen:** La diapositiva muestra una topología de red en anillo (una línea roja circular conectando a varias computadoras). Sobre el anillo, viaja un bloque rectangular morado etiquetado explícitamente como **"Token"**, acompañado de una flecha negra que indica su sentido de circulación de una máquina a la siguiente. Esta imagen refuerza el concepto de que el acceso al medio no es competitivo, sino estrictamente secuencial.

## **Protocolo de Cuenta Atrás Binaria (Binary Countdown)**
Este protocolo surge como una mejora directa al protocolo de mapa de bits. En redes grandes, tener una ranura de contención por cada estación (como en el *bitmap*) desperdicia mucho tiempo; este método reduce esas ranuras utilizando direcciones binarias.
*   **Funcionamiento:** Durante el periodo de contención, todas las estaciones que desean transmitir envían su propia dirección binaria al medio, bit a bit. El cable o medio físico combina las señales mediante una suma lógica (operación OR). La regla de arbitraje es crucial: **si una estación envía un bit "0", pero detecta que el canal registra un "1", se rinde** inmediatamente y queda fuera de esa ronda de transmisión. La estación que termina de transmitir toda su dirección sin rendirse, gana el acceso.
*   **Análisis de la imagen:** Esta es una de las representaciones visuales más detalladas de la presentación. Muestra una competencia entre cuatro estaciones con direcciones binarias: **0010, 0100, 1001 y 1010**. 
    *   En el **Tiempo de bit 0**, las estaciones 1001 y 1010 envían un "1", mientras que 0010 y 0100 envían un "0". El resultado en el medio es un "1" (por la operación OR). Un texto en la imagen señala explícitamente: *"Las estaciones 0010 y 0100 ven este 1 y se rinden"*.
    *   En el **Tiempo de bit 2**, la estación 1001 envía un "0", pero la estación 1010 envía un "1". El resultado es "1". Otro texto señala: *"La estación 1001 ve este 1 y se rinde"*.
    *   Finalmente, la estación **1010** resulta ganadora porque tiene la dirección más alta, demostrando visualmente que este protocolo favorece implícitamente a las estaciones con numeraciones mayores.



## **Protocolo de Árbol Adaptativo (Adaptive Tree-Walk)**

La diapositiva presenta un diagrama de un grafo jerárquico estructurado como un **árbol binario**.
*   En la cima del diagrama se encuentra el **Nodo 1** (la raíz), del cual se desprenden dos ramas hacia los Nodos 2 y 3.
*   Esta subdivisión continúa hacia los Nodos 4, 5, 6 y 7.
*   En la base del árbol, las "hojas" están etiquetadas con las letras **A, B, C, D, E, F, G, H**, acompañadas del texto *"Stations"* (Estaciones). 

El protocolo opera realizando una búsqueda o recorrido (walk) a través de las ramas del árbol para resolver quién tiene el turno de transmitir:
1.  **Ranura 0 (Competencia global):** En la primera ranura de tiempo, el protocolo permite que todas las estaciones que están bajo el **Nodo 1** (es decir, todas las estaciones de la A a la H) intenten transmitir simultáneamente. 
    *   Si solo una estación transmite, adquiere el canal con éxito.
    *   Si ocurre una colisión, significa que dos o más estaciones están compitiendo.
2.  **Búsqueda en profundidad (Nodo 2):** Ante la colisión en el Nodo 1, el algoritmo restringe la competencia en la siguiente ranura (ranura 1) **solo a la mitad izquierda del árbol**: las estaciones situadas bajo el **Nodo 2** (es decir, A, B, C y D). Las estaciones de la mitad derecha (bajo el Nodo 3) deben guardar silencio obligatoriamente.
3.  **Resolución recursiva:** Si vuelve a haber una colisión en el Nodo 2 (por ejemplo, A y C intentan hablar), en la siguiente ranura el turno se restringe aún más, pasando al **Nodo 4** (solo compiten A y B). 
4.  **Descarte de ramas vacías:** Si al evaluar un nodo (por ejemplo, el Nodo 4), la ranura resulta estar inactiva o tiene una transmisión exitosa, el algoritmo sabe de inmediato que ya no hay más estaciones esperando en esa pequeña rama. Se detiene la búsqueda ahí y se pasa al siguiente subgrupo (el Nodo 5, que cubre a C y D).

**La naturaleza "Adaptativa"**
El término "adaptativo" proviene de la capacidad del protocolo de ajustarse a la carga de la red. Si la red está fuertemente congestionada (muchas estaciones listas para transmitir), es un hecho matemático casi seguro que permitir que todas compitan en el Nodo 1 terminará en una colisión. 
Para optimizar el tiempo y no desperdiciar ranuras en colisiones predecibles, el protocolo estima cuántas estaciones están activas. Bajo cargas pesadas, **omite por completo la competencia en el Nodo 1 (la raíz) y comienza la búsqueda directamente en los nodos inferiores** (por ejemplo, desde el Nodo 2 o más abajo), comportándose en la práctica como un protocolo libre de colisiones.

Siguiente: [Ethernet Clásico](ethernet_clasico.md)