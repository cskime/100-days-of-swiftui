# Day12

## How to create your own classes

- You can make one class build upon functionality in another class, gaining all its properties and methods as a starting point.
- Classes don't have a memberwise initializer
- When you copy an instance of a class, both copies share the same data
- When the final copy of a class instance is destroyed, a deinitializer is called
- Even if you make a class constant, yoy can change its variable properties

```swift
class Game {
    var score = 0 {
        didSet { print("Score is now \(score)") }
    }
}

let newGame = Game()
newGame.score += 10
```

### Why does Swift have both classes and structs?

- Classes and structs give Swift developers the ability to create custom, complex types with properties and methods
- They have five important differences:
    - Classes do not come with synthesized memberwise initializers.
    - One class can be inhert from another class
    - Copies of structs are always unique, whereas copies of classes actually point to the same shared data.
    - Classes have deinitializers which are methods that are called when an instance of the class is destroyed
    - Constant instance of classes can change variables they have

### Why don't Swift classes have a memberwise initializer?

- Classes have inheritance, which would make memberwise initializers difficult to work with.
- If you add some properties to super class later, all the places which your class instances are used are affected.
- Instead of having a memberwise initializer, classes must have their own initializer.
- In this way, it's guaranteed all of properties have value when a class instance is just created.

## How to make one class inherit from another

- Swift lets us create classes by basing them on existing classes: inheritance.
- You can make small additions or changes to customize the new class behaves basing its super class.
- You can change functionality provided from the parent class using `override` keyword.

```swift
class Employee {
    let hours: Int
    init(hours: Int) { self.hours = hours }

    // Shared to child classes
    func printSummary() { print("I work \(hours) hours a day.") }
}

class Developer: Employee {
    // add custom method using super class'es property 'hours'
    func work() { print("I'm writing code for \(hours) hours.") }

    // override functionality
    override func printSummary() { 
        print("I'm a developer who will sometimes work \(hours) hours a day")
    }
}

class Manager: Employee {
    // add custom method using super class'es property 'hours'
    func work() { print("I'm going to meetings for \(hours) hours.") }
}

let robert = Developer(hours: 8)
robert.work()  // call custom method
robert.printSummary()  // shared from parent, but overrided

let joseph = Manager(hours: 10)
joseph.work()  // call custom method
joseph.printSummary()  // shared from parent
```

- If you know for sure that your class should not support inheritance, you can mark it as `final`.

```swift
class Employee {}
final class Developer: Employee {}  // You can inherit from Employee
class iOSDeveloper: Developer {}  // x. You can't inherit from final class
```

### When would you want to override a method?

- Override can replace the parent's implementation with onf of their own.
- You can keep all the behavior you want, and just change one or two little parts in a custom subclass

### Which classes should be declared as final?

- When you want to prevent a class is used for inheritance.

### How to add initializers for classes

- If a child class has any custom initializers, it must always call the parent's initializer after it has finished setting up its own properties.
- It guarantees that all properties are initialized even parent's one.

```swift
class Vehicle {
    let isElectric: Bool

    init(isElectric: Bool) {
        self.isElectric = isElectric
    }
}

class Car: Vehicle {
    let isConvertible: Bool

    init(isElectric: Bool, isConvertible: Bool) {
        self.isConvertible = isConvertible
        super.init(isElectric: isElectric)  // you must call parent's initializer after child properties are finisied initializing
    }
}
```

## How to copy classes

- All copies of a class instance share the same data
- It means that any changes you make to one copy will automatically change the other copies.

```swift
class User {
    var username = "Anonymous"
}

var user1 = User()
var user2 = user1  // shallow copy
user2.username = "Taylor"

print(user1.username)  // Taylor (not "Anonymous")
print(user2.username)  // Taylor
```

- Class does basically shallow copy.
- If you want to create a unique copy of a class instance, you need to create a new instance.
- It means that you should implement deep copy your own.

```swift
class User {
    var username = "Anonymous"

    func copy() -> User {
        let user = User()
        user.username = username
        return user
    }
}

var user1 = User()
var user2 = user.copy()  // deep copy. 'user2' is totally different instance from 'user1'.
user2.username = "Taylor"

print(user1.username)  // Anonymous
print(user2.username)  // Taylor
```

### Why do copies of a class share their data?

- Class
    - Copies of the same class share their data.
    - Classes are "reference type", which means they refer to a value somewhere else.
    - Reference type instance does the shallow copy.
- Struct
    - Copies of the same struct have their own unique data.
    - Structs are "value type", which means they hold simple values.
    - Value type instance does the deep copy.

## How to create a deinitializer for a class

- Deinitializer is a function just like initializers.
- Deinitializer can naver take parameters or return data, even they don't have parentheses.
- Deinitializer will automatically be called when the final copy of a class instance is destroyed.
- Structs don't have deinitializers.
- When a value exits scope,
    - the data of struct is being destroyed
    - the data of class is just going away
    - if the final copy of class goes away, the data of class is destroyed.

```swift
class User {
    let id: Int

    init(id: Int) {
        self.id = id
        print("User \(id): I'm alive!")
    }

    deinit {
        print("User \(id): I'm dead!")
    }
}

let user = User(id: i)
print("User \(user.id): I'm in control!")

// prints
// User 1: I'm alive!
// User 1: I'm in control!
// User 1: I'm dead!
```

### Why do classes have deinitializers and structs don't?

- Deinitializer is to tell us when a class instance was destroyed.
- It's clear that when the struct instance is destroyed.
- Classes have complex copying behavior; class is destroyed when all copied instances are destroyed.
- ARC tracks how many copies of each class instance exists. When class reference count becomes 0, class is destroyed.

## How to work with variables inside classes

- The data inside the class has changed, but the class instance itself has not changed.
- Constant instance, constant property : always points to the same instance, which always has the same data.
- Constant instance, variable property : always points to the same instance, but their data can be changed.
- Variable instance, constant property : can point to different instance, but their data can't be changed.
- Variable instance, variable property : can point ot different instance, and their data can be changed

### Why can variable properties in constant classes be changed?

- When we change one of struct's properties, we are changing the entrie struct.
- You can change any part of classes without having to destroy and recreate the value.