# Compatibilidad de versiones

Este libro describe Swift 5.1, la versión de Swift por defecto incluida en Xcode 11. Se puede usar Xcode 11 para compilar código escrito ya sea en Swift 5.1, Swift 4.2 o Swift 4.

> ## NOTA
>
> Cuando el compilador de Swift 4 está trabajando sobre código en Swift 3, identifica el lenguaje con la versión 3.2. En consecuencia, se puede usar bloques de compilación condicional como `#if swift(>=3.2)` para escribir código compatible con múltiples versiones del compilador de Swift.
>
> Cuando se usa Xcode 9.2 para compilar código de Swift 3, la gran mayoría de las funcionalidades nuevas de Swift 4 están disponibles. Sin embargo, las siguientes características solo están disponibles para código en Swift 4:
>
> * Operaciones _substring_ devuelven instancias del tipo `Substring`, no del tipo `String`.
> * El atributo `@objc` as insertado implícitamente en menos lugares.
> * Extensiones sobre un tipo en el mismo archivo pueden acceder propiedades privadas de ese tipo.
>
> Un _target_ escrito en Swift 4 puede depender de un _target_ escrito en Swift 3 y vice versa. Esto significa que si se tiene un proyecto grande dividido en varios _frameworks_, se puede migrar el código de Swift 3 a Swift 4 de a un _framework_.

