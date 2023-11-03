# Day4

## Type Annotation

- Swift is able to figure out what type of data a constant or variable holds based on **what we assign to it**.
- Sometimes, we don't want to assign a value immediately, or we want to override Swift's default type.
- Type annotation flet us be explicit about waht data type we want.
- The type annotation isn't required

```swift
let surname = "Lasso"  // The inferred type is String
let score = 0  // The inferred type is Int

let surname: String = "Lasso"  // The type is String
let score: Double = 0  // The type is overrided to Double (not Int)
```

- I think, it looks better you only use the type annotation when you're not sure what type is,
- or, there is specific type you want.

```swift
let score: Double = 0
let stringArray = [String]()  // You can figure out what type is without type annotation.
```

### Why does Swift have type annotations?

- When should i use type annotations in Swift?
- First, Swift can't figure out what type should be used.
- Second, You want Swift to use a different type from its default.
- Thrid, You don't want to assign a value just yet.


