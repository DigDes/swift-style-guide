# swift-style-guide

## Содержание
* [Форматирование](#форматирование)
* [Комментарии](#комментарии)
* [Соглашение об именовании](#соглашение-об-именовании)
* [Константы](#константы)
* [Структура файла](#структура-файла)
* [Структура проекта](#структура-проекта)

## Форматирование
### Пробелы и табуляция
- Используем 4 пробела вместо табуляции.
- Строки не должны содержать "замыкающиеся" пробелы. [![SwiftLint: trailing_whitespace](https://img.shields.io/badge/SwiftLint-trailing__whitespace-blue.svg)][swiftlint_trailing_whitespace]

### Скобки
- Используем ["единственный правильный скобочный стиль"][the one true brace style].  
**Исключение:** блоки кода, состоящие из одной строки (но, если строка содержит логику, то рекомендуется перенести её на новую строку).

##### Хорошо:
```swift
if user.isHappy {
    // ...
} else {
    // ...
}
```

##### Тоже хорошо:
```swift
guard let value = value else { return 0 }

defer { file.close() }

switch someEnum {
case .first: return 5
case .second: return 10
case .third: return 20
}

let squares = numbers.map { $0 * $0 }

var someProperty: Int {
    get { return otherObject.property }
    set { otherObject.property = newValue }
}

var someProperty: Int { return otherObject.somethingElse() }

required init?(coder aDecoder: NSCoder) { fatalError("no coder") }
```

##### Плохо:
```swift
if user.isHappy
{  
    // ...
}  
else {
    // ...
}
```

##### Плохо:
```swift
if let user = user { usernameLabel.text = user.firstName + user.middleName + user.lastName }
```

### Ограничения по длине
- Длина строки ограничена 120 символами. [![SwiftLint: line_length](https://img.shields.io/badge/SwiftLint-line__length-blue.svg)][swiftlint_line_length]
- Длина файла ограничена 500 строками. [![SwiftLint: file_length](https://img.shields.io/badge/SwiftLint-file__length-blue.svg)][swiftlint_file_length]

### Точка с запятой
- Символ `;` в конце строки не используется без необходимости.

##### Хорошо:
```swift
func printSum(_ a: Int, _ b: Int) {
    let sum = a + b
    print(sum)
}
```

##### Плохо:
```swift
func printSum(_ a: Int, _ b: Int) {
    let sum = a + b;
    print(sum);
}
```

### Горизонтальные отступы
- Зарезервированные слова (такие как `if`, `guard`, `while`, `switch`) отделяются от выражения, следующего за ними, одним пробелом.

##### Хорошо:
```swift
if (x == 0 && y == 0) || z == 0 {
    // ...
}
```

##### Плохо:
```swift
if(x == 0 && y == 0) || z == 0 {
    // ...
}
```

- Если фигурные скобки используются в одной строке с некоторым кодом, то они отделяются от него одним пробелом ('{' отделяется с двух сторон, '}' отделяется только спереди).

##### Хорошо:
```swift
let nonNegativeCubes = numbers.map { $0 * $0 * $0 }.filter { $0 >= 0 }
```

##### Плохо:
```swift
let nonNegativeCubes = numbers.map { $0 * $0 * $0 } .filter { $0 >= 0 }
let nonNegativeCubes = numbers.map{$0 * $0 * $0}.filter{$0 >= 0}
```

- Бинарные и тернарные операторы отделяются пробелом с двух сторон.
**Исключение:** операторы `..<` и `...`.

##### Хорошо:
```swift
var x = 5

func sum(_ numbers: [Int], initialValue: Int = 0) {
    // ...
}

let substring = string[index..<string.endIndex]
```

##### Плохо:
```swift
var x=5

func sum(_ numbers: [Int], initialValue: Int=0) {
    // ...
}

let substring = string[index ..< string.endIndex]
```

- После символов `,` и `:` ставится пробел, но перед ними не ставится.

##### Хорошо:
```swift
let numbers = [1, 2, 3]

var nameAgeMap: [String: Int] = []
```

##### Плохо:
```swift
let numbers = [1,2,3]
let numbers = [1 ,2 ,3]
let numbers = [1 , 2 , 3]

var nameAgeMap: [String:Int] = []
var nameAgeMap: [String : Int] = []
```

- Использование горизонтального выравнивания в коде запрещено.

##### Хорошо:
```swift
struct DataPoint {
    var value: Int
    var primaryColor: UIColor
}
```

##### Плохо:
```swift
struct DataPoint {
    var value:        Int
    var primaryColor: UIColor
}

struct DataPoint {
    var primaryColor: UIColor
           var value: Int
}
```

### Вертикальные отступы
- Одна пустая строка используется в следующих местах:
    - Между функциями и свойствами
    - При необходимости разделить код на логические части
    - В конце файла
- Использование двух пустых строк подряд не допускается. [![SwiftLint: vertical_whitespace](https://img.shields.io/badge/SwiftLint-vertical__whitespace-blue.svg)][swiftlint_vertical_whitespace]

## Комментарии
- После `//` и `///` используется 1 пробел.
- Если комментарий находится в одной строке с кодом, то он отделяется спереди двумя пробелами.

##### Хорошо:
```swift
let initialFactor = 2  // Warm up the modulator.
```

##### Плохо:
```swift
let initialFactor = 2 //    Warm up the modulator.
```

- Использование блочных комментариев (`/* ... */`) не допускается.

### Документация
- Для документационных комментариев используем `///`
- Использование Javadoc-комментариев (`/** ... */`) не допускается.

##### Хорошо:
```swift
/// Returns the numeric value of the given digit represented as a Unicode scalar.
///
/// - Parameters:
///   - digit: The Unicode scalar whose numeric value should be returned.
///   - radix: The radix, between 2 and 36, used to compute the numeric value.
/// - Returns: The numeric value of the scalar.
func numericValue(of digit: UnicodeScalar, radix: Int = 10) -> Int {
    // ...
}
```

##### Плохо:
```swift
/**
 * Returns the numeric value of the given digit represented as a Unicode scalar.
 *
 * - Parameters:
 *   - digit: The Unicode scalar whose numeric value should be returned.
 *   - radix: The radix, between 2 and 36, used to compute the numeric value.
 * - Returns: The numeric value of the scalar.
 */
func numericValue(of digit: UnicodeScalar, radix: Int = 10) -> Int {
    // ...
}
```

- Приветствуется [использование специальной разметки][formatting quick help] для более информативного просмотра документации через Quick Help .
- Для автоматической генерации шаблона документации можно использовать сочетание **⌘ ⌥ /**.

## Соглашение об именовании

## Константы

## Структура файла

## Структура проекта



[comment]: # (Ссылки)
[the one true brace style]: https://en.wikipedia.org/wiki/Indentation_style#Variant:_1TBS_(OTBS)
[formatting quick help]: https://developer.apple.com/library/archive/documentation/Xcode/Reference/xcode_markup_formatting_ref/SymbolDocumentation.html#//apple_ref/doc/uid/TP40016497-CH51-SW1

[comment]: # (Правила)
[swiftlint_trailing_whitespace]: https://github.com/realm/SwiftLint/blob/master/Rules.md#trailing-whitespace
[swiftlint_vertical_whitespace]: https://github.com/realm/SwiftLint/blob/master/Rules.md#vertical-whitespace
[swiftlint_line_length]: https://github.com/realm/SwiftLint/blob/master/Rules.md#line-length
[swiftlint_file_length]: https://github.com/realm/SwiftLint/blob/master/Rules.md#file-line-length
