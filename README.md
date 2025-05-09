# Simulacro2

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

