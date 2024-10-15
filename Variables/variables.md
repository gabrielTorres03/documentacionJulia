#Variables
Una variable, en Julia, es un nombre asociado (o vinculado) a un valor. Es útil cuando se desea almacenar un valor (que se obtuvo después de realizar algunos cálculos, por ejemplo) para su uso posterior. 

Por ejemplo:

```Julia
# Asignamos el valor de 10 a la variables x
julia> x = 10
10

julia> x + 1
11

julia> x = 1 + 1
2

julia> x = "Hello World!"
"Hello World!"
```

Julia ofrece un sistema extremadamente flexible para nombrar variables. Los nombres de las variables distinguen entre mayúsculas y minúsculas y no tienen significado semántico (es decir, el lenguaje no tratará las variables de forma diferente en función de sus nombres).

```Julia
julia> x = 1.0
1.0

julia> y = -3
-3

julia> Z = "My string"
"My string"

julia> customary_phrase = "Hello world!"
"Hello world!"
```

Julia incluso te permitirá copiar constantes y funciones exportadas existentes con funciones locales (aunque esto no se recomienda para evitar posibles confusiones):
```Julia
julia> pi = 3
3

julia> pi
3

julia> sqrt = 4
4

julia> length() = 5
length (function generica con 1 metodo)

julia> Base.length
length (function generica con 79 metodos)
```

