## De formas de onda a bits

### Bases teóricas

Los **datos** son entidades que contienen un significado o información específica. Para ser transmitidos, se representan mediante **señales**, que son las formas eléctricas o electromagnéticas que efectivamente se propagan de manera física a través de un medio de comunicación. La **transmisión de datos** es precisamente el proceso de enviar esta información entre un transmisor y un receptor, lo cual se logra variando las propiedades de la señal a lo largo del tiempo.

Para estudiar las señales en el **dominio del tiempo**, se clasifican según su forma y comportamiento:
*   **Señal analógica:** Es aquella cuya amplitud varía suavemente y de forma continua en el tiempo.
*   **Señal digital:** Es aquella que mantiene un nivel constante (por ejemplo, un voltaje) durante un periodo y luego cambia abruptamente a otro nivel constante.
*   **Señales periódicas y aperiódicas:** Se definen por tener un patrón que se repite exactamente igual en el tiempo (periódica) o un patrón que no se repite (aperiódica).

### Análisis de Fourier

El puente fundamental para comprender cómo viajan estas señales físicamente es el **Análisis de Fourier**. Este principio matemático establece que cualquier señal en el tiempo se puede descomponer en una sumatoria de ondas sinusoidales (senos y cosenos), formadas por una frecuencia fundamental y múltiples armónicas con distintas amplitudes. Esta descomposición nos permite trasladar el estudio de las señales desde el dominio del tiempo hacia el **dominio de la frecuencia**.

Al analizar la transmisión en el dominio de la frecuencia, es imperativo distinguir entre tres conceptos interconectados: el espectro, el ancho de banda de la señal y el ancho de banda del canal.

**1. Espectro de la señal**
Es el rango total de frecuencias que están contenidas en una señal. Según el análisis de Fourier, si queremos representar una señal digital perfecta (como las variaciones abruptas de una onda cuadrada), necesitamos sumar infinitas armónicas. Por lo tanto, el espectro de una señal digital teórica es infinito.

**2. Ancho de banda de la señal**
Aunque el espectro pueda ser infinito, no todas las frecuencias que componen la señal tienen la misma potencia o importancia. El ancho de banda de la señal es el rango específico de frecuencias donde se concentra la mayor parte de su energía.

**3. Ancho de banda del canal**
Mientras que los dos conceptos anteriores describen a la señal, este describe al medio físico (cable de cobre, fibra óptica, el aire, etc.). Cualquier canal de transmisión tiene un rango máximo de frecuencias que es capaz de transportar sin sufrir una atenuación (pérdida de potencia) o distorsión severa. Esta es una **propiedad física** ineludible del medio, que depende de factores como la construcción, el grosor, la longitud y el material utilizado.

**La interacción fundamental para la transmisión de datos:**

La regla de oro de la comunicación física es que **un canal no puede transportar eficientemente una señal cuyo ancho de banda sea mayor que el suyo propio**.

Cuando una señal digital (con su amplio espectro) intenta viajar por un canal físico, este último actúa como un filtro. De todas las armónicas que componen la señal original, el canal solo dejará pasar intactas aquellas frecuencias que entren dentro de su ancho de banda limitado. Las armónicas de mayor frecuencia serán atenuadas o eliminadas por completo. 

Al perder estas frecuencias altas, la onda cuadrada pierde sus bordes rectos y sufre distorsión. Las imágenes de las diapositivas y los textos ilustran claramente este efecto: si un canal es muy limitado y solo deja pasar 1 armónica, la señal resultante es apenas una onda suave; si el ancho de banda es mayor y permite el paso de 2, 4 u 8 armónicas, la curva resultante se aproxima cada vez más a la onda cuadrada digital original. 

Afortunadamente para las redes de computadoras, el objetivo de la transmisión digital no es recibir una onda cuadrada matemáticamente perfecta. El objetivo es que el ancho de banda del canal deje pasar un número suficiente de armónicas para que el receptor pueda leer la señal con la fidelidad necesaria para reconstruir correctamente la secuencia de bits (los ceros y unos). Si se intenta transmitir a una tasa de bits tan alta que el ancho de banda del canal no permite el paso de los armónicos fundamentales, la señal llegará tan deformada que los datos se perderán irremediablemente.

### Señales de audio
Las señales de audio abarcan el espectro completo de frecuencias que el oído humano es capaz de percibir, el cual se sitúa en un rango de 20 Hz a 20 kHz. Sin embargo, dentro de este amplio espectro, la voz humana concentra la mayor parte de su información y energía en una banda mucho más estrecha, que va específicamente desde los 100 Hz hasta los 7 kHz. 

Una de las grandes ventajas de las señales de audio desde la perspectiva de las telecomunicaciones es que resultan muy fáciles de convertir a señales electromagnéticas análogas, facilitando así su transmisión a través de cables.

**Análisis a partir del gráfico de espectro de las diapositivas**

La imagen proporcionada en las diapositivas ilustra de manera muy clara cómo se distribuye la relación de potencia (medida en decibelios) de los distintos tipos de señales en función de la frecuencia. A partir de este gráfico podemos extraer varias conclusiones clave:

*   **Rango dinámico de la música:** La curva etiquetada como "MUSIC" demuestra que las señales musicales tienen un rango dinámico muy amplio. Su energía abarca desde frecuencias sumamente bajas (cerca de los 20 Hz) y se extiende hasta frecuencias muy altas que superan los 10 kHz, acercándose al límite superior de audición.
*   **Rango dinámico de la voz ("SPEECH"):** La curva de la voz humana muestra un comportamiento distinto. Comienza a tener una potencia significativa por encima de los 100 Hz y su curva decae mucho antes que la de la música. Esto confirma visualmente que la voz requiere un ancho de banda considerablemente menor para ser transmitida de forma inteligible.
*   **Limitación del canal telefónico:** El gráfico destaca un bloque rectangular fuertemente delimitado llamado "Telephone channel". Para optimizar el uso de los medios físicos, los sistemas telefónicos no transmiten toda la gama de frecuencias de la voz humana, sino que aplican filtros artificiales que cortan las frecuencias por debajo de los 300 Hz y por encima de los 3400 Hz. A este canal se le asigna un bloque estándar de 4000 Hz (4 kHz). En el gráfico, esto se ve como una "ventana" estricta a través de la cual debe pasar la señal de voz.
*   **Límites de radiodifusión y piso de ruido:** La imagen también contrasta estas señales con los límites superiores de transmisión de las radios AM y FM (siendo el de FM mucho más amplio que el de AM) y muestra un bloque rectangular en la parte inferior que representa el piso de "Noise" (Ruido), situado en el rango de -40 a -50 decibelios. Toda señal que caiga dentro de este piso oscuro corre el riesgo de perderse por las interferencias.

**Digitalización de la señal filtrada**

Esta limitación analógica de 4 kHz dictada por los filtros telefónicos es la base para la digitalización moderna. Cuando esta señal analógica de audio se introduce en la red troncal telefónica, un dispositivo llamado códec la transforma en bits mediante Modulación por Impulsos Codificados (PCM). Para cumplir con el teorema de Nyquist, la red toma exactamente 8.000 muestras por segundo de ese canal de 4 kHz. Al usar 8 bits por muestra, obtenemos la velocidad estándar mundial para enviar una llamada de voz digital: 64.000 bits por segundo (64 kbps).

