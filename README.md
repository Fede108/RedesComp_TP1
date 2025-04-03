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

---

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

---

### IPv6
El motivo que ha conducido a la adopción de una nueva versión ha sido la limitación impuesta por el campo de dirección de 32 bits en IPv4. Algunas de las razones por las que es inadecuado utilizar estas direcciones de 32 bits son las siguientes:
- **Espacio de direcciones limitado**:
IPv4 usa un campo de 32 bits, lo que permite alrededor de 4.000 millones de direcciones. Aunque parecía suficiente en un principio, con el crecimiento explosivo de dispositivos conectados y la proliferación de redes (como múltiples LAN y redes inalámbricas), ese número se quedó corto.

- **Ineficiencia en la asignación**:
La estructura en dos niveles de las direcciones en IPv4 (número de red y número de host) obliga a asignar un número de red completo a cada red, incluso si no se utiliza completamente el rango de direcciones disponible en esa red, desperdiciando así parte del espacio.

- **Demanda creciente**:
El incremento en el uso de TCP/IP en nuevos ámbitos, como dispositivos electrónicos de puntos de venta, receptores de televisión por cable y la posibilidad de que cada computador tenga múltiples direcciones IP, elevó aún más la necesidad de contar con más direcciones.

- **Nuevos requerimientos técnicos**:
Además de ampliar el espacio de direcciones, era necesario incorporar mejoras en la configuración de red, flexibilidad en el encaminamiento y funcionalidades adicionales para gestionar el tráfico de forma más eficiente.

Además de ampliar el espacio de direcciones (pasando de 32 a 128 bits), se incorporaron mejoras en la configuración de red, las opciones se trasladaron a cabeceras de extension separadas, se logro una mayor flexibilidad de direccionamiento al introducir las direcciones anycast y funcionalidades adicionales como permitir la asignación dinámica de direcciones.

- **Cabecera fija de 40 octetos:**  
  Es la única obligatoria y contiene la información esencial para el envío del paquete.

- **Cabeceras de extensión:**  
  Se ubican entre la cabecera IPv6 y la cabecera de la capa de transporte. Entre ellas se incluyen:
  
  - **Opciones salto a salto:** Procesadas en cada nodo.
  
  - **Encaminamiento:** Permite especificar rutas alternativas.
  
  - **Fragmentación:** Maneja la división y reensamblado de paquetes.
  
  - **Autenticación y Encapsulamiento de carga de seguridad:** Proveen integridad, autenticación y privacidad.
  
  - **Opciones para destino:** Opciones específicas para ser evaluadas en el nodo destino.
    
### Cabecera IPv6

Paquete IPv6 con un ejemplar de cada cabecera:

![image](https://github.com/user-attachments/assets/ecdc0057-0a48-4624-b674-0845cd53394a)

La cabecera IPv6 tiene una longitud fija de 40 octetos, que consta de los siguientes campos:

![image](https://github.com/user-attachments/assets/81aab859-286c-4a5f-bb42-c4055ba8aecf)

---

### PROTOCOLO DE MENSAJES DE CONTROL DE INTERNET (ICMP)

ICMP transfiere mensajes de error y diagnóstico entre dispositivos de red. Se envía en respuesta a un datagrama y proporciona información de realimentación sobre problemas de comunicación.

## Características de ICMP

- **Ubicación en la pila de protocolos**: ICMP está al mismo nivel que IP pero actúa como usuario de IP.  
- **Encapsulación**: ICMP se encapsula dentro de un datagrama IP, por lo que no garantiza su entrega.  

## Formato de mensaje ICMP

Cada mensaje ICMP contiene:

- **Tipo (8 bits)**: especifica el tipo de mensaje.  
- **Código (8 bits)**: parámetros codificados del mensaje.  
- **Suma de comprobación (16 bits)**: validación de integridad.  
- **Parámetros (32 bits)**: información adicional.  

Los mensajes ICMP se utilizan para indicar errores de entrega, notificar problemas de red y realizar diagnósticos, como con el comando `ping`.

# Primer parte:

## 2) Construir el diagrama de red propuesto en el software de simulación/emulación elegido.
Usamos el software de simulacion Packet Tracer:

![image](https://github.com/user-attachments/assets/5ad5ee69-d85c-4450-9cb7-350720e6714c)



## 3) ¿Que diferencias que tienen los simuladores y los emuladores en el contexto de redes?
Las diferencias que tienen los simuladores y los emuladores en el contexto de redes se basan en cómo representan el comportamiento de una red real.
Un simulador de redes reproduce el comportamiento de una red en base a modelos matemáticos y lógicos, sin la ejecución de software real de dispositivos de red. La ventaja es que permite probar configuraciones sin equipos físicos. Se usa para la investigación y la educación. Un claro ejemplo de un simulador de redes es Packet Tracer.
En cambio un emulador de redes recrea una red real usando software original (como el de routers y switches), lo que permite probar configuraciones de forma más precisa. Se puede conectar con dispositivos físicos, esto genera que sea más preciso pero la desventaja es que requiere más recursos. A diferencia del simulador de redes, el emulador se usa para pruebas de rendimiento y depuración en entornos cercanos a la realidad. Un ejemplo es el software GNS3, que es propuesto para realizar esta actividad también.



## 4) Evaluar conectividad entre todos los host enviando 3 (tres) paquetes ICMPv4, utilizando el comando `ping` para IPv4.

- Conexión de h1 a h2:
  
 ![image](https://github.com/user-attachments/assets/ba511464-1d8c-45c8-bcab-a73415df273e)

- Conexión de h1 a h3:
  
 ![image](https://github.com/user-attachments/assets/f0cf37d0-307f-4d49-9c29-91b1548ca947)



## 5) Evaluar conectividad entre todos los host enviando 3 (tres) paquetes ICMPv6, utilizando el comando `ping6` para IPv6.

- Conexión entre h1 y h2:
  
 ![image](https://github.com/user-attachments/assets/048fa9d5-875c-4cba-be7c-5c47f0657b02)
 
- Conexión entre h1 y h3:

![image](https://github.com/user-attachments/assets/2d041322-21ba-4243-8177-5e7db8fe107c)

## 6) Iniciar tráfico ICMP en el Cliente 1 con destino Cliente 2. Analizar tráfico sobre las dos redes, capturar screenshots y responder las siguientes preguntas:
### a) ¿Cuáles son las comunicaciones ARP que observan? Explicar y ejemplificar con capturas cómo funciona la traducción de direcciones lógicas a direcciones físicas


Antes de enviar un paquete IP a un destino en la misma red, el dispositivo origen necesita conocer la MAC de ese destino (o la MAC de su Gateway si el destino está en otra red). ARP permite que un dispositivo descubra la dirección física (MAC) asociada a una dirección lógica (IP).  

![image](https://github.com/user-attachments/assets/c0fb92c6-344a-4a35-b335-56cecaa47826)

En este caso, el Cliente 1 (PC0) detecta que Cliente 2 (PC1) con IP `192.168.2.10` está fuera de su red `192.168.1.0/24`. El PC revisa su tabla de enrutamiento y ve que el siguiente salto (*next-hop*) es la IP del router, `192.168.1.11`.  

Se envía una trama Ethernet con destino `FF:FF:FF:FF:FF:FF` (broadcast) preguntando:  
> “¿Quién tiene la IP `192.168.1.11`? Responder a `192.168.1.10`”.

El dispositivo con esa IP (Router0) recibe el broadcast, reconoce su IP y responde con un ARP Reply:  
> “La IP `192.168.1.11` está asociada a la MAC `00:11:22:33:44:55`”.

Una vez que el PC origen encapsula el paquete IP con la MAC del router, este recibe el paquete y lo reenvía hacia la red `192.168.2.0/24`. Para esto, el router envía otra trama para conocer la dirección MAC del Cliente 2 (PC1).  

El campo **Type: `0x0806`** en la parte Ethernet del PDU indica que se trata de una ARP.  
El **Target MAC**: normalmente `00:00:00:00:00:00` en el Request, es porque aún no se conoce la dirección MAC de destino.



Una vez que el PC origen encapsula el paquete IP con MAC del router, el router recibe el paquete y lo reenvía hacia la red 192.168.2.0/24. Para esto el router envía otra trama para conocer la dirección MAC del cliente 2 (PC1).

![image](https://github.com/user-attachments/assets/3aa01845-cf36-4c01-a7ca-7930f879902d)

El campo type: 0x0806 en la parte Ethernet del PDU indica que se trata de una ARP. El Target MAC: normalmente 00:00:00:00:00:00 en el Request, es porque no se sabe aún la dirección.

---

### b) ¿Cuáles son las direcciones IP en los datagramas? Indicar con un ejemplo.

Cuando se envía el mensaje ICMP, este se pasa a IP, que lo encapsula con una cabecera IP y lo transmite de la forma habitual.  
- **Dirección IP de origen**: Cliente 1 (PC0).  
- **Dirección IP de destino**: Cliente 2 (PC1).  

![image](https://github.com/user-attachments/assets/2e1046bd-525c-4b4b-b00a-f5c29d4fc3f1)

---

### c) ¿Cómo determina el enrutador la comunicación entre un host y otro?

El enrutador encamina los paquetes basándose en direcciones lógicas (IP) usando **tablas de enrutamiento**, que mantiene actualizadas para determinar la mejor ruta hacia cada destino.


---

## d) ¿Para qué usamos el switch? ¿Por qué el switch no tiene asignadas direcciones IP en sus interfaces?

El **switch** es utilizado para conectar dos redes LAN que utilizan el mismo protocolo LAN. Actúa como un **filtro de direcciones**, recogiendo paquetes de una LAN que van dirigidos a otra y reenviándolos sin modificar su contenido.  

El switch **mantiene una tabla de direcciones MAC** para cada uno de sus puertos. Cuando recibe una trama, consulta su tabla para decidir a qué puerto reenviarla o si descartarla.  

**Motivo por el cual no tiene IP en sus interfaces:**  
El switch opera en la **Capa 2 (Enlace de Datos)** del modelo OSI, usando direcciones MAC para el reenvío de tramas. Por esta razón, **sus interfaces no requieren direcciones IP** para el proceso de conmutación.

---

## e) ¿Qué datos contiene la tabla ARP de h1?
Contiene las asociaciones entre direcciones IP y MAC conocidas por `h1`. En este caso, incluiría:  

  ![image](https://github.com/user-attachments/assets/ef63a83c-ceb2-4aeb-84ff-ba38cb55d0a7)


---

## f) ¿Qué datos contiene la tabla ARP de h3?
Contiene las asociaciones de direcciones IP y MAC conocidas por `h3`, como:  

![image](https://github.com/user-attachments/assets/7887f1df-c3ea-48f8-a6e3-99adfd5acc3d)


---

## g) ¿Qué datos contiene la tabla ARP del router?
El router mantiene registros de los dispositivos en ambas redes, por lo que su tabla ARP incluirá:  
- **IP y MAC del Cliente 1 (PC0)**.  
- **IP y MAC del Cliente 2 (PC1)**.  
- **IP y MAC de otros dispositivos conectados en ambas redes**.

![image](https://github.com/user-attachments/assets/f737716b-b7fa-4399-bbe1-babeeac0dbdb)


---

## h) ¿Qué son las direcciones de broadcast en IPv4? ¿Cuál es su utilidad?

Las direcciones de **broadcast** permiten enviar un mensaje a **todos los dispositivos** en una red.  
**Ejemplo común**: `255.255.255.255`, que envía un mensaje a todos los dispositivos de la red local.  

### **Utilidad**
Facilitan la comunicación masiva sin necesidad de conocer cada dirección individual. Se usan en protocolos como:  
- **ARP Request** para resolución de direcciones.  
- **Mensajes de descubrimiento de red**.  
- **Envío de alertas o notificaciones en redes locales**.

---

## i) ¿Qué son las direcciones de multicast en IPv4? ¿Cuál es su utilidad?

Las direcciones **multicast** permiten enviar datos a **un grupo específico de dispositivos** en una red en lugar de a todos (como en broadcast).  

- **Rango de direcciones multicast**: `224.0.0.0` a `239.255.255.255`.  
- **Ejemplos de uso**:
  - Videoconferencias.
  - Transmisión de datos en tiempo real (streaming).
  - Protocolos como **IGMP (Internet Group Management Protocol)** para gestionar grupos multicast.


# 7) Análisis de comunicaciones NDP

## a) ¿Cuáles son las comunicaciones NDP que suceden? 

Identifique los distintos tipos de mensajes NDP haciendo foco en las direcciones IP de origen y destino de cada uno.

Existen dos tipos de comunicaciones NDP que suceden en esta situación:
1. **Cuando una PC envía paquetes a otra dentro de la misma red.**
2. **Cuando una PC debe enviar paquetes fuera de su red y necesita encontrar un router.**

Aquí se observan los distintos tipos de mensajes NDP en la simulación:

![image](https://github.com/user-attachments/assets/e956d03e-7967-4775-bfbd-1ed67030502d)

![image](https://github.com/user-attachments/assets/82f901e8-0e1c-4ce5-a1db-ec716b82284f)

![image](https://github.com/user-attachments/assets/47aceaf2-298f-4d6e-98a2-631e911818c1)

![image](https://github.com/user-attachments/assets/54c6a497-5294-49a4-959a-3ffce7c8ab18)


---

## b) ¿NDP reemplaza a ARP?

NDP sí reemplaza a ARP, ya que IPv6 reemplaza a IPv4. ARP se utiliza en redes IPv4 para mapear direcciones IP a direcciones MAC dentro de una red local. En cambio, NDP realiza una función similar en redes IPv6, pero con capacidades adicionales, como la detección de duplicados de direcciones, el descubrimiento de routers y la autoconfiguración de direcciones, lo que lo hace más avanzado que ARP.

---

## c) Describir las funciones de NDP

Las funciones de **NDP (Neighbor Discovery Protocol)** incluyen:

- **Descubrimiento de vecinos**:  
  Permite resolver direcciones IPv6 en direcciones MAC mediante los mensajes:
  - **NS (Neighbor Solicitation)**  
  - **NA (Neighbor Advertisement)**  

- **Descubrimiento de routers**:  
  Un host puede encontrar routers en la red local mediante:
  - **RS (Router Solicitation)**  
  - **RA (Router Advertisement)**  

- **Resolución de direcciones**:  
  Un host usa un **NS** para preguntar por la dirección MAC de una IP, y recibe un **NA** con la respuesta.

- **Detección de direcciones duplicadas (DAD - Duplicate Address Detection)**:  
  Un host envía un **NS** para verificar si otra máquina ya usa la misma dirección IPv6.  
  - Si recibe un **NA**, significa que la dirección está ocupada.

- **Redirección de tráfico**:  
  A través de un **Redirect Message**, un router puede indicar a un host una mejor ruta hacia un destino.

---

## d) ¿Cómo se reemplaza la función de broadcast en IPv6?

En IPv6 el broadcast del IPv4 se reemplaza por el uso del multicast o unicast para mejorar la eficiencia de la red y reducir la congestión. Esto se debe a que el broadcast envía mensajes a todos los dispositivos de la red generando tráfico innecesario, empeorando el rendimiento y genera poca seguridad. En cambio en el IPv6, el multicast envía mensajes a un grupo de dispositivos y el unicast envía mensajes a un solo dispositivo de la red.

---

## e) ¿Cuál es la diferencia entre las direcciones link-local, unique-local y global? ¿En qué caso usaría cada una? Ejemplificar.

- Link-local: Son direcciones usadas solo para comunicarse dentro de la misma red local, como en una casa o una oficina.

- Unique-local: Son direcciones privadas para redes internas, como las de empresas, oficinas o redes caseras, y no se pueden usar en Internet.

- Global: Son direcciones públicas que se usan para acceder a dispositivos en Internet desde cualquier parte del mundo.

PARTE PRÁCTICA:

## Características principales del switch Cisco

Los switches Cisco Catalyst son dispositivos de red utilizados en entornos empresariales debido a su alta fiabilidad y rendimiento. A continuación, se presentan algunas de sus características más relevantes:
Rendimiento y capacidad: Capacidad de switching de hasta 216 Gbps y una tasa de reenvío de hasta 107.1 Mpps, dependiendo del modelo.


Puertos: Disponibilidad de 24 o 48 puertos Gigabit Ethernet, con opciones de enlaces ascendentes de 1G y 10G SFP+.


Apilamiento: Soporta tecnología FlexStack-Plus, permitiendo apilar hasta 8 switches con un ancho de banda de apilamiento de 80 Gbps.


Eficiencia energética: Utiliza Cisco EnergyWise para reducir el consumo energético y mejorar la eficiencia.


Seguridad: Implementa autenticación 802.1X, listas de control de acceso (ACL) y protección contra ataques DoS.


Calidad de servicio (QoS): Permite la priorización del tráfico crítico para garantizar un rendimiento óptimo de las aplicaciones.

a)

Lo realizado en este punto fue:

1. Conectar el cable de consola al puerto serial de la PC y al puerto consola del switch.
2. Dentro de PuTTY seleccionar la opción serial y configurar los parámetros correspondientes.
3. Una vez configurado los parámetros se da acceso a la administración del switch y cambio de claves

![image](https://github.com/user-attachments/assets/54e91ebd-b707-408f-a40b-921b5f15d3e1)

Aquí se accede a la terminal de PuTTY y mediante el comando enable y se ingresa al modo privilegiado

Luego se accede al modo de configuración global donde se cambia la contraseña de la consola
![image](https://github.com/user-attachments/assets/80fe12b0-1c5a-4ca8-b176-3adc61a89e27)

c)
Lo realizado en este punto fue:
1. Conectar dos computadoras a los puertos FastEthernet del switch
2. Asignar IP estáticas a cada computadora

![image](https://github.com/user-attachments/assets/82ac68cd-f8d2-41fd-b636-9cd1b9f859e6)

3. Se verifica conectividad mediante el comando ping

![image](https://github.com/user-attachments/assets/86d39cd8-777e-4d6c-be1f-12f8a69d6c4f)

![image](https://github.com/user-attachments/assets/6fce6bf2-6bfd-4754-8159-cc5194fa7339)

d)
Lo que se hizo en este punto fue la configuración de mirroring de puertos para monitoreo:

1. Se accede al modo de configuración global mediante el comando configure terminal
2. Luego se configura el puerto origen y el puerto destino del tráfico

![image](https://github.com/user-attachments/assets/12fbb68f-0ce2-4341-951c-0a51fdf91969)

3)
Esta captura fue tomada desde wireshark en la que se puede observar el tráfico ICMP, en la que se hace la solicitud de ping mediante “echo request” desde la PC con la IP  169.254.125.248 hacia la PC con la IP 169.254.125.25 y luego se da la respuesta mediante “echo reply” donde se observa que la PC destino recibió los paquetes.

![image](https://github.com/user-attachments/assets/2214d8ce-1b9e-4a9c-a938-bd0e2bee8346)






  






