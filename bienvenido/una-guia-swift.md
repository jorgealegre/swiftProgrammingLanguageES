> ##### Aclaración del autor
Dada la definición de la palabra _swift_, el título de esta sección se supone que quiere decir que esto es una guía breve y rápida, una guía _Swift_.

# Una guía Swift
La tradición sugiere que el primer programa en un lenguaje nuevo debería imprimir las palabras "Hello, World!" ("Hola Mundo") en la pantalla. En Swift, esto se puede hacer con una sola línea:

    print("Hello, world!")

Si alguna vez has escrito código en C u Objective-C, esta sintaxis te puede resultar familiar. En Swift, esta línea es un programa completo. No es necesario importar una librería externa para funcionalidades como entrada/salida o manejo de _strings_. Código escrito con alcance global es usado como punto de entrada del programa, no es necesaria una función al estilo `main()`. Tampoco son necesarios los punto y coma al final de cada declaración.

Esta guía expondrá suficiente información para empezar a escribir código en Swift al mostrarte cómo lograr varias tareas de la programación. No te preocupes si no se entiende algo, todo lo que se instroduzca acá será explicado en mayor detalle en el resto del libro.

> NOTA
> En una Mac, descargue el siguiente [_Playground_](https://developer.apple.com/go/?id=swift-tour) y haga doble click en el archivo para abrirlo en Xcode

## Simple Values
Usa `let` para declarar constantes y `var` para declarar variables. El valor de una constante no es necesario al momento de compilar pero sí se le debe asignar un valor exactamente una vez. Esto significa que se puede usar constantes para darle nombre a un valor que se planea usar en muchos lugar.

    var myVariable = 42
    myVariable = 50
    let myConstant = 42

Una constante o variable deben tener el mismo tipo que el valor que se le desea asignar. Sin embargo, no siempre es necesario expresar el tipo explícitamente. Al proveer un valor al declarar la constante o variable, el compilador puede inferir su tipo. En el ejemplo de arriba, el compilador infiere que el tipo de `myVariable` es un entero porque su valor inicial es un entero.

Si el valor inicial no provee suficiente información (o no hay un valor inicial), se puede especificar el tipo escribiendolo seguido del nombre de la variable, separado por dos puntos.

    let implicitInteger = 70
    let implicitDouble = 70.0
    let explicitDouble: Double = 70

> EXPERIMENTO

> Crea una constante con el tipo Float explícitamente declarado y con un valor de 4.

Nunca se convierten implícitamente valores de un tipo a otro. Si eso llegara a ser necesario, se debe crear una instancia del tipo deseado.

    let label = "The width is "
    let width = 94
    let widthLabel = label + String(width)
