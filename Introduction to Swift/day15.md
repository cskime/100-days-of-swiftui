# Day15

## Variable and Constant

```swift
// variable
var name = "Ted"
name = "Rebecca"  // o

// constant
let user = "Daphne"
user = "someone"  // x
```

## Types

### String

```swift
// creating string
let actor = "Tom Cruise"

// using double quote in string with escaping character '\'
let quote = "He tapped a sign saying \"Believe\" and walked away."

// multiline string
let movie = """
A day in
the life of an
Apple engineer
"""

// joining strings(interpolation) using '\()' syntax.
let name = "Taylor"
let age = 26
let message = "I'm \(name) and I'm \(age) years old."

// useful functions
quote.hasPrefix("He")  // whether it contains specific string at the start of the given string.
quote.hasSuffix("Away.")  // whether it contains specific string at the end of the given string.
```

### Int

```swift
// creating integer
var score = 10

// compound assignment operator
score += 10

// useful functions
score.isMultiple(of: 2)  // whether it's multiple of specific integer
Int.random(in: 1...100)  // making random integers in a specific range
```

### Decinal(Double)

```swift
// creating decimal
var score = 3.0
var number: Double = 3
```

### Bool

```swift
// creating booleans
let goodDogs = true
let gameOver = false

// useful functions
goodDogs.toggle()  // flipping the value to opposite value
```

## Collection

### Arrays

```swift
// creating array
var colors = ["Red", "Green", "Blue"]

// accessing a value using index
colors[0]  // "Red"
colors[3]  // fatal error. this index is out of range.

// adding a value
colors.append("Orange")

// removing the value
colors.remove(at: 0)
colors.remove(at: 3)  // fatal error. this index is out of range.

// counting the number of items in array
colors.count

// checking whether there is a specific item in the array
colors.contains("Blue")
```

### Dictionaries

```swift
// creating dictionary
let employee = [
    "name": "Taylor",
    "job": "Singer"
]

// adding and updating a data
employee["gender"] = "Women"
employee["name"] = "Taylor Swift"

// reading a data
employee["name"]  // Optional("Taylor")
employee["address"]  // nil

// reading a data with default value
employee["address", default: "Unknown"]  // "Unknown"
```

### Sets

```swift
// creating set (remove duplicates)
var numbers = Set([1, 1, 3, 5, 7])  // [1, 3, 5, 7]

// adding a data
numbers.insert(10)

// checking whether there is a specific item in the set
numbers.contains(5)
```

## Enums

```swift
enum Weekday {
    case monday, tuesday, wendsday, thursday, friday
}

var day = Weekday.monday
day = .friday
```

## Type annotations

```swift
var player: String = "Roy"
var number: Int = 13
var score: Double = 0
var isEnabled: Bool = true
var albums: [String] = ["Red", "Fearless"]
var user: [String: String] = ["id": "@twostraws"]
var books: Set<String> = Set(["The Bluest Eye", "Foundation"])
```

## Conditions

```swift
// if-elseif-else statement
if condition1 {
    // execute when condition1 is true
} else if condition2 {
    // exectue when condition1 is false and condition2 is true
} else if condition3 && condition4 || condition5 {
    // execute when condition1 and condition2 are false,
    // and the result of expression with condition3, 4, 5 is true
    // the expression is executed according to priority
    //   1. condition3 and condition4 with && operator
    //   2. result of 1 and condition5 with || operator
} else {
    // execute when both conditions are false
}

// switch statement
switch condition {
case case1:
    // execute when the condition matches for case1
case case2:
    // execute when the condition matches for case2
case case3:
    // execute when the condition matches for case3
default:
    // execute when there are no cases which matches to condition
}

// ternary conditional operator
let result = condition ? true : false
```

## Loops

```swift
// for loop
for item in {range or collection} {
    // execute with item of collection and range
}

// while loop
while condition {
    // execute until the condition becomes false
}

// flow control
for os in ["iOS", "macOS", "tvOS", "watchOS"] {
    guard os == "iOS" else {
        continue  // ignore other codes and run next loop
        break     // stop running and exit this loop block immediately
    }

    print(os)
}
```

## Functions

```swift
// creating function
//   - name           : execute
//   - argument label : with
//   - parameter      : value
//   - parameter type : Int
//   - return type    : String
func execute(with value: Int = 0) -> String {
    return String(value)  // return value
}

execute(with: 10)

// returning multiple values using tuple
func getUser() -> (firstName: String, lastName: String) {
    ("Taylor", "Swift")
}

var user = getUser()
print("Name: \(user.firstName) \(user.lastname)")

// providing default values for parameters
// the default value of 'formal' parameter is 'false'
func greet(_ person: String, formal: Bool = false) { ... }
greet("Tim", formal: true)  // provide 'true' to formal
greet("Taylor")  // use default value to formal

// handling errors
//   - use 'throws' keyword before returnning syntax (->)
//   - use 'throw' keyword to trigger some error
//   - If there's no needs to trigger an error, just return a value
//   - when you call throwing function, use `try` keyword in front of call and wrap it 'do' block
//   - you have to write following 'catch' block to handle throwing errors
enum PasswordError: Error {
    case short, obvious
}

func checkPassword(_ password: String) throws -> String {
    if password.count < 5 {
        throw PasswordError.short
    } else {
        return "GOOD"
    }
}

do {
    try checkPassword("12345")
} catch {
    // execute when 'checkPassword()' function throws some errors
    // you can access that error with 'error' variable which hides in 'catch' block
}
```

## Closures

```swift
// creating closure
// the anonymous function which has no name
let sayHello = { (name: String) -> String in
    "Hi \(name)!"
}
sayHello("Taylor")

// provide a closure as a function type parameter
// 'filter' function has one parameter which type is '(String) -> Bool'
let team = []"Gloria", "Suzanne", "Tiffany", "Tasha"]
let onlyT = team.filter({ (name: String) -> Bool in 
    return name.hasPrefix("T") 
})

// shorthand syntax
//   1. remove 'return' keyword when the closure has just a single line
//   2. remove types when we sure parameter and return types
//   3. remove braces when the function type parameter is the latest one; trailing closure
//   4. switch parameter to short form; $0
let onlyT = team.filter { $0.hasPrefix("T") }
```

## Structs

```swift
// creating struct
struct Employee {
    let name: String
    let vacationAllocated: Int

    // property observer
    let vacationTaken = 0 {
        willSet {
            print("The value will be changed from \(vacationTaken) to \(newValue)")
        }

        didSet {
            print("The value is changed from \(oldValue) to \(vacationTaken)")
        }
    }

    // computed property; getter and setter
    var vacationRemaining: Int {
        get { vacationAllocated - vacationTaken }
        set { vacationAllocated = vacationTaken + newValue }
    }

    // marking as mutating when a function changes one of its properties
    mutating func removeFromSale() {
        someProperty = false
    }

    // custom initializer
    init(name: String) {
        self.name = name
        vacationAllocated = 14
    }
}
```

### Access control

```swift
struct BankAccount {
    // it can be changed only inside of this struct (private setter)
    // but, it can be read from any other places (internal getter)
    private(set) var funds = 0
}
```

### Static property and methods

```swift
struct AppData {
    // it can be read from the type directly rather than from the instance    
    static let version = "1.3 beta 2"
    static let settings = "settings.json"
}
```

## Classes

```swift
class Employee {
    let hours: Int
    
    init(hours: Int) {
        self.hours = hours
    }

    func printSummary() {
        print("I work \(hours) hours a day.")
    }
}

// class can inherit functionality to subclass
class Developer: Employee {

    // you can acccess properties and methods inherited from super class
    func work() {
        print("I'm coding for \(hours) hours.")
    }
}

let novall = Developer(hours: 8)  // inherited initializer
novall.work()  // own method
novall.printSummary()  // inherited method
```

### Class initializer

```swift
class Vehicle {
    let isElectric: Bool

    // Classes don't have a memberwise initializer
    init(isElectric: Bool) {
        self.isElectric = isElectric
    }
}

class Car: Vehicle {
    let isConvertible: Bool

    init(isElectric: Bool, isConvertible: Bool) {
        self.isConvertible = isConvertible

        // In a child class initializer, you have to call the parent's initializer
        // after it has finished setting up its own properties
        super.init(isElectric: isElectric)
    }

    // Classes have a deinitializer that gets called when the last reference to an object is destroyed.
    deinit {
        print("All of instances is destroyed")
    }
}
```

## Protocols

```swift
// creating protocol
protocol Vehicle {

    // protocols can have properties list with getter/setter keyword
    // you have to implement constant stroed property or get-only computed property
    var name: String { get } 
    // you have to implement variable stored property or get/set computed property 
    var currentPassenters: Int { get set }

    // protocols can have methods list
    func estimateTime(for distance: Int) -> Int
    func travel(distance: Int)
}

// conforming protocol
struct Car: Vehicle {
    func estimateTime(for distance: Int) -> Int {
        distance / 50
    }

    func travel(distance: Int) {
        print("I'm driving \(distance)km.")
    }
}

struct Bicycle: Vehicle { ... }

// You can pass any instance to 'vehicles' which conforms 'Vehicle' protocol.
func commute(distance: Int, using vehicle: Vehicle) {
    if vehicle.estimateTime(for: distance) > 100 {
        print("Too slow!")
    } else {
        vehicle.travel(distance: distance)
    }
}

let car = Car()
commute(distance: 100, using: car)

let bicycle = Bicycle()
commute(distance: 10, using: bicycle)
```

## Extensions

```swift
extension String {

    // adding method to type
    func trimmed() -> String {
        self.trimming Characters(in: .whitespaceAndNewlines)
    }

    // changing self value directly
    mutating func trim() {
        self = self.trimmed()
    }

    // adding computed property ty type
    // you can't add stored property into extension
    var lines: [String] {
        self.components(separatedBy: .newlines)
    }
}
```

## Protocol extensions

```swift
extension Collection {

    // this extended property can be accessed from any types conforming this protocol
    // e.g. arrays, dictionaries, sets
    var isNotEmpty: Bool {
        isEmpty == false
    }
}

// You can add default implementation for defined in protocol
protocol SomeProtocol {
    func execute()
}

extension SomeProtocol {
    func execute() { ... }
}
```

## Optionals

```swift
let opposites = [
    "Mario": "Wario",
    "Luigi": "Waluigi"
]

// It'll be nil, because the dictionary doesn't have value for the key "Peach".
let peachOpposite = opposites["Peach"]

// Unwrapping with 'if let' syntax
if let peachOpposite = opposites["Peach"] {
    print(peachOpposite)
}

// Unwrapping with `guard let` syntax in function
func printSquare(of number: Int?) {
    guard let number = number else {
        print(number)
        return
    }
}

// Unwrapping with nil-coalescing
let peachOpposite = opposites["Peach"] ?? "Unknown"

// Unwrapping with optional chaining
let names = ["Arya", "Bran", "Robb", "Sansa"]
// If the return value of 'randomElement()' is not nil, it'll be unwrapped and transfer to `uppercased()`
// If the return value of 'randomElement()' is nil, `uppercased()` will not call
let chosen = names.randomElement()?.uppercased()
```

## Optional try

```swift
func getUser(id: Int) throws -> String {
    throw UserError.networkFailed
}

// use try? if you don't need to handle each specific error case
// the only thing you'll care is whether the execution is succeed or not
if let user = try? getUser(id: 23) {
    print(user)
}
```