# Algoritmo-simple-para-romper-contrase-as-fuerza-bruta-controlada-
Implementar un algoritmo básico que intente “adivinar” una contraseña de prueba generada por el propio estudiante, usando un método de fuerza bruta. El fin es comprender la vulnerabilidad de contraseñas débiles y la importancia de políticas seguras.

##  Manual de funcionamiento del código de fuerza bruta ##

1. Librerías utilizadas
Este segmento importa la librería necesaria para registrar el tiempo de ejecución del programa.

import time

3. Definición de la contraseña de prueba
Aquí se establece la contraseña que el algoritmo intentará descifrar. Puedes cambiar este valor para probar diferentes casos.

contraseña = "Ab3!"

3. Definición del alfabeto
En esta sección se definen los caracteres que el algoritmo usará para generar las combinaciones. Primero, se crean variables separadas para los distintos tipos de caracteres y luego se unen en una sola cadena.

minusculas = "abcdefghijklmnopqrstuvwxyz"
mayusculas = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
numeros    = "0123456789"
signos     = "!@#$%^&*()_+-=[]{}|;':\",./<>?`~ "

alfabeto = minusculas + mayusculas + numeros + signos

4. Inicialización de contadores y bandera
Se inicializan las variables que rastrearán el número de intentos y el estado de la búsqueda.

intentos = 0
encontrada = False
5. Inicio del tiempo de ejecución
Esta línea registra el momento exacto en que comienza el proceso de búsqueda para calcular la duración total.

tiempo_inicio = time.time()


6. Generación de combinaciones
Este es el núcleo del algoritmo, donde se generan y prueban todas las posibles combinaciones de caracteres. El código se estructura en bucles anidados para iterar sobre longitudes y combinaciones.

for longitud in range(1, len(contraseña) + 1):
    if encontrada:
        break

    indices = [0] * longitud
    total = len(alfabeto) ** longitud

    for num in range(total):
        intento = ""
        temp = num

        for i in range(longitud - 1, -1, -1):
            indices[i] = temp % len(alfabeto)
            temp //= len(alfabeto)
            intento += alfabeto[indices[i]]

        intentos += 1
7. Comparación con la contraseña y salida de resultados
Finalmente, este fragmento compara cada combinación generada con la contraseña objetivo. Si hay una coincidencia, calcula el tiempo transcurrido y muestra los resultados en la consola antes de detener la ejecución.

if intento == contraseña:
    encontrada = True
    tiempo_final = time.time()
    tiempo_transcurrido = tiempo_final - tiempo_inicio
    print(f"Contraseña encontrada: {intento}")
    print(f"Intentos: {intentos}")
    print(f"Tiempo transcurrido: {tiempo_transcurrido:} segundos")
    break
