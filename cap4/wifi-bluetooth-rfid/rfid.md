# **Redes RFID** 

## **Definición, Estándar y Características Generales**

Las redes de Identificación por Radiofrecuencia fueron creadas para revolucionar la logística a nivel mundial.

*   **Estándar y Organización:** El protocolo fue desarrollado por el consorcio **EPCglobal** y estandarizado formalmente como **EPC Gen 2** (*Electronic Product Code Generation 2*) en el año **2008**.
*   **El Identificador:** El corazón de la tecnología es el **EPC** (*Electronic Product Code* - Código Electrónico de Producto), el cual se almacena en la etiqueta y se compone de exactamente **96 bits** de datos.
*   **Ventajas Técnicas y Comerciales:**
    *   Fue diseñado específicamente como el **reemplazo comercial del código de barras**.
    *   Posee un alcance de lectura extendido de **hasta 10 metros**.
    *   Funciona **omnidireccionalmente**; es decir, no requiere una línea de visión directa entre el lector y la etiqueta para operar.

## **Clasificación de la Capa Física y Modulación**

Para la transmisión inalámbrica, el estándar define reglas físicas estrictas:

*   **Frecuencia de Operación:** Trabaja en la banda **ISM** (*Industrial, Scientific and Medical*) de **900 MHz**, ubicada en el espectro de **UHF** (*Ultra High Frequency* - Frecuencia Ultra Alta).
*   **Técnica de Mitigación:** Emplea salto de frecuencia (*Frequency Hopping*) para evadir interferencias electromagnéticas de otros equipos.
*   **Modulación y Transmisión de Bits:**
    *   Utiliza la modulación **ASK** (*Amplitude Shift Keying* - Modulación por desplazamiento de amplitud).
    *   **El Lector (*Reader*):** Utiliza la duración de un periodo de señal para enviar bits 0/1 hacia las etiquetas.
    *   **La Etiqueta (*Tag*):** Las etiquetas no tienen baterías para transmitir, por lo que envían señales de **Backscatter** (Dispersión en retroceso o retrodispersión) en forma de pulsos para devolver los bits 0/1 al lector.


## **Subcapa MAC: Protocolo de Resolución de Colisiones**

Para coordinar a múltiples etiquetas intentando hablar al mismo tiempo, el estándar implementa un riguroso algoritmo de acceso en la subcapa MAC:

1.  **Inicio y Timing:** El Lector (*Reader*) es quien inteligentemente configura el temporizador (*timing*) de la comunicación y conoce de antemano el formato esperado.
2.  **Trama Query (Consulta):** El Lector inicia enviando tramas de *Query* hacia las etiquetas, las cuales establecen la estructura y el número de ranuras de tiempo (*slots*) disponibles.
3.  **Respuesta y Colisión:** Los *Tags* eligen una ranura de forma aleatoria (randómica) y responden enviando una pequeña trama **RN16** (*Random Number 16-bit* - Número Aleatorio de 16 bits). Debido a la aleatoriedad, las respuestas RN16 de distintas etiquetas **pueden colisionar** si eligen el mismo *slot*.
4.  **Confirmación y Datos:** Si una etiqueta gana el *slot*, el Lector le pide a ese *Tag* su identificador exacto a través de una trama **ACK** (*Acknowledgment* - Acuse de Recibo).
5.  **Envío Final:** Solo tras recibir el ACK, el *Tag* responde enviando sus datos finales (los 96 bits del EPC).
6.  **Bucle:** El proceso continúa cíclicamente iterando con todos los *tags* presentes.

## **Formato de Trama Gen2 (Trama de Query)**

De acuerdo con el estándar y las imágenes proporcionadas en la diapositiva, las tramas emitidas por el Lector varían dependiendo del comando o tipo específico. 

El esquema visual detalla la estructura exacta de la trama de **Query**, la cual se encarga de contener los parámetros de comunicación y la detección de errores. Se compone de los siguientes campos secuenciales, sumando un total de 22 bits de cabecera de control:

*   **Command (Comando) - 4 bits:** Identifica el tipo de instrucción. En el ejemplo del diagrama, el comando de *Query* lleva el valor binario explícito de `1000`.
*   **Campos de Parámetros Físicos (*Physical Parameters*):** Configuran cómo debe responder la etiqueta en el medio inalámbrico.
    *   **DR - 1 bit:** Ratio de división (*Divide Ratio*).
    *   **M - 2 bits:** Ciclos de modulación o subportadora.
    *   **TR - 1 bit:** Referencia de calibración de tiempo (*Timing Reference*).
*   **Campos de Selección de Etiqueta (*Tag Selection*) y Ranuras:**
    *   **Sel - 2 bits:** Selecciona qué grupo de etiquetas debe participar en el inventario.
    *   **Session (Sesión) - 2 bits:** Indica la sesión de inventario actual.
    *   **Target (Objetivo) - 1 bit:** Determina el estado de inventario (A o B) que las etiquetas deben tener para responder.
*   **Q - 4 bits:** Es el parámetro clave de contención que le dicta a las etiquetas cuántos *slots* (ranuras) aleatorios estarán disponibles para competir (estadísticamente $2^Q$ ranuras).
*   **CRC - 5 bits:** Secuencia de Comprobación de Redundancia Cíclica (*Cyclic Redundancy Check*). Proporciona la corrección y detección de errores obligatoria para evitar interpretar comandos corruptos.
