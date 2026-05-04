¡Excelente! Sigamos avanzando en nuestra guía de estudio con el rigor que nos caracteriza. Para completar de forma exhaustiva el **Punto 1.5 del esquema**, nos adentraremos en los mecanismos que hacen que las redes Wi-Fi sean eficientes en consumo de batería, justas en la distribución del ancho de banda y ricas en funcionalidades. 

Alineándome a nuestra **Regla de Oro**, desglosaré cada técnica, fórmula, ventaja y acrónimo presente en la **Diapositiva 9** y en la literatura técnica complementaria del Capítulo 4.

---

### **1. Técnicas de Ahorro de Energía en Redes Inalámbricas**

La duración de la batería es un problema crítico en dispositivos móviles. El estándar **IEEE 802.11** define exhaustivamente dos métodos para que las estaciones no malgasten energía escuchando un canal inactivo:

#### **A. PSM (Power Save Mode - Modo de Ahorro de Energía)**
Es el mecanismo clásico establecido en las primeras versiones del estándar.
*   **Características de Funcionamiento:** 
    1.  El host (cliente) avisa explícitamente al **AP (*Access Point* - Punto de Acceso)** que entrará en modo de ahorro de energía (dormirá).
    2.  El AP deja de enviarle tramas y las almacena en un búfer de memoria temporal.
    3.  El AP emite periódicamente (típicamente cada 100 ms) tramas de administración llamadas **Balizas (*Beacons*)**.
    4.  El *Beacon* incluye un "mapa de tráfico" (*Traffic Indication Map*). 
    5.  El host despierta periódicamente solo para leer el *Beacon*. Si el mapa indica que hay paquetes almacenados para él, el host se despierta por completo y envía un mensaje de sondeo, específicamente una trama **PS-Poll (*Power Save-Poll*)**, para que el AP se los entregue.

#### **B. APSD (Automated Power Save Delivery - Entrega Automatizada de Ahorro de Energía)**
Introducido en la enmienda **IEEE 802.11e** (Año 2005), es un mecanismo mucho más avanzado.
*   **Características de Funcionamiento:** 
    *   Define un "periodo de servicio" (*Service Period*).
    *   El AP envía tramas al cliente en dos instancias:
        *   a) Durante los periodos de servicio programados (*Scheduled APSD*).
        *   b) Justo después de recibir tramas enviadas por el propio cliente (*Unscheduled APSD*).
*   **Ventajas:** 
    *   Es significativamente más eficiente que el PSM tradicional.
    *   Funciona de manera excelente para aplicaciones como **VoIP (*Voice over IP* - Voz sobre IP)**, donde hay tráfico bidireccional muy frecuente (ej. cada 20 ms), permitiendo que el dispositivo duerma profundamente entre esos breves intervalos sin esperar a la baliza de los 100 ms.

---

### **2. Técnicas de Calidad de Servicio (QoS - *Quality of Service*)**

Para evitar que una descarga pesada interrumpa una llamada de voz o un video, el estándar **IEEE 802.11e** (2005) modificó el protocolo MAC agregando reglas estrictas de prioridad. Se divide en dos técnicas fundamentales:

#### **A. Intervalos AIFS (*Arbitration Inter Frame Space* - Espacio de Inter-Trama de Arbitraje)**
Reemplaza al tiempo de espera predeterminado (DIFS) para crear jerarquías de tráfico. Además, define nuevos valores variables para la ventana de contención **CW (*Contention Window*)** según el tipo de dato.
*   **AIFS1 (Alta Prioridad):** Es un intervalo corto (menor que DIFS pero mayor que SIFS). Lo utiliza el AP para el tráfico crítico de voz o video. Al tener que esperar menos tiempo de silencio, estas tramas "saltan" al frente de la cola y le ganan el canal a los datos normales.
*   **AIFS4 (Baja Prioridad):** Es un intervalo largo (mayor que DIFS). Se utiliza para el tráfico de fondo (ej. descargas grandes o actualizaciones). Obliga a este tráfico a esperar más, cediendo el paso a las tramas normales.

#### **B. TXOP (*Transmission Opportunity* - Oportunidad de Transmisión)**
*   **El Problema Matemático: La Anomalía de la Tasa de Datos (*Rate Anomaly*):** En el CSMA/CA clásico, las estaciones se turnan enviando *una trama por vez*. Si una estación rápida (ej. a 54 Mbps) compite con una lenta (ej. a 6 Mbps), la rápida se pasa la vida esperando a que la lenta termine de hablar. **Fórmula/Resultado:** Ambas terminarán obteniendo un *throughput* promedio idéntico y deficiente (ej. 5.4 Mbps), penalizando injustamente al equipo rápido.
*   **La Solución TXOP:** En lugar de ceder el canal "por trama", se cede el canal **por un periodo de tiempo equitativo (tiempo de aire)**. 
*   **Ventaja Técnica:** Durante su TXOP, la estación de 54 Mbps puede enviar una ráfaga masiva de paquetes, mientras que la de 6 Mbps apenas enviará uno. Las tasas de salida se distribuyen equitativamente (ej. el lento obtiene 3 Mbps y el rápido obtiene 27 Mbps, salvando el rendimiento de la red).

---

### **3. Clasificación Exhaustiva de los Servicios IEEE 802.11**

De acuerdo con la tabla de las imágenes de la presentación y la literatura técnica, el estándar provee **9 servicios obligatorios**, clasificados según el proveedor que los ejecuta:

#### **Servicios provistos por el Sistema de Distribución (DS - *Distribution System*)**
1.  **Asociación (*Association*):** Utilizado por la estación móvil para conectarse a un AP al entrar en su área. Aprende capacidades (velocidad, seguridad) y el **SSID (*Service Set Identifier*)**.
2.  **Reasociación (*Reassociation*):** Permite a una estación cambiar de su AP actual a un nuevo AP dentro de la misma red (traspaso o *handover*), idealmente sin perder datos.
3.  **Disociación (*Disassociation*):** Pone fin a la relación. La estación lo usa antes de apagarse, o el AP lo usa antes de mantenimiento. 
4.  **Distribución (*Distribution*):** Determina cómo enrutar la trama cuando llega al AP (si se envía por el aire a un cliente local o por el cable a la red principal).
5.  **Integración (*Integration*):** Maneja las traducciones necesarias para sacar una trama de la red 802.11 hacia una red externa (por ejemplo, hacia Internet a través de un enrutador).

#### **Servicios provistos por la Estación (*Station*)**
6.  **Autenticación (*Authentication*):** Provee acceso a la LAN y seguridad. Históricamente usaba **WEP (*Wired Equivalent Privacy*)** (hoy obsoleto e inseguro). Actualmente usa **WPA (*Wi-Fi Protected Access*)** o **IEEE 802.1X** (que permite uso de contraseñas complejas o chips telefónicos mediante **EAP-SIM**).
7.  **Desautenticación (*Deauthentication*):** Revoca el acceso a la red de una estación.
8.  **Privacidad (*Privacy*):** Consiste en el cifrado y encriptación de la capa de enlace para evitar espionaje del tráfico aéreo.
9.  **Entrega de MSDU (*MSDU delivery - MAC Service Data Unit*):** Es el servicio puro de entrega de datos entre estaciones. **Características:** Es de tipo "mejor esfuerzo" (*best-effort*), lo que significa que la subcapa MAC *no garantiza* la entrega confiable al 100%; los errores los corrigen las capas superiores (como TCP).

*(Nota adicional del estándar: Otros servicios complementarios menores incluyen la Sincronización de Temporizadores, el Control de Potencia de Transmisión para cumplir normas legales, y la Selección Dinámica de Frecuencias para no interferir con radares militares o meteorológicos en la banda de 5 GHz).*
