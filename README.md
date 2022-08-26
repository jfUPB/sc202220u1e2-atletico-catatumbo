# Parcial #2: ASSEMBLE
Jose Miguel López Giraldo - 448927
Manuela Cuervo Zapata - 446641
Juan Pablo Correa Cataño - 449689
##Altlético Catatumbo

## Enunciado
* Debes hacer una aplicación en el lenguaje ensamblador estudiado en esta unidad. La aplicación deberá funcionar en un loop infinito. La aplicación lee el teclado y pinta la pantalla de negro si la tecla presionada es la misma almacenada en la posición 0 de la RAM. La aplicación debe borrar la pantalla si la tecla presionada es la misma almacenada en la posición 1 de la RAM. No olvides que la aplicación debe correr en un ciclo infinito.

* Una vez crees la aplicación en lenguaje ensamblador y funcione, debes traducirla a lenguaje C/C++ tal como lo realizaste en esta unidad.

## Consideraciones
* Aquí está el enlace de la evaluación.

* Debes crear un equipo de trabajo al cual se unirán todos los miembros. El equipo solo lo crea un integrante y los demás miembros solo deben unirse.

* CLONA el repositorio.

* Cámbiate al directorio problem.

* Edita ÚNICAMENTE el archivo program.asm.

* No olvides hacer commits y push.

* Cuando pruebes el programa con la herramienta CPUEmulator.sh no olvides escribir manualmente en las posiciones 0 y 1 de la RAM el código ASCII de las teclas que usarás.

* Ten en cuanta que cada que hagas push al repositorio remoto se probará tu código.

* La traducción al lenguaje C/C++ la debes realizar en el archivo README.md. Indica al comienzo del archivo los nombre completos de todos los integrantes del equipo y el ID.

## Criterios de evaluación
* Funcionamiento correcto del programa en lenguaje ensamblador 2 unidades.

* Sustentación del programa en lenguaje C/C++ 3 unidades por contestar correctamente las preguntas realizadas a cada miembro del equipo.

# Traducción a C++
```

MEMORY[16] = 16384;

while (true)
{
    if (MEMORY[KEYBOARD] != 0)
    {
        if (MEMORY[KEYBOARD] == MEMORY[0])
        {
            while(MEMORY[18] <= 24576)
            {
                MEMORY[18] = MEMORY[18] + 1;
                MEMORY[MEMORY[18]] = 0x0000;
            }
            MEMORY[18] = 16384
         }
        
        else if (MEMORY[KEYBOARD] == MEMORY[0])
        {
            if (MEMORY[KEYBOARD] == MEMORY[0])
            {
                while(MEMORY[18] <= 24576)
                {
                    MEMORY[18] = MEMORY[18] + 1;
                    MEMORY[MEMORY[18]] = 0x0000;
                }
                MEMORY[18] = 16384
            }
        }
    }

```

# Code Overview

* Empezamos a analizar el código en el idioma ASSEMBLER, esta primera parte inizializa un cilco while para leer el teclado
```

(START)            // while (true)
    @KBD
    D=M
    @FILLORCLEAR    // if (kbd != 0)
    D;JNE
    @START
    0;JMP
```

* En este ciclo lo que se busca es guardar el dato de entrada del teclado en la posición 0 y luego en la posición 1, dependiendo de la condición que se cumpla, este pasa a **FILL** o **CLEAR**

```
(FILLORCLEAR)
    @j
    M = D
    @0
    D = D-M
    @FILL
    D;JEQ
    @j
    D = M
    @1
    D = D - M
    @CLEAR
    D;JEQ
    @START
    0;JMP
```

* Este caso hace que se llene la pantalla de negro si el valor que se compara es igual al almacenado en la memoria

```
(FILL)
    @value
    M = -1
    @DRAW
    0;JMP
```

* Este caso hace que se llene la pantalla de blanco si el valor que se compara es igual al almacenado en la memoria

```
(CLEAR)
    @value
    M = 0
    @DRAW
    0;JMP
```

* Esta condición es la que se ejecuta luego de pasar por el paso de **FILL** o **CLEAR**, compara la posición del pixel actual para pintar

```
(DRAW)
    @SCREEN
    D = A
    @i
    M = D
```

* Esta condición hace que el ciclo repida hasta terminar de llenarse la pantalla

```
(LOOP)
    @value
    D = M
    @i
    A = M
    M = D
    @i
    M = M + 1
    @24576
    D = A
    @i
    D = M - D
    @LOOP
    D;JNE
    @START
    0;JMP
```
