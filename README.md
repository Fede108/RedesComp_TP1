# Trabajo Practico nro 1
**Facultad de Ciencias Exactas, Fisicas y Naturales de la U.N.C**

**Redes de Computadoras**

**Profesores**
- Santiago M. Henn
- Facundo N. Oliva C.
  
**Nombre del grupo : Kiritoro** 

**Integrantes**
- Federico Cechich
- Juan Manuel Ferrero
- Luciano Trachta


**27 de Marzo de 2025**


**Información de contacto**:  _juan.manuel.ferrero@mi.unc.edu.ar_, _federico.cechich@mi.unc.edu.ar_, _ltrachta@mi.unc.edu.ar_ 

## Resumen
En este trabajo se analizaron los principios fundamentales de la interconexión de redes mediante el estudio de los protocolos de comunicación IP. Se realizaron pruebas prácticas para analizar el tráfico ICMP, la resolución de direcciones mediante ARP y NDP, así como la función de los switches y routers en la comunicación entre hosts. Se exploró el uso de simuladores de redes como Packet Tracer y dispositivos reales como el switch Cisco Catalyst 2950 Series.

## Introduccion
La primera parte del trabajo se centró en la configuración y el análisis de tráfico en entornos IPv4 e IPv6, se examinó el comportamiento de protocolos de resolución de direcciones (ARP y NDP) y se utilizó DHCP para la asignación dinámica de direcciones. Se realizaron actividades tales como el inicio de tráfico ICMP entre clientes, el análisis de las comunicaciones ARP y NDP, apoyándose en simuladores.

La segunda parte profundizó en el manejo y configuración de equipamiento físico, se llevaron a cabo actividades como modificar claves de acceso, la configuración de un switch empresarial (modelo Cisco Catalyst 2950 Series) y la realización de pruebas de conectividad y monitoreo de tráfico mediante técnicas como el port mirroring.

## Marco Teórico

Los protocolos de red permiten la comunicación entre dispositivos mediante la organización y gestión de los datos transmitidos. Sus funciones principales incluyen:

- **Encapsulamiento**: Agrega información de control a los datos, como direcciones, códigos de error y detalles del protocolo.  

- **Fragmentación y Reensamblado**: Divide grandes bloques de datos en unidades más pequeñas para adaptarse a las limitaciones de la red y mejorar la eficiencia del control de errores.  

- **Control de Conexión**: En protocolos orientados a conexión, establece, mantiene y finaliza las sesiones de comunicación.  

- **Entrega Ordenada**: Numeración de paquetes para asegurar que lleguen en el orden correcto, evitando desorden en la transmisión.  

- **Control de Flujo**: Regula la cantidad de datos enviados para evitar sobrecarga en el receptor.  

- **Control de Errores**: Detecta y corrige errores en la transmisión mediante la retransmisión de datos corruptos.  

- **Direccionamiento**: Identifica de manera única a los dispositivos en la red mediante direcciones IP y direcciones MAC.  

- **Multiplexación**: Permite que múltiples conexiones compartan un mismo canal de comunicación.  

- **Servicios de Transmisión**: Define cómo se transmiten los datos según las necesidades de las aplicaciones.

### Principios de la Interconexión Entre Redes

Cada red constituyente de una internet permite la comunicación entre los dispositivos conectados a esa red; estos dispositivos se conocen como sistemas finales (ES, End Systems). Además, las redes se conectan por dispositivos denominados en los documentos ISO como sistemas intermedios (IS, Intermediate Systems). Los IS proporcionan caminos de comunicación y realizan las funciones de retransmisión y encaminamiento necesarias para que los datos se puedan intercambiar entre los dispositivos conectados en las diferentes redes de la internet. Existen dos tipos de IS:
- **Puente (bridge):**
Un IS utilizado para conectar dos redes LAN que utilizan el mismo protocolo LAN. El puente actúa como un filtro de direcciones, recogiendo paquetes de una LAN que van dirigidos a un destino en otra LAN y pasándolos hacia adelante. El puente no modifica el contenido del paquete ni incorpora nada al mismo. Opera en la capa 2 del modelo OSI.
- **Dispositivo de encaminamiento (router):**
Un IS utilizado para conectar dos redes que pueden o no ser similares. El dispositivo de encaminamiento utiliza un protocolo de internet presente en cada dispositivo de encaminamiento y en cada computador de la red. Opera en la capa 3 del modelo OSI.



### El Protocolo Internet (IP)

Es parte del conjunto de protocolos TCP/IP. IP ofrece un servicio en el que cada paquete (o datagrama) se trata de forma independiente, sin establecer previamente una conexión dedicada entre el origen y el destino. Se corresponde con el mecanismo de operación no orientado a conexión. En cada dispositivo de encaminamiento se toma una decisión de encaminamiento (independientemente para cada unidad de datos) relativa al siguiente salto.  

Para que el protocolo de interconexión funcione correctamente, es necesario disponer de un protocolo adicional que permita acceder a cada red particular:

- **Una subcapa superior** que se encarga de la interconexión entre redes (funciones lógicas de encaminamiento, por ejemplo, utilizando IP).  
- **Una subcapa inferior** que se encarga del acceso a la red concreta (por ejemplo, Ethernet), proporcionando el mecanismo físico y de enlace de datos para transmitir la información.  


### IPv4

Los servicios a proporcionar entre las capas de protocolos adyacentes (por ejemplo, entre IP y TCP) se expresan en términos de **primitivas y parámetros**.  
Una primitiva especifica la función que se va a ofrecer y los parámetros se utilizan para pasar datos e información de control.  

IP proporciona dos primitivas de servicio en la interfaz con la capa superior:  

- **Send (envío):** Se utiliza para solicitar la transmisión de una unidad de datos.  
- **Deliver (entrega):** Utiliza IP para notificar a un usuario la llegada de una unidad de datos.  

Los parámetros asociados a estas primitivas son los siguientes:

- **Dirección origen:** Dirección global de red de la entidad IP que envía la unidad de datos.  
- **Dirección destino:** Dirección global de red de la entidad IP de destino.  
- **Protocolo:** Entidad de protocolo receptor (un usuario IP, como por ejemplo TCP).  
- **Indicadores del tipo de servicio:** Especifica el tratamiento de la unidad de datos en su transmisión a través de los componentes de las redes.  
- **Identificador:** Se utiliza en combinación con las direcciones origen y destino y el protocolo usuario para identificar de forma única la unidad de datos. Es necesario para reensamblar e informar de errores.  
- **Indicador de no fragmentación:** Indica si IP puede fragmentar los datos para realizar el transporte.  
- **Tiempo de vida:** Medido en segundos.  
- **Longitud de los datos:** Longitud de los datos que se transmiten.  
- **Datos de opción:** Opciones solicitadas por el usuario IP.  
- **Datos:** Datos de usuario que se van a transmitir.  

> **Nota:** Los parámetros **identificador**, **indicador de no fragmentación** y **tiempo de vida** están presentes en la primitiva `Send`, pero no en la primitiva `Deliver`, ya que proporcionan instrucciones a IP que no son de la incumbencia del usuario IP destino.  



### Cabecera IPv4  

A continuación, se muestra la estructura de la cabecera de un paquete IPv4:

![image](https://github.com/user-attachments/assets/8e63f1a5-af18-4ab1-8ad6-012eeffe8763)


