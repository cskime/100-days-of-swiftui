# Day2

## Storing truth with booleans

- The boolean type(`Bool`) stores either true or false.
- Whether the string has specific characters at suffix or not. (`hasSuffix("a")`)
- Whether the number is multiple of two or not. (`isMultiple(of: 2)`)

```swift
let trueValue = true
let falseValue = false

let filename = "paris.jpg"
print(filename.hasSuffix(".png"))  // false

let number = 120
print(number.isMultiple(of: 2))  // true
```

- Booleans don't have artimetic operators such as `+`, `-`.
- Booleans have `!` operator, which means 'not'. This flips a value from true to false, for false to true.

```swift
var trueValue = true
var falseValue = !trueValue
```

- `toggle()` method flips a value to opposite value.

```swift
var trueValue = true
trueValue.toggle()  // 'trueValue' variable's value becomes 'false'.
```

## How to join strings together

You can combine strings with `+` operator.

```swift
var first = "Hello, "
var second = "World"
var greeting = first + second + "!"   
print(greeting)  // Hello, World!
```

Or, you can use string interpolation.

```swift
let name = "Tayylor"
let age = 26
let message = "Hello, my name is \(name) and I'm \(age) years old."
print(message)  // Hello, my name is Taylor and I'm 26 years old.
```

### Why does Swift have string interpolation?

- To inject custom data into strings at runtime. (dynamically)
- It replaces some parts of a string with data provided by us.
- You can place any kind of data inside string interpolation: `Int`, `String`, `Bool`, `Double` ...