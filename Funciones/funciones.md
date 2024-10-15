# Funciones

En Julia, una función es un objeto que asigna una tupla de valores de argumentos a un valor de retorno. Las funciones de Julia no son funciones matemáticas puras, ya que pueden modificarse y verse afectadas por el estado global del programa. La sintaxis básica para definir funciones en Julia es:
```Julia
julia> function f(x, y)
           x + y
       end
f (generic function with 1 method)
```
Esta función acepta dos argumentos xy y devuelve el valor de la última expresión evaluada, que es x + y.

# Función detallada
```Julia
function saludo(nombre)
    return "¡Hola, $nombre!"
end
```
println(saludo("Julia"))

Existe una segunda sintaxis más concisa para definir una función en Julia. La sintaxis de declaración de 
función tradicional que se muestra arriba es equivalente a la siguiente "forma de asignación" compacta:
```Julia
julia> f(x, y) = x + y
f (generic function with 1 method)
```

En la forma de asignación, el cuerpo de la función debe ser una expresión única, aunque puede ser una expresión compuesta (consulte Expresiones compuestas). Las definiciones de funciones breves y simples son comunes en Julia. La sintaxis de función breve es, por lo tanto, bastante idiomática, lo que reduce considerablemente tanto el ruido de escritura como el visual.

Una función se llama utilizando la sintaxis de paréntesis tradicional:
```Julia
julia> f(2, 3)
5
```

Sin paréntesis, la expresión f se refiere al objeto de función y puede pasarse como cualquier otro valor:
```Julia
julia> g = f;

julia> g(2, 3)
5
```

Al igual que con las variables, Unicode también se puede utilizar para nombres de funciones:
```Julia
julia> ∑(x, y) = x + y
∑ (generic function with 1 method)

julia> ∑(2, 3)
5
```

## Comportamiento de paso de argumentos

Los argumentos de las funciones de Julia siguen una convención que a veces se denomina "pass-by-sharing", lo que significa que los valores no se copian cuando se pasan a las funciones. Los argumentos de las funciones actúan como nuevos enlaces de variables (nuevos "nombres" que pueden hacer referencia a valores), de forma muy similar a las asignaciones argument_name = argument_value, de modo que los objetos a los que hacen referencia son idénticos a los valores pasados. Las modificaciones a los valores mutables (como Arrays) realizadas dentro de una función serán visibles para el llamador. (Este es el mismo comportamiento que se encuentra en Scheme, la mayoría de los lenguajes Lisp, Python, Ruby y Perl, entre otros lenguajes dinámicos)
```Julia
function f(x, y)
    x[1] = 42    # mutates x
    y = 7 + y    # new binding for y, no mutation
    return y
end
```
La declaración x[1] = 42 muta el objeto xy, por lo tanto, este cambio será visible en la matriz pasada por el llamador para este argumento. Por otro lado, la asignación y = 7 + y cambia el enlace ("nombre") y para hacer referencia a un nuevo valor 7 + y, en lugar de mutar el objeto original al que hace referencia yy, por lo tanto, no cambia el argumento correspondiente pasado por el llamador. Esto se puede ver si llamamos a f(x, y):
```Julia
julia> a = [4, 5, 6]
3-element Vector{Int64}:
 4
 5
 6

julia> b = 3
3
```

julia> f(a, b) # returns 7 + b == 10
10

julia> a  # a[1] is changed to 42 by f
3-element Vector{Int64}:
 42
  5
  6

julia> b  # not changed
3
```

Como convención común en Julia (no un requisito sintáctico), dicha función normalmente se nombraría f!(x, y) en lugar de f(x, y), como un recordatorio visual en el sitio de la llamada de que al menos uno de los argumentos (a menudo el primero) está siendo mutado.

## Declaraciones de tipo argumento

Puede declarar los tipos de argumentos de una función agregando ::TypeName al nombre del argumento, como es habitual en las declaraciones de tipos en Julia. Por ejemplo, la siguiente función calcula los números de Fibonacci de forma recursiva:

```Julia
fib(n::Integer) = n ≤ 2 ? one(n) : fib(n-1) + fib(n-2)
```
Y la ::Integer especificación significa que solo será invocable cuando n sea un subtipo del tipo abstracto Integer.

## Return - palabra clave
El valor devuelto por una función es el valor de la última expresión evaluada, que, por defecto, es la última expresión en el cuerpo de la definición de la función. En la función de ejemplo, f, de la sección anterior, este es el valor de la expresión x + y. Como alternativa, como en muchos otros lenguajes, return hace que una función retorne inmediatamente, proporcionando una expresión cuyo valor se devuelve:
```Julia
function g(x, y)
    return x * y
    x + y
end
```
Dado que las definiciones de funciones se pueden introducir en sesiones interactivas, es fácil comparar estas definiciones:
```Julia
julia> f(x, y) = x + y
f (generic function with 1 method)

julia> function g(x, y)
           return x * y
           x + y
       end
g (generic function with 1 method)

julia> f(2, 3)
5

julia> g(2, 3)
6
```

Por supuesto, en un cuerpo de función puramente lineal como g, el uso de return no tiene sentido ya que la expresión x + y nunca se evalúa y podríamos simplemente hacer x * y la última expresión en la función y omitir el return. Sin embargo, junto con otro flujo de control, return es de verdadera utilidad. Aquí, por ejemplo, hay una función que calcula la longitud de la hipotenusa de un triángulo rectángulo con lados de longitud x y, evitando el desbordamiento:
```Julia
julia> function hypot(x, y)
           x = abs(x)
           y = abs(y)
           if x > y
               r = y/x
               return x*sqrt(1 + r*r)
           end
           if y == 0
               return zero(x)
           end
           r = x/y
           return y*sqrt(1 + r*r)
       end
hypot (generic function with 1 method)

julia> hypot(3, 4)
5.0
```

Hay tres posibles puntos de retorno de esta función, que retorna los valores de tres expresiones diferentes, según los valores de x y. El return de la última línea se puede omitir ya que es la última expresión.
