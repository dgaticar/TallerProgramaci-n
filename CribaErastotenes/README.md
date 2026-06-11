# 🧮 Criba de Eratóstenes (Sieve of Eratosthenes)

La **Criba de Eratóstenes** es un algoritmo clásico utilizado para encontrar todos los números primos menores o iguales a un número (N). Es una de las técnicas más importantes en teoría de números y programación competitiva.

---

# 🎯 ¿Qué problema resuelve?

Dado un número (N), queremos obtener todos los números primos en el rango:

[
1 \le x \le N
]

Ejemplo:

```text id="8xv7q2"
N = 20
```

Primos:

```text id="b91k2m"
2, 3, 5, 7, 11, 13, 17, 19
```

---

# 💡 Idea principal

La idea es simple:

1. Consideramos todos los números como potencialmente primos.
2. Empezamos desde el primer primo (2).
3. Eliminamos todos sus múltiplos.
4. Repetimos con el siguiente número no eliminado.

Al final, los números que no fueron eliminados son primos.

---

# 🔍 Ejemplo rápido

Para (N = 10):

```text id="q2m9aa"
2 3 4 5 6 7 8 9 10
```

* Marcamos múltiplos de 2 → 4,6,8,10
* Marcamos múltiplos de 3 → 6,9
* Resultado:

```text id="p7xk11"
2 3 5 7
```

---

# 🚀 Optimización clave

Cuando procesamos un primo (p), no necesitamos empezar desde (2p), sino desde:

[
p^2
]

Porque todos los múltiplos menores ya fueron marcados por primos anteriores.

---

# 💻 Implementación básica

```cpp id="c8d1xq"
vector<bool> prime(N + 1, true);
prime[0] = prime[1] = false;

for (int i = 2; i * i <= N; i++) {
    if (prime[i]) {
        for (int j = i * i; j <= N; j += i) {
            prime[j] = false;
        }
    }
}
```

---

# ⏱️ Complejidad

* Tiempo:
  [
  O(N \log \log N)
  ]

* Memoria:
  [
  O(N)
  ]

---

# 📦 Aplicaciones importantes

La criba no solo sirve para encontrar primos. Es una herramienta base para muchos problemas.

---

## 1. 🔢 Conteo de primos

Permite contar rápidamente cuántos primos hay hasta (N):

```cpp id="m2v9lp"
int count = 0;
for (int i = 2; i <= N; i++)
    if (prime[i]) count++;
```

---

## 2. 🔗 Múltiplos de un número

Una vez construida la criba, podemos responder rápidamente:

> ¿Cuáles son los múltiplos de un número?

Ejemplo:

* Múltiplos de 7 hasta (N):

```cpp id="k9p1ab"
for (int i = 7; i <= N; i += 7)
    cout << i << " ";
```

Esto se combina con la criba para resolver problemas como:

* contar números que no son múltiplos de primos
* eliminar números compuestos por condiciones

---

## 3. 🧩 Divisores eficientes

Usando la criba o SPF (Smallest Prime Factor), podemos obtener divisores de forma eficiente.

Si tenemos el SPF:

```text id="spf123"
12 → 2 × 2 × 3
```

los divisores se generan combinando factores:

[
1, 2, 3, 4, 6, 12
]

Esto permite resolver:

* número de divisores
* suma de divisores
* generación de todos los divisores

---

## 4. ⚡ Factorización rápida (SPF)

Una de las aplicaciones más importantes.

Precomputamos el **menor factor primo (SPF)** de cada número.

Ejemplo:

```text id="spfex"
10 → 2
12 → 2
15 → 3
21 → 3
```

Luego, factorizar un número es muy rápido:

### Ejemplo: 84

```text id="fact84"
84 → 2 × 42
42 → 2 × 21
21 → 3 × 7
7  → 7
```

Resultado:

[
84 = 2^2 \cdot 3 \cdot 7
]

Complejidad:

[
O(\log N)
]

---

## 5. 📊 Número de divisores

Con la factorización rápida:

Si

[
n = p_1^{a_1} p_2^{a_2} \cdots p_k^{a_k}
]

entonces:

[
d(n) = (a_1+1)(a_2+1)\cdots(a_k+1)
]

Ejemplo:

```text id="div84"
84 = 2^2 × 3^1 × 7^1
```

[
d(84) = (2+1)(1+1)(1+1) = 12
]

---

## 6. 🧮 Criba de múltiplos para problemas de conteo

La criba también puede adaptarse para marcar propiedades distintas a “ser primo”.

Ejemplo:

* contar números con exactamente 2 divisores primos
* eliminar números con factores repetidos
* filtrar múltiplos de un conjunto de primos

Esto se usa en problemas tipo:

> “cuántos números entre 1 y N no son divisibles por ningún primo menor que 20”

---

# ⚠️ Errores comunes

### ❌ No marcar 0 y 1

```cpp id="err01"
prime[0] = false;
prime[1] = false;
```

---

### ❌ Empezar en 2*i en vez de i*i

Menos eficiente.

---

### ❌ Overflow en i*i

```cpp id="overflow"
(long long)i * i
```

---

# 🏆 Problemas típicos

* Contar primos en rangos grandes
* Factorización de múltiples números
* Número de divisores
* Función de Euler φ(n)
* Problemas de optimización con divisibilidad
* Preprocesamiento para consultas rápidas

---

# 📌 Resumen

La Criba de Eratóstenes es una técnica fundamental que permite:

✅ Encontrar todos los primos hasta (N)
✅ Preprocesar información de divisibilidad
✅ Facilitar factorización rápida (SPF)
✅ Resolver problemas de conteo y teoría de números

Su versatilidad la convierte en una herramienta esencial en programación competitiva y matemáticas computacionales.
