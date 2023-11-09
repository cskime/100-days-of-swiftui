# Day9

## How to create and use closures

- You can assign functions to variables, pass into functions, and return from functions.

```swift
func greetUser() {
    print("Hi there!")
}

greetUser()  // call the function

var greetCopy = greetUser  // assign to variable
greetCopy()
```

- You can skip creating a separate function and assign the functionality directly to a constant or variable.
- The closure expression is a chunk of code we can pass and call whenever we want.
- Closure is a function that doesn't have a name.
- `in` is used to mark the end of the parameters and return type.
- External parameter isn't needed when calling closure.

```swift
// `name` is the parameter of closure
// `String` is the return type of closure
let sayHello = { (name: String) -> String in 
    "Hi \(name)!"
}
```

- Function type : `(PARAMETER_LIST) -> RETURN_TYPE`
- It's same as the function : `func FUNCTION_NAME(PARAMETER_LIST) -> RETURN_TYPE {}`

```swift
func getUserData(for id: Int) -> String { ... }
let data: (Int) -> String = getUserData
let user = data(10)
```

- `sorted()` actually allows us to poass in a custom sorting function, and this function must accept two strings and return boolean.
- You can pass a function, or also can pass a closure. These has two `String` parameters and returns `Bool` type value.

```swift
// pass a function
func captainFirstSecond(name1: String, name2: String) -> Bool {
    if name1 == "Suzanne" { return true }
    else if name2 == "Suzanne" { return false }
    return name1 < name2
}

let captainFirstTeam1 = team.sorted(by: captainFirstSecond)

// pass a closure
let captainFirstTeam2 = team.sorted(by: { (name1: String, name2: String) -> Bool in 
    if name1 == "Suzanne" { return true }
    else if name2 == "Suzanne" { return false }
    return name1 < name2
})
```

### What the heck are closures and why does Swift love them so much?

- To store functionality; it's able to say "here's some work Iw ant you to do at some point, but not necessariliy now."
- Running some code after a delay. (e.g. after an animation has finished, when a download has finished)
- Closures let us wrap up some functionality in a single value, then store that somewhere.

### Why are Swift's closure parameters inside the braces?

- It can be confused if you write like this: `let payment = (user: String, amount: Int)`.
- It would look like a tuple.
- `in` keyword is so important. Without that it's hard for Swift to know where your closure body actually starts.

### How do you return a value from a closure that takes no parameters?

- Use empty parentheses for your parameter list.

```swift
let payment = { () -> Bool in 
    print("Paying an anonymous person...")
    return true
}
```

## How to use trailing closures and shorthand syntax

- We don't need to specify the types because they must be `String`.
- We don't need to specify a return type because it must be a `Bool`.
- Trailing closure; We can start the closure directly without the parameter name.
- Use `$0`, `$1` for first and second parameters.

```swift
// Original Code
let captainFirstTeam2 = team.sorted(by: { (name1: String, name2: String) -> Bool in 
    if name1 == "Suzanne" { return true }
    else if name2 == "Suzanne" { return false }
    return name1 < name2
})

// Skip types
let captainFirstTeam2 = team.sorted(by: { name1, name2 in 
    if name1 == "Suzanne" { return true }
    else if name2 == "Suzanne" { return false }
    return name1 < name2
})

// Trailing closure
let captainFirstTeam2 = team.sorted { name1, name2 in 
    if name1 == "Suzanne" { return true }
    else if name2 == "Suzanne" { return false }
    return name1 < name2
}

// Replace parameter
let captainFirstTeam2 = team.sorted {
    if $0 == "Suzanne" { return true }
    else if $1 == "Suzanne" { return false }
    return $0 < $1
}

// More simpler
let reverseTeam = team.sorted { $0 > $1 }  // skip `return` when function and closure body has single line code.
```

### Why does Swift have trailing closure syntax?

- To read easier.
- You can see what the closure is doing.

### When should you use shorthand parameter names?

- If there're may parameters, you may be much harder to read.
- If the parameter is used several times in your method, you should probably use a real name.
- What matters is that your code is easy to read and understand.

## How to accept functions as parameters

- Use parameter's type as function type.

```swift
func makeArray(size: Int, using generator: () -> Int) -> [Int] {
    var numbers = [Int]()
    for _ in 0..<size {
        let newNumber = generator()
        numbers.append(newNumber)
    }
    return numbers
}

let rolls = makeArray(size: 50) { Int.random(in: 1...20) }
print(rolls)
```

- When there are multiple parameters, the first trailing closure is identical.
- But the second and third are formatted differently: You write external parameter name.

```swift
func execute(first: () -> Void, second: () -> Void, third: () -> Void) {
    first()
    second()
    third()
}

execute { 
    print("This is the first work") 
} second: {
    print("This is the second work")
} third: {
    print("This is the third work")
}
```

### Why would you want to use closures as parameters?

- Swift's closures can be used as the type of data, which meas you can pass them into functions.
- It launches our app in the background and passes in a closure that we can call when we're done.
- When we request data from the internet we do so with closures; "fetch this data, and when you're done run this closure"
- We don't force our user interface to freeze while some slow work is happening.