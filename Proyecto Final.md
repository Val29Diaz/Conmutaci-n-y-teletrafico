
---

# PROYECTO FINAL
## Conmutación y Teletráfico

**Título:** Implementación de una Arquitectura de Servicios Diferenciados con Orquestación de Contenedores, Detección de Logos con IA y Políticas de Calidad de Servicio (QoS)

**Autor:** [Tu nombre completo]  
**Asignatura:** Conmutación y Teletráfico  
**Institución:** Universidad Distrital Francisco José de Caldas (UDFJC)  
**Fecha:** Junio de 2026  

---

## Índice
1. [Introducción](#1-introducción)  
2. [Objetivos](#2-objetivos)  
3. [Marco Teórico](#3-marco-teórico)  
4. [Arquitectura del Proyecto](#4-arquitectura-del-proyecto)  
5. [Desarrollo e Implementación](#5-desarrollo-e-implementación)  
    - 5.1 Fase 1: Entorno Base  
    - 5.2 Fase 2: Servidores DHCP  
    - 5.3 Fase 3: Contenedor YOLO (Detección de Logos)  
    - 5.4 Fase 4: Contenedor Chatbot  
    - 5.5 Fase 5: Contenedor Parrot OS (Auditoría)  
    - 5.6 Fase 6: Clúster de Juego (Kubernetes + Agones + SuperTuxKart)  
    - 5.7 Fase 7: Tráfico Competidor (Streaming UDP)  
    - 5.8 Fase 8: Análisis con Wireshark y Políticas ACL/QoS  
    - 5.9 Fase 9: Dashboard Grafana  
6. [Pruebas y Resultados](#6-pruebas-y-resultados)  
7. [Conclusiones](#7-conclusiones)  
8. [Anexos](#8-anexos)

---

## 1. Introducción

El proyecto final de la asignatura Conmutación y Teletráfico tiene como propósito aplicar los conceptos de calidad de servicio (QoS), control de admisión y diferenciación de tráfico en un entorno convergente. Se diseñó una arquitectura que integra microservicios, inteligencia artificial, orquestación de contenedores y políticas de red, simulando un escenario real donde el tráfico crítico (un juego multijugador) compite con flujos secundarios (streaming de vídeo procesado por IA). La implementación se realizó en un entorno híbrido: virtualizado (WSL/Docker/Kubernetes) para los servicios y físico (router y switch Cisco) para la aplicación de ACL y QoS.

## 2. Objetivos

**Objetivo General:**  
Diseñar, implementar y validar una arquitectura de servicios diferenciados utilizando contenedores, orquestación con Kubernetes, detección de logos con YOLO y políticas de calidad de servicio en equipos Cisco, demostrando la priorización de tráfico de red en tiempo real.

**Objetivos Específicos:**  
1. Desplegar servidores DHCP en entornos Docker y Kubernetes para comprender la asignación dinámica de direcciones.  
2. Entrenar un modelo YOLOv8 personalizado para la detección de logos de herramientas DevOps.  
3. Integrar un chatbot con voz y texto que explique las tecnologías detectadas.  
4. Orquestar un servidor de juego multijugador (SuperTuxKart) utilizando Agones en Kubernetes.  
5. Generar tráfico UDP competitivo (streaming) y analizar la competencia con Wireshark.  
6. Configurar equipos Cisco con ACL y QoS para priorizar el tráfico del juego sobre el streaming.  
7. Monitorear el clúster con Prometheus y Grafana.

## 3. Marco Teórico

**Calidad de Servicio (QoS):** Mecanismos que permiten dar tratamiento diferenciado a distintos tipos de tráfico en una red. Se implementan mediante clasificación, marcado, encolamiento y planificación de paquetes. En este proyecto, se emplea el modelo DiffServ con políticas de prioridad estricta y limitación de ancho de banda.  
**YOLO (You Only Look Once):** Red neuronal convolucional para detección de objetos en tiempo real. Se entrenó con un dataset personalizado de logos.  
**Kubernetes y Agones:** Kubernetes es un orquestador de contenedores; Agones es una extensión que añade recursos personalizados para gestionar servidores de juegos (GameServers, Fleets).  
**Wireshark:** Analizador de protocolos que permite capturar y visualizar el tráfico de red. Se utilizó para comparar el tráfico antes y después de aplicar QoS.

## 4. Arquitectura del Proyecto

La arquitectura sigue el diagrama presentado en la clase, compuesta por los siguientes bloques:

- **Administración:** Dashboard de monitoreo (Grafana) y análisis de tráfico (Wireshark).  
- **Servicios de Red:** Servidores DHCP en Docker y Kubernetes.  
- **Inteligencia Artificial:** Contenedor YOLO para clasificación de logos y Chatbot para explicación por voz y texto.  
- **Seguridad:** Contenedor Parrot OS para auditoría con Nmap.  
- **Orquestación:** Kubernetes con Agones gestionando servidores de SuperTuxKart.  
- **Tráfico:** Generación de tráfico UDP (puerto 1234) que compite con el juego (puerto 2759).  
- **Equipos Físicos:** Router y switch Cisco donde se aplican ACL y QoS para priorizar el juego.

## 5. Desarrollo e Implementación

A continuación, se detalla cada fase del proyecto con los comandos y configuraciones realizadas.

### 5.1 Fase 1: Entorno Base

Se utilizó Windows 11 con WSL2 (Ubuntu 24.04) y Docker Desktop integrado. Se instalaron las herramientas de línea de comandos:

```bash
# Instalación de kubectl
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl && sudo mv kubectl /usr/local/bin/

# Minikube con driver Docker
minikube start --cpus=3 --memory=4096 --driver=docker

# Helm
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
```

*Evidencia: Terminal mostrando `minikube start` exitoso y `kubectl version`.*

### 5.2 Fase 2: Servidores DHCP

**DHCP en Docker:**
```bash
docker network create --driver bridge --subnet=192.168.100.0/24 --ip-range=192.168.100.128/25 dhcp-net
docker run -d --name dhcp-server --network dhcp-net --cap-add=NET_ADMIN \
  -v $PWD/dnsmasq.conf:/etc/dnsmasq.conf andyshinn/dnsmasq:latest -d --conf-file=/etc/dnsmasq.conf
```
Se verificó con un cliente Alpine que obtuvo IP `192.168.100.130`.

**DHCP en Kubernetes:**
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: dhcp-server
spec:
  replicas: 1
  selector:
    matchLabels:
      app: dhcp
  template:
    metadata:
      labels:
        app: dhcp
    spec:
      hostNetwork: true
      containers:
      - name: dnsmasq
        image: andyshinn/dnsmasq:latest
        command: ["dnsmasq"]
        args: ["-d", "--interface=eth0", "--dhcp-range=192.168.99.100,192.168.99.200,12h"]
        securityContext:
          capabilities:
            add: ["NET_ADMIN", "NET_RAW"]
```

*Evidencia: Captura de `docker ps` y `kubectl get pods` mostrando ambos servidores DHCP.*

### 5.3 Fase 3: Contenedor YOLO (Detección de Logos)

**Dataset:** Se etiquetaron 8 clases (Ansible, Docker, Jenkins, Kubernetes, Nmap, Podman, QEMU, Terraform) en Roboflow, exportando en formato YOLOv8.

**Entrenamiento:**
```bash
cd ~/proyecto-final/yolo-logo
source venv/bin/activate
pip install ultralytics roboflow
python -c "
from ultralytics import YOLO
model = YOLO('yolov8n.pt')
model.train(data='Logos-1/data.yaml', epochs=20, imgsz=320, batch=8)
"
```
Se obtuvo un mAP50 de 0.949 en validación. El modelo se guardó en `runs/detect/train-3/weights/best.pt`.

**Script de detección (`detect_logos.py`):** Carga el modelo, procesa una imagen y guarda la clase detectada en `detected_class.txt`.

**Integración:** Se ejecutó el pipeline YOLO + Chatbot:
```bash
python detect_logos.py imagen.jpg
cd ~/proyecto-final/chatbot && source venv_chatbot/bin/activate && python chatbot.py $(cat ~/proyecto-final/yolo-logo/detected_class.txt)
```

*Evidencia: Terminal mostrando detección (ej. QEMU: 31.06%) y respuesta del chatbot con audio.*

### 5.4 Fase 4: Contenedor Chatbot

Se creó un entorno virtual exclusivo (`venv_chatbot`) y un script `chatbot.py` que recibe una clase y genera explicación en texto y voz usando `gTTS` y `mpg123`. Incluye información de empresas que usan cada tecnología, siguiendo el ejemplo del profesor.

*Evidencia: Captura de la explicación de QEMU y reproducción de audio.*

### 5.5 Fase 5: Contenedor Parrot OS (Auditoría)

Se construyó una imagen con `nmap` y un script `audit.sh` que escanea la red local y los puertos del clúster Kubernetes.

```bash
docker build -t parrot-audit .
docker run --rm --network host parrot-audit
```

*Evidencia: Salida de nmap mostrando hosts activos y puertos.*

### 5.6 Fase 6: Clúster de Juego (Kubernetes + Agones + SuperTuxKart)

**Instalación de Agones:**
```bash
helm repo add agones https://agones.dev/chart/stable
helm repo update
helm install agones agones/agones --namespace agones-system --create-namespace
```

**Imagen del servidor:** Se creó `stk-server:latest` con SuperTuxKart en modo servidor.

**Fleet:**
```yaml
apiVersion: agones.dev/v1
kind: Fleet
metadata:
  name: stk-fleet
spec:
  replicas: 2
  template:
    spec:
      health:
        disabled: true
      ports:
      - name: default
        portPolicy: Dynamic
        containerPort: 2759
        protocol: UDP
      template:
        metadata:
          labels:
            app: stk-server
        spec:
          containers:
          - name: stk
            image: stk-server:latest
            imagePullPolicy: Never
```

**Túnel UDP:** Se utilizó `socat` para redirigir el tráfico desde el host al pod del juego:
```bash
sudo socat UDP4-LISTEN:2759,fork,reuseaddr,bind=0.0.0.0 UDP4:<IP_DEL_POD>:2759 &
```

**Tráfico simulado (para pruebas):**
```bash
while true; do echo "GAME" | nc -u -w0 192.168.10.2 2759; sleep 0.05; done &
```

*Evidencia: `kubectl get gameservers` y `ss -ulpn | grep 2759`.*

### 5.7 Fase 7: Tráfico Competidor (Streaming UDP)

Se creó `stream_video.py`, un script que envía paquetes UDP de 1024 bytes hacia `192.168.49.2:1234` simulando un flujo de vídeo.

```bash
cd ~/proyecto-final/yolo-logo && source venv/bin/activate && python stream_video.py &
```

*Evidencia: `tcpdump` o Wireshark mostrando paquetes hacia el puerto 1234.*

### 5.8 Fase 8: Análisis con Wireshark y Políticas ACL/QoS

**Captura SIN QoS:**  
Se deshabilitó la política de QoS en el router y se capturó tráfico en Wireshark (interfaz Ethernet). Se generó el IO Graph comparativo (puertos 2759 y 1234).

**Configuración de Equipos Cisco (Router y Switch):**

*Switch:*
```cisco
vlan 10
 name DEMO
interface GigabitEthernet0/1
 switchport mode access
 switchport access vlan 10
interface GigabitEthernet0/24
 switchport mode trunk
 switchport trunk allowed vlan 10
```

*Router:*
```cisco
interface GigabitEthernet0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0
!
ip access-list extended BLOQUEAR-STREAMING
 deny udp any any eq 1234
 permit ip any any
interface GigabitEthernet0/0.10
 ip access-group BLOQUEAR-STREAMING in
!
class-map match-all JUEGO
 match access-group name ACL-JUEGO
class-map match-all STREAMING
 match access-group name ACL-STREAMING
policy-map PRIORIZAR-JUEGO
 class JUEGO
  priority percent 50
 class STREAMING
  bandwidth percent 20
 class class-default
  fair-queue
interface GigabitEthernet0/0
 service-policy output PRIORIZAR-JUEGO
```

**Captura CON QoS:**  
Se aplicó la política y se repitió la captura. El IO Graph mostró la línea del juego estable y la del streaming reducida.

*Evidencia: `show class-map`, `show policy-map`, y capturas de Wireshark (sin QoS y con QoS).*

### 5.9 Fase 9: Dashboard Grafana

Se instaló el stack de monitoreo con Helm:
```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm install monitoring prometheus-community/kube-prometheus-stack --namespace monitoring --create-namespace
kubectl port-forward -n monitoring svc/monitoring-grafana 8080:80 --address=0.0.0.0 &
```
Se accedió a `http://localhost:8080` y se exploraron dashboards de red.

*Evidencia: Captura del dashboard de Kubernetes Networking o del Explore de Prometheus.*

## 6. Pruebas y Resultados

**Tabla 1. Comparación de tráfico antes y después de aplicar QoS**

| Métrica                       | Sin QoS (compiten libremente) | Con QoS (prioridad al juego) |
|-------------------------------|-------------------------------|------------------------------|
| Puerto 2759 (juego)           | Fluctuante, similar al streaming | Estable, ocupa ~50% del ancho de banda |
| Puerto 1234 (streaming)       | Similar al juego               | Reducido, irregular           |
| Latencia percibida (juego)    | Mayor variación               | Menor variación               |

**Resultados de YOLO:**  
El modelo entrenado alcanzó un mAP50 de 0.949 en validación, detectando correctamente logos como Docker, Kubernetes, QEMU, etc. La integración con el chatbot funcionó como se esperaba.

**Resultados de Auditoría:**  
Parrot OS identificó hosts activos en la red del clúster y puertos abiertos en el nodo Kubernetes.

**Resultados de DHCP:**  
Ambos servidores (Docker y Kubernetes) asignaron direcciones IP correctamente a clientes de prueba.

## 7. Conclusiones

- La arquitectura de microservicios permitió separar cada componente (YOLO, Chatbot, Parrot, juego) en entornos independientes, facilitando la gestión y la demostración.
- La implementación de QoS en equipos Cisco demostró empíricamente cómo las políticas de priorización pueden beneficiar el tráfico de misión crítica (juego) frente a flujos secundarios (streaming), validando los principios de conmutación y teletráfico.
- El entrenamiento de YOLOv8 con un dataset personalizado fue exitoso, y la integración con un chatbot que responde por voz y texto añadió valor didáctico al proyecto.
- Aunque la conexión directa al juego enfrentó limitaciones técnicas, los generadores de tráfico permitieron emular el comportamiento de la red y obtener resultados válidos para la comparación de QoS.
- Se logró monitorear el clúster Kubernetes con Prometheus y Grafana, completando el ciclo de observabilidad.

## 8. Anexos

**Anexo 1:** Capturas de pantalla del entorno virtual:
- `kubectl get gameservers`
- `docker ps`
- `ss -ulpn | grep 2759`

**Anexo 2:** Configuración de equipos Cisco (capturas de `show running-config`, `show class-map`, `show policy-map`).

**Anexo 3:** Capturas de Wireshark (IO Graph sin QoS y con QoS).

**Anexo 4:** Captura de YOLO detectando un logo y del chatbot respondiendo.

**Anexo 5:** Dashboard de Grafana mostrando métricas.

---

Este documento refleja todo el trabajo realizado. Solo necesitas añadir tus capturas de pantalla en los espacios indicados y ajustar los nombres de archivo si es necesario. ¡Enhorabuena por finalizar el proyecto! Si necesitas ajustar algo más, no dudes en decírmelo.
