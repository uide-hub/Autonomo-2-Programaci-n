# Autonomo-2-Programaci-n
# tarea de programación avance el 50%
# Lista que contiene las representaciones en arte ASCII del ahorcado para cada intento fallido.
dibujo_ahorcado = [
    '''
        +---+
        |   |
            |
            |
            |
            |
    =========
    ''',
    '''
        +---+
        |   |
        O   |
            |
            |
            |
    =========
    ''',
    '''
        +---+
        |   |
        O   |
        |   |
            |
            |
    =========
    ''',
    '''
        +---+
        |   |
        O   |
       /|   |
            |
            |
    =========
    ''',
    '''
        +---+
        |   |
        O   |
       /|\  |
            |
            |
    =========
    ''',
    '''
        +---+
        |   |
        O   |
       /|\  |
       /    |
            |
    =========
    ''',
]

# Palabra secreta que el jugador debe adivinar. Se convierte en una lista de caracteres.
palabra = list('calavera')
# Lista que representa la palabra con guiones bajos, lo que el jugador ve.
palabra_oculta =['_']*len(palabra)
# Número de intentos que el jugador tiene.
intentos = 6
# Lista de todas las letras válidas del abecedario en español.
lista_abecedario = list('abcdefghijklmnñopqrstuvwxyz')
# Lista para guardar las letras que el jugador ha descartado (ha fallado).
letras_descartadas = []

# Función para mostrar el estado actual del juego.
def mostrar_estado():
    # Muestra los intentos restantes, las letras falladas y el progreso de la palabra.
    print(f'Intentos restantes: {intentos}')
    print(f'Letras descartadas: {", ".join(letras_descartadas)}\n')
    print(f'Palabra: {" ".join(palabra_oculta)}\n')
    # Imprime el dibujo del ahorcado según el número de intentos restantes.
    print(dibujo_ahorcado[6 - intentos])

# Función para verificar si la letra introducida por el usuario es válida.
def letra_valida(letra):
    # Comprueba si el usuario introdujo más de una letra.
    if len(letra) != 1 :
        print('Has puesto más de una letra, inténtalo de nuevo.')
        return False
    # Comprueba si la letra está en el abecedario.
    elif letra not in lista_abecedario:
        print('No has introducido una letra del abecedario')
        return False
    # Comprueba si la letra ya ha sido adivinada.
    elif letra in palabra_oculta:
        print('La letra que has introducido ya la has acertado, inténtalo de nuevo.')
        return False
    # Comprueba si la letra ya ha sido descartada.
    elif letra in letras_descartadas:
        print('Esa letra ya la habías dicho, inténtalo de nuevo.')
        return False
    # Si pasa todas las comprobaciones, la letra es válida.
    else:
        return True

# Función para gestionar una letra que el jugador ha adivinado correctamente.
def gestion_letra(letra):
    # Itera sobre la palabra secreta para encontrar todas las ocurrencias de la letra.
    for i in range(len(palabra)):
        if palabra[i] == letra:
            # Reemplaza el guion bajo en la palabra oculta por la letra correcta.
            palabra_oculta[i] = letra
            # Marca la letra en la palabra secreta como ya encontrada para evitar duplicados.
            palabra[i] = '_'

# Inicio del juego: imprime un mensaje de bienvenida y las reglas.
print('BIENVENIDO AL JUEGO DEL AHORCADO 🎃 EDICIÓN HALLOWEEN 🎃\n')
print('Reglas del juego: Introduce letras para adivinar la palabra oculta .')
print(f'Tienes {intentos} intentos. ¡Buena suerte!')

# Bucle principal del juego: continúa mientras queden intentos y la palabra no esté completa.
while intentos > 0 and '_' in palabra_oculta:
    # Muestra el estado actual del juego.
    mostrar_estado()
    print('-'*50)
    # Pide al usuario que introduzca una letra y la convierte a minúscula.
    letra = input('INTRODUCE LETRA: ').lower()

    # Bucle para validar la entrada del usuario. Se repite hasta que se introduzca una letra válida.
    while not letra_valida(letra):
        letra = input('INTRODUCE OTRA LETRA: ').lower()

    # Comprueba si la letra está en la palabra secreta.
    if letra in palabra:
        # Si acierta, llama a la función para actualizar la palabra oculta.
        gestion_letra(letra)
        print('-'*50)
        print('¡Has acertado la letra! Sigue así.')
    else:
        # Si falla, reduce un intento y añade la letra a la lista de descartadas.
        print('-'*50)
        print('¡Has fallado la letra!')
        letras_descartadas.append(letra)
        intentos -= 1
