# MetodosNumericosTema3Problemario
## Problemario Gabriel Hernández 

### Equipo

- Agis Mogollan Kate Michelle
- De Santiago Castillo Evelyn
- Alvarez Rivera Angel
- Hernández Zavala Gabriel
- López Gutiérrez Nili Estefanía


## Método de Eliminación Gaussiana
### Descripcion 

El Método de Eliminación de Gauss consiste en utilizar reiteradas veces las propiedades de los sistemas lineales, que hemos visto ante- riormente, para transformar un sistema de ecuaciones lineales en otro equivalente (con las mismas soluciones) pero que sea triangular.

### Pseudocódigo 

PROCEDURE resolverSistema(matriz)
    filas = LONGITUD(matriz)
    columnas = LONGITUD(matriz[0]) - 1  // Ignoramos la última columna (soluciones)

    // Aplicar eliminación gaussiana
    PARA i DESDE 0 HASTA filas - 2 HACER
        PARA j DESDE i + 1 HASTA filas - 1 HACER
            factor = matriz[j][i] / matriz[i][i]
            PARA k DESDE i HASTA columnas HACER
                matriz[j][k] = matriz[j][k] - factor * matriz[i][k]

    // Realizar sustitución hacia atrás
    ARREGLO soluciones CON LONGITUD(filas)
    PARA i DESDE filas - 1 HASTA 0 CON PASO -1 HACER
        suma = 0
        PARA j DESDE i + 1 HASTA filas - 1 HACER
            suma = suma + matriz[i][j] * soluciones[j]
        soluciones[i] = (matriz[i][columnas] - suma) / matriz[i][i]

    // Mostrar las soluciones
    IMPRIMIR "Soluciones:"
    PARA i DESDE 0 HASTA filas - 1 HACER
        IMPRIMIR "x" + (i + 1) + " = " + soluciones[i]
FIN PROCEDIMIENTO

// Llamar a la función con la matriz de ejemplo
matrizEjemplo = {
    {2, 1, -1, 8},
    {-3, -1, 2, -11},
    {-2, 1, 2, -3}
}
resolverSistema(matrizEjemplo)


### Implementacion 
- Implementacion en Python

def resolver_sistema(matriz):
    filas = len(matriz)
    columnas = len(matriz[0]) - 1  # Ignoramos la última columna (soluciones)

    #Aplicar eliminación gaussiana
    for i in range(filas - 1):
        for j in range(i + 1, filas):
            factor = matriz[j][i] / matriz[i][i]
            for k in range(i, columnas + 1):
                matriz[j][k] -= factor * matriz[i][k]

    #Realizar sustitución hacia atrás
    soluciones = [0] * filas
    for i in range(filas - 1, -1, -1):
        suma = 0
        for j in range(i + 1, filas):
            suma += matriz[i][j] * soluciones[j]
        soluciones[i] = (matriz[i][columnas] - suma) / matriz[i][i]

 
    print("Soluciones:")
    for i in range(filas):
        print(f"x{i + 1} = {soluciones[i]}")

#Matriz de ejemplo
matriz_ejemplo = [
    [2, 1, -1, 8],
    [-3, -1, 2, -11],
    [-2, 1, 2, -3]
]

#Llamar a la función con la matriz de ejemplo
resolver_sistema(matriz_ejemplo)


### Ejercicios en java

[Ejemplo 1](https://github.com/GABOHDEZ2001/ProblemarioTema3/blob/main/ProblemarioTema3/src/EliminacionGaussianaEjemplo1.java)

[Resultado Ejemplo 1](https://github.com/GABOHDEZ2001/ProblemarioTema3/blob/main/ProblemarioTema3/src/EliminacionGaussianaEjemplo1.java)

[Ejemplo 2](https://github.com/GABOHDEZ2001/ProblemarioTema3/blob/main/ProblemarioTema3/src/EliminacionGaussianaEjemplo2.java)

[Ejemplo 3](https://github.com/GABOHDEZ2001/ProblemarioTema3/blob/main/ProblemarioTema3/src/EliminacionGaussianaEjemplo3.java)

[Ejemplo 4](https://github.com/GABOHDEZ2001/ProblemarioTema3/blob/main/ProblemarioTema3a/src/EliminacionGaussianaEjemplo4.java)

[Ejemplo 5](https://github.com/GABOHDEZ2001/ProblemarioTema3/blob/main/ProblemarioTema3a/src/EliminacionGaussianaEjemplo5.java)




==========================================================================================================================


## Método de Gauss Jordan
### Descripcion 

El método de eliminación Gauss-Jordan consiste en representar el sistema de ecuaciones por medio de una matriz y obtener a partir de ella lo que se define como la matriz escalonada equivalente, a través de la cual se determina el tipo de solución de la ecuación.

### Pseudocódigo 

    FUNCIÓN principal():
        matriz = {
            {2, 1, -1, 8},
            {-3, -1, 2, -11},
            {-2, 1, 2, -3}
        }
        resolverSistema(matriz)

    FUNCIÓN resolverSistema(matriz):
        filas = longitud(matriz)
        columnas = longitud(matriz[0])

        // Escalonar la matriz
        PARA cada i de 0 hasta filas - 1 HACER
            pivote = matriz[i][i]
            PARA cada j de i + 1 hasta filas - 1 HACER
                factor = matriz[j][i] / pivote
                PARA cada k de i hasta columnas - 1 HACER
                    matriz[j][k] -= matriz[i][k] * factor
                FIN PARA
            FIN PARA
        FIN PARA

        // Reducir la matriz a forma escalonada reducida
        PARA cada i de filas - 1 hasta 0 HACER
            pivote = matriz[i][i]
            PARA cada j de i - 1 hasta 0 HACER
                factor = matriz[j][i] / pivote
                PARA cada k de i hasta columnas - 1 HACER
                    matriz[j][k] -= matriz[i][k] * factor
                FIN PARA
            FIN PARA
        FIN PARA

        // Normalizar la matriz
        PARA cada i de 0 hasta filas - 1 HACER
            pivote = matriz[i][i]
            PARA cada j de i hasta columnas - 1 HACER
                matriz[i][j] /= pivote
            FIN PARA
        FIN PARA

        // Imprimir la solución
        PARA cada i de 0 hasta filas - 1 HACER
            IMPRIMIR "x" + (i + 1) + " = " + matriz[i][columnas - 1]
        FIN PARA

FIN CLASE


### Implementacion 

def resolver_sistema(matriz):
    filas = len(matriz)
    columnas = len(matriz[0])

    for i in range(filas):
        pivote = matriz[i][i]
        for j in range(i + 1, filas):
            factor = matriz[j][i] / pivote
            for k in range(i, columnas):
                matriz[j][k] -= matriz[i][k] * factor

    for i in range(filas - 1, -1, -1):
        pivote = matriz[i][i]
        for j in range(i - 1, -1, -1):
            factor = matriz[j][i] / pivote
            for k in range(i, columnas):
                matriz[j][k] -= matriz[i][k] * factor

    for i in range(filas):
        pivote = matriz[i][i]
        for j in range(columnas):
            matriz[i][j] /= pivote

    for i in range(filas):
        print("x" + str(i + 1) + " =", matriz[i][columnas - 1])

matriz = [
    [2, 1, -1, 8],
    [-3, -1, 2, -11],
    [-2, 1, 2, -3]
]

resolver_sistema(matriz)


### Ejercicios en java

[Ejemplo 1](https://github.com/GABOHDEZ2001/ProblemarioTema3/blob/main/ProblemarioTema3/src/GaussJordanEjemplo1.java)

[Ejemplo 2](https://github.com/GABOHDEZ2001/ProblemarioTema3/blob/main/ProblemarioTema3/src/GaussJordanEjemplo2.java)

[Ejemplo 3](https://github.com/GABOHDEZ2001/ProblemarioTema3/blob/main/ProblemarioTema3/src/GaussJordanEjemplo3.java)

[Ejemplo 4](https://github.com/GABOHDEZ2001/ProblemarioTema3/blob/main/ProblemarioTema3a/src/GaussJordanEjemplo4.java)

[Ejemplo 5](https://github.com/GABOHDEZ2001/ProblemarioTema3/blob/main/ProblemarioTema3a/src/GaussJordanEjemplo5.java)




==========================================================================================================================


## Método de Gauss Seidel
### Descripcion 

Es un método iterativo, lo que significa que se parte de una aproximación inicial y se repite el proceso hasta llegar a una solución con un margen de error tan pequeño como se quiera. Buscamos la solución a un sistema de ecuaciones lineales, en notación matricial: donde: , esto es, la matriz N es triangular superior.

### Pseudocódigo 

CONSTANTES:
        MAX_ITERATIONS = 100
        TOLERANCIA = 0.0001

    FUNCIÓN principal():
        // Matriz de coeficientes del sistema de ecuaciones
        coefficients = {
            {10, -1, 2, 0},
            {-1, 11, -1, 3},
            {2, -1, 10, -1},
            {0, 3, -1, 8}
        }
        
        // Valores iniciales para las incógnitas
        initialValues = {0, 0, 0, 0}

        // Llamar al método gaussSeidel para obtener las soluciones
        soluciones = gaussSeidel(coefficients, initialValues)

        // Mostrar las soluciones
        MOSTRAR "Soluciones:"
        PARA cada i de 0 hasta longitud(soluciones) - 1 HACER
            MOSTRAR "x[" + i + "] = " + soluciones[i]
        FIN PARA

    FUNCIÓN gaussSeidel(coefficients, initialValues):
        n = longitud(coefficients) // Obtener la dimensión del sistema
        soluciones = arreglo de tamaño n
        nuevasSoluciones = arreglo de tamaño n
        iteraciones = 0
        error = 0.0

        REPETIR:
            PARA cada i de 0 hasta n - 1 HACER
                suma = 0.0
                PARA cada j de 0 hasta n - 1 HACER
                    SI j != i ENTONCES
                        suma += coefficients[i][j] * nuevasSoluciones[j]
                    FIN SI
                FIN PARA
                nuevasSoluciones[i] = (initialValues[i] - suma) / coefficients[i][i]
            FIN PARA

            error = 0.0
            PARA cada i de 0 hasta n - 1 HACER
                error = MAX(error, ABS(nuevasSoluciones[i] - soluciones[i]))
                soluciones[i] = nuevasSoluciones[i]
            FIN PARA

            iteraciones++

        HASTA QUE error <= TOLERANCIA O iteraciones >= MAX_ITERATIONS

        SI iteraciones >= MAX_ITERATIONS ENTONCES
            MOSTRAR "Se alcanzó el máximo de iteraciones sin convergencia"
        FIN SI

        RETORNAR soluciones

FIN CLASE

### Implentacion 

 - Implementacion usando Python

MAX_ITERACIONES = 100
TOLERANCIA = 0.0001

def gauss_seidel(coeficientes, valores_iniciales):
    n = len(coeficientes)
    soluciones = [0] * n
    nuevas_soluciones = [0] * n
    iteraciones = 0
    error = 0.0

    while iteraciones < MAX_ITERACIONES:
        for i in range(n):
            suma = 0.0
            for j in range(n):
                if j != i:
                    suma += coeficientes[i][j] * nuevas_soluciones[j]
            nuevas_soluciones[i] = (valores_iniciales[i] - suma) / coeficientes[i][i]

        error = max(abs(nuevas_soluciones[i] - soluciones[i]) for i in range(n))
        
        if error < TOLERANCIA:
            break
        
        soluciones = nuevas_soluciones.copy()
        iteraciones += 1

    if iteraciones >= MAX_ITERACIONES:
        print("Se alcanzó el máximo de iteraciones sin convergencia")
    
    return soluciones

coeficientes = [
    [10, -1, 2, 0],
    [-1, 11, -1, 3],
    [2, -1, 10, -1],
    [0, 3, -1, 8]
]
valores_iniciales = [0, 0, 0, 0]

soluciones = gauss_seidel(coeficientes, valores_iniciales)
print("Soluciones:")
for i, sol in enumerate(soluciones):
    print(f"x[{i}] = {sol}")



### Ejercicios en java

[Ejemplo 1](https://github.com/GABOHDEZ2001/ProblemarioTema3/blob/main/ProblemarioTema3/src/GaussSeidelEjemplo1.java)

[Ejemplo 2](https://github.com/GABOHDEZ2001/ProblemarioTema3/blob/main/ProblemarioTema3/src/GaussSeidelEjemplo2.java)

[Ejemplo 3](https://github.com/GABOHDEZ2001/ProblemarioTema3/blob/main/ProblemarioTema3/src/GaussSeidelEjemplo3.java)

[Ejemplo 4](https://github.com/GABOHDEZ2001/ProblemarioTema3/blob/main/ProblemarioTema3a/src/GaussSeidelEjemplo4.java)

[Ejemplo 5](https://github.com/GABOHDEZ2001/ProblemarioTema3/blob/main/ProblemarioTema3a/src/GaussSeidelEjemplo5.java)



==========================================================================================================================


## Método de Jacobi
### Descripcion 
La base del método consiste en construir una sucesión convergente definida iterativamente. El límite de esta sucesión es precisamente la solución del sistema. A efectos prácticos si el algoritmo se detiene después de un número finito de pasos se llega a una aproximación al valor de x de la solución del sistema.

### Pseudocódigo 

PROCEDIMIENTO calcularNuevoX(x, y, z)
    RETORNAR (4 - 2 * y + z) / 6.0

PROCEDIMIENTO calcularNuevoY(x, y, z)
    RETORNAR (3 - x - z) / 5.0

PROCEDIMIENTO calcularNuevoZ(x, y, z)
    RETORNAR (27 - 2 * x - y) / 4.0

PROCEDIMIENTO jacobi(x, y, z, tolerancia, maxIteraciones)
    iteraciones = 0
    MIENTRAS iteraciones < maxIteraciones HACER
        nuevoX = calcularNuevoX(x, y, z)
        nuevoY = calcularNuevoY(x, y, z)
        nuevoZ = calcularNuevoZ(x, y, z)
        
        maxDiferencia = MAX(ABS(nuevoX - x), MAX(ABS(nuevoY - y), ABS(nuevoZ - z)))
        
        SI maxDiferencia < tolerancia ENTONCES
            IMPRIMIR "Convergencia alcanzada en la iteración " + iteraciones
            IMPRIMIR "x = " + nuevoX
            IMPRIMIR "y = " + nuevoY
            IMPRIMIR "z = " + nuevoZ
            RETORNAR
        FIN SI
        
        x = nuevoX
        y = nuevoY
        z = nuevoZ
        
        iteraciones = iteraciones + 1
    FIN MIENTRAS
    
    IMPRIMIR "No se alcanzó la convergencia después de " + maxIteraciones + " iteraciones."

PROCEDIMIENTO principal()
    x = 0 // Valor inicial de x
    y = 0 // Valor inicial de y
    z = 0 // Valor inicial de z
    tolerancia = 0.0001 // Tolerancia
    maxIteraciones = 100 // Número máximo de iteraciones
    
    jacobi(x, y, z, tolerancia, maxIteraciones)

LLAMAR principal()



### Implementacion 

 - Implementacion usando Python

def calcular_nuevo_x(y, z):
    return (4 - 2 * y + z) / 6.0

def calcular_nuevo_y(x, z):
    return (3 - x - z) / 5.0

def calcular_nuevo_z(x, y):
    return (27 - 2 * x - y) / 4.0

def jacobi(x, y, z, tolerancia, max_iteraciones):
    iteraciones = 0
    while iteraciones < max_iteraciones:
        nuevo_x = calcular_nuevo_x(y, z)
        nuevo_y = calcular_nuevo_y(x, z)
        nuevo_z = calcular_nuevo_z(x, y)

        max_diferencia = max(abs(nuevo_x - x), abs(nuevo_y - y), abs(nuevo_z - z))

        if max_diferencia < tolerancia:
            print("Convergencia alcanzada en la iteración", iteraciones)
            print("x =", nuevo_x)
            print("y =", nuevo_y)
            print("z =", nuevo_z)
            return

        x, y, z = nuevo_x, nuevo_y, nuevo_z
        iteraciones += 1

    print("No se alcanzó la convergencia después de", max_iteraciones, "iteraciones.")

x = 0
y = 0
z = 0


tolerancia = 0.0001
max_iteraciones = 100


jacobi(x, y, z, tolerancia, max_iteraciones)


### Ejercicios en java

[Ejemplo 1](https://github.com/GABOHDEZ2001/ProblemarioTema3/blob/main/ProblemarioTema3/src/MetodoJacobiEjemplo1.java)

[Ejemplo 2](https://github.com/GABOHDEZ2001/ProblemarioTema3/blob/main/ProblemarioTema3/src/MetodoJacobiEjemplo2.java)

[Ejemplo 3](https://github.com/GABOHDEZ2001/ProblemarioTema3/blob/main/ProblemarioTema3/src/MetodoJacobiEjemplo3.java)

[Ejemplo 4](https://github.com/GABOHDEZ2001/ProblemarioTema3/blob/main/ProblemarioTema3a/src/MetodoJacobiEjemplo4.java)

[Ejemplo 5](https://github.com/GABOHDEZ2001/ProblemarioTema3/blob/main/ProblemarioTema3a/src/MetodoJacobiEjemplo5.java)
















