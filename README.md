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
