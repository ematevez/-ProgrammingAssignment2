### Introducción

Esta segunda asignación de programación requerirá que escriba una R
función que es capaz de almacenar en caché cálculos que pueden consumir mucho tiempo.
Por ejemplo, tomar la media de un vector numérico suele ser una
operación. Sin embargo, para un vector muy largo, puede llevar demasiado tiempo
calcular la media, especialmente si tiene que calcularse repetidamente (p. ej.
en un bucle). Si el contenido de un vector no cambia, puede hacer
sentido almacenar en caché el valor de la media para que cuando lo necesitemos de nuevo,
se puede buscar en el caché en lugar de volver a calcular. En esto
Asignación de programación, se beneficiará de las reglas de alcance de
el lenguaje R y cómo se pueden manipular para preservar el estado dentro
de un objeto R.

### Ejemplo: almacenamiento en caché de la media de un vector

En este ejemplo introducimos el operador `<< -` que se puede usar para
asignar un valor a un objeto en un entorno que es diferente del
entorno actual. A continuación se muestran dos funciones que se utilizan para crear un
objeto especial que almacena un vector numérico y almacena en caché su media.

La primera función, `makeVector` crea un" vector "especial, que es
realmente una lista que contiene una función para

1. establece el valor del vector
2. obtener el valor del vector
3. establecer el valor de la media
4. obtener el valor de la media

<! - ->

    makeVector <- función (x = numeric ()) {
            m <- NULO
            set <- función (y) {
                    x << - y
                    m << - NULO
            }
            obtener <- función () x
            setmean <- función (media) m << - media
            getmean <- función () m
            lista (establecer = establecer, obtener = obtener,
                 setmean = setmean,
                 getmean = getmean)
    }

La siguiente función calcula la media del "vector" especial
creado con la función anterior. Sin embargo, primero verifica si el
la media ya se ha calculado. Si es así, "obtiene" la media del
caché y omite el cálculo. De lo contrario, calcula la media de
los datos y establece el valor de la media en la caché a través de `setmean`
función.

    cachemean <- función (x, ...) {
            m <- x $ getmean ()
            if (! is.null (m)) {
                    mensaje ("obteniendo datos en caché")
                    volver (m)
            }
            datos <- x $ get ()
            m <- media (datos, ...)
            x $ setmean (m)
            metro
    }

### Asignación: Almacenamiento en caché de la inversa de una matriz

La inversión de matrices suele ser un cálculo costoso y puede haber algunos
Beneficio de almacenar en caché la inversa de una matriz en lugar de calcularla
repetidamente (también hay alternativas a la inversión de matriz que
no discutir aquí). Tu tarea es escribir un par de funciones que
almacenar en caché la inversa de una matriz.

Escribe las siguientes funciones:

1. `makeCacheMatrix`: Esta función crea un objeto especial de" matriz "
    que puede almacenar en caché su inverso.
2. `cacheSolve`: esta función calcula la inversa de la especial
    "matriz" devuelta por `makeCacheMatrix` arriba. Si la inversa tiene
    ya se ha calculado (y la matriz no ha cambiado), entonces
    `cacheSolve` debería recuperar el inverso del caché.

El cálculo de la inversa de una matriz cuadrada se puede hacer con el "solve"
función en R. Por ejemplo, si `X` es una matriz cuadrada invertible, entonces
`solve (X)` devuelve su inverso.

Para esta asignación, suponga que la matriz proporcionada siempre es
invertible.
