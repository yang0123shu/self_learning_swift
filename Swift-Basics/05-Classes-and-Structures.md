# Classes and Structures in Swift

## Introduction
Classes and structures are fundamental building blocks for organizing code in Swift. They're similar in many ways but have important differences.

## Structures

### Basic Structure
```swift
struct Person {
    var name: String
    var age: Int
    
    func introduce() {
        print("Hi, I'm \(name) and I'm \(age) years old")
    }
}

// Creating an instance
let person = Person(name: "Alice", age: 30)
person.introduce()
```

### Structures with Computed Properties
```swift
struct Rectangle {
    var width: Double
    var height: Double
    
    var area: Double {
        return width * height
    }
    
    var perimeter: Double {
        return 2 * (width + height)
    }
}

let rect = Rectangle(width: 10, height: 5)
print("Area: \(rect.area)")
print("Perimeter: \(rect.perimeter)")
```

### Mutating Methods
Methods that modify properties must be marked as mutating:

```swift
struct Counter {
    var count = 0
    
    mutating func increment() {
        count += 1
    }
    
    mutating func reset() {
        count = 0
    }
}

var counter = Counter()
counter.increment()
counter.increment()
print(counter.count)  // 2
counter.reset()
print(counter.count)  // 0
```

## Classes

### Basic Class
```swift
class Vehicle {
    var currentSpeed = 0.0
    var description: String {
        return "traveling at \(currentSpeed) miles per hour"
    }
    
    func makeNoise() {
        // Default implementation does nothing
    }
}

let vehicle = Vehicle()
vehicle.currentSpeed = 50
print("Vehicle is \(vehicle.description)")
```

### Initializers
```swift
class Person {
    var name: String
    var age: Int
    
    init(name: String, age: Int) {
        self.name = name
        self.age = age
    }
    
    convenience init(name: String) {
        self.init(name: name, age: 0)
    }
}

let person1 = Person(name: "Alice", age: 30)
let person2 = Person(name: "Bob")
```

### Inheritance
```swift
class Animal {
    var name: String
    
    init(name: String) {
        self.name = name
    }
    
    func makeSound() {
        print("Some generic sound")
    }
}

class Dog: Animal {
    var breed: String
    
    init(name: String, breed: String) {
        self.breed = breed
        super.init(name: name)
    }
    
    override func makeSound() {
        print("\(name) says: Woof!")
    }
}

let dog = Dog(name: "Buddy", breed: "Golden Retriever")
dog.makeSound()  // "Buddy says: Woof!"
```

### Properties

#### Stored Properties
```swift
class Car {
    var brand: String = "Unknown"
    var model: String = "Unknown"
    var year: Int = 0
}
```

#### Computed Properties
```swift
class Temperature {
    var celsius: Double = 0
    
    var fahrenheit: Double {
        get {
            return celsius * 9/5 + 32
        }
        set {
            celsius = (newValue - 32) * 5/9
        }
    }
}

let temp = Temperature()
temp.celsius = 25
print(temp.fahrenheit)  // 77.0
temp.fahrenheit = 86
print(temp.celsius)     // 30.0
```

#### Property Observers
```swift
class StepCounter {
    var totalSteps: Int = 0 {
        willSet {
            print("About to set totalSteps to \(newValue)")
        }
        didSet {
            if totalSteps > oldValue {
                print("Added \(totalSteps - oldValue) steps")
            }
        }
    }
}

let counter = StepCounter()
counter.totalSteps = 100
counter.totalSteps = 200
```

#### Type Properties
```swift
struct SomeStructure {
    static var storedTypeProperty = "Some value"
    
    static var computedTypeProperty: Int {
        return 42
    }
}

print(SomeStructure.storedTypeProperty)
print(SomeStructure.computedTypeProperty)
```

## Key Differences: Class vs Struct

### Value Types vs Reference Types

**Structures are value types:**
```swift
struct Point {
    var x: Int
    var y: Int
}

var point1 = Point(x: 1, y: 2)
var point2 = point1  // Creates a copy
point2.x = 5

print(point1.x)  // 1 (unchanged)
print(point2.x)  // 5
```

**Classes are reference types:**
```swift
class PointClass {
    var x: Int
    var y: Int
    
    init(x: Int, y: Int) {
        self.x = x
        self.y = y
    }
}

let pointA = PointClass(x: 1, y: 2)
let pointB = pointA  // Both reference the same object
pointB.x = 5

print(pointA.x)  // 5 (changed!)
print(pointB.x)  // 5
```

### When to Use Structures
- When you need simple data encapsulation
- When you want value semantics (copying)
- When you're working with small, simple types
- When you don't need inheritance

### When to Use Classes
- When you need inheritance
- When you want reference semantics (sharing)
- When you need to work with Objective-C APIs
- When you need a deinitializer

## Practical Examples

### Example 1: Bank Account
```swift
class BankAccount {
    private var balance: Double
    let accountNumber: String
    
    init(accountNumber: String, initialBalance: Double) {
        self.accountNumber = accountNumber
        self.balance = initialBalance
    }
    
    func deposit(_ amount: Double) {
        guard amount > 0 else { return }
        balance += amount
        print("Deposited $\(amount). New balance: $\(balance)")
    }
    
    func withdraw(_ amount: Double) -> Bool {
        guard amount > 0 && amount <= balance else {
            print("Insufficient funds")
            return false
        }
        balance -= amount
        print("Withdrew $\(amount). New balance: $\(balance)")
        return true
    }
    
    func getBalance() -> Double {
        return balance
    }
}

let account = BankAccount(accountNumber: "123456", initialBalance: 1000)
account.deposit(500)
account.withdraw(200)
```

### Example 2: Student Grade System
```swift
struct Student {
    let name: String
    var grades: [Double]
    
    var average: Double {
        guard !grades.isEmpty else { return 0 }
        return grades.reduce(0, +) / Double(grades.count)
    }
    
    var letterGrade: String {
        switch average {
        case 90...100: return "A"
        case 80..<90: return "B"
        case 70..<80: return "C"
        case 60..<70: return "D"
        default: return "F"
        }
    }
    
    mutating func addGrade(_ grade: Double) {
        grades.append(grade)
    }
}

var student = Student(name: "Alice", grades: [85, 90, 78])
print("\(student.name)'s average: \(student.average)")
print("Letter grade: \(student.letterGrade)")
student.addGrade(95)
print("New average: \(student.average)")
```

## Practice Exercises
1. Create a `Book` structure with properties for title, author, and pages
2. Create a `Circle` class with a radius property and methods to calculate area and circumference
3. Create an `Employee` class that inherits from `Person` and adds a salary property
4. Build a simple `ShoppingCart` class that can add/remove items and calculate total
