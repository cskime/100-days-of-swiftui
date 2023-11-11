# Day11

## How to limit access to internal data using access control

- The access control lets you hide some data from external access.
- We can prevent specific properties or functions should be accessible only inside the struct.
- `private` : It means "don't let anything outside the struct use this."
- `fileprivate` : It means "don't let anything outside the **current file** use this."
- `public` : It means "let anyone, anywhere use this."
- `private(set)` : It means "let anyone read this property, but only let my methods write it."

```swift
struct BankAccount {
    private var funds = 0

    mutating func deposit(amount: Int) {
        funds += amount
    }

    mutating func withdraw(amount: Int) -> Bool {
        if funds >= amount {
            funds -= amount
            return true
        } else {
            return false
        }
    }
}

let account = BankAccount()
account.funds -= 100  // x
```

### What's the point of access control?

- Access control lets us determine how a value should be used.
- If something needs to accessed very carefully then you must follow the rules.
- It also lets us control how other people see our code.
- If a struct has 30 variables and 25 of those are marked as `private`, it's clear which properties are accessible.

## Static properties and methods

- You can create properties and methods to the struct **itself**, rather than to one particular instance.
- Use `static` keyword.
- You can modify static property without `mutating` keyword because that doesn't exist uniquely on instance.

```swift
struct School {
    static var studentCount = 0
    static func add(student: String) {
        print("\(student) joined")
        studentCount += 1
    }
}

School.add(student: "TaylorSwift")
```

- Static properties and methods can't use non-static properties and methods.
- If you want to use static properties and methods in non-static code, you have to use `Type` or `Self`.
- `self` : current **value**
- `Self` : current **type**

### What's the point of static properties and methods in Swift?

- To store common functionality you use across an entire app.