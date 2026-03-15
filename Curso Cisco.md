
---

##  Resumen Módulo 1: Comunicación en un mundo conectado

En esta parte aprendí que Internet no tiene un "dueño", sino que es una **"red de redes"** que funciona gracias a estándares comunes.

### 1. Clasificación de Redes por Tamaño

* **Redes Domésticas:** Pocos dispositivos conectados.
* **SOHO (Small Office/Home Office):** Permite a trabajadores remotos conectarse a una red corporativa.
* **Redes Medianas a Grandes:** Corporaciones y escuelas con miles de hosts.
* **Internet:** La red global que conecta cientos de millones de computadoras.

### 2. Clientes, Servidores y P2P

* **Hosts:** Cualquier dispositivo conectado a la red que envía o recibe mensajes.
* **Clientes:** Dispositivos que solicitan información (ej. tu navegador pidiendo una web).
* **Servidores:** Dispositivos con software específico para proporcionar información (web, email, archivos).
* **Redes P2P (Peer-to-Peer):** Una misma PC actúa como cliente y servidor al mismo tiempo. Son fáciles de configurar y baratas, pero **no son escalables** y tienen **menos seguridad**.

### 3. Componentes de la Infraestructura

La red se divide en tres categorías de hardware:

1. **Dispositivos Finales (Hosts):** La interfaz entre el usuario y la red (PC, tablets, cámaras de seguridad, sensores).
2. **Dispositivos Intermedios:** Conectan los dispositivos finales (Switches, Routers, Access Points).
3. **Medios de Red:** El canal por donde viaja la información (cables o aire).

---

##  Resumen Módulo 2: Componentes, tipo y conexiones de red

Aquí el enfoque cambia hacia **cómo** se mueven los datos y cómo nos conectamos al mundo.

### 1. La Naturaleza de los Datos

* **El Bit:** La unidad más pequeña de datos (0 o 1).
* **Tipos de Datos Personales:**
* **Voluntarios:** Lo que compartes explícitamente (perfiles sociales).
* **Observados:** Capturados por tus acciones (ubicación GPS).
* **Inferidos:** Basados en el análisis de los anteriores (como tu historial crediticio).



### 2. Métodos de Transmisión (Señales)

Los bits viajan de tres formas principales:

* **Eléctricas:** Pulsos de electricidad en cables de **cobre**.
* **Ópticas:** Pulsos de luz en **fibra óptica**.
* **Inalámbricas:** Ondas electromagnéticas (microondas, radio, infrarrojos) a través del **aire**.

### 3. Ancho de Banda vs. Rendimiento

* **Ancho de Banda:** Capacidad teórica de un medio para transportar datos (se mide en Kbps, Mbps, Gbps).
* **Rendimiento:** La cantidad real de datos transferidos. Se ve afectado por el tráfico y la **latencia** (el tiempo que tardan los datos en viajar de un punto a otro).

### 4. Conectividad al ISP

El **ISP (Proveedor de Servicios de Internet)** es tu puente hacia el mundo.

* **Conexiones comunes:** Cable, DSL, datos celulares, satelital y telefonía.
* **El Router doméstico:** Es un "todo en uno" que incluye un switch (para cables), un AP (para Wi-Fi) y seguridad básica.

---

> **Dato clave:** El **rendimiento** casi nunca es igual al **ancho de banda** debido a la latencia y la congestión de la red.

## Resumen módulos 3 y 4 del curso corto de Cisco: Conceptos básicos de redes

### Módulo 3: Redes inalámbricas y móviles

### Redes inalámbricas y telefonía móvil

Los teléfonos móviles utilizan ondas de radio para enviar señales de voz a antenas ubicadas en torres celulares dentro de áreas geográficas específicas. Cuando se realiza una llamada, la señal se transmite de una torre a otra hasta llegar al destino.

Las redes celulares se utilizan para realizar llamadas telefónicas, enviar mensajes de texto y transmitir datos móviles.

Una de las redes celulares más comunes es GSM. Las tecnologías 3G, 4G, 4G LTE y 5G representan diferentes generaciones de redes móviles diseñadas para mejorar la velocidad y la eficiencia en la transmisión de datos. Actualmente, 4G es la red más utilizada por la mayoría de los teléfonos.

### Conexiones inalámbricas en smartphones

Los teléfonos inteligentes pueden conectarse a redes y dispositivos de varias formas:

**Wi-Fi:** permite conectar el teléfono a redes locales y a internet. Las redes Wi-Fi pueden ser privadas o públicas. Un hotspot o zona de cobertura es un área donde hay señal Wi-Fi disponible.

**Bluetooth:** es una tecnología inalámbrica de corto alcance que permite conectar dispositivos entre sí y compartir recursos. Consume poca energía y se utiliza para conectar accesorios como auriculares, teclados, mouse, altavoces y sistemas de audio.

**NFC (Near Field Communication):** es una tecnología de comunicación inalámbrica que permite intercambiar datos entre dispositivos que se encuentran muy cerca entre sí, generalmente a pocos centímetros de distancia.

### Sistemas operativos móviles

Los sistemas operativos móviles más populares son Android y Apple iOS.

Los dispositivos móviles generalmente se conectan automáticamente a una red Wi-Fi disponible. Si no hay Wi-Fi disponible, utilizan la red de datos celulares para conectarse a internet.

### Seguridad en redes Wi-Fi

Para proteger las comunicaciones en redes inalámbricas se recomiendan las siguientes prácticas:

* No enviar información de inicio de sesión o contraseñas sin cifrado.
* Utilizar una conexión VPN cuando se transmiten datos confidenciales.
* Habilitar la seguridad en las redes domésticas.
* Utilizar WPA2 o un cifrado superior para proteger la red.

### Emparejamiento Bluetooth

El emparejamiento Bluetooth ocurre cuando dos dispositivos establecen una conexión para compartir recursos.

El proceso consiste en activar Bluetooth en los dispositivos, buscar dispositivos cercanos y detectar aquellos que estén en modo visible. Durante la detección, el dispositivo transmite información como el nombre, la clase de Bluetooth, los servicios disponibles y características técnicas.

Durante el proceso de emparejamiento puede solicitarse un PIN para autenticar la conexión entre los dispositivos.

---

### Módulo 4: Crear una red doméstica

### Conceptos básicos de redes domésticas

Una red doméstica es una pequeña red de área local (LAN) donde varios dispositivos se conectan a un router para compartir información y acceder a internet.

Generalmente existen dos redes:

* Una red pública proporcionada por el proveedor de servicios de internet.
* Una red privada dentro del hogar.

El router doméstico normalmente incluye conectividad cableada e inalámbrica.

### Dispositivos en una red doméstica

En una red doméstica pueden conectarse diferentes dispositivos, entre ellos:

* Computadoras de escritorio y portátiles
* Consolas de videojuegos
* Televisores inteligentes
* Impresoras y escáneres
* Cámaras de seguridad
* Dispositivos de control de temperatura y otros dispositivos inteligentes

Los routers domésticos suelen incluir dos tipos principales de puertos:

* Puertos Ethernet
* Puertos de internet (WAN)

Además, muchos routers incorporan antenas y un punto de acceso inalámbrico.

### Tecnologías de red en el hogar

Las redes inalámbricas utilizan ondas electromagnéticas para transportar información entre dispositivos. Estas ondas forman parte del espectro electromagnético.

Las redes domésticas utilizan principalmente las bandas de frecuencia de 2.4 GHz y 5 GHz.

Bluetooth también utiliza la banda de 2.4 GHz para comunicación de corto alcance.

Las redes Wi-Fi utilizan estándares IEEE 802.11 y ofrecen mayor alcance y rendimiento que Bluetooth.

### Tecnologías cableadas

Aunque muchas redes domésticas usan Wi-Fi, algunas aplicaciones se benefician de conexiones cableadas.

La tecnología cableada más común es Ethernet, que utiliza cables de par trenzado no blindado (UTP). El cableado más común es de categoría 5e, que incluye cuatro pares de cables trenzados para reducir interferencias.

En hogares sin cableado UTP se pueden utilizar tecnologías como redes a través de líneas eléctricas para distribuir la conectividad.

### Estándares inalámbricos

El estándar IEEE 802.11 regula las redes LAN inalámbricas. Estas redes utilizan las bandas de frecuencia de 2.4 GHz y 5 GHz y se conocen comúnmente como Wi-Fi.

La Wi-Fi Alliance certifica dispositivos inalámbricos de diferentes fabricantes para asegurar compatibilidad.

### Configuración de redes Wi-Fi

Los routers inalámbricos incluyen varios ajustes importantes:

**Modo de red:** define el estándar inalámbrico utilizado, como 802.11b, 802.11g, 802.11n o modo mixto.

**SSID:** es el nombre de la red inalámbrica. Todos los dispositivos que desean conectarse deben utilizar el mismo SSID.

**Canal:** define el canal de comunicación inalámbrica. Normalmente se configura en automático para que el router seleccione el mejor canal.

**Transmisión de SSID:** determina si el nombre de la red se muestra públicamente a los dispositivos cercanos.

### Velocidad y compatibilidad

El máximo rendimiento se obtiene cuando todos los dispositivos utilizan el mismo estándar Wi-Fi. En modo mixto se permite la conexión de dispositivos con diferentes estándares, aunque puede afectar la velocidad.

### Configuración de un router doméstico

Para configurar un router doméstico generalmente se siguen estos pasos:

1. Conectar una computadora al router mediante un cable Ethernet.
2. Conectar el cable al puerto LAN del router.
3. Verificar que las luces de la tarjeta de red indiquen conexión.
4. Obtener automáticamente una dirección IP mediante DHCP.
5. Acceder al router a través de un navegador web para realizar la configuración.

### Planificación de la red

Antes de configurar la red es recomendable definir el nombre de la red (SSID), identificar los dispositivos que se conectarán y establecer las políticas de seguridad.

### Seguridad en redes domésticas

Muchos routers permiten utilizar filtrado de direcciones MAC para controlar qué dispositivos pueden conectarse a la red inalámbrica.

También es posible configurar una red de invitados, que permite acceso a internet para visitantes pero restringe el acceso a los dispositivos internos de la red doméstica.
