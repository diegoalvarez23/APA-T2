# Segunda tarea de APA 2026: Manejo de números primos

> [!Caution]
>
> El objetivo de esta tarea es manejar los tipos de datos y las estructuras de control de flujo de
> Python. Existen bibliotecas que resuelven los apartados del enunciado de una manera más eficiente
> y, sin duda, más sencilla, pero su uso está prohibido.
>
> Además, se valorará también el uso de Markdown en la redacción del fichero README.md; en concreto,
> la inclusión de código fuente con las herramientas propias de Markdown para su realce sintáctico, y
> la inclusión de imágenes con las capturas de pantalla solicitadas. El fichero README.md deberá ser
> visualizado correctamente desde la página principal del repositorio GitHub del alumno sin ninguna
> intervención por parte del profesor.
>
> Dispone del fichero MARKDOWN.md con información básica para el uso de Markdown, así como con enlaces
> a la documentación oficial del mismo.
>
> ¿Quiere saber más?, consulte con el profesorado.
  
# Segunda tarea APA 2026 – Manejo de números primos

##  Nombre

Diego Álvarez

---

##  Archivo

* `primos.py`

---

##  Ejecución de tests

![Tests](tests.png)

---

##  Código

```python
"""
Nombre: Diego Álvarez

>>> [numero for numero in range(2, 50) if esPrimo(numero)]
[2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47]

>>> primos(50)
(2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47)

>>> descompon(36 * 175 * 143)
(2, 2, 3, 3, 5, 5, 7, 11, 13)

>>> mcm(90, 14)
630

>>> mcd(924, 780)
12

>>> mcm(42, 60, 70, 63)
1260

>>> mcd(840, 630, 1050, 1470)
210
"""


def esPrimo(numero):
    if not isinstance(numero, int) or numero <= 1:
        raise TypeError("El número debe ser natural mayor que 1")

    if numero == 2:
        return True

    if numero % 2 == 0:
        return False

    divisor = 3
    while divisor * divisor <= numero:
        if numero % divisor == 0:
            return False
        divisor += 2

    return True


def primos(numero):
    if not isinstance(numero, int) or numero <= 1:
        raise TypeError("El número debe ser natural mayor que 1")

    resultado = []

    for candidato in range(2, numero):
        if esPrimo(candidato):
            resultado.append(candidato)

    return tuple(resultado)


def descompon(numero):
    if not isinstance(numero, int) or numero <= 1:
        raise TypeError("El número debe ser natural mayor que 1")

    factores = []
    divisor = 2
    n = numero

    while n > 1:
        while n % divisor == 0:
            factores.append(divisor)
            n //= divisor
        divisor += 1

    return tuple(factores)


def mcd(*numeros):
    if len(numeros) < 2:
        raise TypeError("Debe introducir al menos dos números")

    for numero in numeros:
        if not isinstance(numero, int) or numero <= 1:
            raise TypeError("Todos los números deben ser naturales mayores que 1")

    descomposiciones = []
    for numero in numeros:
        descomposiciones.append(list(descompon(numero)))

    comunes = descomposiciones[0][:]

    for factores in descomposiciones[1:]:
        nueva_comunes = []
        factores_copia = factores[:]

        for factor in comunes:
            if factor in factores_copia:
                nueva_comunes.append(factor)
                factores_copia.remove(factor)

        comunes = nueva_comunes

    resultado = 1
    for factor in comunes:
        resultado *= factor

    return resultado


def mcm(*numeros):
    if len(numeros) < 2:
        raise TypeError("Debe introducir al menos dos números")

    for numero in numeros:
        if not isinstance(numero, int) or numero <= 1:
            raise TypeError("Todos los números deben ser naturales mayores que 1")

    descomposiciones = []
    for numero in numeros:
        descomposiciones.append(list(descompon(numero)))

    union = []

    for factores in descomposiciones:
        factores_copia = factores[:]

        for factor in union:
            if factor in factores_copia:
                factores_copia.remove(factor)

        union.extend(factores_copia)

    resultado = 1
    for factor in union:
        resultado *= factor

    return resultado
```
