
---
#  Resúmenes — Conceptos Básicos de Redes (Cisco Networking Academy)

> Curso: **Networking Basics** | Plataforma: Cisco NetAcad  
> Módulos: 1 al 17 | Idioma: Español
> Autor: Valentina Diaz

---

## Módulo 1: Comunicación en un mundo conectado

Internet no tiene un "dueño": es una **"red de redes"** que funciona gracias a estándares y protocolos comunes compartidos por todos.

### Clasificación de redes por tamaño

| Tipo | Descripción |
|------|-------------|
| **Doméstica** | Pocos dispositivos conectados en un hogar |
| **SOHO** (Small Office/Home Office) | Permite a trabajadores remotos acceder a una red corporativa |
| **Mediana a Grande** | Corporaciones y escuelas con miles de hosts |
| **Internet** | La red global que conecta cientos de millones de computadoras |

### Clientes, Servidores y P2P

- **Hosts:** Cualquier dispositivo conectado a la red que envía o recibe mensajes.
- **Clientes:** Dispositivos que *solicitan* información (ej. navegador pidiendo una página web).
- **Servidores:** Dispositivos con software especializado para *proporcionar* información (web, email, archivos).
- **Redes P2P (Peer-to-Peer):** Una misma PC actúa como cliente y servidor simultáneamente. Son fáciles de configurar y económicas, pero **no son escalables** y tienen **menor seguridad**.

### Componentes de la infraestructura de red

1. **Dispositivos Finales (Hosts):** Interfaz entre usuario y red (PC, tablets, cámaras, sensores).
2. **Dispositivos Intermedios:** Conectan los dispositivos finales (Switches, Routers, Access Points).
3. **Medios de Red:** El canal por donde viaja la información (cables o aire).

---

## Módulo 2: Componentes, tipos y conexiones de red

Este módulo se enfoca en **cómo** se mueven los datos y cómo nos conectamos a Internet.

### La naturaleza de los datos

- **El Bit:** La unidad más pequeña de datos (0 o 1).
- **Tipos de datos personales:**
  - **Voluntarios:** Lo que compartes explícitamente (redes sociales, formularios).
  - **Observados:** Capturados por tus acciones (ubicación GPS, historial de navegación).
  - **Inferidos:** Resultado del análisis de los anteriores (ej. historial crediticio).

### Métodos de transmisión (señales)

| Medio | Tipo de señal | Canal |
|-------|--------------|-------|
| Eléctrica | Pulsos de electricidad | Cables de **cobre** |
| Óptica | Pulsos de luz | **Fibra óptica** |
| Inalámbrica | Ondas electromagnéticas | **Aire** (microondas, radio, infrarrojos) |

### Ancho de Banda vs. Rendimiento

- **Ancho de Banda:** Capacidad *teórica* de un medio (Kbps, Mbps, Gbps).
- **Rendimiento:** Cantidad *real* de datos transferidos. Se ve reducido por el tráfico y la **latencia** (tiempo que tardan los datos en viajar de un punto a otro).

>  **Dato clave:** El rendimiento casi nunca es igual al ancho de banda.

### Conectividad al ISP

- **ISP (Proveedor de Servicios de Internet):** Tu puente hacia el mundo.
- **Conexiones comunes:** Cable, DSL, datos celulares, satelital y telefonía.
- **El Router doméstico:** "Todo en uno" que incluye switch (cables), AP (Wi-Fi) y seguridad básica.

---

## Módulo 3: Redes inalámbricas y móviles

### Telefonía móvil y redes celulares

Los teléfonos móviles usan ondas de radio para enviar señales de voz a antenas en torres celulares. Al realizarse una llamada, la señal se transmite de torre en torre hasta llegar al destino.

- **Tecnologías celulares:** GSM, 3G, 4G, 4G LTE y 5G representan generaciones de redes con mayor velocidad y eficiencia. Actualmente **4G/LTE** es la más utilizada.
- **Usos:** Llamadas telefónicas, mensajes de texto y transmisión de datos móviles.

### Tipos de conexión inalámbrica en smartphones

| Tecnología | Descripción |
|-----------|-------------|
| **Wi-Fi** | Conecta a redes locales e internet. Puede ser pública o privada. |
| **Bluetooth** | Corto alcance, baja energía. Para accesorios: audífonos, teclados, altavoces. |
| **NFC** | Intercambio de datos a pocos centímetros de distancia. |

### Sistemas operativos móviles

Los más populares son **Android** y **Apple iOS**. Los dispositivos se conectan automáticamente a Wi-Fi disponible; si no hay, usan datos celulares.

### Seguridad en redes Wi-Fi

- No enviar credenciales sin cifrado.
- Usar **VPN** al transmitir datos confidenciales.
- Habilitar seguridad en redes domésticas.
- Usar **WPA2** o cifrado superior para proteger la red.

### Emparejamiento Bluetooth

El proceso de emparejamiento consiste en: activar Bluetooth → buscar dispositivos cercanos → detectar dispositivos en modo visible → autenticarse (a veces con PIN).

---

## Módulo 4: Crear una red doméstica

### Conceptos básicos

Una red doméstica es una pequeña **LAN (Red de Área Local)** donde varios dispositivos se conectan a un router para compartir información y acceder a internet.

- **Red pública:** Proporcionada por el ISP.
- **Red privada:** Dentro del hogar, administrada por el router.

### Dispositivos en una red doméstica

Computadoras, consolas de videojuegos, Smart TVs, impresoras, cámaras de seguridad, termostatos inteligentes, entre otros.

**Puertos comunes de un router doméstico:**
- Puertos **Ethernet** (LAN)
- Puerto **WAN** (conexión al ISP)
- Antenas para **Wi-Fi**

### Tecnologías de red en el hogar

- **Bandas de frecuencia Wi-Fi:** 2.4 GHz (mayor alcance) y 5 GHz (mayor velocidad).
- **Bluetooth:** También usa 2.4 GHz, para comunicación de corto alcance.
- **Estándar:** IEEE 802.11 regula las redes Wi-Fi.

### Tecnologías cableadas

- **Ethernet (UTP):** La más común. Categoría **5e** incluye 4 pares trenzados para reducir interferencias.
- **Redes por línea eléctrica:** Para hogares sin cableado UTP estructurado.

### Configuración del router doméstico

Los ajustes más importantes son:

| Parámetro | Descripción |
|-----------|-------------|
| **Modo de red** | Estándar inalámbrico (802.11b/g/n/ac o modo mixto) |
| **SSID** | Nombre de la red Wi-Fi (todos los dispositivos deben usarlo) |
| **Canal** | Canal de comunicación (recomendado: automático) |
| **Transmisión SSID** | Define si el nombre de la red es visible públicamente |

### Seguridad en redes domésticas

- **Filtrado por MAC:** Controla qué dispositivos pueden conectarse.
- **Red de invitados:** Permite acceso a internet a visitantes sin acceder a la red interna.

---

## Módulo 5: Principios de comunicación

### Reglas de la comunicación

Toda comunicación necesita de **reglas (protocolos)** que determinen: cómo se inicia, cómo se mantiene y cómo se termina una conversación.

En redes, los **protocolos** cumplen esta función. Definen el formato, tamaño, temporización, codificación, encapsulación y proceso de los mensajes.

### Codificación y encapsulación

- **Codificación:** Transformar información en un formato transmisible por el medio.
- **Encapsulación:** Envolver los datos con información de control (encabezados y pies de página) para cada capa del modelo de red.

### Modelos de referencia

- **Modelo OSI (7 capas):** Referencia conceptual para entender cómo viajan los datos.
- **Modelo TCP/IP (4 capas):** Modelo práctico usado en Internet.

| Capas TCP/IP | Equivalente OSI |
|-------------|----------------|
| Aplicación | Aplicación, Presentación, Sesión |
| Transporte | Transporte |
| Internet | Red |
| Acceso a la red | Enlace de datos, Física |

### PDUs (Unidades de datos del protocolo)

Cada capa llama de forma diferente a los datos que maneja:
- **Datos** (capa de aplicación)
- **Segmento** (capa de transporte)
- **Paquete** (capa de red/internet)
- **Trama** (capa de enlace de datos)
- **Bits** (capa física)

---

## Módulo 6: Medios de red

### Tipos de medios de transmisión

1. **Cable de par trenzado (UTP/STP):** Económico, flexible, el más común en LANs. Categorías: Cat5e, Cat6, Cat6a.
2. **Cable de fibra óptica:** Transporta luz en lugar de electricidad. Ideal para largas distancias y alta velocidad. Inmune a interferencias electromagnéticas.
3. **Inalámbrico:** Usa ondas de radio o microondas. Flexible pero susceptible a interferencias.

### Comparación de medios

| Característica | UTP | Fibra Óptica | Inalámbrico |
|---------------|-----|-------------|-------------|
| Velocidad | Media-Alta | Muy Alta | Media |
| Distancia | Corta (~100m) | Larga (km) | Variable |
| Costo | Bajo | Alto | Medio |
| Interferencias | Susceptible | Inmune | Susceptible |

### Normas y estándares

Los medios de red se rigen por estándares internacionales (ISO, IEEE, TIA/EIA) que garantizan compatibilidad entre dispositivos de diferentes fabricantes.

---

## Módulo 7: La capa de acceso

### Función de la capa de acceso

La **capa de acceso** (Enlace de datos + Física en OSI) conecta los hosts a la red. Se encarga de que los datos lleguen correctamente al dispositivo destino dentro de una misma red local.

### Ethernet

**Ethernet** es el estándar dominante para redes LAN cableadas. Define la forma en que los datos se formatean y transmiten a través de la red.

- **Trama Ethernet:** Contiene dirección MAC de origen, dirección MAC de destino, datos y un FCS (verificación de errores).
- **Dirección MAC:** Identificador único de 48 bits (6 bytes en hexadecimal) grabado en la tarjeta de red. Ejemplo: `00:1A:2B:3C:4D:5E`.

### Switches

El **Switch** es el dispositivo central de la capa de acceso:
- Aprende las direcciones MAC de los dispositivos conectados.
- Reenvía las tramas solo al puerto del dispositivo destino (comunicación punto a punto).
- Reduce colisiones al crear dominios de colisión separados por puerto.

>  A diferencia de un **Hub** (que envía datos a todos los puertos), el switch es inteligente y eficiente.

---

## Módulo 8: El Protocolo de Internet (IP)

### Función del protocolo IP

El **Protocolo de Internet (IP)** opera en la capa de red y es responsable del **direccionamiento** y **enrutamiento** de los paquetes de datos desde el origen hasta el destino, incluso a través de múltiples redes.

### Características de IP

- **Sin conexión:** No establece una sesión antes de enviar datos.
- **No confiable:** No garantiza la entrega de paquetes (eso lo hace TCP).
- **Independiente del medio:** Funciona sobre cualquier tipo de red física.

### Estructura de un paquete IPv4

Cada paquete IP contiene: dirección IP de origen, dirección IP de destino, TTL (tiempo de vida) y los datos.

### Direccionamiento IPv4

- Dirección de **32 bits** dividida en 4 octetos: `192.168.1.10`
- Cada dispositivo en red necesita una **dirección IP única**.
- Debe configurarse también la **máscara de subred** y el **gateway predeterminado**.

---

## Módulo 9: Direccionamiento IPv4 y segmentación de red

### Máscara de subred

La **máscara de subred** determina qué parte de la dirección IP corresponde a la **red** y qué parte corresponde al **host**.

- Ejemplo: IP `192.168.1.10` con máscara `255.255.255.0` → Red: `192.168.1.0`, Host: `.10`

### Tipos de direcciones IPv4

| Tipo | Descripción | Ejemplo |
|------|-------------|---------|
| **Unicast** | Un solo destino | `192.168.1.5` |
| **Broadcast** | Todos los hosts de la red | `192.168.1.255` |
| **Multicast** | Grupo específico de hosts | `224.0.0.1` |

### Clases de direcciones y direcciones especiales

- **Privadas (RFC 1918):** No enrutables en Internet. Usadas en redes internas.
  - `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`
- **Loopback:** `127.0.0.1` — prueba interna del adaptador de red.
- **APIPA:** `169.254.x.x` — asignada automáticamente si no hay servidor DHCP disponible.

### Subnetting básico

Dividir una red grande en subredes más pequeñas mejora la seguridad y la eficiencia. La notación **CIDR** (Classless Inter-Domain Routing) se usa para representar la máscara: `192.168.1.0/24`.

---

## Módulo 10: Formatos y reglas de direccionamiento IPv6

### ¿Por qué IPv6?

IPv4 solo permite ~4,300 millones de direcciones. El agotamiento de estas llevó al desarrollo de **IPv6**, que ofrece un espacio de direcciones prácticamente ilimitado.

### Estructura de IPv6

- Dirección de **128 bits** representada en **8 grupos de 4 dígitos hexadecimales**.
- Ejemplo: `2001:0db8:85a3:0000:0000:8a2e:0370:7334`

### Reglas de simplificación

1. **Omitir ceros a la izquierda:** `0db8` → `db8`
2. **Reemplazar grupos de ceros consecutivos con `::`** (solo una vez por dirección).
   - `2001:0db8:0000:0000:0000:0000:0370:7334` → `2001:db8::370:7334`

### Tipos de direcciones IPv6

| Tipo | Descripción |
|------|-------------|
| **Unicast global** | Equivalente a una IPv4 pública |
| **Link-local** | Solo válida en el segmento local (`FE80::/10`) |
| **Multicast** | Para grupos de dispositivos |
| **Loopback** | `::1` |

---

## Módulo 11: Direccionamiento dinámico con DHCP

### ¿Qué es DHCP?

**DHCP (Dynamic Host Configuration Protocol)** asigna automáticamente configuración de red a los dispositivos, eliminando la necesidad de configuración manual.

### Parámetros asignados por DHCP

- Dirección **IP**
- **Máscara** de subred
- **Gateway** predeterminado
- Servidor **DNS**

### Proceso DHCP (DORA)

1. **D**iscover — El cliente busca un servidor DHCP en la red.
2. **O**ffer — El servidor ofrece una dirección IP disponible.
3. **R**equest — El cliente acepta la oferta.
4. **A**cknowledge — El servidor confirma la asignación.

### Ventajas de DHCP

- Elimina errores de configuración manual.
- Centraliza la administración de direcciones IP.
- Ideal para redes grandes donde la configuración manual sería inviable.

>  Si no hay DHCP disponible, el dispositivo puede asignarse una dirección **APIPA** (`169.254.x.x`) automáticamente.

---

## Módulo 12: Gateway hacia otras redes

### Gateway predeterminado

El **gateway predeterminado** (o puerta de enlace) es el router que conecta la red local con otras redes o con Internet. Todo tráfico destinado fuera de la red local pasa por él.

- Si el destino está en la **misma red local** → el paquete se envía directamente.
- Si el destino está en una **red diferente** → el paquete se envía al gateway.

### Función del router

El router examina la dirección IP de destino de cada paquete y consulta su **tabla de enrutamiento** para decidir por dónde enviarlo (próximo salto).

### Comunicación entre redes

Para que dos hosts en diferentes redes se comuniquen, se necesita:
1. Una **dirección IP** correctamente configurada.
2. Una **máscara de subred** correcta.
3. Un **gateway predeterminado** válido.

---

## Módulo 13: El proceso ARP

### ¿Qué es ARP?

**ARP (Address Resolution Protocol)** traduce direcciones IP a direcciones MAC. Es necesario porque dentro de una red local, los datos viajan usando **direcciones MAC** (no IP).

### ¿Cómo funciona?

1. El dispositivo origen necesita la MAC del destino.
2. Envía un **ARP Request** en broadcast a toda la red: *"¿Quién tiene la IP X.X.X.X?"*
3. El dispositivo con esa IP responde con un **ARP Reply** unicast con su dirección MAC.
4. La respuesta se almacena en la **tabla ARP (caché ARP)** para futuras comunicaciones.

### Tabla ARP

La caché ARP almacena temporalmente las correspondencias IP ↔ MAC para evitar consultas repetidas.

```
Interfaz: 192.168.1.5
  Dirección IP    Dirección física   Tipo
  192.168.1.1     00-1A-2B-3C-4D-01  dinámico
  192.168.1.20    00-1A-2B-3C-4D-20  dinámico
```

---

## Módulo 14: Enrutamiento entre redes

### Función del enrutamiento

El **enrutamiento** es el proceso de seleccionar la mejor ruta para enviar paquetes de datos entre redes. El dispositivo que realiza esta función es el **router**.

### Tabla de enrutamiento

El router mantiene una tabla con las rutas conocidas:

| Red destino | Máscara | Próximo salto | Interfaz |
|-------------|---------|--------------|---------|
| 192.168.1.0 | /24 | Conectado directamente | Gi0/0 |
| 10.0.0.0 | /8 | 192.168.1.1 | Gi0/1 |
| 0.0.0.0 | /0 | 203.0.113.1 | Gi0/2 |

### Tipos de rutas

- **Rutas directamente conectadas:** Redes a las que el router está físicamente conectado.
- **Rutas estáticas:** Configuradas manualmente por el administrador.
- **Rutas dinámicas:** Aprendidas automáticamente mediante protocolos de enrutamiento (RIP, OSPF, EIGRP).
- **Ruta predeterminada (`0.0.0.0/0`):** Se usa cuando no existe una ruta específica para el destino (la "ruta de último recurso").

---

## Módulo 15: TCP y UDP

### La capa de transporte

La **capa de transporte** es responsable de la comunicación extremo a extremo entre aplicaciones. Usa dos protocolos principales:

### TCP (Transmission Control Protocol)

Protocolo **orientado a la conexión**, confiable. Garantiza que los datos lleguen completos y en orden.

**Características:**
- Establece conexión con el **saludo de 3 vías** (SYN → SYN-ACK → ACK).
- Usa **números de secuencia** para reensamblar segmentos en orden.
- Solicita retransmisión de paquetes perdidos.
- Control de flujo y congestión.

**Usos:** Navegación web (HTTP/HTTPS), correo electrónico, transferencia de archivos.

### UDP (User Datagram Protocol)

Protocolo **sin conexión**, no confiable pero más rápido.

**Características:**
- No establece sesión previa.
- No garantiza entrega ni orden.
- Menor sobrecarga (encabezado más pequeño).

**Usos:** Streaming de video/audio, videojuegos en línea, DNS, aplicaciones sensibles a la latencia.

### Números de puerto

Los puertos identifican qué aplicación debe recibir los datos:

| Servicio | Protocolo | Puerto |
|---------|----------|--------|
| HTTP | TCP | 80 |
| HTTPS | TCP | 443 |
| FTP | TCP | 21 |
| SSH | TCP | 22 |
| DNS | UDP/TCP | 53 |
| DHCP | UDP | 67/68 |
| SMTP | TCP | 25 |
| POP3 | TCP | 110 |
| IMAP4 | TCP | 143 |

>  Un **socket** = Dirección IP + Número de puerto. Ejemplo: `192.168.1.5:443`

---

## Módulo 16: Servicios de la capa de aplicación

### Función de la capa de aplicación

La **capa de aplicación** es la interfaz entre el usuario y la red. Proporciona los protocolos que permiten a las aplicaciones comunicarse a través de la red.

### Protocolos principales

#### DNS (Domain Name System)
Traduce nombres de dominio legibles (`www.cisco.com`) a direcciones IP (`72.163.4.161`). Sin DNS tendríamos que memorizar IPs.

#### HTTP / HTTPS
- **HTTP** (Puerto 80): Protocolo para transferencia de páginas web.
- **HTTPS** (Puerto 443): Versión segura con cifrado TLS/SSL.
- Una **URL** contiene: protocolo + dominio + ruta del recurso.

#### Correo electrónico
- **SMTP** (Puerto 25): Envío de correos.
- **POP3** (Puerto 110): Descarga de correos del servidor (los elimina del servidor).
- **IMAP4** (Puerto 143): Accede a correos en el servidor sin eliminarlos.

#### FTP (File Transfer Protocol)
Protocolo para transferencia de archivos. Usa dos conexiones: puerto **21** (control) y puerto **20** (datos).

#### HTML
Lenguaje de marcado usado para crear páginas web, que los navegadores interpretan y renderizan.

---

## Módulo 17: Utilidades de prueba de red

### Herramientas de diagnóstico de red

Estas herramientas permiten verificar conectividad, resolver problemas y obtener información sobre la configuración de red.

### Comando `ping`

- **Función:** Prueba la conectividad extremo a extremo entre dos dispositivos usando mensajes ICMP.
- **Resultado:** Tiempo de ida y vuelta (ms) y porcentaje de pérdida de paquetes.
- **Limitación:** Si falla, no indica exactamente dónde está el problema.

```bash
ping 192.168.1.1
ping -4 google.com   # Forzar IPv4
ping -6 google.com   # Forzar IPv6
ping -t google.com   # Ping continuo
ping -a 192.168.1.1  # Resolver a nombre de host
```

### Comando `tracert` / `traceroute`

- **Función:** Muestra la ruta completa (salto a salto) que toman los paquetes hasta el destino.
- **Diferencia con ping:** Identifica en qué router/salto específico hay un problema.
- Envía 3 pings a cada salto y muestra el nombre de dominio e IP de cada uno.

```bash
tracert www.google.com
```

### Comando `ipconfig`

- **Función:** Muestra la configuración IP del adaptador de red.

```bash
ipconfig           # Ver configuración IP
ipconfig /all      # Ver toda la configuración detallada
ipconfig /release  # Liberar dirección IP asignada por DHCP
ipconfig /renew    # Solicitar nueva dirección IP al servidor DHCP
ipconfig /flushdns # Vaciar caché de DNS
ipconfig /displaydns # Ver caché de DNS actual
```

### Comando `netstat`

- **Función:** Muestra todas las conexiones TCP activas establecidas en el equipo.
- Sin opciones: lista todas las conexiones TCP activas.

### Comando `nslookup`

- **Función:** Consulta directamente al servidor DNS para obtener información sobre un dominio.
- Útil para verificar que la resolución de nombres funciona correctamente.

### Resumen de utilidades

| Comando | Función principal |
|---------|------------------|
| `ping` | Probar conectividad con otro host |
| `tracert` | Mostrar la ruta hasta el destino |
| `ipconfig` | Ver/gestionar configuración IP |
| `netstat` | Ver conexiones de red activas |
| `nslookup` | Consultar servidores DNS |

---

##  Resumen General del Curso

| Módulo | Tema |
|--------|------|
| 1 | Comunicación en un mundo conectado |
| 2 | Componentes, tipos y conexiones de red |
| 3 | Redes inalámbricas y móviles |
| 4 | Crear una red doméstica |
| 5 | Principios de comunicación y protocolos |
| 6 | Medios de red |
| 7 | La capa de acceso (Ethernet y Switches) |
| 8 | El Protocolo de Internet (IP) |
| 9 | Direccionamiento IPv4 y segmentación |
| 10 | Formatos y reglas de IPv6 |
| 11 | Direccionamiento dinámico con DHCP |
| 12 | Gateway hacia otras redes |
| 13 | El proceso ARP |
| 14 | Enrutamiento entre redes |
| 15 | TCP y UDP |
| 16 | Servicios de la capa de aplicación |
| 17 | Utilidades de prueba de red |

---

*Resúmenes elaborados con base en el contenido del curso **Networking Basics** de Cisco Networking Academy.*
