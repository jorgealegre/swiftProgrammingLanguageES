# Compatibilidad con versiones
Este libro describe Swift 4.1, la versión de Swift por defecto incluida en Xcode 9.2. Se puede usar Xcode 9.2 para compilar **TODO targets** escritos ya sea en Swift 4 o Swift 3.

>###### NOTA

> When the Swift 4 compiler is working with Swift 3 code, it identifies its language version as 3.2. As a result, you can use conditional compilation blocks like `#if swift(>=3.2)` to write code that’s compatible with multiple versions of the Swift compiler.

>When you use Xcode 9.2 to build Swift 3 code, most of the new Swift 4 functionality is available. That said, the following features are available only to Swift 4 code:

>* Substring operations return an instance of the `Substring` type, instead of `String`.
* The `@objc` attribute is implicitly added in fewer places.
* Extensions to a type in the same file can access that type’s private members.

>A target written in Swift 4 can depend on a target that’s written in Swift 3, and vice versa. This means, if you have a large project that’s divided into multiple frameworks, you can migrate your code from Swift 3 to Swift 4 one framework at a time.