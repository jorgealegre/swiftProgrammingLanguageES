# Una guía Swift

> ### Aclaración del autor
>
> Dada la definición de la palabra _swift_, el título de esta sección se supone que quiere decir que esto es una guía breve y rápida, una guía _Swift_.

## Una guía Swift

La tradición sugiere que el primer programa en un lenguaje nuevo debería imprimir las palabras "Hello, World!" \("Hola Mundo"\) en la pantalla. En Swift, esto se puede hacer con una sola línea:

```swift
print("Hello, world!")
// Imprime "Hello, world!"
```

Si alguna vez has escrito código en C u Objective-C, esta sintaxis te puede resultar conocida. En Swift, esta línea es un programa completo. No es necesario importar una librería externa para funcionalidades como entrada/salida o manejo de _strings_. Código escrito con alcance global es usado como punto de entrada del programa, no es necesaria una función al estilo `main()`. Tampoco son necesarios los punto y coma al final de cada declaración.

Esta guía expondrá suficiente información para empezar a escribir código en Swift al mostrarte cómo lograr varias tareas de la programación. No te preocupes si no se entiende algo, todo lo que se instroduzca acá será explicado en mayor detalle en el resto del libro.

{% hint style="info" %}
Para una mejor experiencia, abra este capítulo como un _Playground_ en Xcode. _Playgrounds_ te permiten editar el código en vivo y ver los resultados de inmediato.

[Descargar Playground](https://docs.swift.org/swift-book/GuidedTour/GuidedTour.playground.zip)
{% endhint %}

## Valores simples

Usa `let` para declarar constantes y `var` para declarar variables. El valor de una constante no es necesario al momento de compilar pero sí se le debe asignar un valor exactamente una vez. Esto significa que se puede usar constantes para darle nombre a un valor que se determina una sola vez pero se planea usar en muchos lugar.

```swift
var myVariable = 42
myVariable = 50
let myConstant = 42
```

Una constante o variable debe tener el mismo tipo que el valor que se le desea asignar. Sin embargo, no siempre es necesario expresar el tipo explícitamente. Al proveer un valor al declarar la constante o variable, el compilador puede inferir su tipo. En el ejemplo de arriba, el compilador infiere que el tipo de `myVariable` es un entero porque su valor inicial es un entero.

Si el valor inicial no provee suficiente información \(o no hay un valor inicial\), se puede especificar el tipo escribiendolo seguido del nombre de la variable, separado por dos puntos.

```swift
let implicitInteger = 70
let implicitDouble = 70.0
let explicitDouble: Double = 70
```

{% hint style="success" %}
EXPERIMENTO  
Crea una constante con el tipo Float explícitamente declarado y con un valor de 4.
{% endhint %}

Nunca se convierten implícitamente valores de un tipo a otro. Si llegara a ser necesario, se debe crear una instancia del tipo deseado.

```swift
let label = "The width is "
let width = 94
let widthLabel = label + String(width)
```

{% hint style="success" %}
EXPERIMENTO  
Intenta sacar la conversión a `String` de la última línea. ¿Qué error puedes observar?
{% endhint %}

Hay una manera más sencilla de incluir valores en _strings_: escribe el valor entre paréntesis, con una barra invertida \(\\) antes de los paréntesis. Por ejemplo:

```swift
let apples = 3
let oranges = 5
let appleSummary = "I have \(apples) apples."
let fruitSummary = "I have \(apples + oranges) pieces of fruit.
```

{% hint style="success" %}
EXPERIMENTO  
Usa \\(\) para incluir una operación de punto flotante en un _string_ y para incluir el nombre de alguien en un saludo.
{% endhint %}

Usa tres comillas dobles \(`"""`\) para _strings_ que ocupan más de una línea. La indentación de cada linea es eliminada siempre y cuando coincidan con las tres comillas que cierren el _string_. Por ejemplo: 

```swift
let quotation = """
Aunque hayan espacios en blanco a la izquierda,
las líneas no están indentadas.
Salvo por esta línea.
Pueden haber comillas dobles (") sin estar escapadas.

Todavía tengo \(apples + oranges) frutas.
    """
```

Crea arreglos y diccionarios usando corchetes \(\[\]\) y accede a sus valores escribiendo el índice o la llave dentro de los corchetes. Está permitido incluir una coma después del último elemento.

```swift
var shoppingList = ["catfish", "water", "tulips", "blue paint"]
shoppingList[1] = "bottle of water"

var occupations = [
    "Malcolm": "Captain",
    "Kaylee": "Mechanic",
]
occupations["Jayne"] = "Public Relations”
```

Para crear un arreglo o diccionario vacío, usa la sintaxis de inicialización.

```swift
let emptyArray = [String]()
let emptyDictionary = [String: Float]()
```

Si se puede inferir el tipo, se puede escribir un arreglo vacío como `[]` y un diccionario vacío como `[:]`–por ejemplo cuando se declara una variable o cuando se pasa un argumento a una función.

```swift
shoppingList = []
occupations = [:]
```

## Control de flujo

Usa `if` y `switch` para condicionales y usa `for-in`, `while` y `repeat-while` para ciclos. Paréntesis envolviendo la condición o la variable del ciclo son opcionales. Llaves envolviendo el cuerpo son obligatorios.

```swift
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
// Imprime "11"
```

En una declaración `if`, la condición debe ser una expresión booleana. Esto significa que código como `if score { ... }` es un error, no una comparación implícita con el 0 \(`score == 0`\).

Se puede usar `if` y `let` juntos para trabajar con valores que pueden no estar presentes. Estos valores son representados como **opcionales**. Un valor opcional puede contener un valor o puede ser `nil` indicando la ausencia de un valor. Escribe un signo de pregunta \(?\) después de un tipo para declarar al valor como opcional.

```swift
var optionalString: String? = "Hello"
print(optionalString == nil)
// Imprime "false"

var optionalName: String? = "John Appleseed"
var greeting = "Hello!"
if let name = optionalName {
    greeting = "Hello, \(name)"
}
```

{% hint style="success" %}
EXPERIMENTO  
Cambia `optionalName` a `nil`. ¿Qué saludo obtuviste? Agrega una clausula `else` que le asigna otro saludo a `greeting` si `optionalName` es `nil`.
{% endhint %}

Si el valor opcional es `nil`, el condicional es falso y el código dentro de las llaves no es ejecutado. Si hay un valor dentro del opcional, el valor es extraído y asignado a la constante declarada con `let`, lo cual hace que tal constante sea accesible dentro del bloque adentro del `if`.

Otra forma de manejar valores opcionales es dar un valor por defecto usando el operador `??`. Si el opcional es nulo, se usa el valor por defecto.

```swift
let nickName: String? = nil
let fullName: String = "John Appleseed"
let informalGreeting = "Hi \(nickName ?? fullName)
```

Los _switches_ soportan una gran cantidad de tipos de datos y comparaciones, no están limitados a enteros y pruebas de igualdad.

```swift
let vegetable = "red pepper"
switch vegetable {
case "celery":
    print("Add some raisins and make ants on a log.")
case "cucumber", "watercress":
    print("That would make a good tea sandwich.")
case let x where x.hasSuffix("pepper"): // `hasSuffix` -> `tienePrefijo`
    print("Is it a spicy \(x)?")
default:
    print("Everything tastes good in soup.")
}
// Imprime "Is it a spicy red pepper?"
```

{% hint style="success" %}
EXPERIMENTO  
Intenta eliminar el caso por defecto \(_default_\). ¿Qué error obtienes?
{% endhint %}

Obseva como usar `let` puede ser usado en un caso para asignar el valor que causó la coincidencia a una constante.

Después de ejecutar el código dentro del caso del _switch_ al cual se entró, el programa sale del bloque del _switch_. La ejecución no continúa al siguiente caso por lo que no hay necesidad de insertar un `break` al final de cada bloque dentro de cada caso.

Se usa un `for-in` para iterar sobre cada elemento en un diccionario, aclarando un nombre para cada par de llaves y valores. Los diccionarios son una colección desordenada asi que al iterar, el orden es arbitrario.

```swift
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

{% hint style="success" %}
EXPERIMENTO  
Agrega otra variable para determinar qué tipo de número fue el más grande además de cuál fue ese número.
{% endhint %}

Usa `while` para repetir un bloque de código hasta que una condición cambie. La condición puede ir al final del _loop_ para garantizar que el bloque sea ejecutado por lo menos una vez.

```swift
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

```swift
var total = 0
for i in 0..<4 {
    total += i
}
print(total)
// Imprime "6"
```

Usa `..<` para omitir el valor superior, `...` para incluirlo.

## Funciones y Clausuras

Usa `func` para declarar una función. Ejecuta una función al incluir una lista de sus argumentos entre paréntesis. Usa `->` para separar el nombre de los parámetros con el tipo del valor de retorno de la función.

```swift
func greet(person: String, day: String) -> String {
    return "Hello \(person), today is \(day)."
}
greet(person: "Bob", day: "Tuesday")
```

>

{% hint style="success" %}
EXPERIMENTO  
Saca el parámetro `day`. Agrega un parámetro para incluir el especial de almuerzo del día en el saludo.
{% endhint %}

Por defecto, las funciones usan el nombre de los parámetros como etiquetas para los argumentos. Escribe una etiqueta distinta antes del nombre del parámetro o escribe `_` para no usar una etiqueta.

```swift
// En este ejemplo, sí traduzco el código al español para que se pueda apreciar 
// lo útil que son las etiquetas de los parámetros y los argumentos.
// Hacen que a la hora de usar la función, se pueda leer muy bien.

func saludaA(_ persona: String, el dia: String) -> String {
    return "Hello \(persona), today is \(dia)."
}
saludaA("John", el: "Wednesday")
```

Usa una tupla para crear un valor compuesto–por ejemplo, para devolver varios valores de una función. Los elementos de la tupla pueden ser referenciados por nombre o por índice.

```swift
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

```swift
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

```swift
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

```swift
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

Las funciones son un caso especial de clausuras: bloques de código que pueden ser ejecutados posteriormente. El código en una clausura puede acceder a las cosas como variables y funciones que estaban disponibles en el alcance donde la clausura fue creada, incluso si la clausura es ejecutada en otro alcance-acabamos de mostrar un ejemplo de esto con las funciones anidadas. Se puede escribir una clausura sin nombre al envolver el código en llaves \(´{}´\). Usa `in` para separar los argumentos y el tipo del valor de retorno del cuerpo de la función.

```swift
numbers.map({ (number: Int) -> Int in
    let result = 3 * number
    return result
})
```

{% hint style="success" %}
EXPERIMENTO  
Transforma la clausura para devolver 0 por cada número impar.
{% endhint %}

Hay muchas formas de escribir clausuras más concisas. Cuando el tipo de la clausura se conoce por adelantado como en una _callback_ para un delegado, se puede omitir el tipo de sus parámetros, el tipo del valor de retorno o ambas cosas. Clausuras con una sola instrucción implícitamente devuelven el valor generado por esa instrucción.

```swift
let mappedNumbers = numbers.map({ number in 3 * number })
print(mappedNumbers)
// Imprime "[60, 57, 21, 36]"
```

Se puede acceder a los parámetros por número en vez de por nombre–este método es muy útil para clausuras muy cortas. Una clausura pasada como último argumento a una función puede estar inmediatamente después del paréntesis. Se pueden omitir los paréntesis por completo si la clausura es el único argumento de la función.

```swift
let sortedNumbers = numbers.sorted { $0 > $1 }
print(sortedNumbers)
// Imprime "[20, 19, 12, 7]"
```

## Objetos y Clases

Usa `class` seguido por un nombre para crear una clase. Declarar una propiedad de una clase se hace de la misma manera que una constante o variable excepto que ahora está en el contexto de la clase. Asímismo, funciones y métodos se declaran de la misma manera.

```swift
class Shape {
    var numberOfSides = 0
    func simpleDescription() -> String {
        return "A shape with \(numberOfSides) sides."
    }
}
```

{% hint style="success" %}
EXPERIMENTO  
Agrega una propiedad constante con `let` y agrega otro método que reciba un argumento.
{% endhint %}

Crea una instancia de la clase al escribir el nombre de la clase seguido por paréntesis. Usa el punto para acceder a propiedades y métodos de la instancia.

```swift
var shape = Shape()
shape.numberOfSides = 7
var shapeDescription = shape.simpleDescription()
```

A esta versión de la clase `Shape` le está faltanto algo importante: un inicializador \(i.e. constructor\) para configurar la clase cuando se crea una nueva instancia. Usa `init` para declarar uno:

```swift
class NamedShape {
    var numberOfSides: Int = 0
    var name: String

    init(name: String) {
        self.name = name
    }

    func simpleDescription() -> String {
        return "A shape with \(numberOfSides) sides."
    }
}
```

Nota como se usa `self` para distinguir la propiedad `name` del argumento `name`. Los argumentos del inicializador se pasan como si fuera una llamada de una función cuando se crea una instancia de la clase. Toda propiedad necesita tener un valor–ya sea en su declaración \(como `numberOfSides`\) o en el inicializador \(como `name`\).

Usa `deinit` para crear un deinicializador si necesitas realizar trabajo de limpieza antes de que el objeto sea liberado.

Subclases incluyen el nombre de sus superclases después de sus propios nombres, separados por dos puntos. No es necesario heredar de una clase raíz o estándar por lo que una superclase es opcional.

Métodos en una subclase que reemplazan la implementación de la superclase son marcados con `override`–reemplazar un método por error, sin `override`, es detectado por el compilador como un error. El compilador también detecta métodos con `override` que no reemplazan ningún método de la superclase.

```swift
class Square: NamedShape {
    var sideLength: Double

    init(sideLength: Double, name: String) {
        self.sideLength = sideLength
        super.init(name: name)
        numberOfSides = 4
    }

    func area() -> Double {
        return sideLength * sideLength
    }

    override func simpleDescription() -> String {
        return "A square with sides of length \(sideLength)."
    }
}
let test = Square(sideLength: 5.2, name: "my test square")
test.area()
test.simpleDescription()
```

{% hint style="success" %}
EXPERIMENTO  
Crea otra subclase de `NamedShape` llamada `Circle` que tome un radio y un nombre como argumentos de su inicializador. Implementa los métodos `area()` y `simpleDescription()` dentro de la clase `Circle`.
{% endhint %}

Además de propiedades simples almacenadas, las propiedades pueden tener _getters_ y _setters_ \(bloques de código ejecutados cada vez que se accede y setea el valor de una propiedad\).

```swift
class EquilateralTriangle: NamedShape {
    var sideLength: Double = 0.0

    init(sideLength: Double, name: String) {
        self.sideLength = sideLength
        super.init(name: name)
        numberOfSides = 3
    }

    var perimeter: Double {
        get {
            return 3.0 * sideLength
        }
        set {
            sideLength = newValue / 3.0
        }
    }

    override func simpleDescription() -> String {
        return "An equilateral triangle with sides of length \(sideLength)."
    }
}
var triangle = EquilateralTriangle(sideLength: 3.1, name: "a triangle")
print(triangle.perimeter)
// Imprime "9.3"
triangle.perimeter = 9.9
print(triangle.sideLength)
// Imprime "3.3000000000000003"
```

En el _setter_ de `perimeter`, el valor nuevo tiene el nombre implícito `newValue`. Se puede declarar un nombre distinto explícitamente con paréntesis después del `set`.

Observa que el inicializador de EquilateralTriangle tiene 3 etapas distintas:

1. Setear el valor de propiedades que la subclase declara.
2. Llamar al inicializador de la superclase.
3. Cambiar el valor de propiedades definidas por la superclase. Cualquier trabajo adicional que use métodos, _getters_ y _setters_ se puede realizar en esta etapa.

Si no es necesario computar la propiedad pero aún así es necesario correr código antes o después de setearle un valor nuevo, usa willSet y didSet. El código que se declare acá se ejecuta cada vez que el valor de la propiedad cambie, salvo dentro del inicializador. Por ejemplo, la clase de abajo garantiza que el largo del lado de su triángulo siempre tenga el mismo largo que el lado de un su cuadrado.

```swift
class TriangleAndSquare {
    var triangle: EquilateralTriangle {
        willSet {
            square.sideLength = newValue.sideLength
        }
    }
    var square: Square {
        willSet {
            triangle.sideLength = newValue.sideLength
        }
    }
    init(size: Double, name: String) {
        square = Square(sideLength: size, name: name)
        triangle = EquilateralTriangle(sideLength: size, name: name)
    }
}
var triangleAndSquare = TriangleAndSquare(size: 10, name: "another test shape")
print(triangleAndSquare.square.sideLength)
// Imprime "10.0"
print(triangleAndSquare.triangle.sideLength)
// Imprime "10.0"
triangleAndSquare.square = Square(sideLength: 50, name: "larger square")
print(triangleAndSquare.triangle.sideLength)
// Imprime "50.0"
```

When working with optional values, you can write `?` before operations like methods, properties, and subscripting. If the value before the `?` is `nil`, everything after the `?` is ignored and the value of the whole expression is `nil`. Otherwise, the optional value is unwrapped, and everything after the `?` acts on the unwrapped value. In both cases, the value of the whole expression is an optional value.

Al trabajar con valores opcionales, podés escribir `?` antes de operaciones como métodos, propiedades o _subscripting_. Si el valor antes del `?` es nulo, todo lo que sigue del `?` es ignorado y el valor de toda la expresión es nulo. Si no, el valor opcional es desenvuelto y todo lo que sigue del `?` actua sobre el valor desenvuelto. En ambos casos, el valor de toda la expresión es un valor opcional.

```swift
let optionalSquare: Square? = Square(sideLength: 2.5, name: "optional square")
let sideLength = optionalSquare?.sideLength
```

## Enumeraciones y Estructuras

Usa enum para crear una enumeración. Como clases y cualquier otro tipo con nombre propio, las enumeraciones pueden tener métodos asociados.

```swift
enum Rank: Int {
    case ace = 1
    case two, three, four, five, six, seven, eight, nine, ten
    case jack, queen, king

    func simpleDescription() -> String {
        switch self {
        case .ace:
            return "ace"
        case .jack:
            return "jack"
        case .queen:
            return "queen"
        case .king:
            return "king"
        default:
            return String(self.rawValue)
        }
    }
}
let ace = Rank.ace
let aceRawValue = ace.rawValue
```

{% hint style="success" %}
EXPERIMENTO  
Escribe una función que compare dos valores de tipo `Rank` por sus `rawValue` \(i.e. valor crudo\).
{% endhint %}

Por defecto, Swift asigna los valores crudos empezando desde cero e incrementando de a uno para cada caso. Se puede cambiar este comportamiento especificando explícitamente los valores. En el ejemplo de arriba, `Ace` recibe un valor crudo explícito de `1` y el resto de los valores crudos son asignados en orden. También se pueden usar _strings_ o números de punto flotante como el tipo crudo de una enumeración. Usa la propiedad `rawValue` para acceder al valor crudo de un caso de una enumeración.

Usa el inicializador `init?(rawValue:)` para crear una instancia de la enumeración a partir de un valor crudo. Devuelve un caso de la enumeración si existe el caso que coincida con el valor dado o nulo si no existe el caso.

```swift
if let convertedRank = Rank(rawValue: 3) {
    let threeDescription = convertedRank.simpleDescription()
}
```

The case values of an enumeration are actual values, not just another way of writing their raw values. In fact, in cases where there isn’t a meaningful raw value, you don’t have to provide one.

Los valores de casos de una enumeración son valores reales, no solo otra forma de escribir sus valores crudos. De hecho, en casos donde no hay un valor crudo significativo, no es necesario proveer uno.

```swift
enum Suit {
    case spades, hearts, diamonds, clubs

    func simpleDescription() -> String {
        switch self {
        case .spades:
            return "spades"
        case .hearts:
            return "hearts"
        case .diamonds:
            return "diamonds"
        case .clubs:
            return "clubs"
        }
    }
}
let hearts = Suit.hearts
let heartsDescription = hearts.simpleDescription()
```

{% hint style="success" %}
EXPERIMENTO  
Agrega un método `color()` a `Suit` que retorna `"black"` para `spades` y `clubs` y `"red"` para `hearts` y `diamonds`.
{% endhint %}

Observa las dos maneras de referenciar al caso `hearts` arriba: cuando se asigna el valor a la constante `hearts`, el caso `Suit.hearts` es referenciado por su nombre completo porque la constante no tiene el tipo explícitamente especificado. Dentro del _switch_, el caso es referenciado por su forma abreviaddad `.hearts` porque se sabe que el tipo de `self` es `Suit`. Se puede usar la manera abreviada cada vez que el tipo se conoce por adelantado.

Si una enumeración tiene valores crudos, esos valores son determinados como parte de la declaración, lo que significa que cada instancia de un caso particular siempre tiene el mismo valor crudo. Otra posibilidad para casos en enumeraciones es que tengan valores asociados. Estos valores son determinados a la hora de crear una instancia y pueden ser distintos para cada instancia de un caso. Se lo puede ver como que los valores asociados tienes propiedades almacenadas distintas para cada instancia. Por ejemplo, considerar el caso de pedir la hora del amanecer y atardecer a un servidor. El servidor puede responder ya sea la información correcta o una descripción del error que ocurra.

```swift
enum ServerResponse {
    case result(String, String)
    case failure(String)
}

let success = ServerResponse.result("6:00 am", "8:09 pm")
let failure = ServerResponse.failure("Out of cheese.")

switch success {
case let .result(sunrise, sunset):
    print("Sunrise is at \(sunrise) and sunset is at \(sunset).")
case let .failure(message):
    print("Failure...  \(message)")
}
// Imprime "Sunrise is at 6:00 am and sunset is at 8:09 pm."
```

{% hint style="success" %}
EXPERIMENTO  
Agrega un tercer caso a `ServerResponse` y al `switch`.
{% endhint %}

Observa como se obtienen las horas del amanecer y atardecer en el mismo lugar donde se compara la instancia particular con los casos posibles en el switch.

Usa struct para crear estructuras. Estructuras soportan mucho del comportamiento de clases como propiedades e inicializadores. Una de las principales diferencias que tienen con clases es que las estructuras siempre se copian cuando se pasan de un lugar al otro en tu código mientras que las clases se pasan por referencia.

```swift
struct Card {
    var rank: Rank
    var suit: Suit
    func simpleDescription() -> String {
        return "The \(rank.simpleDescription()) of \(suit.simpleDescription())"
    }
}
let threeOfSpades = Card(rank: .three, suit: .spades)
let threeOfSpadesDescription = threeOfSpades.simpleDescription()
```

{% hint style="success" %}
EXPERIMENTO  
Escribe una función que devuelva un arreglo con un mazo completo de cartas, con una carta para cada combinación de rango y palo \(`Rank` y `Suit`\).
{% endhint %}

## Protocolos y Extensiones

Usa `protocol` para declarar un protocolo.

```swift
protocol ExampleProtocol {
    var simpleDescription: String { get }
    mutating func adjust()
}
```

Clases, enumeraciones y estructuras pueden adoptar protocolos.

```swift
class SimpleClass: ExampleProtocol {
    var simpleDescription: String = "A very simple class."
    var anotherProperty: Int = 69105
    func adjust() {
        simpleDescription += "  Now 100% adjusted."
    }
}
var a = SimpleClass()
a.adjust()
let aDescription = a.simpleDescription

struct SimpleStructure: ExampleProtocol {
    var simpleDescription: String = "A simple structure"
    mutating func adjust() {
        simpleDescription += " (adjusted)"
    }
}
var b = SimpleStructure()
b.adjust()
let bDescription = b.simpleDescription
```

{% hint style="success" %}
EXPERIMENTO  
Agrega un nuevo requerimiento al protocolo. ¿Qué cambios necesitas hacer en `SimpleClass` y `SimpleStructure` para que el código compile?
{% endhint %}

Observa la palabra clave `mutating` en la declaración de `SimpleStructure` para denotar que un método modifica la estructura. La declaración de `SimpleClass` no lo necesita ya que cualquier método de una clase puede modificar su estructura interna.

Usa `extension`  para agregar funcionalidades a un tipo existente, como por ejemplo métodos o propiedades computadas. Se puede usar una extensión para hacer que un tipo declarado en otro lado adopte un protocolo o incluso sobre un tipo importado de una librería o _framework_.

```swift
extension Int: ExampleProtocol {
    var simpleDescription: String {
        return "The number \(self)"
    }
    mutating func adjust() {
        self += 42
    }
}
print(7.simpleDescription)
// Imprime "The number 7"
```

{% hint style="success" %}
EXPERIMENTO  
Escribe una extensión sobre el tipo `Double` que agrega una propiedad `valorAbsoluto`.
{% endhint %}

Se puede usar el nombre de un protocolo como cualquier otro tipo nombrado–por ejemplo para crear una arreglo de objetos de diferentes tipos pero que todos adoptan el mismo protocolo. Cuando trabajas con valores cuyo tipo sea un protocolo, se pierde acceso a cualquier propiedad o método declarada fuera del protocolo.

```swift
let protocolValue: ExampleProtocol = a
print(protocolValue.simpleDescription)
// Imprime "A very simple class.  Now 100% adjusted."
// print(protocolValue.anotherProperty)  // Descomentar para ver el error.
```

Aunque la variable `protocolValue` sea del tipo `SimpleClass` en _runtime_ el compilador la trata como del tipo declarado, es decir, `ExampleProtocol`. Esto significa que no se puede accidentalmente acceder a propiedades o métodos que implemente la clase.

## Manejo de Errores

