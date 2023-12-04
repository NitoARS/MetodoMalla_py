# MetodoMalla_py
Resolución de mallas con modelamiento en python

import numpy as np

# Solicitar al usuario el valor de R1 hasta R9 (incluyendo los términos independientes)
R1 = float(input("Ingrese el valor de R1: "))
R2 = float(input("Ingrese el valor de R2: "))
R3 = float(input("Ingrese el valor de R3: "))
R4 = float(input("Ingrese el valor de R4: "))
R5 = float(input("Ingrese el valor de R5: "))
R6 = float(input("Ingrese el valor de R6: "))
VS1 = float(input("Ingrese el valor de VS1: "))
VS2 = float(input("Ingrese el valor de VS2: "))
VS3 = float(input("Ingrese el valor de VS3: "))

# Crear la matriz 3x3 con los valores ingresados (coeficientes del sistema)
matriz_coeficientes = np.array([
    [R1 + R2 + R3, -R2, -R3],
    [-R2, R1 + R2 + R4, -R5],
    [-R3, -R5, R3 + R5 + R6]
])

# Mostrar la matriz ingresada por el usuario
print("\nLa matriz de coeficientes es:")
print(matriz_coeficientes)

# Calcular el determinante de la matriz de coeficientes
determinante_coeficientes = np.linalg.det(matriz_coeficientes)

# Mostrar el determinante de la matriz de coeficientes
print(f"\nEl determinante de la matriz de coeficientes es: {determinante_coeficientes}\n")

# Matriz de términos independientes
matriz_terminos_independientes = np.array([VS1, VS2, VS3])

# Mostrar la matriz de términos independientes
print("La matriz de términos independientes es:")
print(matriz_terminos_independientes)

# Matrices al reemplazar cada columna por la matriz de términos independientes
matrices_reemplazadas = []
for i in range(3):
    matriz_reemplazada = matriz_coeficientes.copy()
    matriz_reemplazada[:, i] = matriz_terminos_independientes
    matrices_reemplazadas.append(matriz_reemplazada)

# Mostrar las matrices reemplazadas
print("\nMatrices al reemplazar cada columna por la matriz de términos independientes:")
for i, matriz in enumerate(matrices_reemplazadas):
    print(f"Matriz {i+1}:")
    print(matriz)

# Calcular los determinantes de las matrices reemplazadas
determinantes_reemplazados = [np.linalg.det(matriz) for matriz in matrices_reemplazadas]

# Mostrar los determinantes de las matrices reemplazadas
print("\nDeterminantes de las matrices reemplazadas:")
for i, determinante in enumerate(determinantes_reemplazados):
    print(f"Determinante {i+1}: {determinante}")

# Calcular i1, i2 e i3
resultados = [determinante / determinante_coeficientes for determinante in determinantes_reemplazados]

# Mostrar los resultados
print("\nResultados:")
print(f"i1 = {resultados[0]}")
print(f"i2 = {resultados[1]}")
print(f"i3 = {resultados[2]}")
