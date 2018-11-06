# Una guía Swift

> #### Aclaración del autor
>
> Dada la definición de la palabra _swift_, el título de esta sección se supone que quiere decir que esto es una guía breve y rápida, una guía _Swift_.

## Una guía Swift

La tradición sugiere que el primer programa en un lenguaje nuevo debería imprimir las palabras "Hello, World!" \("Hola Mundo"\) en la pantalla. En Swift, esto se puede hacer con una sola línea:

```text
print("Hello, world!")
```

Si alguna vez has escrito código en C u Objective-C, esta sintaxis te puede resultar familiar. En Swift, esta línea es un programa completo. No es necesario importar una librería externa para funcionalidades como entrada/salida o manejo de _strings_. Código escrito con alcance global es usado como punto de entrada del programa, no es necesaria una función al estilo `main()`. Tampoco son necesarios los punto y coma al final de cada declaración.

Esta guía expondrá suficiente información para empezar a escribir código en Swift al mostrarte cómo lograr varias tareas de la programación. No te preocupes si no se entiende algo, todo lo que se instroduzca acá será explicado en mayor detalle en el resto del libro.

> NOTA En una Mac, descargue el siguiente [_Playground_](https://developer.apple.com/go/?id=swift-tour) y haga doble click en el archivo para abrirlo en Xcode

### Valores simples

Usa `let` para declarar constantes y `var` para declarar variables. El valor de una constante no es necesario al momento de compilar pero sí se le debe asignar un valor exactamente una vez. Esto significa que se puede usar constantes para darle nombre a un valor que se planea usar en muchos lugar.

```text
var myVariable = 42
myVariable = 50
let myConstant = 42
```

Una constante o variable deben tener el mismo tipo que el valor que se le desea asignar. Sin embargo, no siempre es necesario expresar el tipo explícitamente. Al proveer un valor al declarar la constante o variable, el compilador puede inferir su tipo. En el ejemplo de arriba, el compilador infiere que el tipo de `myVariable` es un entero porque su valor inicial es un entero.

Si el valor inicial no provee suficiente información \(o no hay un valor inicial\), se puede especificar el tipo escribiendolo seguido del nombre de la variable, separado por dos puntos.

```text
let implicitInteger = 70
let implicitDouble = 70.0
let explicitDouble: Double = 70
```

> EXPERIMENTO
> Crea una constante con el tipo Float explícitamente declarado y con un valor de 4.

Nunca se convierten implícitamente valores de un tipo a otro. Si eso llegara a ser necesario, se debe crear una instancia del tipo deseado.

```text
let label = "The width is "
let width = 94
let widthLabel = label + String(width)
```

> EXPERIMENTO
> Intenta sacar la conversión a `String` de la última línea. ¿Qué error puedes observar?

Hay una manera más sencilla de incluir valores en _strings_: escribe el valor entre paréntesis, con una barra invertida \(\\) antes de los paréntesis. Por ejemplo:

```text
let apples = 3
let oranges = 5
let appleSummary = "I have \(apples) apples."
let fruitSummary = "I have \(apples + oranges) pieces of fruit.
```

> EXPERIMENTO
> Usa \\(\) para incluir una operación de punto flotante en un _string_ y para incluir el nombre de alguien en un saludo.

Usa tres comillas dobles \("""\) para _strings_ que ocupan más de una línea. La indentación de cada linea es eliminada siempre y cuando coincidan con las tres comillas que cierren el _string_. Por ejemplo: let quotation = """ I said "I have \(apples\) apples." And then I said "I have \(apples + oranges\) pieces of fruit." ""”

Crea arreglos y diccionarios usando corchetes \(\[\]\) y accede a sus valores escribiendo el índice o la llave dentro de las llaves. Está permitido incluir una coma después del último elemento.

```text
var shoppingList = ["catfish", "water", "tulips", "blue paint"]
shoppingList[1] = "bottle of water"

var occupations = [
    "Malcolm": "Captain",
    "Kaylee": "Mechanic",
]
occupations["Jayne"] = "Public Relations”
```

Para crear un arreglo o diccionario vacío, usa la sintaxis de inicializador.

```text
let emptyArray = [String]()
let emptyDictionary = [String: Float]()
```

Si se puede inferir el tipo, se puede escribir un arreglo vacío como \[\] y un diccionario vacío como \[:\]–por ejemplo cuando se declara una variable o cuando se pasa un argumento a una función.

```text
shoppingList = []
occupations = [:]
```

### Control de flujo

Usa `if` y `switch` para condicionales y usa `for-in`, `while` y `repeat-while` para ciclos. Paréntesis envolviendo la condición o la variable del ciclo son opcionales. Llaves envolviendo el cuerpo son obligatorios.

```text
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
```

En una declaración `if`, la condición debe ser una expresión booleana. Esto significa que código como `if score { ... }` es un error, no una comparación implícita con el 0 \(`score == 0`\).

Se puede usar `if` y `let` juntos para trabajar con valores que pueden no estar presentes. Estos valores son representados como **opcionales**. Un valor opcional puede contener un valor o puede ser `nil` indicando la ausencia de un valor. Escribe un signo de pregunta \(?\) después de un tipo para indicar al valor como opcional.

```text
var optionalString: String? = "Hello"
print(optionalString == nil)

var optionalName: String? = "John Appleseed"
var greeting = "Hello!"
if let name = optionalName {
    greeting = "Hello, \(name)"
}
```

> EXPERIMENTO
> Cambiá `optionalName` a `nil`. ¿Qué saludo obtuviste? Agrega una clausula `else` que le asigna otro saludo a `greeting` si `optionalName` es `nil`.

Si el valor opcional es `nil`, el condicional es falso y el código dentro de las llaves no es ejecutado. Si hay un valor dentro del opcional, el valor es extraído y asignado a la constante declarada con `let`, lo cual hace que tal constante sea accesible dentro del bloque adentro del `if`.

Otra forma de manejar valores opcionales es dar un valor por defecto usando el operador `??`. Si el opcional es nulo, se usa el valor por defecto.

```text
let nickName: String? = nil
let fullName: String = "John Appleseed"
let informalGreeting = "Hi \(nickName ?? fullName)
```

Los _switches_ soportan una gran cantidad de tipos de datos y comparaciones, no están limitados a enteros y pruebas de igualdad.

```text
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
// Imprime "Is it a spicy red pepper?"
```

> EXPERIMENTO
> Intenta eliminar el caso por defecto \(_default_\). ¿Qué error obtienes?

Obsevar como usar `let` puede ser usado en un caso para asignar el valor que causó la coincidencia a una constante.

Después de ejecutar el código dentro del caso del _switch_ al cual se entró, el programa sale del bloque del _switch_. La ejecución no continúa al siguiente caso por lo que no hay necesidad de insertar un `break` al final de cada bloque dentro de cada caso.

Se usa un `for-in` para iterar sobre cada elemento en un diccionario, aclarando un nombre para cada par de llaves y valores. Los diccionarios son una colección desordenada asi que al iterar, el orden es arbitrario.

```
let interestingNumbers = [
    "Prime": [2, 3, 5, 7, 11, 13],
    "Fibonacci": [1, 1, 2, 3, 5, 8],
    "Square": [1, 4, 9, 16, 25],
]
var largest = 0
for (kind, numbers) in interestingNumbers {
    for number in numbers {
        if number > largest {
            largest = number
        }
    }
}
print(largest)
// Imprime "25"
```

> EXPERIMENT
> Agrega otra variable para determinar qué tipo de número fue el más grande además de cuál fue ese número.

Usá `while` para repetir un bloque de código hasta que una coindición cambie. La condición puede ir al final del _loop_ para garantizar que el bloque sea ejecutado por lo menos una vez.

```
var n = 2
while n < 100 {
    n *= 2
}
print(n)
// Imprime "128"

var m = 2
repeat {
    m *= 2
} while m < 100
print(m)
// Imprime "128"
```

Se puede usar `..<` para crear rangos de índices y así saber tener acceso al índice actual dentro del _loop_.

```
var total = 0
for i in 0..<4 {
    total += i
}
print(total)
// Imprime "6"
```

Usá `..<` para omitir el valor superior, `...` para incluirlo.

### Funciones y Clausuras

Usá `func` para declarar una función. Ejecuta una función al incluir una lista de sus argumentos entre paréntesis. Usá `->` para separar el nombre de los parámetros con el tipo del valor de retorno de la función.

```
func greet(person: String, day: String) -> String {
    return "Hello \(person), today is \(day)."
}
greet(person: "Bob", day: "Tuesday")
```

> EXPERIMENT
> Saca el parámetro `day`. Agrega un parámetro para incluir el especial de almuerzo del día en el saludo.

Por defecto, las funciones usan el nombre de los parámetros como etiquetas para los argumentos. Escribe una etiqueta distinta antes del nombre del parámetro o escribe `_` para no usar una etiqueta.

```
func greet(_ person: String, on day: String) -> String {
    return "Hello \(person), today is \(day)."
}
greet("John", on: "Wednesday")
```

Usa una tupla para crear un valor compuesto-por ejemplo, para devolver varios valores de una función. Los elementos de la tupla pueden ser referenciados por nombre o por índice.

```
func calculateStatistics(scores: [Int]) -> (min: Int, max: Int, sum: Int) {
    var min = scores[0]
    var max = scores[0]
    var sum = 0

    for score in scores {
        if score > max {
            max = score
        } else if score < min {
            min = score
        }
        sum += score
    }

    return (min, max, sum)
}
let statistics = calculateStatistics(scores: [5, 3, 100, 3, 9])
print(statistics.sum)
// Imprime "120"
print(statistics.2)
// Imprime "120"
```

Se pueden anidar funciones, las cuales tienen acceso a variables declaradas en la función que las engloba. Se pueden usar funciones anidadas para organizar el código en una función larga o compleja.

```
func returnFifteen() -> Int {
    var y = 10
    func add() {
        y += 5
    }
    add()
    return y
}
returnFifteen()
```

Las funciones son tipos de primer orden, lo que signifca que una función puede devolver una función como valor de retorno.

```
func makeIncrementer() -> ((Int) -> Int) {
    func addOne(number: Int) -> Int {
        return 1 + number
    }
    return addOne
}
var increment = makeIncrementer()
increment(7)
```

Una función puede recibir otra función como uno de sus argumentos.

```
func hasAnyMatches(list: [Int], condition: (Int) -> Bool) -> Bool {
    for item in list {
        if condition(item) {
            return true
        }
    }
    return false
}
func lessThanTen(number: Int) -> Bool {
    return number < 10
}
var numbers = [20, 19, 7, 12]
hasAnyMatches(list: numbers, condition: lessThanTen)
```

Las funciones son un caso especial de clausuras: bloques de código que pueden ser ejecutados posteriormente. El código en una clausura puede acceder a las cosas como variables y funciones que estaban disponibles en el alcance donde la clausura fue creada, incluso si la clausura es ejecutada en otro alcance-acabamos de mostrar un ejemplo de esto con las funciones anidadas. Se puede escribir una clausura sin nombre al envolver el código en llaves (´{}´). Usa `in` para separar los argumentos y el tipo del valor de retorno del cuerpo de la función.

```
numbers.map({ (number: Int) -> Int in
    let result = 3 * number
    return result
})
```

> EXPERIMENT
> Transforma la clausura para devolver 0 por cada número impar.

Hay muchas formas de escribir clausuras más concisas. Cuando el tipo de la clausura se conoce por adelantado como en una _callback_ para un delegado, se puede omitir el tipo de sus parámetros, el tipo del valor de retorno o ambas cosas. Clausuras con una sola instrucción implícitamente devuelven el valor generado por esa instrucción.

```
let mappedNumbers = numbers.map({ number in 3 * number })
print(mappedNumbers)
// Imprime "[60, 57, 21, 36]"
```

You can refer to parameters by number instead of by name—this approach is especially useful in very short closures. A closure passed as the last argument to a function can appear immediately after the parentheses. When a closure is the only argument to a function, you can omit the parentheses entirely.
Se puede acceder a los parámetros por número en vez de por nombre–este método es muy útil para clausuras muy cortas. Una clausura pasada como último argumento a una función puede estar inmediatamente después del paréntesis. Se pueden omitir los paréntesis por completo si la clausura es el único argumento de la función.

```
let sortedNumbers = numbers.sorted { $0 > $1 }
print(sortedNumbers)
// Imprime "[20, 19, 12, 7]"
```

### Objetos and Clases
