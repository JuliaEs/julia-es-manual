# [Variables](@id man-variables)

Una variable, en Julia, es un nombre asociado (o ligado) a un valor. Es útil cuando quieres
almacenar un valor (que se obtuvo después de algunas matemáticas, o algún proceso) para usarlo más tarde. Por ejemplo:
```julia-repl
# Asignar un valor a la variable x
julia> x = 10
10

# Calcular algo con el valor de x
julia> x + 1
11

# Reasignar el valor de x
julia> x = 1 + 1
2

# Se puede asignar valores de otros tipos, como cadenas
julia> x = "¡Hola Mundo!"
"¡Hola Mundo!"
```

Julia proporciona un sistema extremadamente flexible para nombrar variables. Los nombres de las variables distinguen entre mayúsculas y minúsculas,
y no tienen significado semántico (es decir, el lenguaje no tratará las variables de manera diferente por sus nombres).
```jldoctest
julia> x = 1.0
1.0

julia> y = -3
-3

julia> Z = "mi cadena"
"mi cadena"

julia> frase_común = "¡Hola Mundo!"
"¡Hola Mundo!"

julia> ComienzoDeclaraciónUniversalDeLosDerechosHumanos = "人人生而自由，在尊严和权利上一律平等。"
"人人生而自由，在尊严和权利上一律平等。"
```

Se permiten nombres en Unicode (encoding de UTF-8):

```jldoctest
julia> δ = 0.00001
1.0e-5

julia> 안녕하세요 = "Hello"
"Hello"
```
En la REPL de Julia y varios otros entornos de edición de Julia, puedes escribir muchos símbolos Unicode con 
el nombre del símbolo LaTeX con barra invertida seguido de tabulador. Por ejemplo, la variable 
`δ` se puede ingresar escribiendo `\delta`- * tab *, o incluso `α̂₂` con `\alpha`- * tab * -`\hat`-
* tabulador * -`\_2`- * tabulador *. (Si encuentra un símbolo en alguna parte, por ejemplo, en el código de otra persona,
que no sabe escribir, la ayuda de REPL le dirá: simplemente escriba `?` y
luego pegue el símbolo.)

Julia incluso le permitirá redefinir las constantes y funciones integradas si es necesario (aunque
esto no se recomienda para evitar posibles confusiones):

```jldoctest
julia> pi = 3
3

julia> pi
3

julia> sqrt = 4
4
```

Sin embargo, si trata de redefinir una constante ya incluida o función que ya esté en uso, Julia escupirá un error:

```jldoctest
julia> pi
π = 3.1415926535897...

julia> pi = 3
ERROR: cannot assign a value to variable MathConstants.pi from module Main

julia> sqrt(100)
10.0

julia> sqrt = 4
ERROR: cannot assign a value to variable Base.sqrt from module Main
```

## Allowed Variable Names

Los nombres de las variables deben comenzar con una letra (A-Z o a-z), un guión bajo o un subconjunto del código Unicode
puntos superiores a 00A0; en particular, [categorías de caracteres Unicode](http://www.fileformat.info/info/unicode/category/index.htm)
Lu / Ll / Lt / Lm / Lo / Nl (letras), Sc / So (monedas y otros símbolos) y algunos otros caracteres similares a letras
(por ejemplo, un subconjunto de los símbolos matemáticos Sm) están permitidos. Los caracteres posteriores también pueden incluir ! y
díglos dígitos (0-9 y otros caracteres en las categorías Nd / No), así como otros puntos de código Unicode: diacríticos
y otras marcas de modificación (categorías Mn / Mc / Me / Sk), algunos conectores de puntuación (categoría Pc),
primos y algunos otros caracteres.

Los operadores como `+` también son identificadores válidos, pero se analizan especialmente. En algunos contextos, los operadores
se puede utilizar como variables; por ejemplo, `(+)` se refiere a la función de suma, y `(+) = f`
lo reasignará. La mayoría de los operadores infijos Unicode (en la categoría Sm), como `⊕`, se analizan
como operadores infijos y están disponibles para métodos definidos por el usuario (por ejemplo, puede usar `const ⊗ = kron`
para definir `⊗` como un producto de Kronecker infijo). Los operadores también pueden tener sufijos con marcas de modificación,
primos y sub/superíndices, p. ej. `+ ̂ₐ ″` se analiza como un operador infijo con la misma precedencia que `+`.
Se requiere un espacio entre un operador que termina con una letra subíndice/superíndice y un
nombre de la variable. Por ejemplo, si `+ᵃ` es un operador, entonces` +ᵃx` debe escribirse como `+ᵃ x` para distinguirlo
de `+ ᵃx`, donde` ᵃx` es el nombre de la variable.

Los únicos nombres explícitamente no permitidos para las variables son los nombres de las [Keywords](@ref) integradas:
```julia-repl
julia> else = false
ERROR: syntax: unexpected "else"

julia> try = "No"
ERROR: syntax: unexpected "="
```
Algunos caracteres Unicode se consideran equivalentes con respecto a sus identificadores.
Distintas formas de ingresar caracteres de combinación Unicode (por ejemplo, acentos)
se tratan como equivalentes (específicamente, los identificadores de Julia son [NFC](http://www.macchiato.com/unicode/nfc-faq) -normalizados).
Los caracteres Unicode `ɛ` (U+025B: letra minúscula latina abierta e)
y `µ` (U+00B5: micro signo) se tratan como equivalentes al las letras griegas correspondientes,
porque se puede acceder fácilmente a las primeras mediante algunos métodos de entrada.

## Stylistic Conventions

Si bien Julia impone pocas restricciones a los nombres válidos, se ha vuelto útil adoptar las siguientes
convenciones:

   * Los nombres de las variables se ponen en minúsculas.
   * La separación de palabras se puede indicar mediante guiones bajos (`'_'`), pero se desaconseja el uso de guiones bajos
     a menos que el nombre sea difícil de leer de otra manera.
   * Los nombres de `Type`s y` Module`s comienzan con una letra mayúscula y la separación de palabras se muestra en la parte superior
     con CamelCase en lugar de guiones bajos.
   * Los nombres de las funciones y los macros están en minúsculas, sin guiones bajos.
   * Las funciones que escriben en sus argumentos tienen nombres que terminan en `!`. A veces se les llama
     funciones "mutadoras" (NB: mutating functions) o "in place" porque están destinadas a producir cambios en sus argumentos
     después de llamar a la función, y no sólo devolver un valor.

Para obtener más información sobre las convenciones estilísticas, consulte la [Style Guide](@ref).
