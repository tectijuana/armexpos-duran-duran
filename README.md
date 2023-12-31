![](https://s3.amazonaws.com/videos.pentesteracademy.com/videos/badges/low/arm-assembly.png)

Borrar y modificar a su gusto este README, pero antes utilizar estas condiciones de entrega del trabajo.

# Equipo 4 EJECUCION DE CONDICIONALES

-Link para  unirse al grupo de wats
https://chat.whatsapp.com/F2orRzEoaAcEsSSmMPbHvT

A nosotros nos toco el tema de ejecucion de condicionales
![](https://i.imgur.com/Ro3FCuD.png)


# INTEGRANTES DEL EQUIPO
Siqueiros Valdes Ivan Antonio

Bringas Alvarado Manuel Abraham

Corrales Quintero Erick Roberto

Garcia Cerrillo Angel Albino

Ortega Jimenez Jordi Joel

Valle Sanchez Leidy Lizeth

San Roman Castillo Gabriel

# Estructura general
Se van a explicar 4 condicionales de las cuales vamos a poner la definición, un ejemplo y el debugeo del ejemplo

                                                      1. EQ(Equals)

  Definicion EQ
 
EQ, =, ==

Igual

                                                      Descripción

EQ equivale a 1 (verdadero) si sus dos operandos son idénticos en valor, o equivale a 0 (falso) si sus dos operandos no son idénticos en valor.
Se utiliza con una instrucción de comparación, lo que permite hacer saltos de flujo en el programa dependiendo de si los valores son iguales o no.

                                                        Ejemplos
       
1 == 2 = 0

2 == 2 = 1

’abc’ == ’abcd’ = 0


                                                        Debuggeo
  
MOV R1,#10

MOV R2, #10

CMP R1,R2 (Se modifican la bandera Z == 1)

ADDEQ R3,R1,R2 (Z==1)????

ADD R1, #-10

2. NE (Not Equal)

  Definicion-Valle Sanchez Leidy Lizeth
  
  Es un término utilizado en el contexto de operaciones de comparación en matemáticas y programación para indicar que dos valores no son iguales entre sí. particularmente en lenguajes de programación y expresiones condicionales, se utiliza el operador "!=" o "<>" para expresar la desigualdad entre dos valores. se utiliza para indicar que dos valores no son iguales, y es un concepto fundamental en la programación y las operaciones de comparación en matemáticas y lenguajes de programación.
  

Debuggeo

MOV R1,#10

MOV R2, #10

CMP R1,R2 (Se modifican las banderas Z===0)

ADDNE R1, #-10 (Z==0)????

ADD R3,R1,R2


3. GE (Signed >=)

![image](https://github.com/tectijuana/armexpos-duran-duran/assets/99369099/508969b6-0bca-4987-8c9d-6184fcaa0918)
https://www.fdi.ucm.es/profesor/rhermida/FC_practica1.pdf

  La condicional "GE" se utiliza para verificar si un número con signo es mayor o igual a cero. Esta condición se basa en el 
  resultado de una instrucción de comparación anterior y se utiliza en combinación con instrucciones de salto condicional
  para tomar decisiones en función de si el valor es mayor o igual a cero.


  Debuggeo-San Roman Castillo Gabriel

    /*
    Ejemplo Del Uso de la condicional GE
    */
    .text
    .global _start  

    _start:
        mov r0, #10      @ Carga el valor 10 en el registro r0
        mov r1, #5       @ Carga el valor 5 en el registro r1
    
        cmp r0, r1       @ Compara r0 y r1
        bge greater_than_or_equal
    
        mov r2, #0       @ Si r0 < r1, carga 0 en r2
    b end_program

    greater_than_or_equal:
        mov r2, #1       @ Si r0 >= r1, carga 1 en r2
    
    end_program:
        @ Tu código continúa aquí (puede haber más instrucciones)

    bx lr             @ Salto de regreso para salir de la función main


4. LT (signed <)

  La condición "LT" (Less Than) en ARM se utiliza para comparar dos valores con signo y determinar si el primer valor 
  es estrictamente menor que el segundo valor. En este contexto, "signed" significa que se 
  están considerando los números como valores con signo, es decir, números positivos y negativos.

  La instrucción "LT" en ARM se usa típicamente en combinación con las instrucciones de salto condicional para 
  tomar decisiones basadas en la comparación de valores. A continuación
  Ejemplo:

    .data
    mensaje:    .asciz "El primer número es menor que el segundo.\n"
    no_mensaje: .asciz "El primer número NO es menor que el segundo.\n"

    .text
    .global main

    main:
      @ Supongamos que tenemos dos números en los registros R0 y R1
      @ R0 contiene 10 y R1 contiene 5 (puedes cambiar estos valores según tus necesidades).

      CMP R0, R1     @ Compara R0 y R1
      BGT no_menor   @ Salta a no_menor si R0 > R1

      @ Si llegamos aquí, significa que R0 no es mayor que R1 (es decir, R0 < R1)
      @ Imprimimos el mensaje correspondiente.
      mov R0, #1      @ R0 se usa para el file descriptor (stdout)
      LDR R1, =mensaje @ Cargamos la dirección del mensaje en R1
      mov R2, #32     @ R2 es la longitud del mensaje
      mov R7, #4      @ Código de llamada para escribir (sys_write)
      swi 0            @ Llamada al sistema para escribir en la consola
      b fin

    no_menor:
      @ Si llegamos aquí, significa que R0 es mayor que R1
      @ Imprimimos el otro mensaje.
      mov R0, #1        @ R0 se usa para el file descriptor (stdout)
      LDR R1, =no_mensaje @ Cargamos la dirección del mensaje en R1
      mov R2, #42       @ R2 es la longitud del mensaje
      mov R7, #4         @ Código de llamada para escribir (sys_write)
      swi 0             @ Llamada al sistema para escribir en la consola

    fin:
      mov R7, #1       @ Código de salida de la llamada al sistema
      swi 0x11          @ Llamada al sistema para salir del programa
  5.GT (Greater than)
  La instrucción GT (Greater Than) en la arquitectura ARM no es una instrucción específica. En su lugar, la arquitectura ARM utiliza una serie de instrucciones condicionales para comparar valores y tomar decisiones basadas en el resultado de esas comparaciones.
  
    CMP R0, R1    @ Compara el valor en R0 con el valor en R1
    BGT mayor     @ Salta a "mayor" si R0 es mayor que R1
    @ Si no se cumple la condición (R0 no es mayor que R1), continúa aquí

  6.MI (Overflow Condition Set):
La instrucción MI se utiliza para realizar una operación condicional en función del estado de desbordamiento negativo (N) en la arquitectura ARM. Se ejecuta si el bit N está activado, lo que indica un resultado negativo.

  7.PL (Overflow Condition Clear):
Descripción: La instrucción PL se utiliza para realizar una operación condicional en función del estado de desbordamiento negativo (N) en la arquitectura ARM. Se ejecuta si el bit N está desactivado, lo que indica un resultado no negativo (positivo o cero).

# FUENTES UTILES
https://azeria-labs.com/arm-conditional-execution-and-branching-part-6/
https://cpulator.01xz.net/?loadasm=share/tmbG7ik.s&sys=arm

