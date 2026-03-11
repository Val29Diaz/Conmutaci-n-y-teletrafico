
---

# Análisis de Red y Diagnóstico de Conectividad

## Taller – Conmutación y Teletráfico

Este documento presenta el análisis del comportamiento de la red en una oficina pequeña mediante herramientas de diagnóstico y captura de tráfico como **Wireshark y CMD de Windows**.

Se analizan protocolos como **TCP, UDP, ARP, SNMP, HTTP, DNS e ICMP**, además del recorrido de un **git push hacia GitHub**.

---

# Primer Punto – Análisis de Protocolos de Red

## a) Comparación entre TCP y UDP en transmisión de video

Cuando una aplicación transmite video puede utilizar **TCP o UDP**.

### Comparación de cabeceras

| Protocolo | Tamaño cabecera | Características                  |
| --------- | --------------- | -------------------------------- |
| UDP       | 8 bytes         | No establece conexión            |
| TCP       | mínimo 20 bytes | Confiable y orientado a conexión |

### Throughput

**UDP es más eficiente en throughput**, ya que:

* tiene menor tamaño de cabecera
* no realiza handshake
* no utiliza retransmisiones

Esto reduce la sobrecarga en la transmisión.

### Control de pérdida de paquetes

**TCP ofrece mayor control sobre la pérdida de paquetes** porque incluye en su cabecera:

* Número de secuencia
* Número de confirmación (ACK)
* Control de flujo
* Control de congestión

Estos mecanismos permiten detectar paquetes perdidos y retransmitirlos.

### Conclusión

En transmisión de **video en tiempo real** suele usarse **UDP**, ya que es preferible perder algunos paquetes antes que detener la transmisión esperando retransmisiones.

---

# b) Protocolo que llena la tabla ARP

Cuando ejecutamos el comando:

```bash
arp -a
```

Windows muestra una tabla con direcciones **IP y MAC**.

### Protocolo responsable

El protocolo que llena esta tabla es **ARP (Address Resolution Protocol)**.

### Función principal

ARP se encarga de **traducir direcciones IP a direcciones MAC dentro de una red local**.

### Funcionamiento

1. Un dispositivo quiere enviar datos a una IP.
2. Verifica si la MAC está en la tabla ARP.
3. Si no está, envía un **ARP Request** en broadcast.
4. El dispositivo con esa IP responde con **ARP Reply** indicando su MAC.

### Relación con la trama Ethernet

La cabecera Ethernet contiene:

| Campo       | Función                      |
| ----------- | ---------------------------- |
| MAC destino | Identifica el receptor       |
| MAC origen  | Identifica el emisor         |
| Tipo        | Indica protocolo encapsulado |

ARP permite llenar el campo **MAC destino**, necesario para que la trama Ethernet llegue al dispositivo correcto.

---

# c) Diferencias entre SNMPv2c y SNMPv3

### Seguridad

| Versión | Seguridad                            |
| ------- | ------------------------------------ |
| SNMPv2c | Usa community strings en texto plano |
| SNMPv3  | Autenticación y cifrado              |

SNMPv2c utiliza comunidades como:

```
public
private
```

Pero estas se transmiten sin cifrado.

SNMPv3 introduce:

* autenticación
* cifrado
* control de usuarios

---

### Tipo de mensajes

SNMPv2c introdujo el mensaje **GetBulk**, que permite consultar grandes cantidades de datos de la MIB.

SNMPv3 mantiene estos mensajes pero agrega diferentes niveles de seguridad:

| Nivel        | Característica          |
| ------------ | ----------------------- |
| noAuthNoPriv | sin autenticación       |
| authNoPriv   | autenticación           |
| authPriv     | autenticación + cifrado |

---

# d) OID y MIB

### MIB

La **MIB (Management Information Base)** es una base de datos jerárquica que contiene información de los dispositivos de red.

### OID

El **OID (Object Identifier)** es el identificador único que apunta a un objeto dentro de la MIB.

Ejemplo:

```
1.3.6.1.2.1.2.2.1.10
```

Este OID puede representar un contador de bytes recibidos.

---

### Operación SNMP para consultar bytes recibidos

El administrador debe utilizar la operación:

```
GET
```

Esto permite consultar el valor actual del contador.

---

### Por qué no usar Trap

Un **Trap** es una notificación automática enviada cuando ocurre un evento importante.

Ejemplos:

* caída de una interfaz
* fallo de autenticación
* error crítico

No es adecuado usar Trap para contar bytes porque el valor cambia constantemente.

---

# Segundo Punto – Análisis de Captura con Wireshark

Supongamos que encontramos el siguiente paquete HTTP.

```
Ethernet II
IPv4
TCP
HTTP GET
```

---

# a) Cabecera Ethernet

| Campo            | Descripción                     |
| ---------------- | ------------------------------- |
| MAC destino      | Dirección física del receptor   |
| MAC origen       | Dirección física del emisor     |
| Tipo (EtherType) | Indica el protocolo encapsulado |

### Significado de 0x0800

El valor **0x0800** indica que el protocolo encapsulado es **IPv4**.

---

# b) Cabecera IPv4

### Campo Protocolo

Indica qué protocolo de transporte contiene el paquete.

| Valor | Protocolo |
| ----- | --------- |
| 1     | ICMP      |
| 6     | TCP       |
| 17    | UDP       |

---

### Campo TTL (Time To Live)

El TTL indica el número máximo de routers que puede atravesar un paquete.

Cada router reduce el TTL en **1**.

Cuando llega a **0**, el paquete se descarta.

Esto evita que los paquetes circulen indefinidamente por la red.

---

# c) Cabecera TCP

### Flag ACK

Confirma la recepción de datos anteriores.

### Flag PSH

Indica que los datos deben enviarse inmediatamente a la aplicación.

---

### Puerto destino 80

El puerto **80** corresponde al protocolo **HTTP**.

Esto indica que el cliente está intentando acceder a un servidor web.

---

# d) Si el paquete fuera IPv6

La cabecera IPv4 sería reemplazada por una **cabecera IPv6**.

### Mejora de IPv6

IPv6 tiene:

* cabecera fija de **40 bytes**
* estructura más simple

Esto permite que los routers procesen paquetes más rápido.

---

# Tercer Punto – Diagnóstico con herramientas de Windows

## Comando

```
pathping 8.8.8.8
```

---

# Información que proporciona

Pathping combina funcionalidades de:

* **ping**
* **tracert**

Permite conocer:

* ruta hacia el destino
* latencia por salto
* pérdida de paquetes por router

---

# Funcionamiento de pathping

El proceso ocurre en dos fases.

### Fase 1 – Descubrimiento de ruta

Funciona como **tracert** para identificar los routers intermedios.

### Fase 2 – Análisis de pérdida

Envía múltiples paquetes ICMP a cada salto para medir:

* latencia promedio
* porcentaje de pérdida

---

# Monitoreo SNMP

```
snmpwalk -v2c -c public 192.168.1.1
```

---

# Trap authenticationFailure

Este Trap ocurre cuando alguien intenta acceder al agente SNMP con una **comunidad incorrecta**.

### Ventaja de los Traps

Los Traps permiten que el dispositivo envíe notificaciones automáticamente.

Esto evita tener que consultar constantemente el estado del router mediante polling.

---

# Cuarto Punto – El viaje de un Commit a GitHub

## Flujo general

```
Computador
   │
   │ DNS
   ▼
Servidor DNS
   │
   ▼
Router local
   │
   ▼
Internet
   │
   ▼
Servidor GitHub
```

---

# Modelo OSI aplicado al git push

| Capa OSI   | Función en el proceso     | Protocolos         |
| ---------- | ------------------------- | ------------------ |
| Aplicación | Comunicación con GitHub   | HTTP / HTTPS / DNS |
| Transporte | Conexión confiable        | TCP                |
| Red        | Enrutamiento de paquetes  | IP / ICMP          |
| Enlace     | Comunicación en red local | Ethernet / ARP     |
| Física     | Transmisión de bits       | Cable / WiFi       |

---

# Paso 1 – Verificación de conectividad

```
ping github.com
```

### Capa OSI

Capa **3 – Red**

### Protocolo

**ICMP**

---

# Resolución DNS

```
nslookup github.com
```

### Protocolo

**DNS**

### Capa OSI

Capa **7 – Aplicación**

---

# Impacto de latencia alta

| Métrica    | Significado                |
| ---------- | -------------------------- |
| Latencia   | tiempo de llegada          |
| Jitter     | variación en latencia      |
| Throughput | velocidad de transferencia |

Una latencia alta puede hacer que el **git push sea más lento**.

---

# Paso 2 – Establecimiento de conexión

Git utiliza **HTTPS**, que funciona sobre **TCP**.

### Three Way Handshake

```
Cliente → SYN
Servidor → SYN-ACK
Cliente → ACK
```

---

# Puertos utilizados

| Puerto         | Función        |
| -------------- | -------------- |
| Puerto origen  | puerto efímero |
| Puerto destino | 443 (HTTPS)    |

---

# Paso 3 – Encapsulamiento de datos

## Proceso de encapsulamiento

```
Datos (Aplicación)
        ↓
Segmento TCP (Transporte)
        ↓
Paquete IP (Red)
        ↓
Trama Ethernet (Enlace)
        ↓
Bits transmitidos (Física)
```

---

# Congestión en routers

Si un router descarta paquetes:

* el git push se vuelve lento
* TCP retransmite datos

Comandos para detectar problemas:

```
tracert github.com
```

```
pathping github.com
```

---

# Campo que evita bucles

El campo **TTL** evita que los paquetes circulen indefinidamente en la red.

Cada router reduce su valor hasta llegar a cero.

---

# Paso 4 – Confirmación y cierre

### Confirmación de datos

TCP utiliza **ACK** para confirmar la recepción.

Si un paquete se pierde, TCP lo retransmite.

Esto garantiza la **fiabilidad**.

---

# Cierre de conexión TCP

```
Cliente → FIN
Servidor → ACK
Servidor → FIN
Cliente → ACK
```

---

# Monitoreo SNMP del tráfico

Un administrador podría monitorear:

| Métrica              | Descripción      |
| -------------------- | ---------------- |
| Bytes transmitidos   | tráfico enviado  |
| Bytes recibidos      | tráfico recibido |
| Paquetes descartados | congestión       |
| Errores de interfaz  | problemas de red |

Si se requiere cifrado se debe usar:

**SNMPv3**

---

# Conclusión

El análisis demuestra cómo múltiples protocolos y herramientas interactúan para permitir la comunicación en redes modernas.

El uso de herramientas como **Wireshark, ping, tracert, pathping y SNMP** permite diagnosticar problemas de conectividad y comprender el comportamiento del tráfico en la red.











