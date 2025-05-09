# Simulacro2

Enlace página:https://fferrlop.github.io/Simulacro2/

Enlace repositorio: https://github.com/fferrlop/Simulacro2.git

# Parte I: Capa de Red

## Pregunta 1: Cálculo de Ruta Más Corta

### a) Funcionamiento del Algoritmo de Dijkstra

El **Algoritmo de Dijkstra** se utiliza para encontrar la **ruta más corta** desde un nodo origen hasta todos los demás nodos en un grafo ponderado sin pesos negativos. Su funcionamiento se basa en los siguientes pasos:

1. **Inicialización**:
   - Se asigna una distancia de `0` al nodo origen y `∞` (infinito) a los demás nodos.
   - Se marcan todos los nodos como no visitados.

2. **Selección del nodo actual**:
   - Se elige el nodo no visitado con la menor distancia conocida.

3. **Actualización de vecinos**:
   - Se actualizan las distancias de los nodos vecinos si la nueva distancia calculada es menor que la conocida.

4. **Marcado como visitado**:
   - El nodo actual se marca como visitado y no se vuelve a revisar.

5. **Repetición**:
   - Se repiten los pasos anteriores hasta visitar todos los nodos o alcanzar el destino.

**Ventajas**:
- Encuentra rutas óptimas.
- Eficiente en grafos densos.
- Evita ciclos y repeticiones innecesarias.

---

### b) Enrutamiento por Inundación (Flooding)

El **enrutamiento por inundación** es una técnica en la que cada nodo reenvía una copia del paquete por todas sus interfaces (excepto la de entrada). No requiere conocimiento previo de la topología de la red.

**Funcionamiento**:
- Cada paquete recibido se reenvía por todas las salidas posibles.
- Se usan mecanismos para evitar bucles, como:
  - **TTL (Time To Live)**: el paquete se elimina al alcanzar un número de saltos.
  - **Identificadores únicos**: se descartan paquetes duplicados ya vistos.

**Ventajas**:
- Alta fiabilidad: el paquete llega por múltiples rutas.
- Simplicidad: no requiere tablas de enrutamiento.

**Desventajas**:
- Consumo excesivo de ancho de banda.
- Genera congestión y redundancia.
- No escala bien con redes grandes.

---

### Comparación: Dijkstra vs Enrutamiento por Inundación

| Característica                  | Dijkstra                              | Enrutamiento por Inundación           |
|---------------------------------|----------------------------------------|----------------------------------------|
| Tipo de algoritmo               | Determinista                          | No determinista                        |
| Ruta elegida                    | La más corta (óptima)                 | Todas posibles                         |
| Consumo de ancho de banda       | Eficiente                             | Alto                                   |
| Escalabilidad                   | Alta                                  | Baja                                   |
| Requiere conocimiento de la red| Sí (matriz de costos)                 | No                                     |
| Complejidad computacional       | Alta (O(n²) o mejor con estructuras)  | Baja, pero elevado coste de red        |


![Comparación_ Dijkstra vs Enrutamiento por Inundación - visual selection](https://github.com/user-attachments/assets/cccafc7f-be9d-4cec-978d-6539860578f0)


## Pregunta 2: Cálculo de Direcciones de Broadcast y Subredes

### a) Subred 172.29.152.0 con máscara 255.255.248.0

**Paso 1: Convertir la máscara a binario**

La máscara `255.255.248.0` se convierte a binario de la siguiente manera:

```
255   = 11111111
255   = 11111111
248   = 11111000
0     = 00000000
-------------------------------
         11111111.11111111.11111000.00000000
```

Esto corresponde a una **máscara /21**, lo que implica que los primeros 21 bits están en 1 y los últimos 11 en 0.

**Paso 2: Determinar la cantidad de direcciones**

Con 11 bits para host, el número total de direcciones en esta subred es:

```
2^11 = 2048 direcciones
```

**Paso 3: Determinar el rango de direcciones**

La dirección de red es `172.29.152.0`. El tercer octeto (`152`) en binario es:

```
152 = 10011000
```

Dado que 3 bits del tercer octeto están dedicados al host (porque son parte de los 11 bits de host), el valor del tercer octeto puede variar desde:

```
10011000 = 152
10011001 = 153
10011010 = 154
10011011 = 155
10011100 = 156
10011101 = 157
10011110 = 158
10011111 = 159
```

Es decir, desde `172.29.152.0` hasta `172.29.159.255`.

**Paso 4: Determinar la dirección de broadcast**

La **última dirección del rango** es la dirección de broadcast:

```
Broadcast: 172.29.159.255
```

---

### b) Bloque 172.18.26.0/23

**Paso 1: Convertir la máscara a binario**

El prefijo `/23` equivale a la máscara `255.255.254.0`, que en binario se representa como:

```
255 = 11111111
255 = 11111111
254 = 11111110
0   = 00000000
-------------------------------
      11111111.11111111.11111110.00000000
```

Esto representa **23 bits en 1** y **9 bits en 0**, es decir, 9 bits para los hosts.

**Paso 2: Calcular número total de direcciones**

Con 9 bits para host:

```
2^9 = 512 direcciones
```

**Paso 3: Determinar el rango de direcciones**

La red empieza en `172.18.26.0`. Como son 512 direcciones, y cada bloque /24 tiene 256 direcciones, esta subred abarca:

- `172.18.26.0 – 172.18.26.255`
- `172.18.27.0 – 172.18.27.255`

Por tanto, el rango completo es:

```
172.18.26.0 hasta 172.18.27.255
```

**Paso 4: Determinar la dirección de broadcast**

La última dirección de este rango es:

```
Broadcast: 172.18.27.255
```

**Justificación**: El bloque `/23` une dos redes `/24`, por lo que la última IP del segundo bloque (`172.18.27.255`) actúa como dirección de broadcast para todo el conjunto.

## Pregunta 3: Última Dirección Válida y Rango de Hosts

### a) Subred 172.30.67.192 con máscara 255.255.255.192

Máscara en binario:

```
255.255.255.192 = 11111111.11111111.11111111.11000000
```

Esta es una máscara **/26**, lo que implica `2^6 = 64` direcciones totales. La subred empieza en `172.30.67.192`, por lo tanto:

- Rango: `172.30.67.192 – 172.30.67.255`
- Dirección de broadcast: `172.30.67.255`
- Última dirección de host válida: `172.30.67.254`

### b) Host 172.22.53.199 con máscara 255.255.252.0

Máscara en binario:

```
255.255.252.0 = 11111111.11111111.11111100.00000000
```

Esta es una máscara **/22**, con bloques de `2^10 = 1024` direcciones. El cuarto octeto varía de 0 a 255, y el tercer octeto varía en bloques de 4:

- `53 / 4 = 13`, por lo que la subred empieza en `172.22.52.0`
- Rango: `172.22.52.0 – 172.22.55.255`
- Rango de hosts válidos: `172.22.52.1 – 172.22.55.254`

---

## Pregunta 4: Capacidad y Segmentación de Subredes

### a) Red 172.26.0.0 con máscara 255.255.255.192

Máscara en binario:

```
255.255.255.192 = 11111111.11111111.11111111.11000000
```

Esto es una máscara **/26**, lo que da `2^6 = 64` direcciones totales por subred.

- Hosts utilizables: `64 - 2 = 62` equipos (se restan red y broadcast)

### b) Host 172.18.171.190/23

Máscara `/23` equivale a `255.255.254.0`, cubre bloques de 512 direcciones.

- El tercer octeto `171` -> `171 / 2 = 85.5`, por lo tanto, bloque comienza en `170`
- Subred: `172.18.170.0/23`
- Rango: `172.18.170.0 – 172.18.171.255`

---

## Pregunta 5: Número de Subredes Necesarias

La fórmula para calcular el número de subredes disponibles es:

```
Número de subredes = 2^s
```

Donde `s` es el número de bits tomados prestados del identificador de host para usarse como identificador de subred.

### Ejemplo:

Si se necesitan al menos 4 subredes:

```
2^s ≥ 4  →  s = 2 bits (porque 2^2 = 4)
```

Entonces, al tomar prestados 2 bits del campo de host, se pueden crear 4 subredes distintas.

---

# Parte II: Capa de Transporte

## Pregunta 6: Comparación entre TCP y UDP

### a) Comparación

| Característica                 | TCP                                      | UDP                                |
|-------------------------------|------------------------------------------|------------------------------------|
| Conexión                      | Requiere establecimiento (orientado a conexión) | No requiere conexión               |
| Fiabilidad                    | Garantiza entrega y orden                | No garantiza entrega ni orden      |
| Control de errores            | Sí, con retransmisiones                  | No                                 |
| Control de flujo/congestión   | Sí                                       | No                                 |
| Velocidad                     | Más lento                                | Más rápido                         |

### b) Ejemplos de aplicaciones que usan UDP

1. **Streaming de video/audio en tiempo real (ej. IPTV, VoIP):** la baja latencia es prioritaria, incluso si se pierden algunos paquetes.
2. **DNS (Domain Name System):** las consultas son pequeñas y rápidas, y no requieren una conexión establecida.

---

## Pregunta 7: Establecimiento y Terminación de Conexión en TCP

### Establecimiento (Three-Way Handshake)

1. **SYN:** el cliente envía un segmento con el flag SYN al servidor.
2. **SYN-ACK:** el servidor responde con un segmento con los flags SYN y ACK.
3. **ACK:** el cliente envía un ACK final y la conexión se establece.

![Establecimiento y Terminación de Conexión en TCP - visual selection (1)](https://github.com/user-attachments/assets/b1846e5b-df92-47d0-8b24-0640e78642be)


### Terminación (Four-Way Handshake)

1. **FIN:** el host que quiere terminar envía un segmento con FIN.
2. **ACK:** el receptor responde con ACK.
3. **FIN:** el receptor envía su propio FIN para cerrar su lado.
4. **ACK:** el iniciador responde con ACK final.


![Establecimiento y Terminación de Conexión en TCP - visual selection](https://github.com/user-attachments/assets/adcf94db-d751-422e-84e2-531e88c5c451)


Cada paso asegura una finalización ordenada y confiable de la conexión.

---

## Pregunta 8: Multiplexación y Demultiplexación

- **Multiplexación ascendente:** múltiples procesos (puertos) envían datos a través de una única conexión de red. Ejemplo: varios servicios en una máquina comparten una sola IP.

- **Multiplexación descendente (demultiplexación):** cuando los datos llegan a un dispositivo, la capa de transporte los entrega al proceso correcto mediante el número de puerto. Ejemplo: un servidor web escucha en el puerto 80 y otro servicio en el puerto 443.

## Pregunta 9: Cálculo del Tamaño de Ventana en TCP

Se tiene un enlace con los siguientes parámetros:

- **RTT** = 50 ms
- **Ancho de banda** = 100 Mbps
- **MSS (Tamaño máximo de segmento)** = 1,500 bytes

### Paso 1: Convertir unidades

- RTT = 50 ms = 0.05 segundos
- Ancho de banda = 100 Mbps = 100 × 10^6 bits por segundo

### Paso 2: Calcular el tamaño óptimo de la ventana

Fórmula:

```
Ventana óptima (bits) = Ancho de banda × RTT
                      = 100,000,000 bps × 0.05 s
                      = 5,000,000 bits
```

Convertimos a bytes:

```
5,000,000 bits ÷ 8 = 625,000 bytes
```

### Paso 3: Calcular número de segmentos MSS simultáneos

```
Número de MSS = Ventana óptima (bytes) ÷ MSS
              = 625,000 ÷ 1,500
              ≈ 416.67 segmentos
```

### Resultado

- Ventana óptima: **625,000 bytes**
- Número de MSS simultáneos: **≈ 417 segmentos**

---

## Pregunta 10: Control de Congestión en TCP

TCP implementa mecanismos para evitar la congestión de red y mantener un rendimiento óptimo. A continuación se describen tres algoritmos clave:

### Algoritmo de Arranque Lento (Slow Start)

**Objetivo:** Aumentar gradualmente la tasa de envío para evitar sobrecargar la red al inicio de una conexión.

**Funcionamiento:** TCP comienza con una ventana de congestión pequeña (generalmente 1 MSS) y la duplica con cada ACK recibido hasta llegar al umbral de congestión (ssthresh), momento en el que cambia a crecimiento lineal (congestion avoidance).

**Contribución:** Permite que TCP detecte rápidamente la capacidad de la red sin generar congestión excesiva.

---

### Algoritmo de Nagle

**Objetivo:** Reducir el número de pequeños segmentos enviados por la red (problema conocido como "silly window syndrome").

**Funcionamiento:** Acumula pequeños datos hasta que se ha recibido un ACK o se alcanza el MSS, y entonces los envía juntos.

**Contribución:** Mejora la eficiencia de la red reduciendo la sobrecarga y la fragmentación.

---

### Algoritmo de Clark

**Objetivo:** Prevenir el envío de segmentos pequeños cuando el receptor anuncia una ventana pequeña.

**Funcionamiento:** El emisor no envía datos hasta que tenga suficiente espacio para un segmento completo (MSS) o hasta que pueda enviar todos los datos pendientes.

**Contribución:** Evita la fragmentación y la sobrecarga innecesaria, mejorando la eficiencia cuando las ventanas son pequeñas.

# Parte III: Capa de Aplicación y Aplicaciones Multimedia

## Pregunta 11: Funcionamiento de DNS

El proceso de resolución de nombres en DNS incluye los siguientes pasos:

1. El usuario ingresa un dominio en el navegador (ej. www.ejemplo.com).
2. El navegador consulta primero su caché local.
3. Si no encuentra respuesta, pregunta al sistema operativo, que consulta su propia caché.
4. Si no hay coincidencia, se realiza una consulta al servidor DNS configurado (normalmente el del ISP).
5. Si el servidor DNS no conoce la respuesta:
   - Consulta un servidor raíz.
   - El servidor raíz responde con la dirección de un servidor TLD (.com, .org, etc.).
   - El TLD responde con la dirección del servidor autoritativo del dominio.
6. El servidor autoritativo proporciona la dirección IP del dominio.
7. Esta IP se devuelve al navegador, que establece la conexión con el servidor correspondiente.


![Funcionamiento de DNS - visual selection](https://github.com/user-attachments/assets/33948c09-9d8e-45c6-9e91-d3937ddbe9a0)


---

## Pregunta 12: Protocolos de Correo Electrónico

| Protocolo | Función principal     | Tipo de uso/acceso        | Almacenamiento de correos                    | Ejemplo de uso                              |
|----------|------------------------|----------------------------|---------------------------------------------|---------------------------------------------|
| POP3     | Descargar correos      | Solo lectura desde un cliente | Localmente en el dispositivo cliente        | Usuario con conexión limitada o sincrónica  |
| IMAP     | Gestionar correos remotos | Acceso desde múltiples dispositivos | En el servidor                             | Usuario con varios dispositivos             |
| SMTP     | Enviar correos         | Salida de mensajes         | No almacena, solo transfiere mensajes       | Envío de correos desde cliente a servidor   |

---

## Pregunta 13: Funcionamiento de HTTP y FTP

### a) HTTP

HTTP es un protocolo sin estado basado en peticiones y respuestas entre cliente y servidor. Los métodos más comunes son:

- **GET**: Solicita un recurso.
- **POST**: Envía datos al servidor.
- **PUT**: Reemplaza un recurso existente.
- **DELETE**: Elimina un recurso.

### b) FTP

FTP (File Transfer Protocol) permite la transferencia de archivos. Usa dos conexiones:

- **Canal de control**: para comandos y respuestas.
- **Canal de datos**: para la transferencia de archivos.

**Diferencias clave** con HTTP:
- FTP mantiene estado de sesión y dos conexiones separadas.
- HTTP usa una sola conexión por cada solicitud.

---

## Pregunta 14: Streaming y VoIP

### a) Tipos de streaming

| Tipo                   | Descripción                                         | Ejemplo                         |
|------------------------|-----------------------------------------------------|----------------------------------|
| UDP Streaming          | Transmisión en tiempo real, sin control de errores  | IPTV, videollamadas              |
| HTTP Streaming         | Transmisión progresiva a través de HTTP             | YouTube                         |
| Adaptive HTTP (DASH)   | Adapta la calidad al ancho de banda disponible      | Netflix, Amazon Prime           |

### b) Funcionamiento de VoIP

- Convierte voz analógica a digital.
- Se comprime y empaqueta.
- Se transmite usando RTP sobre UDP.
- Se reconstruye en el receptor.

**Problemas comunes**:
- **Retardo**: se mitiga con QoS y priorización.
- **Pérdida de paquetes**: uso de buffers y corrección de errores.
- **Eco**: canceladores de eco en hardware/software.

---

## Pregunta 15: Control de Congestión en Redes Multimedia

1. **Buffering en el cliente**:
   - Almacena parte del contenido antes de reproducirlo.
   - Previene interrupciones ante variaciones de red.

2. **Marcado de paquetes (DiffServ)**:
   - Clasifica paquetes con distintos niveles de prioridad.
   - Asegura tratamiento diferenciado para flujos multimedia sensibles.

---

## Pregunta 16: Best-Effort vs Servicios Multiclase

| Característica          | Best-Effort                          | Servicios Multiclase                    |
|-------------------------|--------------------------------------|-----------------------------------------|
| Manejo del tráfico      | Todos los paquetes tratados igual    | Priorización según tipo de tráfico      |
| Garantía de calidad     | No garantiza QoS                     | Puede ofrecer garantías de QoS          |
| Ejemplos de uso         | Navegación web, correo electrónico   | Videollamadas, streaming, VoIP          |

---

# Parte IV: Seguridad en Redes

## Pregunta 17: Problemas de Seguridad en Redes

| Área              | Descripción                                         | Solución habitual                  |
|-------------------|-----------------------------------------------------|------------------------------------|
| Confidencialidad  | Evitar acceso no autorizado a la información        | Cifrado (SSL/TLS, AES)             |
| Autenticación     | Verificar identidad del usuario o sistema           | Contraseñas, tokens, MFA           |
| No repudio        | Garantizar que un emisor no niegue su mensaje       | Firmas digitales                   |
| Integridad        | Asegurar que el mensaje no ha sido alterado         | Hashing (SHA-256), HMAC            |

---

## Pregunta 18: Cifrado Simétrico vs Asimétrico

| Característica         | Simétrico                      | Asimétrico                          |
|------------------------|--------------------------------|--------------------------------------|
| Nº de claves           | 1 clave compartida             | Par de claves (pública/privada)     |
| Velocidad              | Rápido                         | Más lento                           |
| Ejemplos               | AES, DES                       | RSA, ECC                            |
| Aplicaciones típicas   | Cifrado de datos masivo        | Intercambio seguro de claves, firma |

---

## Pregunta 19: Funcionamiento del Algoritmo RSA

### a) Proceso de generación de claves

1. Elegir dos primos `p` y `q`.
2. Calcular `n = p × q`.
3. Calcular `ϕ(n) = (p-1)(q-1)`.
4. Elegir `e` tal que sea coprimo con `ϕ(n)`.
5. Calcular `d` como el inverso modular de `e` mod `ϕ(n)`.

### b) Ejemplo con p=3, q=11, e=7, M=4

1. `n = 3 × 11 = 33`
2. `ϕ(n) = (3-1)(11-1) = 2 × 10 = 20`
3. `e = 7`
4. Buscar `d` tal que `7 × d ≡ 1 mod 20` → `d = 3`
5. Cifrado: `C = M^e mod n = 4^7 mod 33 = 16384 mod 33 = 16`
6. Descifrado: `M = C^d mod n = 16^3 mod 33 = 4096 mod 33 = 4`

---

## Pregunta 20: Firewalls, VPN e IPSec

### a) Firewall

- **Filtrado de paquetes**: inspecciona encabezados de IP y decide permitir o denegar.
- **Firewall de estado**: guarda el estado de conexiones activas para decisiones más inteligentes.

Ambos protegen de accesos no autorizados.

### b) VPN vs IPSec

| Característica     | VPN                                 | IPSec                                 |
|--------------------|--------------------------------------|----------------------------------------|
| Propósito          | Crear túnel seguro entre redes       | Proveer cifrado a nivel de red         |
| Funcionamiento     | Usa protocolos como PPTP, L2TP, SSL  | Funciona en modo transporte o túnel    |
| Ejemplo de uso     | Acceso remoto de usuarios móviles    | Conexión cifrada entre routers         |

---

## Pregunta 21: SSL/TLS y DNS Spoofing

### a) SSL/TLS

- Protocolo que cifra la comunicación entre cliente y servidor.
- Se usa en HTTPS para garantizar confidencialidad, autenticación e integridad.
- Involucra handshake con intercambio de claves y establecimiento de sesión segura.

### b) DNS Spoofing y DNSSEC

- **DNS Spoofing**: ataque que suplanta una respuesta DNS legítima por una falsa.
- **DNSSEC**: protege la integridad de las respuestas DNS mediante firmas digitales, asegurando que provienen de fuentes legítimas.
