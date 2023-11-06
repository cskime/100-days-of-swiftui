# Day6

## For loop

- `for {variable} in {group: collection or range}` loop
- loop body : The code inside the braces
- loop iteration : One cycle through the loop budy
- loop variable : The group's item which change to a new value in the next loop iteration

```swift
let platforms = ["iOS", "macOS", "tvOS", "watchOS"]
for os in platforms {
    print("Swift works great on \(os).")
}
```

- Nested loop : You can put loops inside loops

```swift
// 1 ~ 12 구구단 출력
for i in 1...12 {
    print("The \(i) times table:")
    for j in 1...12 {
        print("  \(j) x \(i) is \(j * i)")
    }
    print()
}
```

- You can replace the loop variable with underscore(`_`) if you don't use the loop variable.

```swift
var lyric = "Haters gonna"

// Variable을 사용하지 않고 단순 loop 반복
for _ in 1...5 {
    lyric += " hate"
}
print(lyric)  // Haters gonna hate hate hate hate hate
```

### Why does Swift use underscore with loops

- You don't actually need the value, you can use underscore instead of loop variable.
- If you use an underscore, we can look at the code and immediately see the loop variable isn't being used.

### Why does Swift have two range operators?

- `..<` : The half-open range which means 'up to but excluding'
- `...` : THe closed range which means 'up to and including'

```swift
let names = ["Piper", "Alex", "Suzanne", "Gloria"]
print(names[1...3])  // ["Alex", "Suzanne", "Gloria"]
print(names[1..<3])  // ["Alex", "Suzanne"]
print(names[2...])   // ["Suzanne", "Gloria"]
```

## While loop

- `while` loop will continually execute the lop body until the condition is `false`.
- It's useful when you just don't know how many times the loop will go around.

```swift
var countdown = 10

while countdown > 0 {
    print("\(countdown)...")
    countdown -= 1
}
```

### When should you use a while loop?

- `for` loops are generally used with finite sequences.
- `while` loops can loop until any arbitrary condition becomes false.
  - the user asks to stop
  - a server tell us to stop
  - we've found the answer we're looking for

## break and continue

- `continue` skips the current loop iteration

```swift
let filenames = ["me.jpg", "work.txt", "sophie.jpg", "logo.psd"]

for filename in filenames {
    if !filename.hasSuffix(".jpg") {
        continue  // It skips iteration for "work.txt" and "logo.psd"
    }
    print("Found picture: \(filename)")  // "me.jpg", "sophie.jpg"
}
```

- `break` skips all remaining iterations

```swift
var multiples = [Int]()

for i in 1...100_100 {
    if i.isMultiple(of: 4) && i.isMultiple(of: 14) {
        multiples.append(i)

        if multiples.count == 10 {
            break  // Exit loop when multiples array has 10 items.
        }
    }
}
```

### Why would you want to exit a loop?

- `break` keyword lets us exit a loop immediately
- Sometimes you want to end your loop prematurely

### Why does Swift have labeled statements?

- It allows us to name certain parts of our code

```swift
let options = ["up", "down", "left", "right"]

outerLoop: for option1 in options {
    for option2 in options {
        for option3 in options {
            print("In loop")
            let attempt = [option1, option2, option3]

            if attempt == ["up", "up", "right"] {
                print("The combination is \(attempt)")
                break outerLoop  // All loops stops although nested loops still can run
            }
        }
    }
}
```

### When to use break and continue

- `continue`
    - It means, "I'm done with the current run of this loop"
    - Swift will skip the rest of the loop 'body', and go to the next item in the loop.
- `break`
    - It means, "I'm done with this loop altogether, so get out completely"
    - Swift will skip the remainder of the body loop, but also skip any other loop items.
