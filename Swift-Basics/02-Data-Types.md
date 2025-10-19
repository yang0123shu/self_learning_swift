# Data Types in Swift

## Introduction
Swift is a type-safe language, which means it helps you be clear about the types of values your code can work with.

## Basic Data Types

### Integers
Used for whole numbers:

```swift
let smallNumber: Int8 = 127       // -128 to 127
let mediumNumber: Int16 = 32767   // -32,768 to 32,767
let largeNumber: Int64 = 9223372036854775807

// Most common - adapts to platform (32-bit or 64-bit)
let count: Int = 42
let unsignedCount: UInt = 42      // Only positive numbers
```

### Floating-Point Numbers
Used for decimal numbers:

```swift
let pi: Double = 3.14159          // 64-bit, 15 decimal digits
let temperature: Float = 98.6     // 32-bit, 6 decimal digits

// Double is preferred in most cases
let preciseValue: Double = 3.141592653589793
```

### Booleans
True or false values:

```swift
let isSwiftAwesome: Bool = true
let isCodingHard: Bool = false

if isSwiftAwesome {
    print("Swift is awesome!")
}
```

### Strings
Text data:

```swift
let name = "Swift"
let greeting = "Hello, \(name)!"  // String interpolation
let multiline = """
    This is a
    multiline
    string
    """

// String operations
let firstName = "John"
let lastName = "Doe"
let fullName = firstName + " " + lastName
print("Length: \(fullName.count)")
```

### Characters
Single character:

```swift
let letterA: Character = "A"
let heart: Character = "♥"
let emoji: Character = "😀"
```

## Collection Types

### Arrays
Ordered collections of values:

```swift
var fruits = ["Apple", "Banana", "Orange"]
fruits.append("Mango")
print(fruits[0])  // "Apple"
print("Count: \(fruits.count)")

// Type annotation
var numbers: [Int] = [1, 2, 3, 4, 5]
```

### Dictionaries
Key-value pairs:

```swift
var person = [
    "name": "John",
    "age": "30",
    "city": "San Francisco"
]

print(person["name"] ?? "Unknown")

// Type annotation
var scores: [String: Int] = ["Alice": 95, "Bob": 87]
```

### Sets
Unordered collections of unique values:

```swift
var uniqueNumbers: Set<Int> = [1, 2, 3, 4, 5]
uniqueNumbers.insert(6)
uniqueNumbers.insert(3)  // Won't add duplicate
print(uniqueNumbers.count)  // 6
```

## Tuples
Group multiple values together:

```swift
let httpStatus = (statusCode: 200, message: "OK")
print("Status: \(httpStatus.statusCode)")
print("Message: \(httpStatus.message)")

// Decomposing
let (code, msg) = httpStatus
print("Code: \(code), Message: \(msg)")
```

## Optionals
Represent values that might be absent:

```swift
var optionalName: String? = "John"
var optionalAge: Int? = nil

// Unwrapping
if let name = optionalName {
    print("Name is \(name)")
} else {
    print("No name")
}

// Nil coalescing
let displayName = optionalName ?? "Guest"
```

## Type Conversion
```swift
let integerValue = 42
let doubleValue = Double(integerValue)
let stringValue = String(integerValue)

let numberString = "123"
if let number = Int(numberString) {
    print("Converted: \(number)")
}
```

## Practice Exercise
1. Create an array of your favorite movies
2. Create a dictionary with 3 cities and their populations
3. Use an optional to represent a middle name (which might not exist)
4. Convert a string to an integer safely
