# Day3

## Array: Storing ordered data in arrays

- It's common to want to have lots of data in a single place: The groupping.
- Array can holds data as many as you want in the order you add it.

```swift
let beatles = ["John", "Paul", "George", "Ringo"]  // String array
let numbers = [4, 8, 15, 16, 23, 42]  // Int array
let temperatures = [25.3, 28.2, 26.4]  // Double array
```

- To read value from an array, we ask for values by the position they appear in the array.
- The position of an item in an array is called `index`.
- Make sure an item exists at the index, otherwise your code will crash.

```swift
print(beatles[0])  // "John"
print(numbers[1])  // 8
print(temperatures[2])  // 26.4
```

- When the array is variable, you can modify it.
- You can add new items using `append()`.

```swift
beatles.append("Adrian")  // o
temperatures.append("Chris")  // x. You can not add String value to Double array
```

- Making array

```swift
let emptyArray1 = Array<String>()
let emptyArray2 = [String]()
let stringArray = ["Folklore"]
```

- Use `.count` to read how many items are in an array.
- Use `remove(at:)` to remove one item at a specific index.
- Use `removeAll()` to remove all items in an array.
- Use `contains()` to check whether an array contains a specific item.
- Use `sorted()` to sort an array.
- Use `reversed()` to reverse order in an array.

```swift
let beatles = ["John", "Paul", "George", "Ringo"]

beatles.count  // 4
beatles.remove(at: 1)  // ["John", "George", "Ringo"]
beatles.removeAll()  // []
beatles.contains("Paul")  // true
beatles.sorted()  // ["George", "John", "Paul", "Ringo"]
beatles.reversed()  // ["Ringo", "George", "Paul", "John"]
```

### Why does Swift have arrays?

- To store many values
- The index starts from zero

## Dictionary: Storing value with key

- Accessing data by its index in the array can be annoyinig or even dangerous.
- Dictionaries let us decide **where items should be stored.**
- Dictionaries store data for key.

```swift
let employee = [
    "name": "Taylor Swift",
    "job": "Singer",
    "location": "Nashville"
]
```

- To read data in the dictionary, you use the same keys when creating it.
- The output is optional by default.
- When reading from a dictionary, you can provide a default value to use if the key doesn't exist.

```swift
employee["name"]  // Optional("Taylor Swift")
employee["age"]  // nil
employee["age", default: "0"]  // 0
employee["name", default: "Unknown"]  // "Taylor Swift"
```

- You can create an empty dictionary using whatever explict types you want to store.

```swift
var heights = [String: Int]()
heights["Yao Ming"] = 229
heights["Shaquille O'Neal"] = 216
```

### Why does Swift have dictionaries as well as arrays?

- Dictionaries and arrays are both ways of storing lots of data in one variable.
  - Dictionaries use 'key' that identifies the item.
  - Arrays just add each item **sequentially**.
- Dictionaries optimize the way they store items for fast retrival.
  - Dictionary : `O(1)` time complexity
  - Array : `O(n)` time complexity

### Why does Swift have default values for dictionaries?

- Whenever you read a value from a dictionary, you might get a value or 'nil'.
- There might be no value for that key in a dictionary.

## Set: Storing value for fast data lookup

- Sets are simillor to arrays
- Sets can't add duplicate items. It removes any duplicate values automatically.
- Sets don't store items in a particular order

```swift
let people = Set(["Denzel Washington", "Tom Cruise", "Nicolas Cage", " Samuel L Jackson"])
```

- Set uses `insert()` to add items.
- The array uses `append()` to add items, which means that an item will be added to the end of the array.
- Because sets doesn't store data in an order, the word 'append' doesn't make sense.

### Why are sets different from arrays in Swift?

- Both sets and arrays are collections of data
- Sets are unordered and cannot contain duplicates.
- Arrays retain their order and can contain duplicates.

## How to create and use enums

- Enum(Enumeration) is a set of named values.
- Enums are more efficient and safer.
- When you want to select a weekday, using strings are dangeruous and inefficient.

```swift
var selected = "Monday"
selected = "Tuesday"
selected = "Wendsday"
```

- When you use enums, it's safe and efficient.
- You never make a mistake using them.

```swift
enum Weekday {
    case monday
    case tuesday
    case wendsday
}
var selected = Weedkay.monday
selected = .tuesday
selected = .wendsday
```