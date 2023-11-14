# Day14

How to unwrap optionals?
1. `if let`
2. `guard let`
3. `??` (nil coalescing)
4. `?.` : Optional chaining

## How to handle missing data with optionals

- It might have a value or not.
- `?` : It means a value might exist or not.
- `String?` : It means a `String` value might exist or not.

```swift
let opposites = [
    "Mario": "Wario",
    "Luigi": "Waluigi"
]

// Compiler doens't know there is a data, or not.
// The data might exist or not.
let peachOpposite: String? = opposites["Peach"]
```

- `nil` : It means "no value".
- Swift likes our code to be predictable, it won't let us use data that might not be there.
- We need to **unwrap** the optional in order to use it.
- `if let` syntax is common way to unwrap the optional value.

```swift
if let marioOpposite = opposites["Mario"] {
    print("Mario's opposite is \(marioOpposite)")
}
```

### Why does Swift have optionals?

- Optionals represent the absence of some data.

### Why does Swift make us unwrap optionals?

- Unwrapping using `if let` is a concise way of working with optionals, taking care of checking and extracting values all at once
- Swift won't let us use optionals without unwrapping.

## How to unwrap optionals with guard

- You can use `guard let` syntax to unwrap a optional values.
- `if let` runs the code inside its braces if the optional had a value.
- `guard let` runs the code inside its braces if the optional 'didn't have' a value.

```swift
if let unwrapped {
    print("Run if optional has a value inside")
}

guard let unwrapped else {
    print("Run if optional doesn't have a value inside")
    return
}
```

### When to use guard let rather than if let

- `guard` is commonly used at the start of the methods to verify that some conditions are correct up front.
- Use `if let` if you just want to unwrap some optionals.
- Use `guard let` if you're specifically checking that there's a value before continuing.

## How to unwrap optionals with nil coalescing

- `??` : nil coalescing operator
- It lets us unwrap an optional and provide a default value if optional was empty.

```swift
let captains = [
    "Enterprise": "Picard",
    "Voyager": "Janeway",
    "Defiant": "Sisko"
]

// using default value
let new = captains["Serenity", default: "N/A"]

// using nil coalescing
let new = captains["Serenity"] ?? "N/A"
```

### When should you use nil coalescing in Swift?

- It's useful when you want to unwrap optionals and provide a default value immediately.
- You can chain nil coalescing.

## How to handle multiple optionals using optional chaining

- Optional chaining is a simplified syntax for reading optionals inside optionals.
- It means "if the optional has a value inside, unwrap it then ..."
- If the optional is emtpy, then next code won't be executed and it returns `nil`.

```swift
// If 'randomElement()' returns 'nil', 'uppercased()' will be ignored and this line returns 'nil'
// When it returns 'nil', it will be replaced to "No one" by nil coalescing operator.
// Finally, 'chosen' has the data '"No one"'.
let chosen = names.randomElement()?.uppercased() ?? "No one"
```

- Another example in struct

```swift
struct Book {
    let title: String
    let author: String?
}

var book: Book? = nil
let author = book?.author?.first?.uppercased() ?? "A"
print(author)  // "A"
```

### Why is optional chaining so important?

- Optional chaining lets us dig through several layers of optionals in a single line of code
- If any one of those layers is 'nil', then the whole line becomes 'nil'.

## How to handle function failure with optionals?

- We can use optional try(`try?`) to have the throwing function return an optional value.
- If the function ran without throwing any errors then the optional will contain the return value.
- If any error was thrown the function will return 'nil'.
- It's useful when you don't care about exact error.

```swift
func getUser(id: Int) throws -> String {
    throw UserError.networkFailed
}

if let user = try? getUser(id: 23) {
    print("User: \(user)")
}
```

### When should you use optional try?

- It's up to how important the error is to you.
- If you want to run a function and care only that it succeeds or fails, then using optional try is a great fit.

```swift
do {
    let result = try runRiskyFunction()
    print(resut)
} catch {
    print("It failed")
}

// much simpler, but you don't know what error occurs exactly.
if let result = try? runRiskyFunction() {
    print(result)
}
```