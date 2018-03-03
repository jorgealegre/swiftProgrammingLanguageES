> ##### Aclaración del autor
Dada la definición de la palabra _swift_, el título de esta sección se supone que quiere decir que esto es una guía breve y rápida, una guía _Swift_.

# Una guía Swift
Tradition suggests that the first program in a new language should print the words “Hello, world!” on the screen. In Swift, this can be done in a single line:

print("Hello, world!")
If you have written code in C or Objective-C, this syntax looks familiar to you—in Swift, this line of code is a complete program. You don’t need to import a separate library for functionality like input/output or string handling. Code written at global scope is used as the entry point for the program, so you don’t need a main() function. You also don’t need to write semicolons at the end of every statement.

This tour gives you enough information to start writing code in Swift by showing you how to accomplish a variety of programming tasks. Don’t worry if you don’t understand something—everything introduced in this tour is explained in detail in the rest of this book.

NOTE

On a Mac, download the Playground and double-click the file to open it in Xcode: https://developer.apple.com/go/?id=swift-tour

‌
Simple Values
Use let to make a constant and var to make a variable. The value of a constant doesn’t need to be known at compile time, but you must assign it a value exactly once. This means you can use constants to name a value that you determine once but use in many places.

var myVariable = 42
myVariable = 50
let myConstant = 42
A constant or variable must have the same type as the value you want to assign to it. However, you don’t always have to write the type explicitly. Providing a value when you create a constant or variable lets the compiler infer its type. In the example above, the compiler infers that myVariable is an integer because its initial value is an integer.

If the initial value doesn’t provide enough information (or if there is no initial value), specify the type by writing it after the variable, separated by a colon.

let implicitInteger = 70
let implicitDouble = 70.0
let explicitDouble: Double = 70

EXPERIMENT

Create a constant with an explicit type of Float and a value of 4.

Values are never implicitly converted to another type. If you need to convert a value to a different type, explicitly make an instance of the desired type.

let label = "The width is "
let width = 94
let widthLabel = label + String(width)