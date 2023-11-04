# Day5

## If: How to check a condition is true or false

- Swift handles some options with `if` statement
- It let us check a condition and run some code if condition is `true`

```swift
if someCondition {
    print("The condition is true.")
}
```

- Use the **comparison operator** to compare two things.
- `>`, `<`, `>=`, `<=`, `==`, `!=`

```swift
if speed >= 88 {
    rint("Where we're going we don't need roads.")
}

let ourName = "Dave Lister"
let friendName = "Arnold Rimmer"
if ourName < friendName {
    print("It's \(ourName) vs \(friendName)")
}
```

- In Swift, getting the number of letters of string isn't very fast because Swift supports many complex strings.
- `.count` makes Swift count all the letters one by one.
- Instead of using `.count` to check the string is empty, use `.isEmpty`.

```swift
if username.count == 0 {
    username = "Anonymous"
}

// better
if username.isEmpty {
    username = "Anonymous"
}
```

### How does Swift let us compare many types of data?

- Use same symbols to compare two values in many types.
- `>`, `<`, `>=`, `<=`, `==`, `!=`
- Many types overloads these operators
    - `Int`, `Double`, `Bool`, `String`, `Date`
    - The type which implements `Comparable` protocol.

```swift
enum Sizes: Comparable {
    case small, medium, large
}

let first = Sizes.small
let second = Sizes.large
print(first < second)  // true
```

## Else, Else If: How to check multiple conditions

- For mutually exclusive conditions, we use `else` block.
- You can use `else if` when you want to check multiple conditions.
- You have to use only one `else` at the end.

```swift
var number = 10
if number > 10 {
    print("The number is over 10.")
} else if number == 10 {
    print("The number is 10.")
} else {
    print("The number is lower than 10.")
}
```

- Use the **logical operator** to combine two conditions together.
- `&&`(AND), `||`(OR)

```swift
enum TransportOption {
    case airplane, helicopter, bicycle, car, scooter
}

let transport = TransportOption.airplane
if transport == .airplane || transport == .helicopter {
    print("Let's fly!")
} else if transport == .bicycle {
    print("I hope there's a bike path...")
} else if transport == .car {
    print("Time to get stuck in traffic.")
} else {
    print("I'm going to hire scooter now!")
}
```

### What's the difference between if and else if?

- `if` : Check the condition
- `else if` : Check the condition if the previous condition is `false`
- `else` : If all the previous conditions are `false`, run this code instead

### How to check multiple conditions

- Use `&&`(AND) or `||`(OR) operator
- There is a priority when you check multiple conditions logically.
  - Run in an order basically.
  - If you want to check specific conditions, wrap them in the parentheses.
- The result can be totally different.

```swift
// 1. Check isOwner and isEditingEnabled with '&&'
// 2. Check 1's result and isAdmin with '||'
if isOwner && isEditingEnabled || isAdmin {
    print("You can delete this post")
}

// 1. Check isEditingEnabled and isAdmin with '||'
// 2. Check isOwner and 2's result with '&&'
if isOwner && (isEditingEnabled || isAdmin) {
    print("You can delete this post")
}
```

## Switch

- When you use `if` and `else if` repeatedly, it's a bit hard to read and it's possible to make mistake like you can miss to check specific condition.
- `switch` makes easier to read, and avoid some problems
- When you check the same condition twice or miss some condition, Swift will complain.

```swift
enum Weather {
    case sun, rain, wind, snow, unknown
}

let forecast = Weather.sun

// if-else statement
if forecase == .sun {
    print("It should be a nice day.")
} else if forecast == .rain {
    print("Pack an umbrella.")
} else {  // missing to check wind, snow, unkown conditions
    print("Our forecast generator is broken!")
}

// switch statement
switch forecast {
case .sun:
    print("It should be a nice day.")
case .rain:
    print("Pack an umbrella.")
case .wind:
    print("Wear something warm")
case .snow:
    print("School is cancelled.")
case .unknown:
    print("Our forecast generator is broken!")
}
```

- All `switch` statements must be exhaustive. If it can't be, use `default` statement.
- Swift will execute cases in an order you write.
- Only one `case` code is run in `switch`. If you want to run next case, use `fallthrough` keyword.

```swift
let place = "Metropolis"

switch place {
case "Gotham":
    print("You're Batman!")
case "Mega-City One":
    print("You're Judge Dredd!")
    fallthrough
case "Wakanda":  // This code will run when 'place' is "Mega-City One"
    print("You're Black Panther!")
default:
    print("Who are you?")
}
```

### When should you use switch statements rather than if?

- `switch` is more safe. 
  - When you use `if-else` statement, 
  - you might accidentally miss a case.
  - you might read the same case multiple times
- `switch` cases allow for advanced pattern matching.

## The ternary conditional operator

- The binary operator works with **two** inputs.
- The ternary operator works with **three** inputs.

```swift
let age = 18
let canVote = (age >= 18) ? "YES" : "NO" // What ? True : "False

// This expression returns same result
let canVote: Bool
if age >= 18 {
    canVote = true
} else {
    canVote = false
}

// or, you can like this
let canVote = age >= 18
```

### When should you use the ternary operator in Swift?

- It lets us choose from one of two results base on a condition in a concise way.
- Use this operator if it makes your code more simple and easier to read.