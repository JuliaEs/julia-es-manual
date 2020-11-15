# Julia Documentation README

La documentación de Julia está escrita en Markdown. Una guía para toda la síntaxis permitida se puede encontrar en la sección del [manual](https://docs.julialang.org/en/v1/stdlib/Markdown/). Toda la documentación se puede encontrar en archivos de Markdown en `doc/src` y en los docstrings de los archivos de Julia en `base/` y en `stdlib/` .

## Requirements

La documentación se construye usando el paquete de [Documenter.jl](https://github.com/JuliaDocs/Documenter.jl).

Todas las dependencias se instalan automáticamente en un directorio de paquetes autocontenido en `doc/deps/` para evitar interferir los paquetes de los usuarios.

## Building

Para construir la documentación de Julia corra
```sh
$ make docs
```

from the root directory. This will build the HTML documentation and output it to the `doc/_build/` folder.
desde su directorio raíz. Esto construye la documentación HTML y lo escribe en el folder `doc/_build/.`

## Testing

Para correr los doctests del manual corra
```sh
$ make -C doc doctest=true
```
desde el directorio raíz.
