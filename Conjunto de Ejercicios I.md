# Conjunto de Ejercicios I

## 3.3.1

### (a) C

1. ![](/dict-c.png)

2. Las constantes númericas pueden ser del tipo Entero o Punto flotante (integer, floating-poing). Un entero es una secuencia de digitos `[0-9]+`. Y las constantes de tipo punto flotante contienen un parte entera, un punto decimal, un parte de fracción, un `e` y un opcional exponente entero.

3. 

## 3.3.2

d. Cadena de a's y b's que solo contiene tres b's.

e. Cadena de a's y b's que tienen un número par de a's y b's.

## 3.3.4

Una posible respuesta es:

```regex
[Ss][Ee][Ll][Ee][Cc][Tt]
```

## 3.3.5

a)

```
palabra → consonante* a (consonante|a)* e (consonante|e)* i (consonante|i)* o (consonante|o)* u (consonante|u)*
consonante -> [bcdfghjklmnñpqrstvwxyz]
```

b)

```
a* b* ... z*
```

c)

```
\/\*([^*"]*|".*"|\*+[^/])*\*\/
```

d)

```
frase -> 0|A?0?1(A0?1|01)*A?0?|A0?
A -> 0?2(02)*
```

e)

```
frase -> (FE*G|(aa)*b)(E|FE*G)
E -> b(aa)*b
F -> a(aa)*b
G -> b(aa)*ab|a
F -> ba(aa)*b
```

## 3.3.7

```
\"\\
```

## 3.3.8

Se puede demostrar lo anterior con una expresión que escriba explicitamente los caractares excepto los que se esta buscando. Dicho de otra manera si el caracter `^` representa en conjunto formado por la negación del conjunto $A$, tambien podemos escribir de manera explicita el conjunto $\bar A$. (La negación de $A$).

## 3.3.10

Si `^` es un par de corchetes, y es la primera letra, eso significa clases complementadas, o significa el final izquierdo de la linea.

## 3.3.11

1. Para reemplazar la cadena `'s'` solo se necesita reconocer que cada caracter es una expresión regular, y como tenemos la concatenación tambien debemos de tener la cadena como una expresión regular
   
   $$
   (c_1) (c_2) (c_3)  \cdots  (c_n)
   $$
   
   Siendo el $c_i$ el caracter de $s$ en la posición $i$.

2. El caracter es trivial pues $(c)$ es una expresión regular

3. Cualquier cadena debe ser una expresión regular por que tenemos la clausura (estrella de Kleen) y la unión
   
   Utilizamos la unión para crear un caracter que acepta a cualquier elemento de nuestro diccionario $\Sigma$. Y a partir de aqui utilizamos la estrella de Kleen
   
   $$
   ((c_1)|(c_2)|\cdots|(c_n))*
   $$

4. Cualquier caracter seria equivalente al paso anterior pero sin la estrella de Kleen

5. Seria en vez de utilizar la concatenación en el literal 1, utilzar la unión.

## 3.3.12

Como SQL solo tiene los dos más rudimentarias formas de reconocimiento de patrones que es el de cualquier caracter, el cual podemos describir con la expresión regular de la unión de todos los caracteres de nuestro alfabeto $\Sigma$, y el siguiente que seria cualquier cadena de 0 o más caracteres que podemos expresar como el anterior con la estrella de Kleen.

Encontramos que todo expresión puede ser expresada como una expresión regular, teniendo en cuenta que cuando encontramos el elemento $e$, este representa escape, o sea, el siguiente elemento tiene que ser el literal en si. El cuál solo necesita de una simple transformación inicial, pasar por la cadena y convertir los elementos siguientes a $e$ al propio literal.

## 3.4.1

d)

![](/transition01.png)

e)

![](/transition02.png)

## 3.4.3

a)

| s    | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   | 9   |
| ---- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| f(s) | 0   | 0   | 1   | 2   | 3   | 2   | 3   | 1   | 2   |

b)

| s    | 1   | 2   | 3   | 4   | 5   | 6   |
| ---- | --- | --- | --- | --- | --- | --- |
| f(s) | 0   | 1   | 2   | 3   | 4   | 5   |

c)

| s    | 1   | 2   | 3   | 4   | 5   | 6   | 7   |
| ---- | --- | --- | --- | --- | --- | --- | --- |
| f(s) | 0   | 0   | 0   | 1   | 1   | 2   | 3   |

## 3.4.4

Es facilmente comprobable que en el primer caso siempre se cumple, ya que el valor siempre tiene que ser cero al buscarse un prefijo y sufijo propios. (Paso base).

Suponga que el algorimo es correcto para cadenas de tamaño $n$.

La linea cuatro del algorimo encuentra el mayor prefijo propio que tambien es un sufijo, encontrado hasta el momento, el cuál por suposición es correcto.

El resto del algorimo busca cuál es elemento hasta el cuál se cumple la relación y le suma uno al final al cumplir con la relación y mantenerse el prefijo propio con sufijo.

$\square$

## 3.4.5

Este hecho es facilmente demostrable por la propiedad obvia de que la función $f$ que $f(x) \le x$. El peor de los casos es cuando $f(x) = x$, por lo cuál se demora un número maximo de $n$ pasos.

$\square$

## 3.4.6

Implementación en Python

```python
def failure(b):
    t = 0
    f = {}
    f[1] = 0
    for s in range(1, len(b)):
        while t > 0 and b[s] != b[t]:
            t = f[t]
        if b[s] == b[t]:
            t = t+1
            f[s+1] = t
        else:
            f[s+1] = 0
    return f


def kmp(a,b):
    f = failure(b)
    s = 0
    for i in range(1, len(a) + 1):
        while s > 0 and a[i-1] != b[s]:
            s = f[s]
        if a[i-1] == b[s]: s = s+1
        if s == len(b): return "Yes"
    return "No"
```

a) 'Yes'

b) 'No'

## 3.4.9

a) El número fibonacci. $\text{fib}(n)$, $\text{fib}(5) = 5$

b) $s_6 = abaababa$

| s    | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   |
| ---- | --- | --- | --- | --- | --- | --- | --- | --- |
| f(s) | 0   | 0   | 1   | 1   | 2   | 4   | 5   | 1   |

c) $s_7 = abaababaabaab$

| s    | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   | 9   | 10  | 11  | 12  | 13  |
| ---- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| f(s) | 0   | 0   | 1   | 1   | 2   | 3   | 2   | 3   | 4   | 5   | 6   | 4   | 5   |

d)

Primero notamos el hecho de que $s_k = s_{k-1}s_{k-2}$  y al mismo tiempo que $s_{k-1} = s_{k-2} s_{k-3}$. De tal manera que $s_k = s_{k-2}s_{k-3}s_{k-2}$.

Notamos que la subcadena siempre tiene un prefijo propio que tambien es sufijo, después a través del $j$ encontramos hasta que punto se ha construido el $s_{k-2}$ (en caso de que no se haya completado). Entonces la diferencia $j - |s_{k-1}|$ representa "cuanto ha sido construido del segundo $s_{k-2}$ presente en $s_k$".

La condición $|s_k| \le j + 1$, solo se agrega para los casos tempranos de fibonacci $f(1)$ y $f(2)$

$\square$

e)

El paso maximo "consecutivo" de llamadas seria $\mathcal{O}(n)$. Y las llamadas totales deberian de ser $\mathcal{O}(mn)$.
