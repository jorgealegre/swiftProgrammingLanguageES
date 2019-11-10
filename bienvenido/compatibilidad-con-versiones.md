# Compatibilidad de versiones

Este libro describe Swift 5.1, la versión de Swift por defecto incluida en Xcode 11. Se puede usar Xcode 11 para compilar código escrito ya sea en Swift 5.1, Swift 4.2 o Swift 4.

## NOTA

La mayoría de las funcionalidades de Swift 5.1 están disponibles cuando se usa Xcode 11 para compilar código en Swift 4 y 4.2. Sin embargo, los siguientes cambios solo están disponibles para Swift 5.1 o superior:

* Funciones que devuelven un tipo opaco requieren el _runtime_ de Swift 5.1.
* La expresión `try?` no introduce un nivel extra de opcionalidad a expresiones que ya devuelven opcionales.
* Inicialización de enteros usando literales son inferidas para ser del tipo correcto. Por ejemplo, `UInt64(0xffff_ffff_ffff_ffff)` evalua al valor correcto en vez de permitir un _overflow_.

Un proyecto escrito en Swift 5.1 puede depender de un proyecto escrito en Swift 4.2 o 3 y vice versa. Esto significa que si se tiene un proyecto dividido en varios componentes, se puede migrar de a uno de Swift 4 a 5.1.

