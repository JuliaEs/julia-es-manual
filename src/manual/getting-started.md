# [Getting Started](@id man-getting-started)

La instalación de Julia es sencilla, ya sea usando binarios precompilados o compilando desde la fuente.
Descargue e instale Julia siguiendo las instrucciones en [https://julialang.org/downloads/](https://julialang.org/downloads/).

Si llega a Julia desde uno de los siguientes idiomas, entonces debería empezar leyendo la sección de diferencias notables de [MATLAB](@ref Noteworthy-differences-from-MATLAB), [R](@ref Noteworthy-differences-from-R), [Python](@ref Noteworthy-differences-from-Python), [C/C++](@ref Noteworthy-differences-from-C/C) o [Common Lisp](@ref Noteworthy-differences-from-Common-Lisp). Esto le ayudará a evitar algunos errores comunes ya que Julia difiere de esos lenguajes en muchas formas sutiles.

La forma más fácil de aprender y experimentar con Julia es iniciando una sesión interactiva (también
conocido como un bucle de lectura-eval-impresión o "REPL") haciendo doble clic en el ejecutable de Julia o ejecutando
"julia" en la terminal:

```@eval
io = IOBuffer()
Base.banner(io)
banner = String(take!(io))
import Markdown
Markdown.parse("```\n\$ julia\n\n$(banner)\njulia> 1 + 2\n3\n\njulia> ans\n3\n```")
```
Para salir de la sesión interactiva, escriba `CTRL-D` (presione la tecla Control/`^` junto con la tecla `d`), o escriba
`exit()`. Cuando se ejecuta en modo interactivo, `julia` muestra un banner y pide al usuario que provea input.
Una vez que el usuario ha introducido una expresión completa, como `1 + 2`, y pulsa enter, la sesión evalúa la expresión
y muestra su valor. Si una expresión se introduce en una sesión interactiva
sesión con un punto y coma al final, su valor no se muestra. La variable `ans` está ligada al
valor de la última expresión evaluada, se muestre o no. La variable `ans` es sólo válida
en sesiones interactivas, y no existe el código de Julia se ejecuta de otras maneras.

Para evaluar las expresiones escritas en un archivo fuente `archivo.jl`, escribe `include(archivo.jl)`.

Para ejecutar código en un archivo de forma no interactiva, puedes darle como primer argumento a `julia`.

```
$ julia script.jl arg1 arg2...
```
Como implica el ejemplo, los siguientes argumentos de la línea de comandos para `julia` se interpretan como
argumentos de la línea de comandos para el programa `script.jl`, pasados en la constante global` ARGS`.
El nombre del script en sí se pasa como el `PROGRAM_FILE` global. Tenga en cuenta que `ARGS` también se define
cuando se da una expresión de Julia usando la opción `-e` en la línea de comando (ver el output
de `julia` a continuación) pero` PROGRAM_FILE` estará vacío. Por ejemplo, para imprimir el
argumentos dados a un script, puede hacer esto:

```
$ julia -e 'println(PROGRAM_FILE); for x in ARGS; println(x); end' foo bar

foo
bar
```
O puedes escribir tu código en un script y correrlo así:

```
$ echo 'println(PROGRAM_FILE); for x in ARGS; println(x); end' > script.jl
$ julia script.jl foo bar
script.jl
foo
bar
```

El delimitador `--`  se puede usar para separar entre argumentos de la terminal y argumentos para Julia>

```
$ julia --color=yes -O -- foo.jl arg1 arg2..
```

Lea también [Scripting](@ref man-scripting) para saber más sobre scripting en Julia.

Julia puede iniciarse en modo paralelo con las opciones `-p` o` --machine-file`. `-p n`
lanzará `n` procesos adicionales, mientras que` --machine-file file` lanzará un trabajador
para cada línea en el archivo `archivo`. Las máquinas definidas en `archivo` deben ser accesibles a sin contraseña vía
`ssh`, con Julia instalada en la misma ubicación que el host actual. Cada definición de máquina
tiene la forma `[cuenta *][usuario@]host[:puerto][bind_addr[:puerto]]`. `usuario` tiene como valor predeterminado el usuario actual,
 y `port` el puerto ssh estándar. `count` es el número de trabajadores que se generarán en el nodo y por default es igual a 1.
La opción `bind-to bind_addr [: port]` especifica la dirección IP y el puerto que otros trabajadores
debe utilizar para conectarse a este trabajador.

Si tienes código que quieres ejecutar cada vez que se comience Julia, lo puedes poner en 
`~/.julia/config/startup.jl`:

```
$ echo 'println("¡Saludos! 你好! 안녕하세요?")' > ~/.julia/config/startup.jl
$ julia
¡Saludos! 你好! 안녕하세요?

...
```


Tenga en cuenta que aunque debería tener un directorio `~ /.julia` una vez que haya ejecutado Julia por 
primera vez, es posible que deba crear la carpeta `~ /.julia/config` y el archivo
`~ /.julia/config/startup.jl` si lo usa.

Hay varias formas de ejecutar el código de Julia y proporcionar opciones, similares a las disponibles para
Programas `perl` y` ruby`:
```
julia [switches] -- [archivo] [args...]
```

 Una lista detallada de todos los switches disponibles se puede encontrar en [Command-line Options](@ref command-line-options).

## Resources

Una lista de recursos particularmente útiles para que puedan aprender nuevos usuarios está en la página de [learning](https://julialang.org/learning/) en el sitio principal de Julia.
