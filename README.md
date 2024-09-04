# Reto 11

1. Desarrolle un programa en Python que permita realizar la suma/resta de matrices. El programa debe validar las condiciones necesarias para ejecutar la operación.

```python
def leer_matriz(nombre: str) -> list:
  
    filas = int(input(f"Ingrese el número de filas de la matriz {nombre}: "))
    columnas = int(input(f"Ingrese el número de columnas de la matriz {nombre}: "))
    print(f"Ingrese los elementos de la matriz {nombre}:")
    matriz = []
    for i in range(filas):
        fila = []
        for j in range(columnas):
            elemento = float(input(f"Elemento ({i+1},{j+1}): "))
            fila.append(elemento)
        matriz.append(fila)
    return matriz

def validar_dimensiones(matriz1: list, matriz2: list) -> bool:
   
    return len(matriz1) == len(matriz2) and len(matriz1[0]) == len(matriz2[0])

def sumar_o_restar_matrices(matriz1: list, matriz2: list, operacion: str) -> list:
  
    filas = len(matriz1)
    columnas = len(matriz1[0])
    
    resultado = []
    for i in range(filas):
        fila_resultado = []
        for j in range(columnas):
            if operacion == 'suma':
                fila_resultado.append(matriz1[i][j] + matriz2[i][j])
            elif operacion == 'resta':
                fila_resultado.append(matriz1[i][j] - matriz2[i][j])
        resultado.append(fila_resultado)
    
    return resultado

def imprimir_matriz(matriz: list) -> None:
   
    for fila in matriz:
        print("[", end=" ")
        for elemento in fila:
            print(f"{elemento:.2f}", end=" ")
        print("]")


print("Operación de suma/resta de matrices")
matriz1 = leer_matriz("A")
matriz2 = leer_matriz("B")

if validar_dimensiones(matriz1, matriz2):
    operacion = input("Ingrese la operación a realizar ('suma' o 'resta'): ").lower()
    
    if operacion in ['suma', 'resta']:
        resultado = sumar_o_restar_matrices(matriz1, matriz2, operacion)
        if operacion == 'suma':
            print("El resultado de la suma es:")
        else:
            print("El resultado de la resta es:")
        imprimir_matriz(resultado)
    else:
        print("Operación no válida. Solo se permiten 'suma' o 'resta'.")
else:
    print("Las dimensiones de las matrices no son compatibles para la operación.")


```

2. Desarrolle un programa que permita realizar el producto de matrices. El programa debe validar las condiciones necesarias para ejecutar la operación.

```python
def leer_matriz(nombre):
    filas = int(input(f"Ingrese el número de filas de la matriz {nombre}: "))
    columnas = int(input(f"Ingrese el número de columnas de la matriz {nombre}: "))
    print(f"Ingrese los elementos de la matriz {nombre}:")
    matriz = []
    for i in range(filas):
        fila = []
        for j in range(columnas):
            elemento = float(input(f"Elemento ({i+1},{j+1}): "))
            fila.append(elemento)
        matriz.append(fila)
    return matriz

def validar_dimensiones(matriz1, matriz2):
    return len(matriz1[0]) == len(matriz2)

def multiplicar_matrices(matriz1, matriz2):
    if not validar_dimensiones(matriz1, matriz2):
        raise ValueError("Las dimensiones de las matrices no son compatibles para la multiplicación.")
    
    filas_m1 = len(matriz1)
    columnas_m2 = len(matriz2[0])
    columnas_m1 = len(matriz1[0])

    resultado = []
    for i in range(filas_m1):
        fila_resultado = []
        for j in range(columnas_m2):
            suma = 0
            for k in range(columnas_m1):
                suma += matriz1[i][k] * matriz2[k][j]
            fila_resultado.append(suma)
        resultado.append(fila_resultado)
    return resultado

def imprimir_matriz(matriz):
    for fila in matriz:
        print("[", end=" ")
        for elemento in fila:
            print(f"{elemento:.2f}", end=" ")
        print("]")

print("Multiplicación de matrices")
matriz1 = leer_matriz("A")
matriz2 = leer_matriz("B")

try:
    resultado = multiplicar_matrices(matriz1, matriz2)
    print("El resultado de la multiplicación es:")
    imprimir_matriz(resultado)
except ValueError as e:
    print(e)

```










   
3. Desarrolle un programa que permita obtener la matriz transpuesta de una matriz ingresada. El programa debe validar las condiciones necesarias para ejecutar la operación.
```python


def leer_matriz() -> list:
    filas = int(input("Ingrese el número de filas de la matriz: "))
    columnas = int(input("Ingrese el número de columnas de la matriz: "))
    print("Ingrese los elementos de la matriz:")
    matriz = []
    for i in range(filas):
        fila = []
        for j in range(columnas):
            elemento = float(input(f"Elemento ({i+1},{j+1}): "))
            fila.append(elemento)
        matriz.append(fila)
    return matriz

def validar_matriz(matriz: list) -> bool:
  
    numero_columnas = len(matriz[0])
    for fila in matriz:
        if len(fila) != numero_columnas:
            return False
    return True

def obtener_transpuesta(matriz: list) -> list:

    filas = len(matriz)
    columnas = len(matriz[0])
    
    transpuesta = []
    for j in range(columnas):
        fila_transpuesta = []
        for i in range(filas):
            fila_transpuesta.append(matriz[i][j])
        transpuesta.append(fila_transpuesta)
    
    return transpuesta

def imprimir_matriz(matriz: list) -> None:
 
    for fila in matriz:
        print("[", end=" ")
        for elemento in fila:
            print(f"{elemento:.2f}", end=" ")
        print("]")


print("Calcular la matriz transpuesta")
matriz = leer_matriz()

if validar_matriz(matriz):
    transpuesta = obtener_transpuesta(matriz)
    print("La matriz transpuesta es:")
    imprimir_matriz(transpuesta)
else:
    print("La matriz ingresada no es válida. Todas las filas deben tener la misma cantidad de columnas.")


```



4.Desarrollar un programa que sume los elementos de una columna dada de una matriz.

```python
def leer_matriz() -> list:
    
    filas = int(input("Ingrese el número de filas de la matriz: "))
    columnas = int(input("Ingrese el número de columnas de la matriz: "))
    print("Ingrese los elementos de la matriz:")
    matriz = []
    for i in range(filas):
        fila = []
        for j in range(columnas):
            elemento = float(input(f"Elemento ({i+1},{j+1}): "))
            fila.append(elemento)
        matriz.append(fila)
    return matriz

def validar_columna(matriz: list, columna: int) -> bool:

    return 0 <= columna < len(matriz[0])

def sumar_columna(matriz: list, columna: int) -> float:

    suma = 0
    for fila in matriz:
        suma += fila[columna]
    return suma

def imprimir_matriz(matriz: list) -> None:
 
    for fila in matriz:
        print("[", end=" ")
        for elemento in fila:
            print(f"{elemento:.2f}", end=" ")
        print("]")


print("Suma de elementos de una columna específica de una matriz")
matriz = leer_matriz()
imprimir_matriz(matriz)

columna = int(input("Ingrese el número de la columna a sumar (comenzando desde 1): ")) - 1

if validar_columna(matriz, columna):
    suma = sumar_columna(matriz, columna)
    print(f"La suma de los elementos de la columna {columna + 1} es: {suma:.2f}")
else:
    print(f"La columna {columna + 1} no es válida para esta matriz.")


```

5. Desarrollar un programa que sume los elementos de una fila dada de una matriz.

```python

def leer_matriz() -> list:
    
    filas = int(input("Ingrese el número de filas de la matriz: "))
    columnas = int(input("Ingrese el número de columnas de la matriz: "))
    print("Ingrese los elementos de la matriz:")
    matriz = []
    for i in range(filas):
        fila = []
        for j in range(columnas):
            elemento = float(input(f"Elemento ({i+1},{j+1}): "))
            fila.append(elemento)
        matriz.append(fila)
    return matriz

def validar_fila(matriz: list, fila: int) -> bool:
   
    return 0 <= fila < len(matriz)

def sumar_fila(matriz: list, fila: int) -> float:
   
    return sum(matriz[fila])

def imprimir_matriz(matriz: list) -> None:
   
    for fila in matriz:
        print("[", end=" ")
        for elemento in fila:
            print(f"{elemento:.2f}", end=" ")
        print("]")

print("Suma de elementos de una fila específica de una matriz")
matriz = leer_matriz()
imprimir_matriz(matriz)

fila = int(input("Ingrese el número de la fila a sumar (comenzando desde 1): ")) - 1

if validar_fila(matriz, fila):
    suma = sumar_fila(matriz, fila)
    print(f"La suma de los elementos de la fila {fila + 1} es: {suma:.2f}")
else:
    print(f"La fila {fila + 1} no es válida para esta matriz.")


```












