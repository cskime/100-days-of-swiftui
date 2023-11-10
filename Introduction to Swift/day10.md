# Day10

## How to create your own structs

- Structs let us create our own custom data types
- In the example code below, we create custom data type `Album` that has three constants and one function.
- Custom type's name starts with a capital-it should be `Album`, not `album`-, and use camel case.

```swift
struct Album {
    let title: String
    let artist: String
    let year: Int

    func printSummary() {
        print("\(title) (\(year)) by \(artist)")
    }
}

let red = Album(title: "Red", artist: "Taylor Swift", year: 2012)
let wings = Album(title: "Wings", artist: "BTS", year: 2016)
```

- When you change values at functions in the struct, you must mark them with `mutating` keyword.

```swift
struct Employee {
    let name: String
    var vacationRemaining: Int

    // Swift generates error if you change variable in a non-mutating function
    mutating func takeVacation(days: Int) {
        if vacationRemaining > days {
            vacationRemaining -= days
            print("Days remaining: \(vacationRemaining)")
        } else {
            print("Opps! There aren't enough days remaining.")
        }
    }
}
```

- If you define struct instance with `let` instead of `var`, Swift refuse to build again because we're trying to call a mutating function on a constant struct.

```swift
var archer = Employee(name: "Sterling archer", vacationRemaining: 14)
archer.takeVacation(days: 5)  // succeed to build

let archer2 = Employee(name: "Sterling archer", vacationRemaining: 14)
archer.takeVacation(days: 5)  // refused to build
```

### What's the difference between a struct and a tuple?

- A tuple is effectively just a struct without a name, like an anonymous struct.
- A tuple can be hard to read if it has several datas and is used multiple points.
- A tuple can't have functions.

```swift
// If you use a tuple, it can be more difficult to read like this:
let user: (name: String, age: Int, city: String)
func authenticate(_ user: (name: String, age: Int, city: String)) { ... }
func showProfile(_ user: (name: String, age: Int, city: String)) { ... }
func signOut(_ user: (name: String, age: Int, city: String)) { ... }

// If you use a struct, it's more easier.
struct User {
    let name: String
    let age: Int
    let city: String
}
func authenticate(_ user: User) { ... }
func showProfile(_ user: User) { ... }
func signOut(_ user: User) { ... }
```

### What's the difference between a function and a method?

- Methods belong to a type while functions do not.

### Why do we need to mark some methods as mutating?

- It's possible to modify the properties of a struct, but only if that struct is created as a variable.
- Inside a struct there's no way of telling whether you'll be working with a variable or constant struct.
- So, struct's method tries to change any properties, you must mark it as `mutating`
- Marking `mutating` will stop the method from being called on constant struct
- A method that is not marked as mutating can't call a mutating function.

## How to compute property values dynamically

- A computed property calculates the value of the property dynamically **every time it's accessed**.
- It's accessed like stored properties, but work like functions.
- You can provide both a getter and a setter with `get`, `set` keyword.
- When you assign value to computed property which has a setter, a `set` block is executed with `newValue` you can access the assigned value. 
- If you provide a getter only, you can skip the `get` keyword.

```swift
var vacationRemaining: Int {
    get { vacationAllocated - vacationTaken }  // getter
    set { vacationAllocated = vacationTaken + newValue }  // setter
}
```

### When should you use a computed property or a stored property?

- A stored property : a value stashed away in some memory to be used later.
    - When you regularly read the property when its value hasn't changed.
- A computed property : a value is recomputed every time it's called.
    - When you read the property rarely and perhaps not at all.
    - When the property relies on the other property.

## How to take action when a property changes

- Property observer runs when properties change.
- `didSet`
    - Run when the property just changed
    - You can use `oldValue` constant inside `didSet`
- `willSet`
    - Run before the property changed
    - You cahn use `newValue` constant inside `willSet`

```swift
struct App {
    var contacts = [String]() {
        willSet {
            print("Current value is: \(contacts)")
            print("New value will be: \(newValue)")
        }

        didSet {
            print("There are new \(contacts.count) contacts.")
            print("Old value was \(oldValue)")
        }
    }
}
```

### When should you use property observers?

- It's guaranteed that your functionality will be executed whenever the property changes.
- Without this, you can forget you have to call a function in every changes of property value.“

### When should you use willSet rather than didSet?

- Usually we want to take action **after** the value is changed, so most the time you will use `didSet`.
- When you need to know the state of your program before a change is made, you will use `willSet`.

## How to create custom initializers

- Initializers are specialized methods that are designed to prepare a new struct instance to be used.
- All properties must have a value by the time the initializer ends.
- Swift automatically generates a **memberwise initializer**.
- `self.name` clarifies; the `name` property that belongs to my current instance.

```swift
struct Player {
    let name: String
    let number: Int

    // memberwise initializer : Generated by Swift
    init(name: String, number: Int) {
        self.name = name
        self.number = number
    }
}
```

### How do Swift's memberwise initializers work?

- All Swift structs get a synthesized memberwise initializer by default.
- If any of your properties have default values, then they'll be incorporated into the initializer as default parameter values.

```swift
struct Employee {
    var name: String
    var yearsActive = 0
}

let roslin = Employee(name: "Laura Roslin")  // memberwise init has default value for `yearsActive` property
let adama = Employee(name: "William Adama", yearsActive: 45)
```

- If you define a custom initializer, Swift removes the memberwise initializer.
- If you define a custom initializer in extension, you still can use default memberwise initializer.

```swift
struct Employee {
    var name: String
    var yearsActive = 0

    init() {
        self.name = "Anonymous"
        print("Creating an anonymous employee...")
    }
}

let anonymous = Employee()  // Use custom initializer
let roslin = Employee(name: "Laura Roslin")  // You can't use memberwise initializer any more.
```

### When would you use self in a method?

- `self` : the current instance of a struct
- If you're likely to want parameter names that match the property names of your type.

```swift
struct Student {
    var name: String
    var bestFriend: String

    init(name: String, bestFriend: String) {
        // Avoiding the conflict of the same property name
        self.name = name
        self.bestFriend = bestFriend
    }
}
```