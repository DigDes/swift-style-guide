# Swift Style Guide

## Содержание
* [Форматирование](#форматирование)
* [Комментарии](#комментарии)
* [Соглашение об именовании](#соглашение-об-именовании)
* [Константы](#константы)
* [Именование графических ресурсов](#именование-графических-ресурсов)
* [Структура файла](#структура-файла)
* [Структура проекта](#структура-проекта)
* [Оформление коммитов](#оформление-коммитов)

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
- Длина строки ограничена 140 символами. [![SwiftLint: line_length](https://img.shields.io/badge/SwiftLint-line__length-blue.svg)][swiftlint_line_length]
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

- Если фигурные скобки используются в одной строке с некоторым кодом, то они отделяются от него одним пробелом (`{` отделяется с двух сторон, `}` отделяется только спереди).

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
let initialFactor = 2  // Комментарий.
```

##### Плохо:
```swift
let initialFactor = 2 //    Комментарий.
```

- Использование блочных комментариев (`/* ... */`) не допускается.

### Документация
- Для документационных комментариев используем `///`
- Использование Javadoc-комментариев (`/** ... */`) не допускается.

##### Хорошо:
```swift
/// Возвращает числовое значение заданной цифры, представленной в виде UnicodeScalar.
///
/// - Parameters:
///   - digit: Unicode-скаляр, числовое значение которого должно быть возвращено.
///   - radix: Основание между 2 и 36, используемое для вычисления числового значения.
/// - Returns: Числовое значение скаляра.
func numericValue(of digit: UnicodeScalar, radix: Int = 10) -> Int {
    // ...
}
```

##### Плохо:
```swift
/**
 * Возвращает числовое значение заданной цифры, представленной в виде UnicodeScalar.
 *
 * - Parameters:
 *   - digit: Unicode-скаляр, числовое значение которого должно быть возвращено.
 *   - radix: Основание между 2 и 36, используемое для вычисления числового значения.
 * - Returns: Числовое значение скаляра.
 */
func numericValue(of digit: UnicodeScalar, radix: Int = 10) -> Int {
    // ...
}
```

- Приветствуется [использование специальной разметки][formatting quick help] для более информативного просмотра документации через Quick Help .
- Для автоматической генерации шаблона документации можно использовать сочетание **⌘ ⌥ /**.

## Соглашение об именовании

## Константы

## Именование графических ресурсов

<!--Image names should be named consistently to preserve organization and developer sanity. They should be named as one camel case string with a description of their purpose, followed by the un-prefixed name of the class or property they are customizing (if there is one), followed by a further description of color and/or placement, and finally their state.//-->

Изображения должны быть названы в [ВерблюжьемРегистре](http://ru.wikipedia.org/wiki/CamelCase) с описанием их назначения, содержать имя класса или свойства, для которого они предназначены (если такое имеется), далее идет цвет или расположение, и в конце состояние элемента, для которого предназначено изображение.

**Хорошо**

* `RefreshBarButtonIcon` / `RefreshBarButtonIcon@2x` and `RefreshBarButtonIconSelected` / `RefreshBarButtonIconSelected@2x`
* `ArticleNavigationBarWhite` / `ArticleNavigationBarWhite@2x` and `ArticleNavigationBarBlackSelected` / `ArticleNavigationBarBlackSelected@2x`.

Изображения, используемые для одинаковых целей должны быть сгруппированы в папки.
##### Важно: Перед добавлением изображения в ассет, переименуйте его. Если переименовать изображение после добавления, имя файла останется прежним.

## Структура файла

## Структура проекта

## Оформление коммитов
- Коммит должен содержать только одно логическое изменение.
- Первая строка коммита (Subject) должна содержать не более 72 символов. 
- Message Subject и Message Body коммита должны быть разделены пустой строкой.
- Перед публикацией коммитов в удалённый репозиторий убедитесь, что все однотипные и незначительные коммиты были объединены.
- Создавая коммит, подумайте, какая информация понадобится вам, если вы наткнётесь на этот коммит через год.

Структура Message коммита:
> [Ключ задачи в JIRA] Краткое описание изменений.
>
> Более подробное описание изменений. Оно должно объяснять, почему требуются изменения, как они решают проблему, и какие могут возникнуть ошибки.

[comment]: # (Ссылки)
[the one true brace style]: https://en.wikipedia.org/wiki/Indentation_style#Variant:_1TBS_(OTBS)
[formatting quick help]: https://developer.apple.com/library/archive/documentation/Xcode/Reference/xcode_markup_formatting_ref/SymbolDocumentation.html#//apple_ref/doc/uid/TP40016497-CH51-SW1

[comment]: # (Правила)
[swiftlint_trailing_whitespace]: https://github.com/realm/SwiftLint/blob/master/Rules.md#trailing-whitespace
[swiftlint_vertical_whitespace]: https://github.com/realm/SwiftLint/blob/master/Rules.md#vertical-whitespace
[swiftlint_line_length]: https://github.com/realm/SwiftLint/blob/master/Rules.md#line-length
[swiftlint_file_length]: https://github.com/realm/SwiftLint/blob/master/Rules.md#file-line-length
