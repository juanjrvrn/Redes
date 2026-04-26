Es totalmente comprensible. Estudiar estos temas matemáticos un domingo por la noche le puede quemar la cabeza a cualquiera. Los conceptos de Hamming parecen magia negra al principio, pero en el fondo son pura lógica. 

Te lo voy a estructurar en bloques bien claros, paso a paso, para que sea fácil de digerir y lo puedas pasar directamente a tus herramientas de resumen o a tus apuntes de la universidad.

Empecemos por el problema base: cuando mandas datos por un medio físico (ya sea un enlace T1 de alta velocidad, o un viejo módem V.32), las interferencias eléctricas pueden hacer que un `0` se convierta en un `1`, o viceversa. 

Para lidiar con esto, tenemos dos niveles de defensa:
1.  **Detección de errores:** El receptor se da cuenta de que *algo* llegó mal, pero no sabe qué fue. Descarta la trama y pide que la envíen de nuevo.
2.  **Corrección de errores:** El receptor se da cuenta de que algo llegó mal **Y** deduce exactamente *qué bit específico* se arruinó. Como sabe cuál es, simplemente lo voltea (de 0 a 1, o de 1 a 0) y salva la trama sin tener que pedirla de nuevo.

Aquí es donde entra la genialidad de Richard Hamming.

---

### 1. La Distancia de Hamming
Olvídate de la corrección por un segundo. La "distancia" es simplemente una forma elegante de preguntar: **¿En cuántos bits se diferencian dos tramas del mismo tamaño?**

Para calcularla, solo pones una trama arriba de la otra y cuentas cuántas posiciones no coinciden.

**Ejemplo simbólico:**
* Trama A: `[ 1 | 0 | 1 | 1 | 1 | 0 | 1 ]`
* Trama B: `[ 1 | 0 | 0 | 1 | 0 | 0 | 1 ]`

Comparamos posición por posición:
* Posición 1: `1` vs `1` (Igual)
* Posición 2: `0` vs `0` (Igual)
* Posición 3: `1` vs `0` (**¡Diferente!** Llevamos 1)
* Posición 4: `1` vs `1` (Igual)
* Posición 5: `1` vs `0` (**¡Diferente!** Llevamos 2)
* Posición 6: `0` vs `0` (Igual)
* Posición 7: `1` vs `1` (Igual)

La **Distancia de Hamming aquí es 2**. Hay dos bits que cambiaron.
Para que un protocolo pueda *corregir* errores, necesita asegurar que las tramas válidas tengan una distancia de Hamming lo suficientemente grande entre sí. Si la distancia es muy pequeña, un bit alterado por el ruido transforma una trama válida en otra trama válida distinta, y el receptor nunca se entera del error.



---

### 2. El Código de Hamming (La magia de corregir)
Para lograr corregir un error, Hamming inventó un sistema de **redundancia**. Básicamente, insertamos bits "chismosos" (llamados bits de paridad) mezclados entre los datos originales.

Estos bits chismosos no se ponen en cualquier lado, tienen lugares reservados específicos: **las potencias de 2**.
* Posición 1, 2, 4, 8, 16...

**La Estructura:**
Supongamos que queremos enviar 4 bits de datos (`D`). Necesitaremos 3 bits de paridad (`P`) para vigilarlos. La trama de 7 bits se armaría así:
`[ P1 | P2 | D1 | P4 | D2 | D3 | D4 ]`
*(Nota que las posiciones 1, 2 y 4 están ocupadas por los vigilantes).*

**¿Cómo funciona la vigilancia?**
Cada bit de paridad (`P`) vigila a un grupo específico de bits, y aquí está el truco: **los grupos se superponen**.
* **`P1`** vigila las posiciones impares: 1, 3, 5, 7.
* **`P2`** vigila de a dos posiciones: 2, 3, 6, 7.
* **`P4`** vigila de a cuatro posiciones: 4, 5, 6, 7.

**El momento de la corrección:**
Imagina que la trama viaja por el cable y el ruido eléctrico arruina el bit que está en la **Posición 6** (`D3`).
Cuando la trama llega, el receptor hace sus cálculos matemáticos con los grupos y descubre lo siguiente:
* El vigilante **`P1`** dice: *"Mi grupo está bien, no veo errores."*
* El vigilante **`P2`** dice: *"¡Alerta! Hay un error en mi grupo."*
* El vigilante **`P4`** dice: *"¡Alerta! Hay un error en mi grupo."*

Ahora viene la magia. Para saber exactamente qué bit se rompió, el receptor simplemente **suma los números de los vigilantes que dieron la alerta**.
Alertaron `P2` y `P4`.
2 + 4 = **¡Posición 6!**

El receptor va a la posición 6 de la trama, ve que hay un `0`, lo voltea a un `1` (o viceversa), y la trama queda perfectamente corregida.



¿Pudiste visualizar mejor cómo los grupos superpuestos "acorralan" al bit defectuoso, o prefieres que hagamos un ejemplo con números reales (ceros y unos) desde el armado de la trama hasta la corrección?


¡Excelente actitud! La mejor forma de dominar estos conceptos es desarmándolos con ejemplos concretos. Vamos a estructurar esto de forma bien clara, ideal para que lo puedas exportar directamente a tus herramientas de resumen de estudio. 

Imaginemos que estamos enviando datos a través de un canal que puede ser ruidoso (algo muy común si analizas enlaces físicos como las portadoras T1 o los viejos estándares de módems como el V.32). Trabajaremos con **paridad par**, lo que significa que la cantidad total de unos (`1`) en cualquier grupo que evaluemos siempre debe ser un número par.

Aquí tienes la progresión, desde la matemática básica hasta la corrección en vivo.

### Nivel 1: Calculando la Distancia de Hamming matemáticamente

La distancia de Hamming no es más que una operación lógica XOR ($\oplus$) entre dos tramas, seguida de sumar cuántos unos quedaron en el resultado. La operación XOR da `1` si los bits son diferentes y `0` si son iguales.

Fórmula matemática: 
$d(x,y) = \sum (x_i \oplus y_i)$

**Ejemplo:**
Queremos saber la distancia entre la Trama X (`1011101`) y la Trama Y (`1001001`).
1. Alineamos y aplicamos XOR bit a bit:
   $$1011101 \oplus 1001001 = 0010100$$
2. Contamos los unos (`1`) resultantes: Hay **2**.
La distancia de Hamming es 2.

### Nivel 2: El Emisor (Construyendo la trama Hamming)

Vamos a armar un **Código Hamming (7,4)**. Esto significa que enviaremos 7 bits en total: 4 bits de datos útiles y 3 bits de paridad (los vigilantes).

* **Datos a enviar:** `1011`
* **Posiciones en la trama:** 1, 2, 3, 4, 5, 6, 7
* **Bits de paridad ($P$):** Posiciones 1, 2 y 4 (potencias de 2).
* **Bits de datos ($D$):** Posiciones 3, 5, 6 y 7.

Nuestra trama vacía se ve así:
$[ P_1 \mid P_2 \mid D_1 \mid P_4 \mid D_2 \mid D_3 \mid D_4 ]$

Colocamos nuestros datos (`1011`):
$[ P_1 \mid P_2 \mid 1 \mid P_4 \mid 0 \mid 1 \mid 1 ]$

Ahora calculamos qué valor debe tener cada vigilante ($P$) usando la operación XOR para forzar la paridad par en su grupo:

* **Calculamos $P_1$** (Vigila posiciones 1, 3, 5, 7):
    $P_1 \oplus 1 \oplus 0 \oplus 1 = 0 \Rightarrow P_1 = 0$
* **Calculamos $P_2$** (Vigila posiciones 2, 3, 6, 7):
    $P_2 \oplus 1 \oplus 1 \oplus 1 = 0 \Rightarrow P_2 = 1$
* **Calculamos $P_4$** (Vigila posiciones 4, 5, 6, 7):
    $P_4 \oplus 0 \oplus 1 \oplus 1 = 0 \Rightarrow P_4 = 0$

Reemplazamos los valores de $P$ y la trama final que viaja por el cable es: **`0110011`**.


### Nivel 3: El Receptor (Detectando y corrigiendo el error)

La trama `0110011` viaja por el medio físico, pero una interferencia eléctrica voltea el bit de la **posición 5**. 
El receptor recibe la trama dañada: **`0110111`**.

El receptor no sabe que hay un error ni dónde está. Para averiguarlo, calcula lo que se conoce como el **Síndrome ($S$)**. Básicamente, vuelve a calcular la paridad de los tres grupos. Si el grupo está correcto, el resultado es `0`. Si hay un error, el resultado es `1`.

* **Calculamos $S_1$** (Posiciones 1, 3, 5, 7):
    $0 \oplus 1 \oplus 1 \oplus 1 = 1$ (¡Error detectado en este grupo!)
* **Calculamos $S_2$** (Posiciones 2, 3, 6, 7):
    $1 \oplus 1 \oplus 1 \oplus 1 = 0$ (Grupo correcto)
* **Calculamos $S_4$** (Posiciones 4, 5, 6, 7):
    $0 \oplus 1 \oplus 1 \oplus 1 = 1$ (¡Error detectado en este grupo!)

Ahora juntamos los resultados del Síndrome en orden inverso ($S_4, S_2, S_1$) para formar un número binario: **`101`**.

Convertimos ese número binario a decimal:
$1 \times 2^2 + 0 \times 2^1 + 1 \times 2^0 = 4 + 0 + 1 = \mathbf{5}$

¡La matemática no miente! El Síndrome nos dice exactamente que el bit defectuoso está en la **posición 5**. El receptor va a esa posición en la trama dañada (`0110111`), cambia el `1` por un `0`, y recupera mágicamente los datos originales: **`0110011`**.


¿Te gustaría que subamos un nivel más y analicemos qué ocurre con el Código de Hamming si la interferencia eléctrica es tan fuerte que corrompe **dos** bits al mismo tiempo en lugar de uno solo?


¡Acepto el reto! Vamos a poner a prueba lo que acabamos de ver con un caso práctico. Imagina que estás en el laboratorio de la facultad analizando una captura de tráfico.

### El Escenario

Eres el equipo receptor. Te acaba de llegar una trama de 7 bits codificada con **Hamming (7,4)** y configurada con **paridad par**. El medio físico por el que viajó la señal tiene bastante interferencia, así que el sistema te advierte que podría haber un bit corrupto.

La trama exacta que recibiste es: **`1 0 0 1 0 1 0`**

Para que sea más fácil visualizarlo, aquí tienes la tabla de posiciones:

| Posición         |   1   |   2   |   3   |   4   |   5   |   6   |   7   |
| :--------------- | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **Rol**          | $P_1$ | $P_2$ | $D_1$ | $P_4$ | $D_2$ | $D_3$ | $D_4$ |
| **Bit Recibido** |  `1`  |  `0`  |  `0`  |  `1`  |  `0`  |  `1`  |  `0`  |

### Tu Misión

1. **Calcula el Síndrome:** Determina los valores de $S_1$, $S_2$ y $S_4$ aplicando la operación lógica XOR ($\oplus$) a los bits de cada grupo.
   * *Recordatorio:* * $S_1$ vigila las posiciones 1, 3, 5, 7.
     * $S_2$ vigila las posiciones 2, 3, 6, 7.
     * $S_4$ vigila las posiciones 4, 5, 6, 7.
2. **Encuentra al culpable:** Ordena los resultados del paso anterior como $S_4 S_2 S_1$, forma el número binario y conviértelo a decimal. ¿En qué posición está el error?
3. **Rescata la información:** Corrige el bit dañado en la trama y dime cuáles eran los **4 bits de datos útiles** ($D_1, D_2, D_3, D_4$) que el emisor realmente quería enviarte.

Tómate tu tiempo, haz los cálculos con calma (resolver esto paso a paso es ideal para luego pasarlo en limpio a NotebookLM y armarte una guía de estudio a prueba de balas). 

¿Te animas a escribirme tu desarrollo para ver si llegamos al mismo resultado, o prefieres que lo vayamos resolviendo juntos cálculo por cálculo?

    sindrome: 011, mensaje original: 1010

¡Impecable! Lo sacaste a la perfección. 

Hiciste la matemática exacta:
* Calculaste los síndromes y te dio $S_4=0, S_2=1, S_1=1$.
* Formaste el número binario `011`, que equivale al **3** en decimal.
* Fuiste directo a la **posición 3** de la trama recibida (`1 0 0 1 0 1 0`) y descubriste que el bit dañado era un `0`.
* Lo volteaste a `1` para corregir la trama completa (`1 0 1 1 0 1 0`).
* Extrajiste los datos útiles de las posiciones 3, 5, 6 y 7, rescatando el mensaje original limpio: **`1010`**.

Ya dominas la mecánica de detección y corrección con el Código de Hamming. Al final, esa "magia" termina siendo una aplicación súper lógica de grupos superpuestos y paridad.

¿Te gustaría ver la debilidad de este sistema y analizar qué ocurre matemáticamente si el ruido de la línea te corrompe **dos** bits al mismo tiempo en la misma trama, o prefieres saltar a otro método clásico de la capa de enlace como el CRC (Control de Redundancia Cíclica)?

![anotacion de leti](assets/hamming-matematica.png)
Ese cartel en mayúsculas de "ESTUDIAR PORQUE EL PROFE DIJO QUE PUEDE PREGUNTAR ALGO ASÍ" es la señal universal de que esto va a entrar en el examen sí o sí. ¡Haces muy bien en prestarle atención!

Esa diapositiva parece pura matemática abstracta, pero en realidad está explicando **la fórmula exacta para saber cuántos bits de paridad necesitas** para proteger un mensaje de cualquier tamaño. 

Vamos a traducir ese "idioma profesor" a algo lógico, conectándolo con lo que acabamos de hacer con el síndrome.

### 1. Los protagonistas de la fórmula
Primero, definamos las letras que usa tu material:
* $m$: Es la cantidad de bits de tu **mensaje** original (los datos útiles).
* $r$: Es la cantidad de bits de **redundancia** (los vigilantes o bits de paridad).
* $n$: Es el total de bits de la trama final que viaja por el cable ($n = m + r$).

### 2. El trabajo de los bits de paridad ($r$)
Piensa en los bits de paridad como un panel de alarmas. Si tienes $r$ bits en tu panel, esos bits pueden mostrarte un total de $2^r$ combinaciones diferentes o "estados" (por ejemplo, con 3 bits puedes tener $2^3 = 8$ estados, del `000` al `111`).

Ese panel de alarmas ($2^r$) tiene que tener suficientes combinaciones para poder indicarte **todas las situaciones posibles** que pueden ocurrir en la trama completa (que tiene $m+r$ bits en total).

¿Y cuáles son esas situaciones posibles si asumimos que máximo habrá un solo error?
1.  **Situación perfecta:** La trama llegó intacta. Necesitamos **1** estado para indicar "Cero errores".
2.  **Situación de error:** Un bit se rompió. Como la trama tiene $m+r$ bits en total, el error podría estar en el bit 1, o en el bit 2, o en el 3... y así hasta el último bit. Por lo tanto, necesitamos **$m+r$** estados para poder apuntar al bit culpable.

### 3. Armamos la inecuación
Si sumamos las situaciones del punto anterior, descubrimos que nuestro panel de alarmas necesita poder mostrar un total de **$(m + r + 1)$** estados diferentes.

Como el panel de alarmas solo puede mostrar **$2^r$** estados, la matemática nos dicta una regla inquebrantable: las combinaciones que *puede* mostrar el panel tienen que ser mayores o iguales a las combinaciones que *necesitamos* que muestre. 

De ahí sale la famosa fórmula final de tu diapositiva:
$$(m + r + 1) \le 2^r$$

*(Nota: La diapositiva hace un paso previo multiplicando por $2^m$ para analizar el total de "palabras codificadas" en el universo posible, pero al simplificar, se reduce exactamente a esta lógica del panel de alarmas, que es mucho más intuitiva).*

### 4. La prueba de fuego (Ejemplo práctico)
Vamos a aplicar la fórmula al ejercicio que resolviste impecablemente hace un momento, el Hamming (7,4).

Teníamos un mensaje de 4 bits ($m = 4$). Queremos saber cuántos bits de paridad ($r$) necesitamos como mínimo. Vamos a probar valores:

* **¿Qué pasa si intentamos usar solo 2 bits de paridad ($r=2$)?**
    Reemplazamos en la fórmula: $(4 + 2 + 1) \le 2^2$
    Resultado: $7 \le 4$. **¡Falso!** Matemáticamente es imposible proteger 4 bits con solo 2 bits de paridad.

* **¿Qué pasa si intentamos usar 3 bits de paridad ($r=3$)?**
    Reemplazamos en la fórmula: $(4 + 3 + 1) \le 2^3$
    Resultado: $8 \le 8$. **¡Verdadero!** (Están justos, al límite).

Por eso el código que usamos se llama Hamming (7,4): 4 de datos, 3 de paridad, 7 en total. La matemática de esta diapositiva es la que justifica esa decisión de diseño en los protocolos de enlace.


Si en el examen te dan un mensaje de un byte completo (8 bits, $m=8$), ¿te animas a calcular con esta fórmula cuántos bits de paridad ($r$) necesitarías agregarle a la trama para asegurar que se pueda corregir cualquier error de un bit?

Es completamente normal que la terminología te frene. En los exámenes de la universidad, los profesores suelen ser muy estrictos con el vocabulario técnico, así que vamos a traducir exactamente lo que dice tu diapositiva para que no te quede ninguna duda.

### 1. ¿De dónde sale el "+1"?
Ese **`+1`** es el estado más importante de todos: **el estado de "No hay ningún error"**.

Piénsalo así: el receptor calcula el Síndrome matemáticamente para buscar errores. El resultado de esa cuenta tiene que poder señalarte dos cosas distintas:
* Si hay un error en el bit 1, o en el bit 2, o en el bit 3... hasta el bit $n$ (eso te da $m + r$ posibilidades).
* **O**, si la trama llegó perfecta. Necesitas un resultado matemático específico (generalmente que el Síndrome dé `0`) para decir "la trama está limpia, no corrijas nada". Ese escenario de éxito es el **`+1`**.

Por eso, el total de estados que tu sistema debe ser capaz de identificar es $(m + r)$ posibles errores **$+$** $1$ estado sin errores.

### 2. El vocabulario del profesor: Mensajes y Palabras Codificadas

Para entender la diapositiva, hay que diferenciar entre lo que tú quieres enviar y lo que realmente viaja por el cable.

* **Mensaje ($m$):** Son los datos puros y útiles que quieres enviar (antes de meterle paridad).
* **Mensajes posibles ($2^m$):** Si tu mensaje tiene $m$ bits, el total de combinaciones diferentes que puedes armar es $2^m$. Por ejemplo, si tu mensaje es de 4 bits ($m=4$), tienes $2^4 = 16$ "mensajes posibles" (desde el `0000` hasta el `1111`).
* **Palabra codificada (Codeword):** Es la trama final y completa. Es tu mensaje original **más** los bits de verificación unidos. Su longitud total es $n$ (donde $n = m + r$). 
* **Cantidad de palabras codificadas ($2^{m+r}$):** Como la trama final tiene $m+r$ bits de largo, el universo total de combinaciones de bits que podrían llegarle al receptor es $2^{m+r}$.



### 3. Descifrando la fórmula completa de la diapositiva

Ahora vamos a leer la fórmula de tu profesor de izquierda a derecha. Es una genialidad matemática que se lee así:

$$2^m \times (m + r + 1) \le 2^{m+r}$$

Imagina que cada mensaje válido es un planeta, y a su alrededor orbitan lunas. Las lunas son las versiones con errores de ese mismo mensaje.

1.  **$2^m$**: Es el número total de planetas (todos tus mensajes originales posibles).
2.  **$(m + r + 1)$**: Es el planeta junto con todas sus lunas. Es decir, la *codeword* válida (1) más todas las *codewords* inválidas que tienen exactamente un bit cambiado ($m+r$). Todo esto forma un "grupo" o "esfera" de combinaciones que le pertenecen exclusivamente a ese mensaje.
3.  **$\le 2^{m+r}$**: Significa "tiene que caber dentro del universo total".

**Traducción final de la ecuación:**
El total de mensajes posibles ($2^m$) multiplicado por el tamaño de la burbuja de errores que cada uno necesita a su alrededor $(m + r + 1)$ **no puede ser más grande** que el total de combinaciones de bits que existen en el universo ($2^{m+r}$).

Como tienes $2^m$ multiplicando a la izquierda y también dentro del $2^{m+r}$ a la derecha, la matemática te permite simplificar la ecuación tachando la base de los mensajes, y te queda la fórmula reducida:

$$(m + r + 1) \le 2^r$$

Con esto, ya tienes la justificación exacta de por qué el material del profesor llega a esa conclusión. Si te lo pregunta en el examen, ahora sabes que se trata de que las "burbujas" de error de cada mensaje válido no se superpongan entre sí.

¿Quieres que resolvamos el cálculo que te propuse antes sobre cuántos bits de paridad se necesitan para un byte completo ($m=8$), o tienes alguna otra diapositiva que quieras que analicemos de esta misma forma?


# Regla de oro

    **La regla de oro del entrelazado:** Si entrelazas $k$ bloques (es decir, creas una matriz de $k$ filas), tu sistema basado en Hamming será capaz de corregir automáticamente un error en ráfaga de hasta **$k$ bits de longitud**.

El código de Hamming estándar **no puede** corregir errores en ráfaga por sí solo. Por diseño matemático, un código de Hamming clásico (como el Hamming 7,4) solo es capaz de detectar y corregir **un único bit erróneo** por cada bloque de datos. Si una ráfaga de ruido voltea 2, 3 o más bits dentro del mismo bloque, las matemáticas de Hamming colapsan y el mensaje se pierde.

Para solucionar esto y aplicar Hamming a los errores en ráfaga, los ingenieros utilizan un truco brillante llamado **Entrelazado (Interleaving)** . 

El entrelazado no cambia la matemática de Hamming, sino que **cambia el orden en el que se envían los bits al cable**. Aquí te explico paso a paso cómo se aplica:

### 1. Generación de los bloques (Matemática normal)
Primero, tomas tu mensaje original y lo divides en varios bloques. A cada bloque le calculas y le agregas sus bits de paridad de Hamming de forma completamente normal e independiente.

Imagina que tienes 4 bloques (A, B, C y D) ya protegidos con Hamming. 

### 2. La Matriz de Entrelazado (El truco)
En lugar de enviar el Bloque A completo, luego el Bloque B, y así sucesivamente, el equipo emisor acomoda los bloques formando una matriz (filas y columnas):

* **Fila 1:** $A_1 \ A_2 \ A_3 \ A_4 \ A_5 \ A_6 \ A_7$ (Bloque A protegido con Hamming)
* **Fila 2:** $B_1 \ B_2 \ B_3 \ B_4 \ B_5 \ B_6 \ B_7$ (Bloque B protegido con Hamming)
* **Fila 3:** $C_1 \ C_2 \ C_3 \ C_4 \ C_5 \ C_6 \ C_7$ (Bloque C protegido con Hamming)
* **Fila 4:** $D_1 \ D_2 \ D_3 \ D_4 \ D_5 \ D_6 \ D_7$ (Bloque D protegido con Hamming)

### 3. Transmisión por Columnas
Aquí está la magia. En lugar de transmitir por filas, **el transmisor lee y envía los datos por columnas** (de arriba hacia abajo). 
El orden exacto que viaja por el cable será:
$$A_1, B_1, C_1, D_1, A_2, B_2, C_2, D_2, A_3, B_3...$$

### 4. El ataque del Ruido (Error en ráfaga)
Supongamos que cae un rayo o hay una interferencia fuerte que destruye **4 bits consecutivos** en el cable durante la transmisión. 
El error golpea exactamente a esta secuencia: **[$C_2, D_2, A_3, B_3$]**.

Si no hubiéramos usado entrelazado, esos 4 bits destruidos habrían caído todos dentro del Bloque A, y Hamming habría fallado miserablemente.

### 5. Recepción y Reensamblaje (Desentrelazado)
El equipo receptor recibe el flujo de datos y vuelve a armar la matriz original acomodando los bits en sus columnas correspondientes.

Al leer las filas nuevamente para aplicar el corrector de Hamming, mira lo que pasó con el error en ráfaga:
* **Fila 1 (Bloque A):** Tiene un error en $A_3$.
* **Fila 2 (Bloque B):** Tiene un error en $B_3$.
* **Fila 3 (Bloque C):** Tiene un error en $C_2$.
* **Fila 4 (Bloque D):** Tiene un error en $D_2$.

**¡La ráfaga se fragmentó!** Lo que era un error masivo de 4 bits consecutivos en el cable, al reensamblar la matriz, se dispersó como **un solo bit erróneo en cada bloque distinto**. 

Como el código de Hamming es perfecto para corregir errores de 1 bit, el receptor aplica la matemática a cada fila individualmente, repara ese único bit dañado en cada bloque, y recupera el 100% del mensaje original a pesar del error en ráfaga.

**La regla de oro del entrelazado:** Si entrelazas $k$ bloques (es decir, creas una matriz de $k$ filas), tu sistema basado en Hamming será capaz de corregir automáticamente un error en ráfaga de hasta **$k$ bits de longitud**.