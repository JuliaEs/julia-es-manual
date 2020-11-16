```@eval
io = IOBuffer()
release = isempty(VERSION.prerelease)
v = "$(VERSION.major).$(VERSION.minor)"
!release && (v = v*"-$(first(VERSION.prerelease))")
print(io, """
    # Documentación de Julia $(v)

    Bienvenidos a la documentación de Julia $(v).

    """)
if !release
    print(io,"""
        !!! warning "¡Trabajo en progreso!"
           Estaa documentación es para una versión no liberada y en desarrollo de Julia. 
        """)
end
import Markdown
Markdown.parse(String(take!(io)))
```
Por favor lea las [release notes](NEWS.md) para ver que ha cambiando desde el último release.

```@eval
release = isempty(VERSION.prerelease)
file = release ? "julia-$(VERSION).pdf" :
       "julia-$(VERSION.major).$(VERSION.minor).$(VERSION.patch)-$(first(VERSION.prerelease)).pdf"
url = "https://raw.githubusercontent.com/JuliaLang/docs.julialang.org/assets/$(file)"
import Markdown
Markdown.parse("""
!!! note
    Este manual también se puede conseguir en formato PDF: [$file]($url).
""")
```

### [Introduction](@id man-introduction)

La informática científica ha requerido tradicionalmente el más alto rendimiento, sin embargo los expertos en el dominio,
se han trasladado en gran parte, a lenguajes dinámicos más lentos para el trabajo diario. Creemos que existen muchas buenas razones
para preferir lenguajes dinámicos para estas aplicaciones, y no preveemos que disminuya su uso.
Afortunadamente, las técnicas modernas de compilación y diseño de lenguajes permiten eliminar
la compensación de rendimiento y proporcionar un entorno único que sea lo suficientemente productivo para la creación de prototipos y
lo suficientemente eficientes para implementar aplicaciones de alto rendimiento. El lenguaje de programación Julia
cumple esta función: es un lenguaje dinámico flexible, apropiado para la computación científica y numérica,
con un rendimiento comparable al de los lenguajes tradicionales de escritura estática.

Debido a que el compilador de Julia es diferente de los intérpretes utilizados para lenguajes como Python o
R, puede que al principio encuentre que la actuación de Julia no sea intuitiva. Si encuentra que algo es
lento, recomendamos leer la sección [Consejos de rendimiento](@ ref man-performance-tips) antes de intentar algo
más. Una vez que comprenda cómo funciona Julia, es fácil escribir código que es casi tan rápido como C.

Julia presenta una escritura opcional, de envío múltiple y de buen rendimiento, logrado mediante inferencia de tipos
y [compilación just-in-time (JIT)](https://en.wikipedia.org/wiki/Just-in-time_compilation),
implementado usando [LLVM](https://en.wikipedia.org/wiki/Low_Level_Virtual_Machine). Es multi-paradigma,
combinando características de programación imperativa, funcional y orientada a objetos. Julia proporciona
facilidad y expresividad para la computación numérica de alto nivel, al igual que lenguajes como
como R, MATLAB y Python, pero también es compatible con la programación general. Para lograr esto, Julia construye
sobre el linaje de los lenguajes de programación matemática, pero también toma prestado mucho de la dinámica popular
idiomas, incluido [Lisp](https://en.wikipedia.org/wiki/Lisp_ (programación_language)), [Perl](https://en.wikipedia.org/wiki/Perl_ (programación_language)),
[Python](https://en.wikipedia.org/wiki/Python_ (lenguaje_programación)), [Lua](https://en.wikipedia.org/wiki/Lua_ (lenguaje_programación)),
y [Ruby](https://en.wikipedia.org/wiki/Ruby_ (programación_language)).

Las divergencias más significativas de Julia en comparación a los lenguajes dinámicos típicos son:

  * El lenguaje central impone muy poco; Julia Base y la biblioteca estándar están escritas en Julia mismo, incluyendo
    operaciones primitivas como aritmética de enteros
  * Un lenguaje abundante en tipos para construir y describir objetos, que también puede ser opcionalmente
    utilizado para hacer declaraciones de tipo
  * La capacidad de definir el comportamiento de la función en muchas combinaciones de tipos de argumentos a través de [envío múltiple] (https://en.wikipedia.org/wiki/Multiple_dispatch)
  * Generación automática de código especializado y eficiente para diferentes tipos de argumentos
  * Buen rendimiento, aproximándose al de lenguajes compilados estáticamente como C

Aunque a veces se habla de lenguajes dinámicos como "sin tipo", definitivamente no lo son:
cada objeto, ya sea primitivo o definido por el usuario, tiene un tipo. La falta de declaraciones de tipo en
La mayoría de los lenguajes dinámicos, sin embargo, significa que no se puede instruir al compilador sobre los tipos de
valores y, a menudo, no pueden hablar explícitamente sobre tipos en absoluto. En lenguajes estáticos, por otro
lado mientras que uno puede, y generalmente debe, anotar tipos para el compilador, los tipos existen solo en
tiempo de compilación y no se puede manipular ni expresar en tiempo de ejecución. En Julia, los tipos son aquellos mismos
objetos en tiempo de ejecución, y también se pueden utilizar para transmitir información al compilador.

Si bien el programador casual no necesita usar explícitamente tipos o envíos múltiples, son el núcleo
de características unificadoras de Julia: las funciones se definen en diferentes combinaciones de tipos de argumentos,
y se aplica enviando a la definición coincidente más específica. Este modelo encaja bien
para la programación matemática, donde no es natural que el primer argumento "posea" una operación
como en el envío tradicional orientado a objetos. Los operadores son solo funciones con notación especial
- para ampliar la adición a nuevos tipos de datos definidos por el usuario, defina nuevos métodos para la función `+`.
El código existente se aplica sin problemas a los nuevos tipos de datos.

En parte debido a la inferencia de tipo en tiempo de ejecución (aumentada por anotaciones de tipo opcionales), y en parte
debido a un fuerte enfoque en el rendimiento desde el inicio del proyecto, la eficiencia del cálculo computacional de Julia
supera la de otros lenguajes dinámicos, e incluso rivaliza con la de los lenguajes compilados estáticamente.
Para problemas numéricos a gran escala, la velocidad siempre ha sido, sigue siendo y probablemente
siempre será crucial: la cantidad de datos que se procesan se ha mantenido fácilmente al ritmo de la Ley de Moore
en las ultimas decadas.

Julia tiene como objetivo crear una combinación sin precedentes de facilidad de uso, potencia y eficiencia en un solo
lenguaje. Además de lo anterior, algunas ventajas de Julia sobre sistemas comparables incluyen:

  * Libre y de código abierto ([con licencia MIT](https://github.com/JuliaLang/julia/blob/master/LICENSE.md))
  * Los tipos definidos por el usuario son tan rápidos y compactos como los integrados
  * No es necesario vectorizar el código para el rendimiento; el código desvectorizado es rápido
  * Diseñado para paralelismo y cálculo distribuido
  * Roscado ligero "verde" ([coroutines] (https://en.wikipedia.org/wiki/Coroutine))
  * Sistema de tipos discreto pero potente
  * Conversiones y promociones elegantes y extensibles para numéricos y otros tipos
  * Soporte eficiente para [Unicode] (https://en.wikipedia.org/wiki/Unicode), que incluye, entre otros,
    a [UTF-8] (https://en.wikipedia.org/wiki/UTF-8)
  * Llame a las funciones de C directamente (no se necesitan wrappers ni API especiales)
  * Potentes capacidades tipo shell para gestionar otros procesos
  * Macros tipo Lisp y otras instalaciones de metaprogramación
