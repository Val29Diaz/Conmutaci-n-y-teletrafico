

---

# Parcial – Conmutación y Teletráfico

Repositorio con el desarrollo del Parcial de análisis de protocolos de red, cabeceras de paquetes, monitoreo SNMP y diagnóstico de conectividad antes de realizar un `git push` hacia GitHub.

---

# 1. Comparación entre TCP y UDP en transmisión de video

## Throughput y control de pérdida de paquetes

En términos de **throughput (rendimiento)**, **UDP es más eficiente que TCP**. Esto se debe a que su cabecera es más pequeña (8 bytes) y no requiere establecer una conexión previa entre el emisor y el receptor.

TCP, en cambio, tiene una cabecera mínima de **20 bytes** y utiliza mecanismos adicionales que generan mayor sobrecarga.

### Anatomía de las cabeceras

| Protocolo | Tamaño cabecera | Características                                 |
| --------- | --------------- | ----------------------------------------------- |
| UDP       | 8 bytes         | Sin control de conexión ni retransmisión        |
| TCP       | ≥20 bytes       | Control de flujo, retransmisión y confiabilidad |

### Control de pérdida de paquetes

TCP ofrece mayor control sobre la pérdida de paquetes porque incluye:

* **Número de secuencia**
* **ACK (Acknowledgment)**
* **Control de flujo**
* **Control de congestión**

Estos mecanismos permiten detectar paquetes perdidos y retransmitirlos.

En aplicaciones de **video en tiempo real**, normalmente se usa **UDP**, ya que es preferible perder algunos paquetes antes que detener la transmisión esperando retransmisiones.

---

# 2. Protocolo que llena la tabla ARP

Al ejecutar el comando en Windows:

```bash
arp -a
```

se muestra una tabla que relaciona **direcciones IP con direcciones MAC**.

## Protocolo utilizado

El protocolo encargado de llenar esta tabla es **ARP (Address Resolution Protocol)**.

## Función principal

ARP permite **traducir direcciones IP (lógicas) en direcciones MAC (físicas)** dentro de una red local.

### Funcionamiento

1. Un host quiere enviar datos a una IP.
2. Verifica si conoce la MAC en la tabla ARP.
3. Si no la conoce, envía un **ARP Request** en broadcast.
4. El dispositivo con esa IP responde con **ARP Reply** indicando su MAC.

## Relación con la trama Ethernet

La trama Ethernet necesita conocer:

* **MAC destino**
* **MAC origen**

ARP proporciona la **MAC destino**, que se coloca en la cabecera Ethernet para que el switch entregue la trama al dispositivo correcto.

---

# 3. Diferencias entre SNMPv2c y SNMPv3

## Seguridad

| Versión | Seguridad                        |
| ------- | -------------------------------- |
| SNMPv2c | Community strings en texto plano |
| SNMPv3  | Autenticación y cifrado          |

SNMPv2c utiliza comunidades como **public** o **private**, que funcionan como contraseñas pero se transmiten sin cifrado.

SNMPv3 introduce:

* Autenticación de usuarios
* Cifrado de mensajes
* Control de acceso

Esto hace que sea mucho más seguro.

## Tipos de mensajes

SNMPv2c introdujo el mensaje **GetBulk**, que permite obtener grandes cantidades de información de la MIB de forma eficiente.

SNMPv3 mantiene estos mensajes pero agrega distintos niveles de seguridad:

* **noAuthNoPriv**
* **authNoPriv**
* **authPriv**

---

# 4. OID y MIB en SNMP

## MIB (Management Information Base)

Es una **base de datos jerárquica** que contiene todos los objetos que pueden ser monitoreados o gestionados en un dispositivo de red.

## OID (Object Identifier)

Es el identificador único que apunta a un objeto dentro de la MIB.

Ejemplo:

```
1.3.6.1.2.1.2.2.1.10
```

Este número identifica un objeto específico dentro del árbol de la MIB.

## Operación SNMP para consultar bytes recibidos

Para conocer la cantidad de bytes recibidos en una interfaz se utiliza la operación:

```
GET
```

Esto permite consultar directamente el valor actual del contador.

## Por qué no usar Trap

Un **Trap** es una notificación enviada automáticamente cuando ocurre un evento importante, por ejemplo:

* caída de una interfaz
* error crítico
* fallo de autenticación

No sería adecuado usar Trap para contar bytes porque ese valor cambia constantemente y generaría demasiadas notificaciones.

---

# 5. Análisis de Cabeceras de Red

## Cabecera Ethernet

Una trama Ethernet contiene los siguientes campos principales:

| Campo            | Función                         |
| ---------------- | ------------------------------- |
| MAC destino      | Dirección física del receptor   |
| MAC origen       | Dirección física del emisor     |
| Tipo (EtherType) | Indica el protocolo encapsulado |
| Datos            | Información transportada        |
| FCS              | Verificación de errores         |

### Valor 0x0800

El valor **0x0800** indica que el protocolo encapsulado es **IPv4**.

---

## Cabecera IPv4

### Campo Protocolo

Indica qué protocolo de transporte contiene el paquete.

| Valor | Protocolo |
| ----- | --------- |
| 1     | ICMP      |
| 6     | TCP       |
| 17    | UDP       |

En el ejemplo mostrado aparece **6**, lo que significa que el paquete contiene un **segmento TCP**.

### Campo TTL (Time To Live)

El TTL indica el número máximo de routers que puede atravesar un paquete.

Cada router reduce el valor en **1**.
Cuando llega a **0**, el paquete se descarta.

Esto evita que los paquetes circulen indefinidamente en la red.

---

## Cabecera TCP

### Flag ACK

Indica que el número de confirmación es válido y que se están confirmando datos recibidos previamente.

### Flag PSH

Indica que los datos deben entregarse inmediatamente a la aplicación receptora.

### Puerto destino 80

El **puerto 80** corresponde al servicio **HTTP**, utilizado para acceder a páginas web.

---

## Diferencia si fuera IPv6

Si el paquete utilizara IPv6, la cabecera IPv4 sería reemplazada por una **cabecera IPv6**.

Una ventaja importante es que IPv6 tiene:

* cabecera de **tamaño fijo (40 bytes)**
* estructura más simple

Esto permite que los **routers procesen los paquetes más rápido**.

---

# 6. Comando Pathping

## Ejecución del comando

```bash
pathping 8.8.8.8
```

## Información que proporciona

Este comando combina las funciones de:

* **ping**
* **tracert**

Permite conocer:

* ruta hacia el destino
* latencia en cada salto
* porcentaje de pérdida de paquetes

---

## Proceso de funcionamiento

### Fase 1 – Descubrimiento de ruta

Primero funciona como **tracert**, identificando todos los routers intermedios.

### Fase 2 – Análisis de pérdida

Luego envía múltiples paquetes ICMP a cada salto para calcular:

* latencia promedio
* pérdida de paquetes

Esto permite identificar dónde se presentan problemas en la red.

---

# 7. Monitoreo de Router con SNMP

Para recorrer todo el árbol MIB del router se puede usar:

```bash
snmpwalk -v2c -c public 192.168.1.1
```

### Parámetros

| Parámetro   | Significado           |
| ----------- | --------------------- |
| -v2c        | versión del protocolo |
| -c public   | comunidad de lectura  |
| 192.168.1.1 | IP del router         |

---

## Trap authenticationFailure

Este Trap se genera cuando alguien intenta acceder al agente SNMP con una **comunidad incorrecta o no autorizada**.

### Ventaja de los Traps

Los Traps permiten que el dispositivo **notifique automáticamente un evento**, evitando que el administrador tenga que consultar constantemente el estado del equipo.

Esto reduce el tráfico de gestión en la red.

---

# 8. Verificación antes de ejecutar git push

## Paso 1 — Conectividad básica

Para verificar conectividad con GitHub:

```bash
ping github.com
```

Este comando verifica principalmente la **capa de red (capa 3 del modelo OSI)** utilizando **ICMP**.

---

## Resolución DNS

Para conocer la dirección IP de github.com se utiliza el protocolo **DNS**.

Se puede verificar con:

```bash
nslookup github.com
```

DNS pertenece a la **capa de aplicación del modelo OSI**.

---

## Impacto de latencia alta

Si el ping muestra latencia alta o variable, las métricas afectadas son:

* **latencia**
* **jitter**

Esto podría hacer que el `git push` tarde más tiempo en completarse.

---

# 9. Establecimiento de la conexión

Cuando se ejecuta:

```bash
git push origin main
```

Git utiliza **HTTPS**, que funciona sobre **TCP**.

## Three Way Handshake

El establecimiento de la conexión TCP ocurre en tres pasos:

1. **SYN** → el cliente solicita conexión
2. **SYN-ACK** → el servidor responde
3. **ACK** → el cliente confirma

---

## Puertos utilizados

| Puerto         | Función                    |
| -------------- | -------------------------- |
| Puerto origen  | puerto efímero del cliente |
| Puerto destino | 443 (HTTPS)                |

Los puertos son gestionados por la **capa de transporte**.

---

# 10. Encapsulamiento de datos

Cuando los datos del commit se envían por la red, pasan por un proceso de encapsulamiento.

| Capa OSI   | Unidad de datos |
| ---------- | --------------- |
| Aplicación | Datos           |
| Transporte | Segmento        |
| Red        | Paquete         |
| Enlace     | Trama           |

Finalmente la trama se envía por la tarjeta de red.

---

## Congestión en routers

Si un router se congestiona y descarta paquetes:

* el `git push` se vuelve más lento
* TCP realiza retransmisiones

Para identificar dónde ocurre la pérdida se puede usar:

```bash
tracert github.com
```

o

```bash
pathping github.com
```

---

## Campo que evita bucles

El campo **TTL (Time To Live)** evita que los paquetes circulen indefinidamente en la red.

Cada router reduce su valor hasta que llega a cero y el paquete se descarta.

---

# 11. Confirmación y cierre de la conexión

TCP confirma la recepción de datos mediante **segmentos ACK**.

Si se pierde un paquete, TCP lo retransmite para garantizar la **fiabilidad de la comunicación**.

## Cierre de conexión

El cierre se realiza mediante intercambio de mensajes:

* **FIN**
* **ACK**

---

# Monitoreo del tráfico con SNMP

Un administrador podría monitorear en el router métricas como:

* bytes transmitidos
* bytes recibidos
* paquetes descartados
* errores de interfaz
* utilización de ancho de banda

Si se requiere cifrado y autenticación, la versión recomendada es **SNMPv3**.

---



