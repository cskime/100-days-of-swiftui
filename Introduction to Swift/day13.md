# Day13

## How to create and use protocols

- Protocol is a new type.
- Protocols let us define what kinds of functionality we expect a data type to support
- They don't implement those properties and methods. They just say that the properties and methods must exist.

```swift
protocol Vehicle {
    func estimateTime(for distance: Int) -> Int
    func travel(distance: Int)
}
```

- When you create new types that conform to the protocol you can add all sorts of other properties and methods as needed.

```swift
struct Car: Vehicle {
    // Actual implementations of the methods we defined in the protocol
    func estimatedTime(for distance: Int) -> Int {
        distance / 50
    }

    // Actual implementations of the methods we defined in the protocol
    func travel(distance: Int) {
        print("I'm driving \(distance)km.")
    }

    // It doesn't come from the protocol. 
    func openSunroof() {
        print("It's a nice day!")
    }
}
```

- Swift knows that any type conforming to `Vehicle` must implement `estimatedTime(for:)` and `travel(distance:)` methods.
- So, it actually lets us use `Vehicle` rather than `Car`.

```swift
func commute(distance: Int, using vehicle: Vehicle) {  // instead of 'Car'
    if vehicle.estimatedTime(for: distance) > 100 {
        print("That's too slow!")
    } else {
        vehicle.travel(distance: distance)
    }
}

let car = Car()
commute(distance: 100, using: car)
```

- If you have another struct `Bicycle` comforms to `Vehicle`, you can pass a `Car` or a `Bicycle` into `Vehicle` parameter.
- When the `estimatedTime()` or `travel()` method is called, Swift will automatically use the appropriate one.

```swift
struct Bicycle: Vehicle {
    func estimateTime(for distance: Int) -> Int {
        distance / 10
    }

    func travel(distance: Int) {
        print("I'm cycling \(distance)km.")
    }
}

let bike = Bicycle()
commute(distance: 50, using: bike)
```

- When you add a property, use `{ get }` if you want to constant or readonly variable.
- Use `{ get set }` if you want to variable or computed property which has both getter and setter.

```swift
protocol Vehicle {
    var name: String { get }
    var currentPassenters: Int { get set }
    ...
}

struct Car: Vehicle {
    let name = "Car"
    var currentPassenters = 1
}
```

### Why does Swift need protocols?

- Protocols let us define how structs, classes, and enums ought to work; what methods and properties they should have.
- Protocols allow us to treat our data in more general terms.
- Although each struct has a different property that wasn't declared in the protocl, it's okay because protocols determine the **minimum required functionality**.

```swift
protocol Purchaseable {
    var name: String { get set }
}

struct Book: Purchaseable {
    var name: String
    var author: String
}

struct Movie: Purchaseable {
    var name: String
    var actors: [String]
}

struct Car: Purchaseable {
    var name: String
    var manufacturer: String
}

// You can pass any types which conform `Purchaseable` protocol
func buy(_ item: Purchaseable) {
    print("I'm buying \(item.name)")
}
```

- So. protocols let us create blueprints of how our types share functionality.
- Then, use those blueprints in our functions to let them work on a wider variety of data.

## How to use opaque return types

- Opaque return types let us remove complexity in our code.
- Both `Int` and `Bool` types conform to `Equatable`, but they're not interchangeable.
- Returning a protocol from a function is useful because it lets us hide information. We don't know exactly what it is.
- It means we can change our code later without breaking codes.

```swift
func getRandomNumber() -> some Equatable {
    Int.random(in: 1...6)
}

func getRandomBool() -> some Equatable {
    Bool.random()
}
```

## How to create and use extensions

- Extensions let us add functionality to any type, whether we create it or not.

```swift
extension String {
    func trimmed() -> String {
        self.trimmingCharacters(in: .whitespacesAndNewlines)
    }
}

let trimmed = quote.trimmed()

// instead of
// quote.trimmingCharecters(in: .whitespaceAndNewlines)
```

- You can write function like this
- But, Extensions are much easier to find.
- Global functions are hard to organize and keep track
- Extension method are a full part of the original type, they get full access to the type's internal data.

```swift
func trim(_ string: String) -> String {
    string.trimmingCharacters(in: .whitespaceAndNewlines)
}

let trimmed = trim(quote)
```

- You can use extensions to add computed poperties, not stored properties.
- Because adding new stored properties would affect the actual size of the data types.

```swift
extension String {
    var lines: [String] {
        components(separatedBy: .newlines)
    }
}

let lyrics = """
But I keep cruising
Can't stop, won't stop moving
It's like I got this music in my mind
Saying it's gonna be alright
"""
print(lyrics.lines.count)
```

- We can add custom initializer inside an extension of struct.
- If then, you can use memberwise initializer too.

```swift
extension Bool {
    init(title: String, pageCount: Int) {
        self.title = title
        self.pageCount = pageCount
        self.readingHours = pageCount / 50
    }
}
```

### When should you use extensions in Swift?

- Extensions let us add functionality to types we don't own.
- Extensions are also useful for organizing our own code.
- Conformance grouping : adding a protocol conformance to a type as an extension, adding all the required methods inside that extension.
- Purpose grouping : creating extensions to do specific tasks, which makes it easier to work with large types.
- The type is exactly the same size it was before, it's just neatly split up.

## How to create and use protocol extensions

- We can extend a whole protocol to add method implementations, meaning that any types conforming to that protocol get those methods.
- When you add `isNotEmpty` property into `Array`, you can use `isNotEmpty` only for arrays, not for dictionaries or sets.
- If you add `isNotEmpty` into `Collection` protocol, you can use the property for all types that conform `Collection`.

```swift
extension Array {
    var isNotEmpty: Bool {
        isEmpty == false
    }
}

extension Collection {
    var isNotEmpty: Bool {
        isEmpty == false
    }
}
```

- By extending the protocol we're adding functionality that would otherwise need to be done inside individual structs.
- It leads to a technique called POP.
- We can list some required methods in a protocol, then add **default implementations** of those inside a protocol extension.

```swift
protocol Person {
    var name: String { get }
    func sayHello()
}

extension Person {
    func sayHello() {
        print("Hi, I'm \(name)")
    }
}

struct Employee: Person {
    var name: String
    // you don't need to implement sayHello. it'll use default implementation.
}
```

### When are protocol extensions useful in Swift?

- We use protocol extensions to add functionality directly to protocols
- It means we don't need to copy that functionality across many structs and classes