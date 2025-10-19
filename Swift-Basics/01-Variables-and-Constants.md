# Variables and Constants in Swift

## Introduction
In Swift, you can store values using variables and constants. The key difference is that variables can be changed after they're created, while constants cannot.

## Variables
Variables are declared using the `var` keyword:

```swift
var greeting = "Hello, World!"
var age = 25
var temperature = 72.5

// You can change the value later
greeting = "Hello, Swift!"
age = 26
```

## Constants
Constants are declared using the `let` keyword:

```swift
let pi = 3.14159
let userName = "John Doe"
let maxLoginAttempts = 3

// This will cause an error:
// pi = 3.14  // Cannot assign to value: 'pi' is a 'let' constant
```

## Type Annotations
Swift can infer types, but you can also explicitly specify them:

```swift
var explicitDouble: Double = 70
var welcomeMessage: String = "Welcome"
var isActive: Bool = true
```

## Best Practices
- Use `let` whenever possible - it makes your code safer and clearer
- Use `var` only when you know the value will change
- Swift encourages immutability for better code quality

## Example
```swift
// Constants for configuration
let appName = "MyApp"
let version = "1.0.0"

// Variables for changing data
var userScore = 0
var isLoggedIn = false

// Usage
userScore += 10  // Score can change
print("\(appName) v\(version) - Score: \(userScore)")
```

## Practice Exercise
Try creating:
1. A constant for your name
2. A variable for your current mood
3. A constant for the year you were born
4. A variable that tracks how many exercises you've completed
