# **Arquitectura de Red IEEE 802.11**

El estándar **IEEE 802.11** define bloques de construcción específicos para estructurar la comunicación. Se clasifican exhaustivamente de la siguiente manera:

## **BSS (Basic Service Set - Conjunto de Servicio Básico)**
Es el bloque de construcción fundamental de la arquitectura Wi-Fi. Un **BSS** define un grupo de estaciones que se comunican entre sí. Según las imágenes de la diapositiva y la teoría, el BSS puede operar en **dos modos de clasificación estricta**:

*   **Modo 1: Red Ad hoc (BSS sin un AP)**
    *   **Características Técnicas:** Es una colección de computadoras o dispositivos que se asocian de manera independiente para enviarse tramas de datos directamente entre ellos. No existe una infraestructura central ni un punto de acceso que coordine el tráfico.
    *   **Detalle de la Imagen:** En los esquemas de la diapositiva, este modo se representa mediante un rectángulo punteado que contiene varias estaciones (computadoras) con flechas que las interconectan de forma directa, demostrando la ausencia total de un dispositivo coordinador.
    *   **Ejemplo:** Dos computadoras portátiles en una sala de reuniones que se conectan entre sí temporalmente para transferir un archivo sin usar el Wi-Fi del edificio.

*   **Modo 2: Modo Infraestructura (BSS con un AP)**
    *   **Características Técnicas:** Todas las estaciones se comunican a través de un nodo coordinador centralizado. Este nodo central es el **AP (Access Point - Punto de Acceso)**. En este modo, las estaciones no se hablan directamente; todo el tráfico, incluso entre dos computadoras en la misma red local, pasa obligatoriamente por el AP.
    *   **Detalle de la Imagen:** El diagrama ilustra este modo con un BSS en el cual todas las computadoras tienen flechas de comunicación que apuntan exclusivamente hacia un dispositivo central (típicamente representado como una caja verde con una antena, etiquetada como "AP").

## **ESS (Extended Service Set - Conjunto de Servicio Extendido)**
Cuando la cobertura de un solo **BSS** no es suficiente (por ejemplo, para cubrir todo un campus universitario o un edificio de oficinas), el estándar permite crear una red de mayor alcance interconectando múltiples BSS.

*   **Características Técnicas:** Un **ESS** es la unión de varios **BSS** en modo infraestructura. Esto permite a los clientes móviles moverse y enviar tramas a otros clientes a través de sus respectivos APs.
*   **DS (Distribution System - Sistema de Distribución):** Es la red cableada que sirve como espina dorsal para conectar los múltiples APs. 
*   **Detalle de la Imagen:** El diagrama avanzado de arquitectura muestra un **ESS** donde tres **BSS** independientes (cada uno con su propio **AP** verde) están conectados hacia arriba a una red principal. El **DS** se ilustra como un gran óvalo central (generalmente de color amarillo), al cual también puede conectarse un servidor o una pasarela (**Gateway**) para dar salida a Internet o a la red corporativa.

## **Identificación de la Red: El SSID**
Para que los usuarios y dispositivos puedan distinguir y conectarse a estas arquitecturas, el estándar implementa un sistema de identificación pública.

*   **SSID (Service Set Identifier - Identificador de Conjunto de Servicio):** 
    *   **Características Técnicas:** Es el nombre público que identifica a la red inalámbrica. Técnicamente, este identificador se transmite en las tramas de administración conocidas como "balizas" (*Beacons*) emitidas por el **AP**.
    *   **Detalle Técnico y Seguridad:** Aunque el AP difunde constantemente las balizas para anunciar la red, el estándar permite que el **SSID** se difunda o se oculte. Si el administrador decide no difundir el **SSID**, la red se vuelve "invisible" y la estación cliente debe conocer el nombre exacto de antemano para poder enviar una solicitud de asociación al **AP**.

Siguiente [Evolucion del estándar 802.11 (evolucion_wifi.md)](evolucion_wifi.md)
