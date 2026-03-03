# Conmutación-y-teletrafico
## Desarrollo de la materia, parciales, talleres y demás

# Parcial primer corte 
### Primer punto 
A) Diferencia entre latencia y jitter: La latencia es el tiempo total que tarda en la transmisión de datos, mientras que el jitter es la variación o inconsistencia de ese tiempo que tarda 

El jitter es la metrica que tendria un impacto mas negativo en una llamada VoIP ya que este esta sujeto a los desfases que presenta la latencia el afecta la parte de conexion continua en tiempo real como las llamadas, videoconferencias haciendo que estas se entre corten, etc

B) TCP y UDP en transmisión de video efectividad en terminos de Troughput y control de perdidas de paquetes En términos de throughput (rendimiento), UDP es más eficiente. Esto se debe a la "anatomía" de su cabecera, que es mucho más ligera (solo 8 bytes) y no requiere el establecimiento de una conexión previa (handshake), lo que reduce el retardo y la sobrecarga de datos.Por otro lado, TCP ofrece un mayor control de la pérdida de paquetes. La razón radica en su cabecera más compleja (mínimo 20 bytes), la cual incluye:

Números de secuencia y de acuse de recibo (ACK): Permiten al receptor confirmar qué paquetes han llegado y solicitar la retransmisión de los que se perdieron.
Mecanismos de control de flujo y congestión: Ajustan la velocidad de envío según el estado de la red.

En video en tiempo real (streaming), solemos preferir UDP porque un pequeño pixelado (pérdida) es preferible a un video que se detiene constantemente para retransmitir datos viejos.

<img width="847" height="534" alt="image" src="https://github.com/user-attachments/assets/8ad0da41-6cfd-4bbd-bef0-b428ffc8ef91" />

### Segundo punto 
<img width="723" height="151" alt="image" src="https://github.com/user-attachments/assets/2f05b134-85f2-4340-acf2-da1f88618677" />
Ethernet IT: nos indica la direccion de destino y la de origen en la parte de tipo el nos indica 
