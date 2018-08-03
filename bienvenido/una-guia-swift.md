> ##### Aclaración del autor
Dada la definición de la palabra _swift_, el título de esta sección se supone que quiere decir que esto es una guía breve y rápida, una guía _Swift_.

# Una guía Swift
La tradición sugiere que el primer programa en un lenguaje nuevo debería imprimir las palabras "Hello, World!" ("Hola Mundo") en la pantalla. En Swift, esto se puede hacer con una sola línea:

    print("Hello, world!")

Si alguna vez has escrito código en C u Objective-C, esta sintaxis te puede resultar familiar. En Swift, esta línea es un programa completo. No es necesario importar una librería externa para funcionalidades como entrada/salida o manejo de _strings_. Código escrito con alcance global es usado como punto de entrada del programa, no es necesaria una función al estilo `main()`. Tampoco son necesarios los punto y coma al final de cada declaración.

Esta guía expondrá suficiente información para empezar a escribir código en Swift al mostrarte cómo lograr varias tareas de la programación. No te preocupes si no se entiende algo, todo lo que se instroduzca acá será explicado en mayor detalle en el resto del libro.

> NOTA
> En una Mac, descargue el siguiente [_Playground_](https://developer.apple.com/go/?id=swift-tour) y haga doble click en el archivo para abrirlo en Xcode

## Valores simples
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

> EXPERIMENTO
> Intenta sacar la conversión a `String` de la última línea. ¿Qué error puedes observar?

Hay una manera más sencilla de incluir valores en _strings_: escribe el valor entre paréntesis, con una barra invertida (\\) antes de los paréntesis. Por ejemplo:

    let apples = 3
    let oranges = 5
    let appleSummary = "I have \(apples) apples."
    let fruitSummary = "I have \(apples + oranges) pieces of fruit.

> EXPERIMENTO
> Usa \\() para incluir una operación de punto flotante en un _string_ y para incluir el nombre de alguien en un saludo.

Usa tres comillas dobles (""") para _strings_ que ocupan más de una línea. La indentación de cada linea es eliminada siempre y cuando coincidan con las tres comillas que cierren el _string_. Por ejemplo:
    let quotation = """
    I said "I have \(apples) apples."
    And then I said "I have \(apples + oranges) pieces of fruit."
    ""”

Crea arreglos y diccionarios usando corchetes ([]) y accede a sus valores escribiendo el índice o la llave dentro de las llaves. Está permitido incluir una coma después del último elemento. 

    var shoppingList = ["catfish", "water", "tulips", "blue paint"]
    shoppingList[1] = "bottle of water"
     
    var occupations = [
        "Malcolm": "Captain",
        "Kaylee": "Mechanic",
    ]
    occupations["Jayne"] = "Public Relations”

Para crear un arreglo o diccionario vacío, usa la sintaxis de inicializador.

    let emptyArray = [String]()
    let emptyDictionary = [String: Float]()

Si se puede inferir el tipo, se puede escribir un arreglo vacío como [] y un diccionario vacío como [:]–por ejemplo cuando se declara una variable o cuando se pasa un argumento a una función.

    shoppingList = []
    occupations = [:]

## Control de flujo
Usa `if` y `switch` para condicionales y usa `for-in`, `while` y `repeat-while` para ciclos. Paréntesis envolviendo la condición o la variable del ciclo son opcionales. Llaves envolviendo el cuerpo son obligatorios.

    let individualScores = [75, 43, 103, 87, 12]
    var teamScore = 0
    for score in individualScores {
        if score > 50 {
            teamScore += 3
        } else {
            teamScore += 1
        }
    }
    print(teamScore)

En una declaración `if`, la condición debe ser una expresión booleana. Esto significa que código como `if score { ... }` es un error, no una comparación implícita con el 0 (`score == 0`).

Se puede usar `if` y `let` juntos para trabajar con valores que pueden no estar presentes. Estos valores son representados como **opcionales**. Un valor opcional puede contener un valor o puede ser `nil` indicando la ausencia de un valor. Escribe un signo de pregunta (?) después de un tipo para indicar al valor como opcional.

	var optionalString: String? = "Hello"
	print(optionalString == nil)
	 
	var optionalName: String? = "John Appleseed"
	var greeting = "Hello!"
	if let name = optionalName {
		greeting = "Hello, \(name)"
	}

> EXPERIMENTO
> Cambiá `optionalName` a `nil`. ¿Qué saludo obtuviste? Agrega una clausula `else` que le asigna otro saludo a `greeting` si `optionalName` es `nil`.

Si el valor opcional es `nil`, el condicional es falso y el código dentro de las llaves no es ejecutado. Si hay un valor dentro del opcional, el valor es extraído y asignado a la constante declarada con `let`, lo cual hace que tal constante sea accesible dentro del bloque adentro del `if`.

Otra forma de manejar valores opcionales es dar un valor por defecto usando el operador `??`. Si el opcional es nulo, se usa el valor por defecto.

	let nickName: String? = nil
	let fullName: String = "John Appleseed"
	let informalGreeting = "Hi \(nickName ?? fullName)

Los _switches_ soportan una gran cantidad de tipos de datos y comparaciones, no están limitados a enteros y pruebas de igualdad.

	let vegetable = "red pepper"
	switch vegetable {
	case "celery":
		print("Add some raisins and make ants on a log.")
	case "cucumber", "watercress":
		print("That would make a good tea sandwich.")
	case let x where x.hasSuffix("pepper"):
		print("Is it a spicy \(x)?")
	default:
		print("Everything tastes good in soup.")
	}

> EXPERIMENTO
> Intenta eliminar el caso por defecto (_default_). ¿Qué error obtienes?
