# Transportadora T1

### 1. El tamaño de la trama (Frame)
* **`24 canales * 8 bits`**: El sistema T1 junta (multiplexa) 24 canales de voz distintos. Cada canal genera una muestra digitalizada de 8 bits (usando modulación PCM). Esto nos da 192 bits de datos puros.
* **`+ 1 bit`**: A esos 192 bits se les suma 1 bit extra de control (llamado "bit de enmarcado" o *framing bit*) que sirve para que el equipo receptor no pierda la sincronización.
* **Resultado parcial**: $(24 \times 8) + 1 = \mathbf{193 \text{ bits por trama (frame)}}$.

### 2. La tasa de muestreo (Tiempo)
* **`8000 muestras/segundo`**: Por el teorema de Nyquist, la red telefónica estandarizó que la voz debe muestrearse 8,000 veces cada segundo para capturarla con claridad.
* **`1 frame/muestra`**: Como bien lo expresas con esta relación de unidades, el sistema debe empaquetar y enviar una trama completa por cada vez que toma una muestra de los 24 canales simultáneamente. Por lo tanto, se transmiten **8,000 tramas en un segundo**.

### 3. El cálculo final (Tasa de bits)
Al aplicar tu fórmula final multiplicando los factores, las unidades de "muestras" y "frames" se cancelan, dejándonos con la velocidad real de transmisión en el cable:
> $193 \text{ bits/frame} \times 8000 \text{ frames/segundo} = \mathbf{1,544,000 \text{ bits/segundo}}$

En el mundo de las telecomunicaciones y en la literatura de redes, ese número es legendario: es exactamente la velocidad estándar de la línea **T1**, la cual siempre se redondea y se conoce comercialmente como **1.544 Mbps**. 

La progresión funciona de la siguiente manera,:
- *Nivel T2:* Combina *4 flujos T1* para alcanzar *6.312 Mbps*. Se utiliza principalmente de forma interna dentro de los sistemas de las compañías telefónicas,.
- *Nivel T3:* Combina *7 flujos T2* para alcanzar *44.736 Mbps*. Este nivel es muy común y es ampliamente alquilado por clientes corporativos que requieren gran ancho de banda.
- *Nivel T4:* Combina *6 flujos T3* para alcanzar *274.176 Mbps*. Se utiliza casi exclusivamente en el núcleo o backbone del sistema telefónico y no es tan conocido por el público general.

# Transportadora E1
Al aplicar tu fórmula vemos claramente cómo se calcula la velocidad de la transportadora europea **E1** y resalta la principal diferencia de diseño que tiene frente a la T1 estadounidense:

### El cálculo:
> $32 \text{ canales} \times 8 \text{ bits} = \mathbf{256 \text{ bits/frame}}$
> $256 \text{ bits/frame} \times 8000 \text{ frames/segundo} = \mathbf{2,048,000 \text{ bits/segundo}}$

Ese resultado es el famoso estándar comercial de **2.048 Mbps** de las líneas E1.

### ¿Qué pasó con el "+ 1 bit" de sincronización que tenía la T1?
Aquí radica la elegancia del sistema europeo (UIT). El E1 **no** suma un bit suelto al final de la trama. En su lugar, de esos 32 canales que calculaste, dedica canales completos para el control:

* **Canales 1 al 15 y 17 al 31 (30 canales en total):** Se usan exclusivamente para transportar la voz o los datos de los usuarios (payload).
* **Canal 0 (Timeslot 0):** Se sacrifica entero (los 8 bits) para enviar los patrones de sincronización (framing). Hace el mismo trabajo que el bit extra del T1, pero de forma más robusta.
* **Canal 16 (Timeslot 16):** Se dedica enteramente a la señalización (para avisar qué teléfono está sonando, colgado, etc.).

En resumen, tu fórmula está perfecta: la trama del E1 es un bloque limpio y exacto de 256 bits que viaja 8,000 veces por segundo.