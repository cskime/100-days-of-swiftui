# Day1

## Storing some data

- variable : the value can change as program runs.
- constant : the value don't change

```swift
var name = "Ted"
name = "Rebecca"  // o

let character = "Daphne"
character = "Eloise"  // x
```

If you can, prefer to use constants rather than variables to optimize and never change a value by accidient.

### Why does Swift have variables?

- To store temporary data and transform it

### Why does Swift have constants as well as variables?

- To avoid some problems
- Since variables can be changed its value, you can lose some control.
- The important data might be replaced or removed at any point in the future.
- Constants don't let us change values once the are set, so you make sure the value never changes.
- **If you created variable and never changed its value, use `let` instead of `var`**

## Create String

- Swift's strings start and end with double quotes
- You can use alphabetic text, punctuation, emoji and other characters
- You can use other double quotes inside string with backslash before them (escaping char `\`)

```swift
let filename = "paris.jpg"
let quote = "Then he tapped a sign saying \"Believe\" and walked away."
```

- To read the lenght of a string, use `count`
- To change a letter to uppercased, use `uppercased()`
- To know whether a string starts or ends with specific letters, use `hasPrefix()` or `hasSuffix()`

```swift
let nameLength = name.count
print(nameLength.uppercased())
print(movie.hasPrefix("A day"))
print(filename.hasSuffix(".jpg"))
```

## Storing whole numbers

The integers.

- Store numbers such as 3, 5, or 5 million.
- Integer can hold negative.
- Swift use underscores(`_`) to break up numbers.
- You can use the `isMultiple(of:)` on an integer to find out whether it's a multiple of other integer.

```swift
let score = 10
let reallyBig = 100_100_100
let number = 120
number.isMultiple(of: 3)
```

- You can create integers from other integers, using the kinds of arithmetic operators: `+`, `-`, `*`, `/`, `%`
- Swift has some special operations that adjust an integer: `+=`

```swift
var count = 10
count = count + 5
count += 5
```

## Storing decimal numbers

- When you're working with decimal numbers such as '3.1', '5.56', '3.141592', you're working with what Swift calls **floating-point** numbers.
- To store very large numbers (e.g. 123,456,789) in the same amount of space as very small numbers (e.g. 0.0000000001), and the only way it can do that is by **moving the decimal point** around based on the size of the number.
- To create floating-point number, use `Double`

```swift
let number = 0.1 + 0.2
print(number)  // 0.30000000000000004
```

- Swift considers decimals to be a wholly different type of data to integers, which means you can't mix them together.
- Integers are always 100% accurate, whereas decimals are not.
- Swift's **Type Safety**
  - Once Swift has decided what data type a constant or variable holds, it must always hold that same data type.

```swift
let a = 1      // Int
let b = 2.0    // Double

let c = a + b          // x
let c = a + Int(b)     // o
let c = Double(a) + b  // o
```

- If there's a dot in number, Swift decides the type for `Double`, otherwise, it's an `Int`.

```swift
let intNumber = 3
let doubleNumber = 3.0
```

### Why does Swift need both Doubles and Integers?

- Integers hold whole numbers (e.g. 0. 1, -100)
- Doubles hold decimal numbers (e.g. 0.1, 1.0, 3.141592)
- Since mixing these two numbers are unsafe, Swift don't allow it.
- 'Unsafe' means that when you try to mix `1` and `2.5`, `0.5` can be losed.

### Why is Swift a type-safe language?

- To make sure we don't make mistake in large program.
- Changing value of `Int` type variable to `String` is obviously not allowed.
