# Control Flow in Swift

## Introduction
Control flow statements let you control the order in which your code executes based on conditions and loops.

## If Statements

### Basic If
```swift
let temperature = 72

if temperature > 80 {
    print("It's hot outside!")
}
```

### If-Else
```swift
let score = 85

if score >= 90 {
    print("Grade: A")
} else if score >= 80 {
    print("Grade: B")
} else if score >= 70 {
    print("Grade: C")
} else {
    print("Grade: F")
}
```

### Multiple Conditions
```swift
let age = 25
let hasLicense = true

if age >= 16 && hasLicense {
    print("You can drive!")
}

if age < 18 || age > 65 {
    print("Special discount available")
}
```

## Switch Statements

### Basic Switch
```swift
let day = "Monday"

switch day {
case "Monday":
    print("Start of the work week")
case "Friday":
    print("Almost weekend!")
case "Saturday", "Sunday":
    print("Weekend!")
default:
    print("Midweek day")
}
```

### Switch with Ranges
```swift
let grade = 85

switch grade {
case 90...100:
    print("A")
case 80..<90:
    print("B")
case 70..<80:
    print("C")
case 60..<70:
    print("D")
default:
    print("F")
}
```

### Switch with Tuples
```swift
let point = (x: 1, y: 1)

switch point {
case (0, 0):
    print("Origin")
case (_, 0):
    print("On the x-axis")
case (0, _):
    print("On the y-axis")
case (-2...2, -2...2):
    print("Inside the box")
default:
    print("Outside the box")
}
```

## For Loops

### For-In Loop
```swift
// Loop through a range
for number in 1...5 {
    print("Number: \(number)")
}

// Loop through an array
let fruits = ["Apple", "Banana", "Orange"]
for fruit in fruits {
    print("I like \(fruit)")
}

// Loop through a dictionary
let scores = ["Alice": 95, "Bob": 87, "Charlie": 92]
for (name, score) in scores {
    print("\(name) scored \(score)")
}
```

### For Loop with Index
```swift
let names = ["Anna", "Alex", "Brian"]
for (index, name) in names.enumerated() {
    print("\(index + 1). \(name)")
}
```

### For Loop with Stride
```swift
// Count by 2s
for number in stride(from: 0, to: 10, by: 2) {
    print(number)  // 0, 2, 4, 6, 8
}

// Countdown
for number in stride(from: 10, through: 0, by: -2) {
    print(number)  // 10, 8, 6, 4, 2, 0
}
```

### Using Underscore
```swift
// When you don't need the loop variable
for _ in 1...3 {
    print("Hello!")
}
```

## While Loops

### While Loop
```swift
var counter = 1

while counter <= 5 {
    print("Count: \(counter)")
    counter += 1
}
```

### Repeat-While Loop
Similar to do-while in other languages:

```swift
var number = 1

repeat {
    print("Number: \(number)")
    number += 1
} while number <= 5
```

## Control Transfer Statements

### Continue
Skip to next iteration:

```swift
for number in 1...10 {
    if number % 2 == 0 {
        continue  // Skip even numbers
    }
    print(number)  // Only prints odd numbers
}
```

### Break
Exit the loop early:

```swift
for number in 1...100 {
    if number > 5 {
        break  // Stop after 5
    }
    print(number)
}
```

### Guard
Early exit from a function or scope:

```swift
func greet(person: [String: String]) {
    guard let name = person["name"] else {
        print("No name provided")
        return
    }
    
    print("Hello, \(name)!")
    
    guard let age = person["age"] else {
        return
    }
    
    print("You are \(age) years old")
}

greet(person: ["name": "John", "age": "30"])
```

## Practical Examples

### Example 1: FizzBuzz
```swift
for number in 1...15 {
    if number % 15 == 0 {
        print("FizzBuzz")
    } else if number % 3 == 0 {
        print("Fizz")
    } else if number % 5 == 0 {
        print("Buzz")
    } else {
        print(number)
    }
}
```

### Example 2: Finding Prime Numbers
```swift
func isPrime(_ number: Int) -> Bool {
    guard number > 1 else { return false }
    
    for divisor in 2..<number {
        if number % divisor == 0 {
            return false
        }
    }
    return true
}

for number in 1...20 {
    if isPrime(number) {
        print("\(number) is prime")
    }
}
```

## Practice Exercises
1. Write a program that prints the multiplication table for 7
2. Create a switch statement that converts numeric grades to letter grades
3. Use a while loop to find the first power of 2 greater than 1000
4. Write a for loop that sums all even numbers from 1 to 100
