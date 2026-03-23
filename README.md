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
 def esPrimo(numero):
    """
    Devuelve True si numero es primo, False en caso contrario.
    """
    if not isinstance(numero, int) or numero <= 1:
        raise TypeError("El número debe ser natural mayor que 1")

    if numero == 2:
        return True

    if numero % 2 == 0:
        return False

    for i in range(3, int(numero ** 0.5) + 1, 2):
        if numero % i == 0:
            return False

    return True


def primos(numero):
    """
    Devuelve una tupla con los números primos menores que numero.
    """
    return tuple(n for n in range(2, numero) if esPrimo(n))


def descompon(numero):
    """
    Devuelve la descomposición en factores primos de numero.
    """
    factores = []
    divisor = 2

    while numero > 1:
        while numero % divisor == 0:
            factores.append(divisor)
            numero //= divisor
        divisor += 1

    return tuple(factores)


def mcd(*numeros):
    """
    Devuelve el máximo común divisor de varios números.
    """
    from collections import Counter

    factorizaciones = [Counter(descompon(n)) for n in numeros]

    comun = factorizaciones[0]

    for f in factorizaciones[1:]:
        comun = {k: min(comun.get(k, 0), f.get(k, 0)) for k in comun}

    resultado = 1
    for primo, exp in comun.items():
        resultado *= primo ** exp

    return resultado


def mcm(*numeros):
    """
    Devuelve el mínimo común múltiplo de varios números.
    """
    from collections import Counter

    factorizaciones = [Counter(descompon(n)) for n in numeros]

    union = {}

    for f in factorizaciones:
        for primo, exp in f.items():
            union[primo] = max(union.get(primo, 0), exp)

    resultado = 1
    for primo, exp in union.items():
        resultado *= primo ** exp

    return resultado


if __name__ == "__main__":
    # Tests
    print([n for n in range(2, 50) if esPrimo(n)])
    print(primos(50))
    print(descompon(36 * 175 * 143))
    print(mcm(90, 14))
    print(mcd(924, 780))
    print(mcm(42, 60, 70, 63))
    print(mcd(840, 630, 1050, 1470))
```

