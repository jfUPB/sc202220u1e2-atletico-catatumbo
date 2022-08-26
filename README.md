#Parcial #2: ASSEMBLE
Jose Miguel López Giraldo - 448927
Manuela Cuervo Zapata - 446641
Juan Pablo Correa Cataño - 449689
##Altlético Catatumbo

##Enunciado
* Debes hacer una aplicación en el lenguaje ensamblador estudiado en esta unidad. La aplicación deberá funcionar en un loop infinito. La aplicación lee el teclado y pinta la pantalla de negro si la tecla presionada es la misma almacenada en la posición 0 de la RAM. La aplicación debe borrar la pantalla si la tecla presionada es la misma almacenada en la posición 1 de la RAM. No olvides que la aplicación debe correr en un ciclo infinito.

* Una vez crees la aplicación en lenguaje ensamblador y funcione, debes traducirla a lenguaje C/C++ tal como lo realizaste en esta unidad.

##Consideraciones
* Aquí está el enlace de la evaluación.

* Debes crear un equipo de trabajo al cual se unirán todos los miembros. El equipo solo lo crea un integrante y los demás miembros solo deben unirse.

* CLONA el repositorio.

* Cámbiate al directorio problem.

* Edita ÚNICAMENTE el archivo program.asm.

* No olvides hacer commits y push.

* Cuando pruebes el programa con la herramienta CPUEmulator.sh no olvides escribir manualmente en las posiciones 0 y 1 de la RAM el código ASCII de las teclas que usarás.

* Ten en cuanta que cada que hagas push al repositorio remoto se probará tu código.

* La traducción al lenguaje C/C++ la debes realizar en el archivo README.md. Indica al comienzo del archivo los nombre completos de todos los integrantes del equipo y el ID.

##Criterios de evaluación
* Funcionamiento correcto del programa en lenguaje ensamblador 2 unidades.

* Sustentación del programa en lenguaje C/C++ 3 unidades por contestar correctamente las preguntas realizadas a cada miembro del equipo.

#Traducción a C++
```

MEMORY[16] = 16384;

while (true)
{
    if (MEMORY[KEYBOARD] == MEMORY[1])
    {
        if ((MEMORY[16] - 16384) > 0)
        {
            MEMORY[16] = MEMORY[16] - 1;
            MEMORY[MEMORY[16]] = 0x0000;
        }
    }
    else if (MEMORY[KEYBOARD] == MEMORY[0])
    {
        if ((MEMORY[16] - 24576) < 0)
        {
            MEMORY[MEMORY[16]] = 0xFFFF;
            MEMORY[16] = MEMORY[16] + 1;
        }
    }
}

```

#Code Overview

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

* 

