# Operaciones matemáticas y funciones elementales
Julia proporciona una colección completa de operadores aritméticos básicos y bit a bit en todos sus tipos primitivos numéricos, además de proporcionar implementaciones portátiles y eficientes de una colección integral de funciones matemáticas estándar.

Los siguientes operadores aritméticos son compatibles con todos los tipos numéricos primitivos:

+x	unario más	- La operación de identidad
-x	unario menos	- asigna valores a sus inversos aditivos
x + y	binario más	- realiza suma
x - y	binario menos	- realiza resta
x * y	veces	        - realiza la multiplicación
x / y	dividir	        - realiza división
x ÷ y	división de enteros	- x / y, truncado a un entero
x \ y	división inversa	- equivalente ay / x
x ^ y	fuerza	        - eleva xa la yenésima potencia
x % y	resto	        - equivalente a rem(x, y)

Un literal numérico colocado directamente antes de un identificador o paréntesis, por ejemplo 2xo 2(x + y), se trata como una multiplicación, excepto que tiene mayor precedencia que otras operaciones binarias. Consulte Coeficientes literales numéricos para obtener más detalles.

El sistema de promoción de Julia hace que las operaciones aritméticas con combinaciones de tipos de argumentos "funcionen" de manera natural y automática. Consulte Conversión y promoción para obtener más detalles sobre el sistema de promoción.

El signo ÷ se puede escribir cómodamente escribiendo \div<tab>en REPL o en el IDE de Julia. Consulte la sección del manual sobre entrada Unicode para obtener más información.

A continuación se muestran algunos ejemplos sencillos que utilizan operadores aritméticos:
```Julia
julia> 1 + 2 + 3
6

julia> 1 - 2
-1

julia> 3*2/12
0.5
```
## Operaciones booleanos 

Los siguientes operadores booleanos son compatibles con Bool:

!x	- negación
x && y	- cortocircuito y
x || y	- cortocircuito o