Enlace al repositorio: https://github.com/fferrlop/Examen_final_redes.git

# Examen de Redes - Misión 1: Reconexión en la Base Eco (Hoth)

**Situación:** La Base Eco en Hoth ha quedado incomunicada tras un bombardeo imperial. La General Leia Organa te encomienda diseñar un nuevo esquema de red para restablecer la comunicación interna y con la flota rebelde.
Cada departamento necesita su propia subred IP. Disponéis de un bloque de direcciones limitado (172.16.0.0/24).

## Requisitos

- Comando Central: ~50 hosts
- Defensa Perimetral: ~30 hosts
- Centro Médico: ~20 hosts
- Hangar y Taller: ~14 hosts
- Enlace troncal (interplanetario): punto a punto (2 hosts)

## Plan de direccionamiento IP (VLSM)

| Departamento       | Dirección de Red | Máscara (CIDR) | Rango de IPs útiles               | Hosts útiles |
|--------------------|------------------|----------------|-----------------------------------|--------------|
| Comando Central    | 172.16.0.0       | /26            | 172.16.0.1 - 172.16.0.62          | 62           |
| Defensa Perimetral | 172.16.0.64      | /27            | 172.16.0.65 - 172.16.0.94         | 30           |
| Centro Médico      | 172.16.0.96      | /27            | 172.16.0.97 - 172.16.0.126        | 30           |
| Hangar y Taller    | 172.16.0.128     | /28            | 172.16.0.129 - 172.16.0.142       | 14           |
| Enlace Troncal     | 172.16.0.144     | /30            | 172.16.0.145 - 172.16.0.146       | 2            |

---

# Examen de Redes - Misión 2: Sabiduría de Yoda - Algoritmos de Enrutamiento y Rutas

**Situación:** Completando tu entrenamiento en Dagobah, el Maestro Yoda evalúa tu comprensión sobre los caminos que recorren los paquetes de datos en una red. Debes demostrar tu entendimiento sobre el enrutamiento estático y dinámico, así como los protocolos y métodos que definen su funcionamiento.

## Comparación entre Enrutamiento Estático y Dinámico

El enrutamiento es la técnica responsable de dirigir el tráfico de datos desde un origen hasta un destino en una red, determinando el camino más eficiente para la transmisión de información.

### 1. Enrutamiento Estático

- Las rutas son configuradas manualmente por un administrador de red.
- Permite simplicidad y control total.
- No se adapta automáticamente a los cambios en la red (falta de adaptabilidad).
- Su mantenimiento se vuelve complejo en redes grandes.
- Adecuado para redes pequeñas o conexiones específicas.

### 2. Enrutamiento Dinámico

- Las rutas se ajustan automáticamente usando protocolos de enrutamiento.
- Alta adaptabilidad a cambios en la red y fallos de enlaces.
- Requiere mayor procesamiento y recursos en los routers.
- Es más eficiente y escalable para grandes redes.

### Ventajas y Desventajas

**Enrutamiento Estático**
- Simplicidad.
- Mayor seguridad y control.
- No se adapta a cambios de topología.
- Requiere mantenimiento manual constante.

**Enrutamiento Dinámico**
- Adaptabilidad automática.
- Optimización del uso de recursos de red.
- Mayor complejidad.
- Requiere más recursos de procesamiento y memoria.

(continúa en siguiente bloque)
### Protocolos de Enrutamiento Dinámico

**Protocolos de Vector de Distancia**
- RIP (Routing Information Protocol): calcula la ruta según el número de saltos.
- IGRP (Interior Gateway Routing Protocol): mejora las limitaciones de RIP.

**Protocolos de Estado de Enlace**
- OSPF (Open Shortest Path First): determina la ruta más corta y eficiente.
- IS-IS (Intermediate System to Intermediate System): se utiliza en grandes redes corporativas.

**Protocolos Híbridos**
- EIGRP (Enhanced Interior Gateway Routing Protocol): combina las ventajas de los protocolos de vector de distancia y de estado de enlace.

### Diferencias Clave: Vector de Distancia vs Estado de Enlace

- **Vector de Distancia:** routers intercambian tablas completas de rutas con sus vecinos. Suelen ser más sencillos pero más lentos y menos escalables (ej.: RIP, IGRP).
- **Estado de Enlace:** cada router tiene una visión completa de la red. Es más rápido, preciso y escalable, pero requiere mayor capacidad de procesamiento y memoria (ej.: OSPF, IS-IS).

### Comportamiento ante Fallos o Escalabilidad

- Enrutamiento Estático: si un nodo cae, la ruta debe ser modificada manualmente.
- Enrutamiento Dinámico: el sistema detecta automáticamente la caída y busca una ruta alternativa, proporcionando redundancia y resiliencia.
- Para grandes redes (ej. conexión entre "muchos planetas") el enrutamiento dinámico es la única opción viable.

---


---

# Examen de Redes - Misión 3: Los Nombres del Holonet - DNS y Resolución de Nombres

**Situación:** La flota rebelde necesita comprender cómo los nombres simbólicos se traducen en direcciones IP para restablecer el servicio DNS rebelde. A bordo de la nave Home One, debes explicar el funcionamiento del Sistema de Nombres de Dominio (DNS) y su importancia.

## Funcionamiento básico del DNS

El Sistema de Nombres de Dominio (DNS) es un sistema jerárquico y descentralizado que traduce nombres de dominio fácilmente legibles (como holonet.rebelion.org) en direcciones IP (como 192.168.10.5). Sin DNS, los usuarios tendrían que recordar direcciones IP numéricas.

## Proceso de resolución de nombres

1. El usuario introduce un nombre de dominio en una aplicación (navegador, cliente de correo).
2. El sistema operativo consulta su caché local. Si no tiene la dirección, consulta al servidor DNS local (del ISP o configurado manualmente).
3. Si el servidor DNS local no dispone de la respuesta, realiza consultas iterativas hacia los servidores raíz, TLD y servidores autoritativos hasta encontrar la dirección IP.
4. Una vez resuelta, la dirección IP se devuelve al cliente.

## Tipos de consultas

- **Recursiva:** el servidor DNS devuelve la respuesta completa al cliente.
- **Iterativa:** el servidor DNS devuelve una referencia al siguiente servidor donde continuar la consulta.

## Tipos de servidores DNS

- **Primario o maestro:** mantiene la base de datos original del dominio.
- **Secundario o esclavo:** copia los datos del servidor primario.
- **Local o de caché:** no mantiene información permanente, solo temporalmente para acelerar futuras consultas.

## Registros DNS más comunes

- **A:** Traduce un nombre de dominio a una dirección IPv4.
- **AAAA:** Traduce un nombre de dominio a una dirección IPv6.
- **CNAME:** Define un alias de un dominio.
- **NS:** Define qué servidores de nombres son responsables de un dominio.
- **MX:** Asocia un dominio a servidores de correo.
- **PTR:** Asocia direcciones IP a nombres de dominio (resolución inversa).

## Ejemplo de resolución

Un usuario introduce en su navegador: holonet.rebelion.org  
El DNS resuelve y devuelve la IP 192.168.10.5 (ejemplo).

## Qué sucede si falla el servidor DNS

Si el servidor DNS no está disponible, no se pueden resolver nombres de dominio, por lo que las comunicaciones que dependen de nombres fallan. Solo es posible conectarse mediante direcciones IP conocidas.

## Importancia del DNS

El DNS facilita la navegación en Internet y redes IP al permitir utilizar nombres fáciles de recordar en lugar de direcciones IP numéricas. Además, aporta flexibilidad: las direcciones IP pueden cambiar sin necesidad de modificar los nombres de dominio.
# Examen de Redes - Misión 4: Es una trampa… de protocolos! – TCP vs UDP

**Situación:** Durante la batalla espacial sobre Endor, se detectan diferencias en la transmisión de datos. Algunas transmisiones son rápidas pero propensas a pérdidas (como streaming de vídeo), mientras otras son lentas pero garantizan la entrega completa (como los planos de la Estrella de la Muerte). Esto se debe al uso de los protocolos TCP y UDP.

### 1. TCP (Transmission Control Protocol)

- Protocolo orientado a conexión.
- Establece un enlace previo entre emisor y receptor antes de transmitir datos.
- Garantiza entrega completa, en orden y sin errores.
- Usa acuses de recibo, retransmisiones y sumas de comprobación.
- Consume más ancho de banda y recursos, introduce mayor latencia.
- Ideal para transmisión de datos críticos donde la integridad es prioritaria.
- Ejemplos: navegación web, correo electrónico, FTP, transferencia de planos de la Estrella de la Muerte.

### 2. UDP (User Datagram Protocol)

- Protocolo sin conexión.
- No establece ni mantiene una conexión entre emisor y receptor.
- Envia datagramas sin verificar la entrega, orden o integridad.
- Mucho más rápido y eficiente, menor retardo.
- Mayor riesgo de pérdida, duplicación o corrupción de datos.
- Adecuado para aplicaciones que priorizan la rapidez sobre la fiabilidad.
- Ejemplos: streaming de vídeo, juegos online, voz sobre IP, envío de coordenadas de combate en tiempo real desde un X-Wing.

### 3. Comparativa entre TCP y UDP

**TCP:**  
- Fiabilidad y precisión.  
- Control de congestión y flujo.  
- Seguridad y autenticación.  
- Mayor consumo de ancho de banda.  
- Introduce latencia y sobrecarga.  

**UDP:**  
- Baja latencia y alta eficiencia.  
- Menor carga de red.  
- Permite multidifusión.  
- No garantiza entrega ni orden.  
- Vulnerable a pérdidas y ataques.  

### Conclusión

TCP es ideal para comunicaciones críticas que requieren fiabilidad absoluta, como la transmisión de información estratégica o documentos importantes. UDP se utiliza cuando la velocidad es esencial y se puede tolerar alguna pérdida de datos, como en la transmisión en vivo de vídeo o coordenadas de combate en una misión rebelde.

---

# Examen de Redes - Misión 5: Comunicación Segura o lado oscuro – Criptografía y Seguridad de la Red

**Situación:** La Alianza Rebelde debe proteger sus comunicaciones de espías imperiales. Se requiere un sistema de cifrado para que los mensajes no puedan ser leídos si son interceptados.

### 1. Cifrado Simétrico

- Utiliza una única clave secreta para cifrar y descifrar la información.
- Rápido y consume pocos recursos, ideal para grandes cantidades de datos.
- Riesgo si la clave es interceptada, ya que compromete la seguridad de todas las comunicaciones.
- Ejemplos de algoritmos: AES, DES, Blowfish.
- Ejemplo galáctico: Leia y Luke comparten una clave para cifrar y descifrar holomensajes (cifrado simétrico).

### 2. Cifrado Asimétrico

- Utiliza un par de claves: una pública para cifrar y una privada para descifrar.
- Evita la necesidad de compartir una clave secreta de antemano.
- Proporciona autenticación y no repudio (el emisor no puede negar haber enviado el mensaje).
- Más lento y consume más recursos que el cifrado simétrico.
- Ejemplos de algoritmos: RSA, ECC, El Gamal.
- Ejemplo galáctico: La Alianza envía un mensaje a un nuevo aliado sin haber compartido una clave previamente (cifrado asimétrico).

### 3. Autenticación y No Repudio

- Autenticación: garantiza que el mensaje proviene de la fuente legítima.
- No repudio: impide que el emisor niegue haber enviado el mensaje.

### 4. Importancia de protocolos seguros

- SSH proporciona un canal cifrado y seguro para administrar remotamente los sistemas de la Alianza.
- Telnet transmite datos sin cifrado, exponiendo las comunicaciones al espionaje imperial.
- Por seguridad, siempre se debe utilizar SSH en lugar de Telnet en redes críticas.

### Conclusión

El cifrado es esencial para proteger las comunicaciones de la Alianza. El cifrado simétrico es más rápido pero requiere una clave compartida; el asimétrico es más seguro para iniciar comunicaciones sin contacto previo. La autenticación, el no repudio y el uso de protocolos seguros como SSH son clave para mantener la integridad y confidencialidad de la red rebelde.
