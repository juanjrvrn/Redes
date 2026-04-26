Para entender esta comparación a fondo, primero debemos recordar la diferencia fundamental entre ambos conceptos:

* **Tasa de Bits (Bit rate):** Es la cantidad de información lógica (ceros y unos) que transmitimos por segundo. Se mide en **bps**.
* **Tasa de Baudios (Baud rate):** Es la cantidad de *cambios físicos de estado* (símbolos) que ocurren en el medio de transmisión por segundo. Se mide en **baudios**.

La relación matemática que los vincula es:
$$\text{Tasa de Bits} = \text{Tasa de Baudios} \times \log_2(M)$$
Donde $M$ es la cantidad de estados físicos diferentes que el esquema puede representar (niveles de voltaje, fases, etc.). Sin embargo, veremos que algunos códigos sacrifican esta eficiencia máxima matemática para ganar ventajas físicas (como sincronización o eliminación de corriente continua).

A continuación, el análisis completo:

### 1. Transmisión en Banda Base (Códigos de Línea)
La transmisión en banda base consiste en enviar los pulsos eléctricos directamente por el cable de cobre sin utilizar una onda portadora. Aquí manipulamos niveles de voltaje. 

* **Esquemas NRZ (No Retorno a Cero):** * Utilizan solo 2 niveles de voltaje (Ej: +5V para "1" y -5V para "0").
    * Aquí $M = 2$, por lo que $\log_2(2) = 1$.
    * **Relación:** La tasa de baudios es igual a la tasa de bits (1 baudio transporta 1 bit).

* **Esquemas Bipolares (AMI y Pseudoternario):**
    * Estos esquemas utilizan **3 niveles de voltaje** (+V, 0V, -V), por lo que también se les llama esquemas ternarios.
    * **Bipolar AMI (Alternate Mark Inversion):** El bit "0" se representa con 0V (sin señal). El bit "1" se representa alternando voltajes positivos y negativos (+V, luego -V, luego +V...).
    * **Pseudoternario:** Es exactamente el inverso de AMI. El bit "1" se representa con 0V, y el bit "0" se representa alternando voltajes (+V, -V).
    * **La trampa matemática:** Aunque tienen 3 niveles físicos, no los usan para comprimir más datos. Usan ese tercer nivel exclusivamente para balancear la señal eléctrica (eliminar la componente DC) y detectar errores. Por lo tanto, en cada intervalo de tiempo se sigue enviando un solo bit lógico.
    * **Relación:** Al igual que en NRZ, la tasa de baudios es **igual** a la tasa de bits (1 baudio = 1 bit).

* **Esquema Manchester:**
    * Es el código usado en las redes Ethernet clásicas. Para garantizar la sincronización entre emisor y receptor, obliga a que haya una transición física de voltaje en la mitad exacta de cada bit.
    * **Relación:** La tasa de baudios es el **doble** de la tasa de bits (se requieren 2 cambios de voltaje físicos para representar 1 solo bit lógico). Es muy robusto, pero muy ineficiente en el uso del ancho de banda.

### 2. Transmisión en Paso Banda (Modulación Digital)
Ocurre cuando los datos se modulan sobre una onda electromagnética de alta frecuencia (Wi-Fi, ADSL, telefonía celular). Aquí manipulamos la Amplitud, Frecuencia o Fase de la onda. 

* **Esquemas Binarios (ASK, FSK, BPSK):**
    * Solo tienen 2 estados posibles de la onda (ej. Fase a 0° y Fase a 180° en BPSK).
    * **Relación:** 1 baudio = 1 bit. La tasa de baudios es igual a la tasa de bits.

* **Esquemas de Fase Múltiple (QPSK, 8-PSK):**
    * QPSK utiliza 4 fases diferentes ($M = 4$). 
    * **Relación:** 1 baudio transporta 2 bits. La tasa de baudios se reduce a la mitad respecto a los bits. En 8-PSK ($M = 8$), 1 baudio transporta 3 bits.

* **Esquemas QAM (Modulación de Amplitud en Cuadratura):**
    * Combina cambios de fase y amplitud simultáneamente. Es la base de las telecomunicaciones de alta velocidad modernas.
    * **16-QAM:** Tiene 16 estados ($\log_2(16) = 4$). 1 baudio transporta 4 bits.
    * **64-QAM:** Tiene 64 estados ($\log_2(64) = 6$). 1 baudio transporta 6 bits.
    * **256-QAM:** Tiene 256 estados ($\log_2(256) = 8$). 1 baudio transporta 8 bits.

---

### Cuadro Comparativo Resumen

| Esquema de Codificación / Modulación | Dominio    | Niveles Físicos ($M$) | Relación Bits vs Baudios              |
| :----------------------------------- | :--------- | :-------------------- | :------------------------------------ |
| **Manchester**                       | Banda Base | 2                     | Tasa Bits $=$ Tasa Baudios / 2        |
| **NRZ**                              | Banda Base | 2                     | Tasa Bits $=$ Tasa Baudios            |
| **AMI / Pseudoternario**             | Banda Base | 3                     | Tasa Bits $=$ Tasa Baudios            |
| **BPSK / FSK**                       | Paso Banda | 2                     | Tasa Bits $=$ Tasa Baudios            |
| **QPSK**                             | Paso Banda | 4                     | Tasa Bits $=$ Tasa Baudios $\times$ 2 |
| **16-QAM**                           | Paso Banda | 16                    | Tasa Bits $=$ Tasa Baudios $\times$ 4 |
| **256-QAM**                          | Paso Banda | 256                   | Tasa Bits $=$ Tasa Baudios $\times$ 8 |

Este cuadro deja ver claramente que, salvo excepciones diseñadas para sincronización (como Manchester) o balanceo eléctrico (como AMI), la tendencia general en la ingeniería de telecomunicaciones es aumentar los niveles ($M$) en la modulación para empaquetar más bits en cada baudio, manteniendo el medio de transmisión trabajando a velocidades físicas manejables.

Para comparar los anchos de banda físicos que requiere cada familia de códigos de línea, debemos aplicar una regla de oro en telecomunicaciones: **el ancho de banda que exige una señal digital es directamente proporcional a su tasa de baudios** (la cantidad de transiciones o cambios de voltaje físicos por segundo). Cuantos más cambios rápidos de voltaje haya, mayor será la frecuencia de la señal y, por ende, más ancho de banda se consumirá del cable.

A continuación, analizamos cómo se comportan estas tres familias, tomando a los códigos NRZ como nuestra medida base :

### 1. Familia NRZ (NRZ-L y NRZI)
* **Demanda de Ancho de Banda:** Es la **medida base** (la llamaremos $B$).
* **Análisis:** En NRZ (No Retorno a Cero), en el peor de los casos (una secuencia de alternancia rápida como 010101...), hay un cambio de voltaje por cada bit. Por lo tanto, su tasa de baudios máxima es igual a la tasa de bits. 
* **Distribución de la energía:** El gran problema de NRZ no es la cantidad de ancho de banda, sino *dónde* está ubicado. La mayor parte de su energía se concentra en frecuencias muy bajas, acercándose a los 0 Hz (corriente continua o DC). Muchos medios de transmisión (como transformadores o líneas telefónicas) no pueden transmitir frecuencias cercanas a cero, lo que distorsiona la señal.

### 2. Familia Bipolar / Multinivel (Bipolar AMI y Pseudoternario)
* **Demanda de Ancho de Banda:** Es **igual a la base de NRZ** (requiere el mismo ancho de banda $B$).
* **Análisis:** Aunque estos esquemas utilizan tres niveles de voltaje (+V, 0, -V), siguen transmitiendo exactamente un cambio de estado por cada bit. Por lo tanto, su tasa de baudios máxima sigue siendo igual a su tasa de bits.
* **Distribución de la energía (La gran ventaja):** A diferencia de NRZ, la alternancia obligatoria entre voltajes positivos y negativos hace que el espectro de energía se desplace. La energía en 0 Hz cae a cero absoluto (eliminando el problema de la corriente continua) y concentra su mayor fuerza justo en la mitad de la tasa de bits ($R/2$). Es un uso extremadamente eficiente y balanceado del ancho de banda disponible.

### 3. Familia Bifásica (Manchester y Manchester Diferencial)
* **Demanda de Ancho de Banda:** Es el **doble** que los esquemas anteriores (requiere $2B$).
* **Análisis:** El diseño fundamental de los códigos bifásicos obliga a que ocurra una transición de voltaje en el medio exacto de *cada uno de los bits* (para garantizar que el reloj del emisor y el receptor estén siempre sincronizados). Si adicionalmente el bit requiere un cambio al inicio del intervalo, tenemos dos transiciones físicas por cada bit lógico.
* **El costo:** Al tener que cambiar de voltaje el doble de rápido, la tasa de baudios se duplica. En consecuencia, el espectro de frecuencias se ensancha enormemente, exigiendo que el cable tenga el **doble de ancho de banda físico** para transmitir la misma cantidad de datos (bps) que NRZ o AMI.

---

### Cuadro Comparativo de Ancho de Banda

Asumiendo una tasa de transmisión de datos fija (ej. 10 Mbps):

| Esquema de Codificación          | Tasa de Baudios Máxima | Ancho de Banda Requerido | Presencia de Componente DC |
| :------------------------------- | :--------------------- | :----------------------- | :------------------------- |
| **NRZ-L / NRZI**                 | 1 baudio por bit       | Base ($B$)               | Sí (Alta)                  |
| **Bipolar AMI / Pseudoternario** | 1 baudio por bit       | Base ($B$)               | **No** (Nula)              |
| **Manchester / Diferencial**     | 2 baudios por bit      | **El Doble** ($2B$)      | No                         |

**Conclusión técnica:** Los esquemas **Manchester** son excelentes para redes de área local cortas (como el estándar Ethernet original) donde el ancho de banda del cable sobra y la sincronización es la máxima prioridad. Sin embargo, para enlaces de larga distancia donde el ancho de banda es escaso y costoso, se prefieren esquemas como **Bipolar AMI o Pseudoternario**, ya que ofrecen la misma eficiencia de espectro que NRZ pero resolviendo sus problemas eléctricos.