# Day8

## How to provide default values for parameters

- Swift lets us specify default values for any or all of our parameters.

```swift
func printTimesTables(for number: Int, end: Int = 12) {
    for i in 1...end {
        print("\(i) x \(number) is \(i * number)")
    }
}

printTimesTables(for: 5, end: 20)
printTimesTables(for: 8)  // The default value is used
```

### When to use default parameters for functions

- When you want to focus on the important parts that do need to change regulary.

## How to handle errors in functions

- First, define the posisble errors that might happen
- Define possible errors with `Error` protocol

```swift
enum PasswordError: Error {
    case short, obvious
}
```

- Use `throw` to trigger or throw errors.
- Use `throws` before the function return type.

```swift
func checkPassword(_ password: String) throws -> String {
    if password.count < 5 {
        throw PasswordError.short
    }

    if password == "12345" {
        throw PasswordError.obvious
    }

    if password.count < 8 {
        return "OK"
    } else if password.count < 10 {
        return "Good"
    } else {
        return "Excellent"
    }
}
```

- Handle errors using `do...try...catch`
    - `do` : The work that might throw errors.
    - `try` : Call throwing function
    - `catch` : Handling any thrown errors
- If there's no thrown error, it continues running the `do` block.
- If an error thrown, the `do` block execution will be interrupted.

```swift
let string = "12345"

do {
    let result = try checkPassword(Password)
    print("Password rating: \(result)")  // There's no error
} catch PasswordError.short {
    print("Please use a longer password.")
} catch PasswordError.obvious {
    print("I have the same combination on my luggage!")
} catch {
    print("There was an error.")
}
```

- `try!`
    - An alternative written as `try!` which does not require `do` and `catch`.
    - If an error is actually thrown, it will crash your code.
- `try?` : The same way, but it will not crash the code even if an error is thrown. It just return `nil`.

### When should you write throwing functions?

- Throwing functions don't mean they will throw errors, just that it's possible they can.
- You can handle the errors inside the function. Or, you can send them all back to whatever called teh function.
- Keep the number of throwing functions low.

### Why does Swift make us use try before every throwing function?

- By forcing to use `try` before every throwing function, we're explicitly acknowledging which parts of our code can cause errors.