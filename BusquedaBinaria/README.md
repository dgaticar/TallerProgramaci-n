# 🔍 Búsqueda Binaria (Binary Search)

La **búsqueda binaria** es uno de los algoritmos fundamentales en programación. Permite encontrar un elemento o responder preguntas sobre un conjunto de datos de manera muy eficiente, reduciendo significativamente el número de operaciones necesarias en comparación con una búsqueda lineal.

---

# 🎯 ¿Qué problema resuelve?

Supongamos que tenemos un arreglo ordenado:

```text
[1, 3, 5, 7, 9, 11, 13]
```

y queremos saber si el número `9` se encuentra en él.

Una búsqueda lineal revisaría los elementos uno por uno:

```text
1 → 3 → 5 → 7 → 9
```

En el peor caso necesitaríamos revisar todos los elementos.

La búsqueda binaria aprovecha que el arreglo está ordenado para descartar la mitad de los elementos en cada paso.

---

# 💡 Idea Principal

En cada iteración:

1. Se observa el elemento del medio.
2. Si es la respuesta, terminamos.
3. Si la respuesta es menor, descartamos la mitad derecha.
4. Si la respuesta es mayor, descartamos la mitad izquierda.

De esta forma el espacio de búsqueda se reduce a la mitad constantemente.

---

# 📖 Ejemplo

Buscar el número `9` en:

```text
[1, 3, 5, 7, 9, 11, 13]
```

### Paso 1

```text
1 3 5 [7] 9 11 13
      ↑
```

El elemento central es `7`.

Como:

```text
9 > 7
```

descartamos toda la mitad izquierda.

---

### Paso 2

```text
9 [11] 13
   ↑
```

El elemento central es `11`.

Como:

```text
9 < 11
```

descartamos la mitad derecha.

---

### Paso 3

```text
[9]
 ↑
```

Encontramos la respuesta.

---

# ⏱️ Complejidad

Cada paso elimina aproximadamente la mitad de los elementos.

Número de operaciones:

```text
n
n/2
n/4
n/8
...
1
```

Por lo tanto:

[
T(n)=O(\log n)
]

Esto es mucho más eficiente que una búsqueda lineal:

| Algoritmo        | Complejidad |
| ---------------- | ----------- |
| Búsqueda Lineal  | (O(n))      |
| Búsqueda Binaria | (O(\log n)) |

---

# 💻 Implementación Clásica

### C++

```cpp
int binarySearch(vector<int>& a, int x) {
    int l = 0;
    int r = (int)a.size() - 1;

    while (l <= r) {
        int mid = l + (r - l) / 2;

        if (a[mid] == x)
            return mid;

        if (a[mid] < x)
            l = mid + 1;
        else
            r = mid - 1;
    }

    return -1;
}
```

---

# 🧠 Invariante

Durante toda la ejecución mantenemos:

```text
La respuesta, si existe, está dentro del intervalo [l, r].
```

Cada actualización conserva esta propiedad.

---

# 📍 Lower Bound

Muchas veces no queremos encontrar exactamente un valor, sino la primera posición donde podría insertarse.

Ejemplo:

```text
[1, 3, 3, 3, 5, 8]
```

Buscar la primera posición donde aparece `3`.

Resultado:

```text
índice = 1
```

Implementación:

```cpp
int lower_bound(vector<int>& a, int x) {
    int l = 0;
    int r = a.size();

    while (l < r) {
        int mid = l + (r - l) / 2;

        if (a[mid] < x)
            l = mid + 1;
        else
            r = mid;
    }

    return l;
}
```

---

# 📍 Upper Bound

Devuelve la primera posición con un valor estrictamente mayor que `x`.

Ejemplo:

```text
[1, 3, 3, 3, 5, 8]
```

Para:

```text
x = 3
```

retorna:

```text
4
```

porque:

```text
a[4] = 5
```

---

# 🚀 Búsqueda Binaria sobre la Respuesta

Una de las aplicaciones más importantes en programación competitiva.

A veces no buscamos un elemento en un arreglo, sino el valor óptimo de una respuesta.

---

## Ejemplo

Disponemos de tablas de madera de distintas longitudes y queremos cortarlas para obtener al menos `k` piezas.

Pregunta:

```text
¿Cuál es la máxima longitud posible de cada pieza?
```

En lugar de probar todas las longitudes posibles, realizamos búsqueda binaria sobre la respuesta.

Definimos:

```text
f(x) = ¿Es posible obtener al menos k piezas
       usando longitud x?
```

Si:

```text
f(x) = verdadero
```

entonces cualquier longitud menor también será posible.

Esto genera una estructura monotónica:

```text
V V V V V V F F F F
```

y podemos aplicar búsqueda binaria.

---

# 📈 Condición para usar Búsqueda Binaria

Generalmente necesitamos:

### Espacio de búsqueda ordenado

Por ejemplo:

```text
1 2 3 4 5 6 7 8
```

---

### Propiedad monotónica

Algo similar a:

```text
F F F F V V V V
```

o

```text
V V V V F F F F
```

donde existe un punto de cambio.

---

# ⚠️ Errores Comunes

### 1. Overflow al calcular el medio

Incorrecto:

```cpp
int mid = (l + r) / 2;
```

Correcto:

```cpp
int mid = l + (r - l) / 2;
```

---

### 2. Intervalos mal definidos

Confundir:

```text
[l, r]
```

con

```text
[l, r)
```

es una de las fuentes más frecuentes de errores.

---

### 3. Bucles infinitos

Si los límites no se actualizan correctamente:

```cpp
l = mid;
r = mid;
```

el algoritmo puede no terminar.

---

# 🏆 Problemas Clásicos

* Encontrar un elemento en un arreglo ordenado.
* Lower Bound / Upper Bound.
* Primer valor verdadero.
* Último valor verdadero.
* Binary Search on Answer.
* Optimización de recursos.
* Problemas de partición y planificación.

---

# 📚 Resumen

La búsqueda binaria es una técnica que reduce el espacio de búsqueda a la mitad en cada paso.

Características principales:

✅ Requiere un dominio ordenado o una propiedad monotónica.

✅ Complejidad:

[
O(\log n)
]

✅ Es una herramienta fundamental para resolver problemas de búsqueda y optimización.

Dominar búsqueda binaria es indispensable para avanzar en algoritmos y programación competitiva.
