# Functions in Swift

## Introduction
Functions are self-contained chunks of code that perform a specific task. They help organize code and make it reusable.

## Basic Functions

### Function Without Parameters
```swift
func sayHello() {
    print("Hello, World!")
}

sayHello()  // Call the function
```

### Function With Parameters
```swift
func greet(name: String) {
    print("Hello, \(name)!")
}

greet(name: "Alice")
```

### Function With Return Value
```swift
func add(a: Int, b: Int) -> Int {
    return a + b
}

let result = add(a: 5, b: 3)
print(result)  // 8
```

### Function With Multiple Parameters
```swift
func introduce(name: String, age: Int, city: String) {
    print("My name is \(name), I'm \(age) years old, and I live in \(city)")
}

introduce(name: "John", age: 30, city: "San Francisco")
```

## Parameter Labels

### External and Internal Parameter Names
```swift
func greet(person name: String, from hometown: String) {
    print("Hello \(name)! Glad you could visit from \(hometown).")
}

greet(person: "Alice", from: "New York")
```

### Omitting External Parameter Names
```swift
func add(_ a: Int, _ b: Int) -> Int {
    return a + b
}

let sum = add(5, 3)  // No parameter labels needed
```

## Default Parameter Values
```swift
func greet(name: String = "Guest", greeting: String = "Hello") {
    print("\(greeting), \(name)!")
}

greet()                           // "Hello, Guest!"
greet(name: "Alice")              // "Hello, Alice!"
greet(greeting: "Hi")             // "Hi, Guest!"
greet(name: "Bob", greeting: "Hey")  // "Hey, Bob!"
```

## Variadic Parameters
Accept multiple values of the same type:

```swift
func average(_ numbers: Double...) -> Double {
    var total = 0.0
    for number in numbers {
        total += number
    }
    return numbers.isEmpty ? 0 : total / Double(numbers.count)
}

print(average(1, 2, 3, 4, 5))     // 3.0
print(average(10.5, 20.5, 30.0))  // 20.33...
```

## In-Out Parameters
Modify parameters that persist after the function returns:

```swift
func swapValues(_ a: inout Int, _ b: inout Int) {
    let temp = a
    a = b
    b = temp
}

var x = 5
var y = 10
swapValues(&x, &y)
print("x: \(x), y: \(y)")  // x: 10, y: 5
```

## Multiple Return Values
Use tuples to return multiple values:

```swift
func minMax(array: [Int]) -> (min: Int, max: Int)? {
    guard !array.isEmpty else { return nil }
    
    var currentMin = array[0]
    var currentMax = array[0]
    
    for value in array[1..<array.count] {
        if value < currentMin {
            currentMin = value
        } else if value > currentMax {
            currentMax = value
        }
    }
    
    return (currentMin, currentMax)
}

if let bounds = minMax(array: [8, -6, 2, 109, 3, 71]) {
    print("Min: \(bounds.min), Max: \(bounds.max)")
}
```

## Function Types
Functions are first-class types in Swift:

```swift
func addNumbers(_ a: Int, _ b: Int) -> Int {
    return a + b
}

func multiplyNumbers(_ a: Int, _ b: Int) -> Int {
    return a * b
}

// Use function as a type
var mathFunction: (Int, Int) -> Int = addNumbers
print(mathFunction(2, 3))  // 5

mathFunction = multiplyNumbers
print(mathFunction(2, 3))  // 6
```

## Functions as Parameters
```swift
func performOperation(_ a: Int, _ b: Int, operation: (Int, Int) -> Int) -> Int {
    return operation(a, b)
}

let sum = performOperation(5, 3, operation: addNumbers)
let product = performOperation(5, 3, operation: multiplyNumbers)
print("Sum: \(sum), Product: \(product)")
```

## Nested Functions
```swift
func chooseStepFunction(backward: Bool) -> (Int) -> Int {
    func stepForward(input: Int) -> Int {
        return input + 1
    }
    
    func stepBackward(input: Int) -> Int {
        return input - 1
    }
    
    return backward ? stepBackward : stepForward
}

var currentValue = 3
let moveNearerToZero = chooseStepFunction(backward: currentValue > 0)
while currentValue != 0 {
    print("\(currentValue)... ")
    currentValue = moveNearerToZero(currentValue)
}
print("zero!")
```

## Practical Examples

### Example 1: Temperature Converter
```swift
func celsiusToFahrenheit(_ celsius: Double) -> Double {
    return celsius * 9/5 + 32
}

func fahrenheitToCelsius(_ fahrenheit: Double) -> Double {
    return (fahrenheit - 32) * 5/9
}

let tempC = 25.0
let tempF = celsiusToFahrenheit(tempC)
print("\(tempC)°C is \(tempF)°F")
```

### Example 2: String Validator
```swift
func isValidEmail(_ email: String) -> Bool {
    return email.contains("@") && email.contains(".")
}

func isValidPassword(_ password: String) -> Bool {
    return password.count >= 8
}

let email = "user@example.com"
let password = "secure123"

if isValidEmail(email) && isValidPassword(password) {
    print("Valid credentials")
}
```

### Example 3: Calculator
```swift
func calculate(_ a: Double, _ b: Double, operation: String) -> Double? {
    switch operation {
    case "+":
        return a + b
    case "-":
        return a - b
    case "*":
        return a * b
    case "/":
        return b != 0 ? a / b : nil
    default:
        return nil
    }
}

if let result = calculate(10, 5, operation: "/") {
    print("Result: \(result)")
}
```

## Practice Exercises
1. Write a function that checks if a number is even
2. Create a function that returns the factorial of a number
3. Write a function that takes an array and returns the sum of all elements
4. Create a function that reverses a string
