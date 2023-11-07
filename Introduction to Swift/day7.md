# Day7

- Functions wrap up pieces of code so it can be used in lots of places.
- We can send data into functions to customize how they work, and get back caculated result data.
- It can make less code duplication. 
- Also, if you change the function, everywhere using it automatically get the new behavior. There's no risk of you forgotting to update one of the places you pasted it into.

## How to reuse code with functions

- We can pull out some code lines into functions, give it a name, and run it whenever and wherever we need.
- Declare a function with `func` keyword and function name.
- As you need, the function can has some parameters.
- When you call the function, you need to explicitly write the **parameter name**.
  - Parameter : placeholder used in function body
  - Argument : actual value we send into

```swift
// func : It marks the start of a function
// printTimesTables(number:end:) : The name of the function
// number, end : Parameters of the function
func printTimesTable(number: Int, end: Int) {
    for i in 1...end {
        print("\(i) x \(number) is \(i * number)")
    }
}

// Call the function with braces and arguments
printTimesTables(number: 5, end: 20)
```

### What code should be put in a function?

- Functions are designed to let us reuse code easily.
- Use functions when you want to the same functionality in many places.
- Use functions when you break up code.
- The function composition; it lets us build big functions by combining smaller functions.

### How many parameters should a function accept?

- A function could take 0~20 paraemters.
- If a function makes many parameters, you need to ask whether that function is perhaps doing a bit too much work.
  - Does it need all six of those parameters?
  - Could that function be split up into smaller functions that take fewer parameters?
  - Should those parameters be grouped somehow?

## How to return values from functions

- Functions perform some computation, then return the result of that work back to the call site.
- Write an arrow then a data type before your function's opening braces; whit kind of data will get sent back.
- Use the `return` keyword to send back your data.

```swift
func areLettersIdentical(string1: String, string2: String) -> Bool {
    let first = string1.sorted()
    let second = string2.sorted()
    return first == second
}
```

- When a function has only one line of code, we can remove the `return` keyword.

```swift
func areLettersIdentical(string1: String, string2: String) -> Bool {
    string1.sorted() == string2.sorted()
}
```

### When is the return keyword not needed in a Swift function?

- A function contains only a single expression.
- When a function contains loops or conditions, you can't remove `return` value.

```swift
func greet(name: String) -> String {
    if name == "Taylor Swift" {
        return "Oh wow!"  // can't remove `return`
    } else {
        return "Hello, \(name)"  // can't remove `return`
    }
}

func greet(name: String) -> String {
    name == "Taylor Swift" ? "Oh wow!" : "Hello, \(name)"  // you can remove `return` if you use ternary operator.
}
```

## How to return multiple values from functions

- If you return two or more values from a function, you could use collections like array, set, dictionary, or **tuples**.

```swift
func getUser() -> [String] {
  ["Taylor", "Swift"]
}

func getUser() -> [String: String] {
  ["firstName": "Taylor", "lastName": "Swift"]
}
```

- Or, you can use **tuples** instead of collections.
- Tuples have a key advantage over dictionaries: we specify exactly which values will exist and what types they have.

```swift
func getUser() -> (firstName: String, lastName: String) {
  (firstName: "Taylor", lastName: "Swift")
}
let user = getUser()
print("Name: \(user.firstName) \(user.lastName)")

// More simmple way
func getUser() -> (String, String) {
  ("Taylor", "Swift")
}
let user = getUser()
print("Name: \(user.0) \(user.1)")

// or
let (firstName, lastName) = getUser()
print("Name: \(firstName) \(lastName)")
```

### When should you use an array, a set, or a tuple in Swift?

- Arrays keep the order and can have duplicates.
- Sets are unordered and can't have duplicates.
- Tuples have a fixed number of values of fixed types.

## How to customize parameter labels

- The naming parameters for external use is so important to Swift that it actually uses the names when it comes to figuring out which method to call.
- Sometimes, these parameter names are less helpful.
- Use `_` as the external name for a parameter. `_` meas "ignore this", and causes there te be no external label for that parameter.

```swift
func isUppercase(_ string: String) -> Bool {
    string == string.uppercased()
}

let string = "HELLO, WORLD"
let result = isUppercase(string)
```

- `printTimesTables(number:)` doesn't read well. It would be much better; `printTimesTables(for:)`
- You can use a internal parameter name for one to use internally.
- External parameter name == argument
- Internal parameter name == parameter

```swift
func printTimesTables(for number: Int) {
    for i in 1...12 {
        print("\(i) x \(number) is \(i * number)")
    }
}
printTimesTables(for: 5)
```

### When should you omit a parameter label?

- The main reason for skipping a parameter name is when your function name is a verb and the first parameter is a noun the verb is acting on.
  - `greet(taylor)` is better than `greet(person: taylor)`
  - `buy(toothbrush)` is better than `buy(item: toothbrush)`
  - `find(customer)` is better than `find(user: customer)`
- This is particulary important when the parameter label is likely to be the same as the name of whatever you're passing in.
  - `sing(song)` is better than `sing(song: song)`
  - `enable(alarm)` is better than `enable(alarm: alarm)`
  - `read(book)` is better than `read(book: book)`