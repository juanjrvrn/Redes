# Subcapa MAC

## **Ubicación y Función de la Subcapa MAC**
La subcapa MAC (Control de Acceso al Medio, por sus siglas en inglés) tiene una responsabilidad fundamental en las redes de difusión (como las LAN): **decidir qué dispositivo es el siguiente en transmitir** cuando se comparte un enlace de acceso múltiple. 

La diapositiva ilustra este concepto mediante un diagrama de pila de protocolos basado en el modelo OSI. La imagen muestra cómo la capa de **Enlace de Datos** se subdivide internamente. La subcapa MAC se ubica en la parte inferior de esta capa de Enlace, sirviendo como interfaz directa con la capa **Física** subyacente, mientras que por encima de ella se sitúa la subcapa LLC (Control de Enlace Lógico) que se comunica con la capa de **Red**. Esta separación es crucial porque aísla los detalles del medio físico compartido (y sus colisiones) de los protocolos de red de nivel superior (como IP).

## **Asignación del Canal: Estática vs. Dinámica**
El desafío principal que resuelve la subcapa MAC es cómo repartir un único canal de comunicación (un cable, fibra o frecuencia de radio) entre varios usuarios que compiten por él y que causarían interferencia si transmiten a la vez. Existen dos enfoques principales:

**Asignación Estática:** Utiliza esquemas tradicionales como la multiplexación por división de frecuencia (FDM), por tiempo (TDM) o CDMA. En este modelo, si hay $N$ usuarios, el canal se divide en $N$ porciones iguales y exclusivas. 
*   *El problema:* Es sumamente ineficiente para las redes de computadoras debido a la naturaleza en "ráfagas" del tráfico de datos. Si un usuario no tiene nada que transmitir, su ancho de banda reservado se pierde por completo y nadie más puede usarlo. De hecho, matemáticamente (teoría de colas), dividir un canal estáticamente en $N$ subcanales independientes hace que el tiempo medio de retardo para enviar una trama sea $N$ veces peor que tener una única cola compartida.

**Asignación Dinámica:** Es la solución moderna adoptada por las LAN. Se basa en algoritmos dinámicos que otorgan el canal a un usuario únicamente cuando realmente necesita transmitir. Al no desperdiciar tiempo en usuarios inactivos, este enfoque es potencialmente $N$ veces más eficiente que la asignación estática.

## **Supuestos Clave para la Asignación Dinámica**
Para modelar y diseñar los protocolos dinámicos de la subcapa MAC (como ALOHA o CSMA), la teoría se basa en cinco supuestos o condiciones fundamentales sobre cómo interactúan las estaciones:

1.  **Tráfico Independiente (Modelo de Estaciones):** El sistema está compuesto por $N$ estaciones independientes (computadoras, teléfonos, etc.) que generan tramas de forma impredecible. La generación de este tráfico se suele modelar matemáticamente con una distribución de Poisson. Una vez que una estación genera una trama, se bloquea y espera hasta transmitirla con éxito.
2.  **Canal Único:** Todas las estaciones utilizan exactamente el mismo canal físico para transmitir y recibir. No existen vías externas o canales secundarios para coordinarse (como levantar la mano para pedir permiso).
3.  **Detección de Portadora (Carrier Sense) o no:** Define si las estaciones tienen la capacidad tecnológica de "escuchar" el canal antes de actuar. Si tienen esta capacidad, pueden verificar si el canal está libre u ocupado y evitar transmitir sobre una señal existente. Si no la tienen, simplemente transmiten a ciegas.
4.  **Colisiones Observables o no:** Asume que si dos o más estaciones transmiten simultáneamente en el canal único, la superposición de señales destruirá ambas tramas, generando una colisión. El supuesto dicta que las estaciones deben ser capaces de determinar después del hecho si su transmisión fue exitosa o si sufrió una colisión.
5.  **Tiempo Continuo vs. Tiempo Ranurado:** Los protocolos pueden diseñarse para operar en "tiempo continuo", donde una estación puede empezar a transmitir su trama en cualquier instante arbitrario, o en "tiempo ranurado", donde el tiempo se divide en intervalos discretos (ranuras) y las transmisiones solo pueden iniciar al comienzo de una ranura específica.

---
**Siguiente:** [Protocolos de Acceso Múltiple](protocolos_acceso_multiple.md)
