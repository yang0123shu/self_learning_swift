# Swift 和 SwiftUI 完整教程

## 1. Swift 6.0 和 SwiftUI 5.0 简介
Swift 是一种强类型、安全且高效的编程语言。Swift 6.0 引入了许多新特性，使得编程变得更加简洁和高效。SwiftUI 5.0 提供了一种声明式的方式来构建用户界面。

## 2. Swift 基础
### 变量与常量
在 Swift 中，使用 `var` 声明变量，使用 `let` 声明常量。
```swift
var name = "John" // 变量
let age = 30 // 常量

// 类型推断
var greeting = "Hello" // Swift 自动推断为 String 类型

// 显式类型声明
var explicitDouble: Double = 70

// 多个变量声明
var x = 0.0, y = 0.0, z = 0.0
```

### 数据类型
Swift 支持多种数据类型，包括：
- 整型（Int）
- 浮点型（Float, Double）
- 字符串（String）
- 数组（Array）
- 字典（Dictionary）

#### 整型和浮点型详细示例
```swift
// 整型
let minValue = Int.min  // -9223372036854775808
let maxValue = Int.max  // 9223372036854775807
let uint: UInt = 42     // 无符号整型

// 浮点型
let pi: Double = 3.14159
let floatPi: Float = 3.14
let scientificNotation = 1.25e2  // 125.0
let hexadecimal = 0xFp2          // 15 * 2^2 = 60.0

// 数字格式化
let paddedDouble = 000123.456
let oneMillion = 1_000_000       // 使用下划线提高可读性
```

#### 字符串操作详细示例
```swift
// 字符串基础
let str1 = "Hello"
let str2 = "World"
let combined = str1 + " " + str2  // "Hello World"

// 字符串插值
let name = "Alice"
let age = 25
let message = "My name is \(name) and I'm \(age) years old."

// 多行字符串
let multiline = """
    这是一个
    多行字符串
    示例
    """

// 字符串长度
let length = message.count

// 字符串判空
let isEmpty = str1.isEmpty

// 字符串遍历
for character in "Swift" {
    print(character)
}

// 字符串索引操作
let greeting = "Hello, World!"
let startIndex = greeting.startIndex
let endIndex = greeting.endIndex
let firstChar = greeting[startIndex]  // "H"
let secondChar = greeting[greeting.index(after: startIndex)]  // "e"

// 字符串截取
let range = greeting.index(greeting.startIndex, offsetBy: 0)..<greeting.index(greeting.startIndex, offsetBy: 5)
let substring = greeting[range]  // "Hello"

// 字符串查找和替换
if greeting.contains("World") {
    print("找到了 World")
}

let replaced = greeting.replacingOccurrences(of: "World", with: "Swift")
// "Hello, Swift!"

// 字符串前缀和后缀
let hasPrefix = greeting.hasPrefix("Hello")  // true
let hasSuffix = greeting.hasSuffix("!")      // true

// 字符串分割
let words = greeting.split(separator: " ")   // ["Hello,", "World!"]

// 字符串转换
let upperCased = greeting.uppercased()       // "HELLO, WORLD!"
let lowerCased = greeting.lowercased()       // "hello, world!"

// 去除空格
let spacedString = "  Swift  "
let trimmed = spacedString.trimmingCharacters(in: .whitespaces)  // "Swift"
```

#### 数组详细示例
```swift
// 创建数组
var numbers = [1, 2, 3, 4, 5]
var emptyArray: [Int] = []
var repeatingArray = Array(repeating: 0, count: 5)  // [0, 0, 0, 0, 0]

// 访问和修改
let firstElement = numbers[0]
numbers[0] = 10
numbers.append(6)           // [10, 2, 3, 4, 5, 6]
numbers.insert(0, at: 0)    // [0, 10, 2, 3, 4, 5, 6]
numbers.remove(at: 0)       // [10, 2, 3, 4, 5, 6]

// 数组属性
let count = numbers.count
let isEmpty = numbers.isEmpty
let first = numbers.first   // Optional(10)
let last = numbers.last     // Optional(6)

// 数组遍历
for number in numbers {
    print(number)
}

for (index, value) in numbers.enumerated() {
    print("Index: \(index), Value: \(value)")
}

// 数组操作
let filtered = numbers.filter { $0 > 3 }      // [10, 4, 5, 6]
let mapped = numbers.map { $0 * 2 }           // [20, 4, 6, 8, 10, 12]
let reduced = numbers.reduce(0, +)            // 30
let sorted = numbers.sorted()                 // [2, 3, 4, 5, 6, 10]

// 数组切片
let slice = numbers[1...3]  // [2, 3, 4]
```

#### 字典详细示例
```swift
// 创建字典
var ages = ["Alice": 25, "Bob": 30, "Charlie": 35]
var emptyDict: [String: Int] = [:]

// 访问和修改
let aliceAge = ages["Alice"]  // Optional(25)
ages["Alice"] = 26
ages["David"] = 28
ages.updateValue(31, forKey: "Bob")
ages.removeValue(forKey: "Charlie")

// 字典属性
let count = ages.count
let isEmpty = ages.isEmpty
let keys = Array(ages.keys)      // ["Alice", "Bob", "David"]
let values = Array(ages.values)  // [26, 31, 28]

// 字典遍历
for (name, age) in ages {
    print("\(name) is \(age) years old")
}

for name in ages.keys {
    print("Name: \(name)")
}

// 字典操作
let filtered = ages.filter { $0.value > 27 }
let mapped = ages.mapValues { $0 + 1 }
```

#### 元组（Tuple）
```swift
// 创建元组
let person = ("Alice", 25, "Engineer")
let coordinates = (x: 10, y: 20)

// 访问元组元素
let name = person.0      // "Alice"
let age = person.1       // 25
let x = coordinates.x    // 10

// 元组解构
let (userName, userAge, userJob) = person
print("\(userName) is \(userAge) years old")

// 函数返回元组
func getMinMax(array: [Int]) -> (min: Int, max: Int)? {
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

if let result = getMinMax(array: [3, 1, 4, 1, 5, 9]) {
    print("Min: \(result.min), Max: \(result.max)")
}
```

#### 集合（Set）
```swift
// 创建集合
var fruits: Set<String> = ["Apple", "Orange", "Banana"]
var emptySet: Set<Int> = []

// 添加和删除
fruits.insert("Grape")
fruits.remove("Orange")

// 集合操作
let set1: Set = [1, 2, 3, 4, 5]
let set2: Set = [3, 4, 5, 6, 7]

let union = set1.union(set2)              // [1, 2, 3, 4, 5, 6, 7]
let intersection = set1.intersection(set2) // [3, 4, 5]
let difference = set1.subtracting(set2)    // [1, 2]
let symmetric = set1.symmetricDifference(set2) // [1, 2, 6, 7]

// 集合判断
let isSubset = set1.isSubset(of: set2)
let isSuperset = set1.isSuperset(of: set2)
let isDisjoint = set1.isDisjoint(with: set2)
```

### 控制流
Swift 提供了多种控制流语句，例如：

#### if-else 语句详细用法
```swift
let age = 20

// 基本 if-else
if age > 18 {
    print("成年人")
} else {
    print("未成年人")
}

// if-else if-else
let score = 85
if score >= 90 {
    print("优秀")
} else if score >= 80 {
    print("良好")
} else if score >= 60 {
    print("及格")
} else {
    print("不及格")
}

// 复合条件
let temperature = 25
let isRaining = false
if temperature > 20 && !isRaining {
    print("适合外出")
}

// 条件绑定
let optionalName: String? = "Alice"
if let name = optionalName {
    print("Hello, \(name)")
} else {
    print("Name is nil")
}

// 多个可选值绑定
let optionalAge: Int? = 25
if let name = optionalName, let age = optionalAge, age >= 18 {
    print("\(name) is an adult")
}
```

#### guard 语句
```swift
func greet(person: [String: String]) {
    guard let name = person["name"] else {
        print("Name not found")
        return
    }
    
    print("Hello, \(name)!")
    
    guard let location = person["location"] else {
        print("Location not found")
        return
    }
    
    print("I hope the weather is nice in \(location).")
}

// 函数提前返回
func divide(_ a: Double, by b: Double) -> Double? {
    guard b != 0 else {
        print("Cannot divide by zero")
        return nil
    }
    return a / b
}
```

#### switch 语句详细用法
```swift
let character = "a"

// 基本 switch
switch character {
case "a":
    print("The first letter of the alphabet")
case "z":
    print("The last letter of the alphabet")
default:
    print("Some other character")
}

// 多个值匹配
let anotherCharacter = "e"
switch anotherCharacter {
case "a", "e", "i", "o", "u":
    print("\(anotherCharacter) is a vowel")
default:
    print("\(anotherCharacter) is a consonant")
}

// 区间匹配
let approximateCount = 62
let naturalCount: String
switch approximateCount {
case 0:
    naturalCount = "no"
case 1..<5:
    naturalCount = "a few"
case 5..<12:
    naturalCount = "several"
case 12..<100:
    naturalCount = "dozens of"
case 100..<1000:
    naturalCount = "hundreds of"
default:
    naturalCount = "many"
}

// 元组匹配
let point = (1, 1)
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

// 值绑定
let anotherPoint = (2, 0)
switch anotherPoint {
case (let x, 0):
    print("On the x-axis with value \(x)")
case (0, let y):
    print("On the y-axis with value \(y)")
case let (x, y):
    print("At (\(x), \(y))")
}

// where 子句
let yetAnotherPoint = (1, -1)
switch yetAnotherPoint {
case let (x, y) where x == y:
    print("On the line x == y")
case let (x, y) where x == -y:
    print("On the line x == -y")
case let (x, y):
    print("At (\(x), \(y))")
}
```

#### for-in 循环详细用法
```swift
// 遍历数组
let names = ["Alice", "Bob", "Charlie"]
for name in names {
    print("Hello, \(name)!")
}

// 遍历字典
let numberOfLegs = ["spider": 8, "ant": 6, "cat": 4]
for (animalName, legCount) in numberOfLegs {
    print("\(animalName)s have \(legCount) legs")
}

// 数值范围
for index in 1...5 {
    print("\(index) times 5 is \(index * 5)")
}

// 半开范围
for index in 1..<5 {
    print(index)  // 1, 2, 3, 4
}

// 忽略值
let base = 3
let power = 10
var answer = 1
for _ in 1...power {
    answer *= base
}

// stride 函数
for tickMark in stride(from: 0, to: 60, by: 5) {
    print(tickMark)  // 0, 5, 10, ..., 55
}

for tickMark in stride(from: 3, through: 12, by: 3) {
    print(tickMark)  // 3, 6, 9, 12
}

// 遍历字符串
for character in "Hello" {
    print(character)
}

// 带索引的遍历
for (index, value) in names.enumerated() {
    print("Item \(index + 1): \(value)")
}

// 反向遍历
for name in names.reversed() {
    print(name)
}
```

#### while 和 repeat-while 循环
```swift
// while 循环
var count = 0
while count < 5 {
    print("Count is \(count)")
    count += 1
}

// repeat-while 循环（至少执行一次）
var number = 0
repeat {
    print("Number is \(number)")
    number += 1
} while number < 3

// 实际应用示例：猜数字游戏
var targetNumber = 42
var guess = 0
var attempts = 0

while guess != targetNumber {
    guess = Int.random(in: 1...100)
    attempts += 1
    if guess < targetNumber {
        print("Too low!")
    } else if guess > targetNumber {
        print("Too high!")
    }
}
print("Correct! It took \(attempts) attempts.")
```

#### 控制转移语句
```swift
// continue：跳过当前迭代
for number in 1...10 {
    if number % 2 == 0 {
        continue
    }
    print(number)  // 只打印奇数
}

// break：终止整个循环
for number in 1...10 {
    if number == 5 {
        break
    }
    print(number)  // 打印 1-4
}

// 标签语句：用于嵌套循环
outerLoop: for i in 1...3 {
    for j in 1...3 {
        if i * j > 4 {
            break outerLoop
        }
        print("\(i) * \(j) = \(i * j)")
    }
}

// fallthrough：继续执行下一个 case
let integerToDescribe = 5
var description = "The number \(integerToDescribe) is"
switch integerToDescribe {
case 2, 3, 5, 7, 11, 13, 17, 19:
    description += " a prime number, and also"
    fallthrough
default:
    description += " an integer."
}
print(description)

// return：从函数返回
func checkPositive(number: Int) -> String {
    if number > 0 {
        return "Positive"
    } else if number < 0 {
        return "Negative"
    }
    return "Zero"
}
```

### 函数
#### 函数基础
```swift
// 基本函数
func greet(name: String) -> String {
    return "Hello, \(name)"
}
print(greet(name: "John"))

// 无返回值函数
func printGreeting(name: String) {
    print("Hello, \(name)")
}

// 多参数函数
func greet(person: String, from hometown: String) -> String {
    return "Hello \(person)! Glad you could visit from \(hometown)."
}
print(greet(person: "Bill", from: "Cupertino"))

// 无参数函数
func sayHello() -> String {
    return "Hello!"
}

// 多返回值函数（元组）
func minMax(array: [Int]) -> (min: Int, max: Int) {
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

let bounds = minMax(array: [8, -6, 2, 109, 3, 71])
print("min is \(bounds.min) and max is \(bounds.max)")

// 可选返回值
func minMaxOptional(array: [Int]) -> (min: Int, max: Int)? {
    if array.isEmpty { return nil }
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

// 隐式返回
func greeting(for person: String) -> String {
    "Hello, " + person + "!"  // 单行表达式可省略 return
}
```

#### 函数参数
```swift
// 默认参数值
func greet(person: String, greeting: String = "Hello") -> String {
    return "\(greeting), \(person)!"
}
print(greet(person: "Alice"))              // Hello, Alice!
print(greet(person: "Bob", greeting: "Hi")) // Hi, Bob!

// 可变参数
func arithmeticMean(_ numbers: Double...) -> Double {
    var total: Double = 0
    for number in numbers {
        total += number
    }
    return total / Double(numbers.count)
}
print(arithmeticMean(1, 2, 3, 4, 5))      // 3.0
print(arithmeticMean(3, 8.25, 18.75))     // 10.0

// 输入输出参数（inout）
func swapTwoInts(_ a: inout Int, _ b: inout Int) {
    let temporaryA = a
    a = b
    b = temporaryA
}

var someInt = 3
var anotherInt = 107
swapTwoInts(&someInt, &anotherInt)
print("someInt is now \(someInt), anotherInt is now \(anotherInt)")

// 参数标签
func greet(_ person: String, from hometown: String) -> String {
    return "Hello \(person)! Glad you could visit from \(hometown)."
}
print(greet("Bill", from: "Cupertino"))
```

#### 函数类型
```swift
// 函数类型作为变量
func addTwoInts(_ a: Int, _ b: Int) -> Int {
    return a + b
}

func multiplyTwoInts(_ a: Int, _ b: Int) -> Int {
    return a * b
}

var mathFunction: (Int, Int) -> Int = addTwoInts
print("Result: \(mathFunction(2, 3))")  // 5

mathFunction = multiplyTwoInts
print("Result: \(mathFunction(2, 3))")  // 6

// 函数类型作为参数
func printMathResult(_ mathFunction: (Int, Int) -> Int, _ a: Int, _ b: Int) {
    print("Result: \(mathFunction(a, b))")
}
printMathResult(addTwoInts, 3, 5)

// 函数类型作为返回值
func stepForward(_ input: Int) -> Int {
    return input + 1
}

func stepBackward(_ input: Int) -> Int {
    return input - 1
}

func chooseStepFunction(backward: Bool) -> (Int) -> Int {
    return backward ? stepBackward : stepForward
}

var currentValue = 3
let moveNearerToZero = chooseStepFunction(backward: currentValue > 0)
while currentValue != 0 {
    print("\(currentValue)... ")
    currentValue = moveNearerToZero(currentValue)
}
```

#### 嵌套函数
```swift
func chooseStepFunction(backward: Bool) -> (Int) -> Int {
    func stepForward(input: Int) -> Int { return input + 1 }
    func stepBackward(input: Int) -> Int { return input - 1 }
    return backward ? stepBackward : stepForward
}
```

### 闭包
闭包是一种自包含的代码块，可以在代码中被传递和使用。

#### 闭包基础
```swift
// 基本闭包语法
let closure = { (name: String) in
    print("Hello, \(name)")
}
closure("John")

// 闭包表达式完整形式
let names = ["Chris", "Alex", "Ewa", "Barry", "Daniella"]
let reversedNames = names.sorted(by: { (s1: String, s2: String) -> Bool in
    return s1 > s2
})

// 根据上下文推断类型
let reversed1 = names.sorted(by: { s1, s2 in return s1 > s2 })

// 单表达式闭包隐式返回
let reversed2 = names.sorted(by: { s1, s2 in s1 > s2 })

// 参数名称缩写
let reversed3 = names.sorted(by: { $0 > $1 })

// 运算符方法
let reversed4 = names.sorted(by: >)
```

#### 尾随闭包
```swift
// 普通调用
func someFunctionThatTakesAClosure(closure: () -> Void) {
    closure()
}
someFunctionThatTakesAClosure(closure: {
    print("Closure is called")
})

// 尾随闭包
someFunctionThatTakesAClosure() {
    print("Closure is called")
}

// 如果闭包是唯一参数，可以省略括号
someFunctionThatTakesAClosure {
    print("Closure is called")
}

// 实际应用：数组操作
let digitNames = [0: "Zero", 1: "One", 2: "Two", 3: "Three", 4: "Four",
                  5: "Five", 6: "Six", 7: "Seven", 8: "Eight", 9: "Nine"]
let numbers = [16, 58, 510]

let strings = numbers.map { (number) -> String in
    var number = number
    var output = ""
    repeat {
        output = digitNames[number % 10]! + output
        number /= 10
    } while number > 0
    return output
}
```

#### 多尾随闭包
```swift
func loadPicture(from server: String, 
                 completion: (String) -> Void, 
                 onFailure: () -> Void) {
    if server == "valid" {
        completion("Picture loaded")
    } else {
        onFailure()
    }
}

// 多尾随闭包调用
loadPicture(from: "valid") { picture in
    print(picture)
} onFailure: {
    print("Failed to load picture")
}
```

#### 捕获值
```swift
func makeIncrementer(forIncrement amount: Int) -> () -> Int {
    var runningTotal = 0
    func incrementer() -> Int {
        runningTotal += amount
        return runningTotal
    }
    return incrementer
}

let incrementByTen = makeIncrementer(forIncrement: 10)
print(incrementByTen())  // 10
print(incrementByTen())  // 20
print(incrementByTen())  // 30

// 新的引用会有独立的存储
let incrementBySeven = makeIncrementer(forIncrement: 7)
print(incrementBySeven())  // 7
```

#### 逃逸闭包
```swift
var completionHandlers: [() -> Void] = []

func someFunctionWithEscapingClosure(completionHandler: @escaping () -> Void) {
    completionHandlers.append(completionHandler)
}

func someFunctionWithNonescapingClosure(closure: () -> Void) {
    closure()
}

class SomeClass {
    var x = 10
    func doSomething() {
        someFunctionWithEscapingClosure { self.x = 100 }
        someFunctionWithNonescapingClosure { x = 200 }
    }
}

let instance = SomeClass()
instance.doSomething()
print(instance.x)  // 200

completionHandlers.first?()
print(instance.x)  // 100
```

#### 自动闭包
```swift
var customersInLine = ["Chris", "Alex", "Ewa", "Barry", "Daniella"]

func serve(customer customerProvider: @autoclosure () -> String) {
    print("Now serving \(customerProvider())!")
}

serve(customer: customersInLine.remove(at: 0))
// 不需要手动创建闭包，参数自动被包装成闭包
```

#### 闭包实际应用场景
```swift
// 1. 数组过滤
let numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
let evenNumbers = numbers.filter { $0 % 2 == 0 }
print(evenNumbers)  // [2, 4, 6, 8, 10]

// 2. 数组映射
let squaredNumbers = numbers.map { $0 * $0 }
print(squaredNumbers)  // [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]

// 3. 数组归约
let sum = numbers.reduce(0) { $0 + $1 }
print(sum)  // 55

// 4. 异步操作
func fetchData(completion: @escaping (String) -> Void) {
    // 模拟异步操作
    DispatchQueue.main.asyncAfter(deadline: .now() + 1.0) {
        completion("Data fetched")
    }
}

fetchData { result in
    print(result)
}

// 5. 事件处理
class Button {
    var onClick: (() -> Void)?
    
    func tap() {
        onClick?()
    }
}

let button = Button()
button.onClick = {
    print("Button was tapped!")
}
button.tap()

// 6. 链式调用
[1, 2, 3, 4, 5]
    .filter { $0 % 2 == 0 }
    .map { $0 * 2 }
    .reduce(0, +)  // 12
```

### 可选值
可选值用于处理可能缺失的值：
```swift
var optionalName: String? = nil
```

## 3. SwiftUI 基础
### 视图
SwiftUI 中的视图是构建用户界面的基本单位：
```swift
struct ContentView: View {
    var body: some View {
        Text("Hello, SwiftUI!")
    }
}
```

### 修饰符
修饰符用于修改视图的外观和行为：
```swift
Text("Hello, SwiftUI!")
    .font(.largeTitle)
    .foregroundColor(.blue)
```

### 状态管理
SwiftUI 提供了多种状态管理方式：
- `@State`
- `@Binding`
- `@StateObject`
- `@ObservedObject`
- `@EnvironmentObject`

### 布局系统
使用 HStack、VStack 和 ZStack 来布局视图：
```swift
HStack {
    Text("Hello")
    Text("World")
}
```

## 4. 中级主题
### 协议（Protocol）
协议定义了方法和属性的蓝图，是实现抽象和接口的关键机制。

#### 协议基础
```swift
// 定义协议
protocol Drawable {
    func draw()
}

// 实现协议
struct Circle: Drawable {
    var radius: Double
    
    func draw() {
        print("Drawing a circle with radius \(radius)")
    }
}

struct Rectangle: Drawable {
    var width: Double
    var height: Double
    
    func draw() {
        print("Drawing a rectangle \(width)x\(height)")
    }
}

let shapes: [Drawable] = [Circle(radius: 5), Rectangle(width: 10, height: 20)]
for shape in shapes {
    shape.draw()
}
```

#### 协议属性要求
```swift
protocol FullyNamed {
    var fullName: String { get }  // 只读属性
}

protocol AgeTrackable {
    var age: Int { get set }  // 可读可写属性
}

struct Person: FullyNamed, AgeTrackable {
    var firstName: String
    var lastName: String
    var age: Int
    
    var fullName: String {
        return "\(firstName) \(lastName)"
    }
}

let person = Person(firstName: "John", lastName: "Doe", age: 30)
print(person.fullName)  // John Doe
```

#### 协议方法要求
```swift
protocol RandomNumberGenerator {
    func random() -> Double
}

class LinearCongruentialGenerator: RandomNumberGenerator {
    var lastRandom = 42.0
    let m = 139968.0
    let a = 3877.0
    let c = 29573.0
    
    func random() -> Double {
        lastRandom = ((lastRandom * a + c).truncatingRemainder(dividingBy: m))
        return lastRandom / m
    }
}

let generator = LinearCongruentialGenerator()
print("Random number: \(generator.random())")
```

#### 协议初始化器要求
```swift
protocol Initializable {
    init(value: String)
}

struct MyStruct: Initializable {
    var value: String
    
    init(value: String) {
        self.value = value
    }
}

class MyClass: Initializable {
    var value: String
    
    required init(value: String) {
        self.value = value
    }
}
```

#### 协议继承
```swift
protocol Named {
    var name: String { get }
}

protocol Aged {
    var age: Int { get }
}

protocol Person: Named, Aged {
    var occupation: String { get }
}

struct Employee: Person {
    var name: String
    var age: Int
    var occupation: String
}
```

#### 协议组合
```swift
protocol Named {
    var name: String { get }
}

protocol Aged {
    var age: Int { get }
}

struct Person: Named, Aged {
    var name: String
    var age: Int
}

func wishHappyBirthday(to celebrator: Named & Aged) {
    print("Happy birthday, \(celebrator.name), you're \(celebrator.age)!")
}

let person = Person(name: "Alice", age: 25)
wishHappyBirthday(to: person)
```

#### 协议扩展
```swift
protocol TextRepresentable {
    var textualDescription: String { get }
}

extension TextRepresentable {
    var textualDescription: String {
        return "Default description"
    }
    
    func printDescription() {
        print(textualDescription)
    }
}

struct Product: TextRepresentable {
    var name: String
    var price: Double
    
    var textualDescription: String {
        return "\(name): $\(price)"
    }
}

let product = Product(name: "iPhone", price: 999)
product.printDescription()  // iPhone: $999
```

#### 协议关联类型
```swift
protocol Container {
    associatedtype Item
    var count: Int { get }
    mutating func append(_ item: Item)
    subscript(i: Int) -> Item { get }
}

struct IntStack: Container {
    typealias Item = Int  // 可以省略，Swift 会自动推断
    
    private var items = [Int]()
    
    var count: Int {
        return items.count
    }
    
    mutating func append(_ item: Int) {
        items.append(item)
    }
    
    subscript(i: Int) -> Int {
        return items[i]
    }
}
```

#### 协议实际应用
```swift
// 1. 委托模式（Delegate Pattern）
protocol DataSourceDelegate: AnyObject {
    func numberOfItems() -> Int
    func itemAt(index: Int) -> String
}

class ListView {
    weak var dataSource: DataSourceDelegate?
    
    func displayItems() {
        guard let dataSource = dataSource else { return }
        for i in 0..<dataSource.numberOfItems() {
            print(dataSource.itemAt(index: i))
        }
    }
}

class DataManager: DataSourceDelegate {
    private let items = ["Apple", "Banana", "Cherry"]
    
    func numberOfItems() -> Int {
        return items.count
    }
    
    func itemAt(index: Int) -> String {
        return items[index]
    }
}

let listView = ListView()
let dataManager = DataManager()
listView.dataSource = dataManager
listView.displayItems()

// 2. 策略模式（Strategy Pattern）
protocol PaymentStrategy {
    func pay(amount: Double)
}

struct CreditCardPayment: PaymentStrategy {
    func pay(amount: Double) {
        print("Paid $\(amount) with credit card")
    }
}

struct PayPalPayment: PaymentStrategy {
    func pay(amount: Double) {
        print("Paid $\(amount) with PayPal")
    }
}

class ShoppingCart {
    private var paymentStrategy: PaymentStrategy
    
    init(paymentStrategy: PaymentStrategy) {
        self.paymentStrategy = paymentStrategy
    }
    
    func checkout(amount: Double) {
        paymentStrategy.pay(amount: amount)
    }
}

let cart = ShoppingCart(paymentStrategy: CreditCardPayment())
cart.checkout(amount: 99.99)
```

### 扩展（Extension）
扩展可以为已有类型添加新功能，包括计算属性、方法、初始化器等。

#### 扩展基础
```swift
// 为整型添加计算属性
extension Int {
    var squared: Int {
        return self * self
    }
    
    var cubed: Int {
        return self * self * self
    }
}

let number = 5
print(number.squared)  // 25
print(number.cubed)    // 125

// 为整型添加方法
extension Int {
    func repetitions(task: () -> Void) {
        for _ in 0..<self {
            task()
        }
    }
}

3.repetitions {
    print("Hello!")
}

// 为整型添加可变方法
extension Int {
    mutating func square() {
        self = self * self
    }
}

var someInt = 3
someInt.square()
print(someInt)  // 9
```

#### 扩展计算属性
```swift
extension Double {
    var km: Double { return self * 1_000.0 }
    var m: Double { return self }
    var cm: Double { return self / 100.0 }
    var mm: Double { return self / 1_000.0 }
    var ft: Double { return self / 3.28084 }
}

let oneInch = 25.4.mm
print("One inch is \(oneInch) meters")  // 0.0254 meters

let threeFeet = 3.ft
print("Three feet is \(threeFeet) meters")  // 0.914... meters
```

#### 扩展初始化器
```swift
struct Size {
    var width = 0.0
    var height = 0.0
}

struct Point {
    var x = 0.0
    var y = 0.0
}

struct Rect {
    var origin = Point()
    var size = Size()
}

extension Rect {
    init(center: Point, size: Size) {
        let originX = center.x - (size.width / 2)
        let originY = center.y - (size.height / 2)
        self.init(origin: Point(x: originX, y: originY), size: size)
    }
}

let centerRect = Rect(center: Point(x: 4.0, y: 4.0),
                     size: Size(width: 3.0, height: 3.0))
```

#### 扩展嵌套类型
```swift
extension Int {
    enum Kind {
        case negative, zero, positive
    }
    
    var kind: Kind {
        switch self {
        case 0:
            return .zero
        case let x where x > 0:
            return .positive
        default:
            return .negative
        }
    }
}

func printIntegerKinds(_ numbers: [Int]) {
    for number in numbers {
        switch number.kind {
        case .negative:
            print("- ", terminator: "")
        case .zero:
            print("0 ", terminator: "")
        case .positive:
            print("+ ", terminator: "")
        }
    }
    print("")
}

printIntegerKinds([3, 19, -27, 0, -6, 0, 7])  // + + - 0 - 0 +
```

#### 扩展实际应用
```swift
// 1. String 扩展
extension String {
    func isValidEmail() -> Bool {
        let emailRegex = "[A-Z0-9a-z._%+-]+@[A-Za-z0-9.-]+\\.[A-Za-z]{2,64}"
        let predicate = NSPredicate(format: "SELF MATCHES %@", emailRegex)
        return predicate.evaluate(with: self)
    }
    
    var isBlank: Bool {
        return trimmingCharacters(in: .whitespaces).isEmpty
    }
    
    subscript(offset: Int) -> Character {
        self[index(startIndex, offsetBy: offset)]
    }
}

let email = "test@example.com"
print(email.isValidEmail())  // true

// 2. Array 扩展
extension Array where Element: Numeric {
    func sum() -> Element {
        return reduce(0, +)
    }
    
    func average() -> Double where Element == Int {
        return isEmpty ? 0 : Double(sum()) / Double(count)
    }
}

let numbers = [1, 2, 3, 4, 5]
print(numbers.sum())      // 15
print(numbers.average())  // 3.0

// 3. Collection 扩展
extension Collection {
    subscript(safe index: Index) -> Element? {
        return indices.contains(index) ? self[index] : nil
    }
}

let array = [1, 2, 3]
print(array[safe: 5] ?? "nil")  // nil
```

### 泛型（Generics）
泛型允许编写灵活、可重用的代码，避免代码重复。

#### 泛型函数
```swift
// 基本泛型函数
func swap<T>(a: inout T, b: inout T) {
    let temp = a
    a = b
    b = temp
}

var int1 = 3
var int2 = 5
swap(&int1, &int2)
print("int1: \(int1), int2: \(int2)")  // int1: 5, int2: 3

var str1 = "hello"
var str2 = "world"
swap(&str1, &str2)
print("str1: \(str1), str2: \(str2)")  // str1: world, str2: hello

// 多类型参数
func printPair<T, U>(first: T, second: U) {
    print("First: \(first), Second: \(second)")
}

printPair(first: 42, second: "Answer")
printPair(first: "Question", second: true)
```

#### 泛型类型
```swift
// 泛型栈
struct Stack<Element> {
    private var items = [Element]()
    
    var isEmpty: Bool {
        return items.isEmpty
    }
    
    var count: Int {
        return items.count
    }
    
    mutating func push(_ item: Element) {
        items.append(item)
    }
    
    mutating func pop() -> Element? {
        return items.popLast()
    }
    
    func peek() -> Element? {
        return items.last
    }
}

var intStack = Stack<Int>()
intStack.push(1)
intStack.push(2)
intStack.push(3)
print(intStack.pop() ?? "nil")  // 3

var stringStack = Stack<String>()
stringStack.push("Hello")
stringStack.push("World")
print(stringStack.peek() ?? "nil")  // World

// 泛型队列
struct Queue<Element> {
    private var items = [Element]()
    
    mutating func enqueue(_ item: Element) {
        items.append(item)
    }
    
    mutating func dequeue() -> Element? {
        return items.isEmpty ? nil : items.removeFirst()
    }
    
    func peek() -> Element? {
        return items.first
    }
}
```

#### 泛型约束
```swift
// 类型约束：T 必须遵循 Equatable 协议
func findIndex<T: Equatable>(of valueToFind: T, in array: [T]) -> Int? {
    for (index, value) in array.enumerated() {
        if value == valueToFind {
            return index
        }
    }
    return nil
}

let strings = ["cat", "dog", "llama", "parakeet", "terrapin"]
if let index = findIndex(of: "llama", in: strings) {
    print("Found at index \(index)")  // Found at index 2
}

// 多重约束
func compareAndPrint<T: Comparable & CustomStringConvertible>(_ a: T, _ b: T) {
    if a < b {
        print("\(a) is less than \(b)")
    } else if a > b {
        print("\(a) is greater than \(b)")
    } else {
        print("\(a) is equal to \(b)")
    }
}

compareAndPrint(5, 10)
compareAndPrint("apple", "banana")
```

#### 关联类型
```swift
protocol Container {
    associatedtype Item
    var count: Int { get }
    mutating func append(_ item: Item)
    subscript(i: Int) -> Item { get }
}

struct IntStack: Container {
    typealias Item = Int
    
    private var items = [Int]()
    
    var count: Int {
        return items.count
    }
    
    mutating func append(_ item: Int) {
        items.append(item)
    }
    
    subscript(i: Int) -> Int {
        return items[i]
    }
}

// 泛型 Container
struct GenericStack<Element>: Container {
    private var items = [Element]()
    
    var count: Int {
        return items.count
    }
    
    mutating func append(_ item: Element) {
        items.append(item)
    }
    
    subscript(i: Int) -> Element {
        return items[i]
    }
}
```

#### where 子句
```swift
// 在扩展中使用 where 子句
extension Array where Element: Numeric {
    func sum() -> Element {
        return reduce(0, +)
    }
}

let numbers = [1, 2, 3, 4, 5]
print(numbers.sum())  // 15

// 泛型函数中使用 where 子句
func allItemsMatch<C1: Container, C2: Container>
    (_ someContainer: C1, _ anotherContainer: C2) -> Bool
    where C1.Item == C2.Item, C1.Item: Equatable {
    
    if someContainer.count != anotherContainer.count {
        return false
    }
    
    for i in 0..<someContainer.count {
        if someContainer[i] != anotherContainer[i] {
            return false
        }
    }
    
    return true
}
```

#### 泛型实际应用
```swift
// 1. 结果类型（Result Type）
enum Result<Success, Failure: Error> {
    case success(Success)
    case failure(Failure)
}

enum NetworkError: Error {
    case badURL
    case requestFailed
    case unknown
}

func fetchData(from url: String) -> Result<String, NetworkError> {
    if url.isEmpty {
        return .failure(.badURL)
    }
    // 模拟网络请求
    return .success("Data from \(url)")
}

let result = fetchData(from: "https://example.com")
switch result {
case .success(let data):
    print("Success: \(data)")
case .failure(let error):
    print("Error: \(error)")
}

// 2. 泛型单例
class Singleton<T> {
    private static var instances = [String: Any]()
    
    static func shared(constructor: () -> T) -> T {
        let key = String(describing: T.self)
        if let instance = instances[key] as? T {
            return instance
        }
        let instance = constructor()
        instances[key] = instance
        return instance
    }
}

// 3. 泛型缓存
class Cache<Key: Hashable, Value> {
    private var storage = [Key: Value]()
    
    func set(_ value: Value, forKey key: Key) {
        storage[key] = value
    }
    
    func get(_ key: Key) -> Value? {
        return storage[key]
    }
    
    func remove(_ key: Key) {
        storage.removeValue(forKey: key)
    }
}

let stringCache = Cache<String, String>()
stringCache.set("Hello", forKey: "greeting")
print(stringCache.get("greeting") ?? "nil")  // Hello
```

### 错误处理
使用 `do-catch` 语句处理错误：
```swift
do {
    try someRiskyFunction()
} catch {
    print("Error occurred: \(error)")
}
```

## 5. 高级主题

### Combine 框架
Combine 是 Apple 提供的声明式 Swift API，用于处理异步事件流。

#### Combine 基础概念
```swift
import Combine

// Publisher: 发布者，产生值的源
// Subscriber: 订阅者，接收值的对象
// Operator: 操作符，转换和处理值

// 1. Just - 发布单个值
let justPublisher = Just("Hello, Combine!")
let cancellable = justPublisher.sink { value in
    print(value)  // Hello, Combine!
}

// 2. Future - 异步产生单个值
func fetchData() -> Future<String, Error> {
    return Future { promise in
        DispatchQueue.main.asyncAfter(deadline: .now() + 1) {
            promise(.success("Data fetched"))
        }
    }
}

let futureCancellable = fetchData().sink(
    receiveCompletion: { completion in
        switch completion {
        case .finished:
            print("Completed")
        case .failure(let error):
            print("Error: \(error)")
        }
    },
    receiveValue: { value in
        print(value)
    }
)

// 3. PassthroughSubject - 手动发送值
let subject = PassthroughSubject<String, Never>()
let subjectCancellable = subject.sink { value in
    print("Received: \(value)")
}

subject.send("First")
subject.send("Second")
subject.send(completion: .finished)

// 4. CurrentValueSubject - 保持当前值
let currentSubject = CurrentValueSubject<Int, Never>(0)
print("Initial value: \(currentSubject.value)")

let currentCancellable = currentSubject.sink { value in
    print("Value: \(value)")
}

currentSubject.send(1)
currentSubject.send(2)
print("Current value: \(currentSubject.value)")  // 2
```

#### Combine 操作符
```swift
import Combine

var cancellables = Set<AnyCancellable>()

// 1. map - 转换值
[1, 2, 3, 4, 5].publisher
    .map { $0 * 2 }
    .sink { print($0) }
    .store(in: &cancellables)

// 2. filter - 过滤值
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10].publisher
    .filter { $0 % 2 == 0 }
    .sink { print("Even: \($0)") }
    .store(in: &cancellables)

// 3. reduce - 归约
[1, 2, 3, 4, 5].publisher
    .reduce(0, +)
    .sink { print("Sum: \($0)") }
    .store(in: &cancellables)

// 4. compactMap - 过滤 nil 并转换
["1", "2", "three", "4", "5"].publisher
    .compactMap { Int($0) }
    .sink { print($0) }
    .store(in: &cancellables)

// 5. removeDuplicates - 移除连续重复值
[1, 1, 2, 2, 3, 3, 3, 4, 5, 5].publisher
    .removeDuplicates()
    .sink { print($0) }
    .store(in: &cancellables)

// 6. debounce - 防抖
let searchText = PassthroughSubject<String, Never>()
searchText
    .debounce(for: .milliseconds(500), scheduler: RunLoop.main)
    .sink { print("Search for: \($0)") }
    .store(in: &cancellables)

// 7. throttle - 节流
let events = PassthroughSubject<String, Never>()
events
    .throttle(for: .seconds(1), scheduler: RunLoop.main, latest: true)
    .sink { print("Event: \($0)") }
    .store(in: &cancellables)

// 8. flatMap - 扁平化
struct User {
    let id: Int
    let name: String
}

func fetchUserDetails(id: Int) -> AnyPublisher<User, Never> {
    Just(User(id: id, name: "User \(id)"))
        .eraseToAnyPublisher()
}

[1, 2, 3].publisher
    .flatMap { fetchUserDetails(id: $0) }
    .sink { user in
        print("User: \(user.name)")
    }
    .store(in: &cancellables)

// 9. combineLatest - 组合最新值
let numbers = PassthroughSubject<Int, Never>()
let letters = PassthroughSubject<String, Never>()

numbers.combineLatest(letters)
    .sink { number, letter in
        print("\(number) - \(letter)")
    }
    .store(in: &cancellables)

numbers.send(1)
letters.send("A")
numbers.send(2)
letters.send("B")

// 10. merge - 合并多个 Publisher
let publisher1 = PassthroughSubject<Int, Never>()
let publisher2 = PassthroughSubject<Int, Never>()

publisher1.merge(with: publisher2)
    .sink { print($0) }
    .store(in: &cancellables)

publisher1.send(1)
publisher2.send(2)
publisher1.send(3)

// 11. zip - 配对值
let nums = [1, 2, 3].publisher
let strs = ["A", "B", "C"].publisher

nums.zip(strs)
    .sink { number, letter in
        print("\(number) - \(letter)")
    }
    .store(in: &cancellables)
```

#### Combine 实际应用
```swift
import Combine

// 1. 网络请求
class NetworkService {
    func fetchData(from urlString: String) -> AnyPublisher<Data, Error> {
        guard let url = URL(string: urlString) else {
            return Fail(error: URLError(.badURL)).eraseToAnyPublisher()
        }
        
        return URLSession.shared.dataTaskPublisher(for: url)
            .map(\.data)
            .eraseToAnyPublisher()
    }
}

// 2. ViewModel 中使用 Combine
class UserViewModel: ObservableObject {
    @Published var username: String = ""
    @Published var isValid: Bool = false
    
    private var cancellables = Set<AnyCancellable>()
    
    init() {
        $username
            .map { $0.count >= 3 }
            .assign(to: &$isValid)
    }
}

// 3. 搜索功能
class SearchViewModel: ObservableObject {
    @Published var searchText: String = ""
    @Published var results: [String] = []
    
    private var cancellables = Set<AnyCancellable>()
    
    init() {
        $searchText
            .debounce(for: .milliseconds(500), scheduler: RunLoop.main)
            .removeDuplicates()
            .map { searchText -> [String] in
                // 模拟搜索
                guard !searchText.isEmpty else { return [] }
                return ["Result 1 for \(searchText)", 
                        "Result 2 for \(searchText)"]
            }
            .assign(to: &$results)
    }
}

// 4. 表单验证
class FormViewModel: ObservableObject {
    @Published var email: String = ""
    @Published var password: String = ""
    @Published var isFormValid: Bool = false
    
    private var cancellables = Set<AnyCancellable>()
    
    init() {
        Publishers.CombineLatest($email, $password)
            .map { email, password in
                return email.contains("@") && password.count >= 6
            }
            .assign(to: &$isFormValid)
    }
}

// 5. 定时器
class TimerViewModel: ObservableObject {
    @Published var currentTime = Date()
    
    private var cancellables = Set<AnyCancellable>()
    
    init() {
        Timer.publish(every: 1, on: .main, in: .common)
            .autoconnect()
            .assign(to: &$currentTime)
    }
}
```

### 自定义视图
SwiftUI 允许创建复杂的自定义视图组件。

#### 自定义视图基础
```swift
import SwiftUI

// 1. 简单自定义视图
struct CustomButton: View {
    let title: String
    let action: () -> Void
    
    var body: some View {
        Button(action: action) {
            Text(title)
                .font(.headline)
                .foregroundColor(.white)
                .padding()
                .frame(maxWidth: .infinity)
                .background(Color.blue)
                .cornerRadius(10)
        }
    }
}

// 使用
CustomButton(title: "Tap Me") {
    print("Button tapped")
}

// 2. 带状态的自定义视图
struct ToggleCard: View {
    @State private var isExpanded = false
    let title: String
    let content: String
    
    var body: some View {
        VStack(alignment: .leading) {
            HStack {
                Text(title)
                    .font(.headline)
                Spacer()
                Image(systemName: isExpanded ? "chevron.up" : "chevron.down")
            }
            .contentShape(Rectangle())
            .onTapGesture {
                withAnimation {
                    isExpanded.toggle()
                }
            }
            
            if isExpanded {
                Text(content)
                    .padding(.top, 5)
                    .transition(.opacity)
            }
        }
        .padding()
        .background(Color.gray.opacity(0.1))
        .cornerRadius(10)
    }
}

// 3. 可配置的自定义视图
struct GradientButton: View {
    let title: String
    let colors: [Color]
    let action: () -> Void
    
    var body: some View {
        Button(action: action) {
            Text(title)
                .font(.headline)
                .foregroundColor(.white)
                .padding()
                .frame(maxWidth: .infinity)
                .background(
                    LinearGradient(
                        gradient: Gradient(colors: colors),
                        startPoint: .leading,
                        endPoint: .trailing
                    )
                )
                .cornerRadius(10)
                .shadow(radius: 5)
        }
    }
}

// 使用
GradientButton(
    title: "Gradient Button",
    colors: [.blue, .purple]
) {
    print("Tapped")
}

// 4. 自定义修饰符
struct CardModifier: ViewModifier {
    func body(content: Content) -> some View {
        content
            .padding()
            .background(Color.white)
            .cornerRadius(10)
            .shadow(color: .gray.opacity(0.3), radius: 5, x: 0, y: 2)
    }
}

extension View {
    func cardStyle() -> some View {
        modifier(CardModifier())
    }
}

// 使用
Text("Card Content")
    .cardStyle()

// 5. 自定义形状
struct Triangle: Shape {
    func path(in rect: CGRect) -> Path {
        var path = Path()
        path.move(to: CGPoint(x: rect.midX, y: rect.minY))
        path.addLine(to: CGPoint(x: rect.maxX, y: rect.maxY))
        path.addLine(to: CGPoint(x: rect.minX, y: rect.maxY))
        path.closeSubpath()
        return path
    }
}

// 使用
Triangle()
    .fill(Color.blue)
    .frame(width: 100, height: 100)

// 6. 自定义进度条
struct CircularProgressView: View {
    let progress: Double  // 0.0 to 1.0
    
    var body: some View {
        ZStack {
            Circle()
                .stroke(Color.gray.opacity(0.3), lineWidth: 10)
            
            Circle()
                .trim(from: 0, to: CGFloat(progress))
                .stroke(Color.blue, style: StrokeStyle(lineWidth: 10, lineCap: .round))
                .rotationEffect(.degrees(-90))
                .animation(.easeInOut, value: progress)
            
            Text("\(Int(progress * 100))%")
                .font(.title)
                .bold()
        }
        .frame(width: 150, height: 150)
    }
}

// 7. 自定义输入框
struct StyledTextField: View {
    let placeholder: String
    @Binding var text: String
    var isSecure: Bool = false
    
    var body: some View {
        HStack {
            Image(systemName: isSecure ? "lock" : "envelope")
                .foregroundColor(.gray)
            
            if isSecure {
                SecureField(placeholder, text: $text)
            } else {
                TextField(placeholder, text: $text)
            }
        }
        .padding()
        .background(Color.gray.opacity(0.1))
        .cornerRadius(10)
        .overlay(
            RoundedRectangle(cornerRadius: 10)
                .stroke(Color.blue, lineWidth: 1)
        )
    }
}
```

### 动画
SwiftUI 提供了强大而简洁的动画系统。

#### 动画基础
```swift
import SwiftUI

// 1. 隐式动画
struct ImplicitAnimationView: View {
    @State private var scale: CGFloat = 1.0
    
    var body: some View {
        Circle()
            .frame(width: 100, height: 100)
            .scaleEffect(scale)
            .animation(.easeInOut(duration: 1), value: scale)
            .onTapGesture {
                scale = scale == 1.0 ? 1.5 : 1.0
            }
    }
}

// 2. 显式动画
struct ExplicitAnimationView: View {
    @State private var rotation: Double = 0
    
    var body: some View {
        Rectangle()
            .frame(width: 100, height: 100)
            .rotationEffect(.degrees(rotation))
            .onTapGesture {
                withAnimation(.spring(response: 0.5, dampingFraction: 0.6)) {
                    rotation += 90
                }
            }
    }
}

// 3. 动画曲线
struct AnimationCurvesView: View {
    @State private var offset: CGFloat = 0
    
    var body: some View {
        VStack(spacing: 20) {
            // Linear
            Circle()
                .frame(width: 50, height: 50)
                .offset(x: offset)
                .animation(.linear(duration: 1), value: offset)
            
            // EaseIn
            Circle()
                .frame(width: 50, height: 50)
                .offset(x: offset)
                .animation(.easeIn(duration: 1), value: offset)
            
            // EaseOut
            Circle()
                .frame(width: 50, height: 50)
                .offset(x: offset)
                .animation(.easeOut(duration: 1), value: offset)
            
            // EaseInOut
            Circle()
                .frame(width: 50, height: 50)
                .offset(x: offset)
                .animation(.easeInOut(duration: 1), value: offset)
            
            // Spring
            Circle()
                .frame(width: 50, height: 50)
                .offset(x: offset)
                .animation(.spring(), value: offset)
            
            Button("Animate") {
                offset = offset == 0 ? 100 : 0
            }
        }
    }
}

// 4. 过渡动画
struct TransitionView: View {
    @State private var showDetails = false
    
    var body: some View {
        VStack {
            Button("Toggle") {
                withAnimation {
                    showDetails.toggle()
                }
            }
            
            if showDetails {
                VStack {
                    Text("Details")
                        .font(.title)
                    Text("More information here")
                }
                .transition(.slide)
            }
        }
    }
}

// 5. 自定义过渡
extension AnyTransition {
    static var moveAndFade: AnyTransition {
        .asymmetric(
            insertion: .move(edge: .trailing).combined(with: .opacity),
            removal: .scale.combined(with: .opacity)
        )
    }
}

struct CustomTransitionView: View {
    @State private var showView = false
    
    var body: some View {
        VStack {
            Button("Toggle") {
                withAnimation(.spring()) {
                    showView.toggle()
                }
            }
            
            if showView {
                Rectangle()
                    .fill(Color.blue)
                    .frame(width: 200, height: 200)
                    .transition(.moveAndFade)
            }
        }
    }
}

// 6. 匹配几何效果
struct HeroAnimationView: View {
    @State private var isExpanded = false
    @Namespace private var animation
    
    var body: some View {
        VStack {
            if !isExpanded {
                RoundedRectangle(cornerRadius: 10)
                    .fill(Color.blue)
                    .matchedGeometryEffect(id: "shape", in: animation)
                    .frame(width: 100, height: 100)
                    .onTapGesture {
                        withAnimation(.spring()) {
                            isExpanded = true
                        }
                    }
            } else {
                RoundedRectangle(cornerRadius: 20)
                    .fill(Color.blue)
                    .matchedGeometryEffect(id: "shape", in: animation)
                    .frame(width: 300, height: 300)
                    .onTapGesture {
                        withAnimation(.spring()) {
                            isExpanded = false
                        }
                    }
            }
        }
    }
}

// 7. 动画实际应用案例
struct LoadingView: View {
    @State private var isAnimating = false
    
    var body: some View {
        HStack(spacing: 10) {
            ForEach(0..<3) { index in
                Circle()
                    .frame(width: 15, height: 15)
                    .foregroundColor(.blue)
                    .scaleEffect(isAnimating ? 1.5 : 1.0)
                    .animation(
                        Animation
                            .easeInOut(duration: 0.6)
                            .repeatForever()
                            .delay(0.2 * Double(index)),
                        value: isAnimating
                    )
            }
        }
        .onAppear {
            isAnimating = true
        }
    }
}

// 8. 卡片翻转动画
struct CardFlipView: View {
    @State private var flipped = false
    @State private var rotate = 0.0
    
    var body: some View {
        ZStack {
            if flipped {
                RoundedRectangle(cornerRadius: 20)
                    .fill(Color.green)
                    .overlay(Text("Back").font(.largeTitle))
            } else {
                RoundedRectangle(cornerRadius: 20)
                    .fill(Color.blue)
                    .overlay(Text("Front").font(.largeTitle))
            }
        }
        .frame(width: 200, height: 300)
        .rotation3DEffect(.degrees(rotate), axis: (x: 0, y: 1, z: 0))
        .onTapGesture {
            withAnimation(.easeInOut(duration: 0.6)) {
                rotate += 180
            }
            DispatchQueue.main.asyncAfter(deadline: .now() + 0.3) {
                flipped.toggle()
            }
        }
    }
}
```

### 数据持久化
iOS 提供多种数据持久化方案。

#### UserDefaults
```swift
import Foundation

// 1. 基本使用
class UserDefaultsManager {
    static let shared = UserDefaultsManager()
    private let defaults = UserDefaults.standard
    
    // 保存数据
    func saveString(_ value: String, forKey key: String) {
        defaults.set(value, forKey: key)
    }
    
    func saveInt(_ value: Int, forKey key: String) {
        defaults.set(value, forKey: key)
    }
    
    func saveBool(_ value: Bool, forKey key: String) {
        defaults.set(value, forKey: key)
    }
    
    // 读取数据
    func getString(forKey key: String) -> String? {
        return defaults.string(forKey: key)
    }
    
    func getInt(forKey key: String) -> Int {
        return defaults.integer(forKey: key)
    }
    
    func getBool(forKey key: String) -> Bool {
        return defaults.bool(forKey: key)
    }
    
    // 删除数据
    func remove(forKey key: String) {
        defaults.removeObject(forKey: key)
    }
}

// 使用
UserDefaultsManager.shared.saveString("John Doe", forKey: "username")
let username = UserDefaultsManager.shared.getString(forKey: "username")

// 2. 使用 @AppStorage 在 SwiftUI 中
struct SettingsView: View {
    @AppStorage("isDarkMode") private var isDarkMode = false
    @AppStorage("fontSize") private var fontSize = 14.0
    
    var body: some View {
        Form {
            Toggle("Dark Mode", isOn: $isDarkMode)
            Slider(value: $fontSize, in: 10...30)
            Text("Font Size: \(Int(fontSize))")
        }
    }
}

// 3. 保存复杂对象
struct User: Codable {
    let name: String
    let age: Int
    let email: String
}

extension UserDefaults {
    func setEncodable<T: Encodable>(_ value: T, forKey key: String) {
        if let data = try? JSONEncoder().encode(value) {
            set(data, forKey: key)
        }
    }
    
    func decodable<T: Decodable>(forKey key: String) -> T? {
        guard let data = data(forKey: key) else { return nil }
        return try? JSONDecoder().decode(T.self, from: data)
    }
}

let user = User(name: "Alice", age: 25, email: "alice@example.com")
UserDefaults.standard.setEncodable(user, forKey: "currentUser")
let savedUser: User? = UserDefaults.standard.decodable(forKey: "currentUser")
```

#### 文件系统
```swift
import Foundation

class FileManager {
    static let shared = FileManager()
    
    // 获取文档目录
    private func getDocumentsDirectory() -> URL {
        FileManager.default.urls(for: .documentDirectory, in: .userDomainMask)[0]
    }
    
    // 保存文件
    func save(_ data: Data, fileName: String) -> Bool {
        let fileURL = getDocumentsDirectory().appendingPathComponent(fileName)
        do {
            try data.write(to: fileURL)
            return true
        } catch {
            print("Error saving file: \(error)")
            return false
        }
    }
    
    // 读取文件
    func load(fileName: String) -> Data? {
        let fileURL = getDocumentsDirectory().appendingPathComponent(fileName)
        return try? Data(contentsOf: fileURL)
    }
    
    // 删除文件
    func delete(fileName: String) -> Bool {
        let fileURL = getDocumentsDirectory().appendingPathComponent(fileName)
        do {
            try FileManager.default.removeItem(at: fileURL)
            return true
        } catch {
            print("Error deleting file: \(error)")
            return false
        }
    }
    
    // 检查文件是否存在
    func fileExists(fileName: String) -> Bool {
        let fileURL = getDocumentsDirectory().appendingPathComponent(fileName)
        return FileManager.default.fileExists(atPath: fileURL.path)
    }
}

// 使用示例
struct Document: Codable {
    let title: String
    let content: String
}

let document = Document(title: "My Document", content: "Hello, World!")
if let data = try? JSONEncoder().encode(document) {
    FileManager.shared.save(data, fileName: "document.json")
}

if let loadedData = FileManager.shared.load(fileName: "document.json"),
   let loadedDocument = try? JSONDecoder().decode(Document.self, from: loadedData) {
    print(loadedDocument.title)
}
```

#### CoreData
```swift
import CoreData

// 1. 设置 Core Data Stack
class PersistenceController {
    static let shared = PersistenceController()
    
    let container: NSPersistentContainer
    
    init() {
        container = NSPersistentContainer(name: "Model")
        container.loadPersistentStores { description, error in
            if let error = error {
                fatalError("Unable to load persistent stores: \(error)")
            }
        }
    }
    
    var context: NSManagedObjectContext {
        return container.viewContext
    }
    
    func save() {
        let context = container.viewContext
        if context.hasChanges {
            do {
                try context.save()
            } catch {
                print("Error saving context: \(error)")
            }
        }
    }
}

// 2. 创建实体（假设已在 .xcdatamodeld 中定义 Person 实体）
extension PersistenceController {
    func createPerson(name: String, age: Int) {
        let person = Person(context: context)
        person.name = name
        person.age = Int16(age)
        person.id = UUID()
        save()
    }
    
    func fetchAllPersons() -> [Person] {
        let request: NSFetchRequest<Person> = Person.fetchRequest()
        do {
            return try context.fetch(request)
        } catch {
            print("Error fetching persons: \(error)")
            return []
        }
    }
    
    func deletePerson(_ person: Person) {
        context.delete(person)
        save()
    }
    
    func updatePerson(_ person: Person, name: String, age: Int) {
        person.name = name
        person.age = Int16(age)
        save()
    }
}

// 3. 在 SwiftUI 中使用
struct ContentView: View {
    @Environment(\.managedObjectContext) private var viewContext
    @FetchRequest(
        sortDescriptors: [NSSortDescriptor(keyPath: \Person.name, ascending: true)],
        animation: .default)
    private var persons: FetchedResults<Person>
    
    var body: some View {
        NavigationView {
            List {
                ForEach(persons) { person in
                    HStack {
                        Text(person.name ?? "Unknown")
                        Spacer()
                        Text("\(person.age)")
                    }
                }
                .onDelete(perform: deletePersons)
            }
            .navigationTitle("Persons")
            .toolbar {
                Button(action: addPerson) {
                    Label("Add", systemImage: "plus")
                }
            }
        }
    }
    
    private func addPerson() {
        withAnimation {
            PersistenceController.shared.createPerson(
                name: "New Person",
                age: 25
            )
        }
    }
    
    private func deletePersons(offsets: IndexSet) {
        withAnimation {
            offsets.map { persons[$0] }.forEach { person in
                PersistenceController.shared.deletePerson(person)
            }
        }
    }
}
```

### 并发编程
Swift 提供了现代化的并发编程模型。

#### async/await 基础
```swift
import Foundation

// 1. 基本 async 函数
func fetchData() async -> String {
    // 模拟网络延迟
    try? await Task.sleep(nanoseconds: 1_000_000_000)
    return "Data fetched"
}

// 调用 async 函数
Task {
    let data = await fetchData()
    print(data)
}

// 2. async throws
enum NetworkError: Error {
    case badURL
    case requestFailed
}

func fetchUserData(userID: Int) async throws -> User {
    guard userID > 0 else {
        throw NetworkError.badURL
    }
    
    try await Task.sleep(nanoseconds: 500_000_000)
    
    return User(name: "User \(userID)", age: 25, email: "user\(userID)@example.com")
}

// 使用 try await
Task {
    do {
        let user = try await fetchUserData(userID: 1)
        print("Fetched user: \(user.name)")
    } catch {
        print("Error: \(error)")
    }
}

// 3. 多个异步操作
func fetchMultipleData() async {
    // 顺序执行
    let data1 = await fetchData()
    let data2 = await fetchData()
    print("\(data1), \(data2)")
    
    // 并发执行
    async let asyncData1 = fetchData()
    async let asyncData2 = fetchData()
    let (result1, result2) = await (asyncData1, asyncData2)
    print("\(result1), \(result2)")
}
```

#### Task 和 TaskGroup
```swift
import Foundation

// 1. Task 基础
func startTask() {
    Task {
        let result = await fetchData()
        print("Task result: \(result)")
    }
    
    // 带优先级的 Task
    Task(priority: .high) {
        let result = await fetchData()
        print("High priority result: \(result)")
    }
}

// 2. 取消 Task
func cancellableTask() {
    let task = Task {
        for i in 1...10 {
            // 检查取消状态
            if Task.isCancelled {
                print("Task was cancelled")
                break
            }
            print("Working on step \(i)")
            try? await Task.sleep(nanoseconds: 500_000_000)
        }
    }
    
    // 取消任务
    DispatchQueue.main.asyncAfter(deadline: .now() + 2) {
        task.cancel()
    }
}

// 3. TaskGroup - 并发执行多个任务
func fetchMultipleUsers(userIDs: [Int]) async -> [User] {
    await withTaskGroup(of: User?.self) { group in
        for userID in userIDs {
            group.addTask {
                try? await fetchUserData(userID: userID)
            }
        }
        
        var users: [User] = []
        for await user in group {
            if let user = user {
                users.append(user)
            }
        }
        return users
    }
}

// 使用
Task {
    let users = await fetchMultipleUsers(userIDs: [1, 2, 3, 4, 5])
    print("Fetched \(users.count) users")
}

// 4. ThrowingTaskGroup
func fetchMultipleUsersWithErrors(userIDs: [Int]) async throws -> [User] {
    try await withThrowingTaskGroup(of: User.self) { group in
        for userID in userIDs {
            group.addTask {
                try await fetchUserData(userID: userID)
            }
        }
        
        var users: [User] = []
        for try await user in group {
            users.append(user)
        }
        return users
    }
}
```

#### Actor - 线程安全
```swift
import Foundation

// 1. Actor 基础
actor Counter {
    private var value = 0
    
    func increment() {
        value += 1
    }
    
    func getValue() -> Int {
        return value
    }
}

// 使用 Actor
let counter = Counter()
Task {
    await counter.increment()
    let value = await counter.getValue()
    print("Counter value: \(value)")
}

// 2. Actor 实际应用 - 缓存
actor Cache<Key: Hashable, Value> {
    private var storage: [Key: Value] = [:]
    
    func set(_ value: Value, forKey key: Key) {
        storage[key] = value
    }
    
    func get(_ key: Key) -> Value? {
        return storage[key]
    }
    
    func remove(_ key: Key) {
        storage.removeValue(forKey: key)
    }
    
    func clear() {
        storage.removeAll()
    }
}

// 使用缓存
let cache = Cache<String, String>()
Task {
    await cache.set("Hello", forKey: "greeting")
    if let value = await cache.get("greeting") {
        print("Cached value: \(value)")
    }
}

// 3. MainActor - UI 更新
@MainActor
class ViewModel: ObservableObject {
    @Published var data: String = ""
    
    func loadData() async {
        // 这个方法在主线程上运行
        let fetchedData = await fetchDataFromBackground()
        data = fetchedData  // UI 更新自动在主线程
    }
    
    nonisolated func fetchDataFromBackground() async -> String {
        // 这个方法可以在后台线程运行
        try? await Task.sleep(nanoseconds: 1_000_000_000)
        return "Background data"
    }
}

// 4. 异步序列（AsyncSequence）
struct AsyncNumberSequence: AsyncSequence {
    typealias Element = Int
    
    let range: ClosedRange<Int>
    
    struct AsyncIterator: AsyncIteratorProtocol {
        var current: Int
        let end: Int
        
        mutating func next() async -> Int? {
            guard current <= end else { return nil }
            try? await Task.sleep(nanoseconds: 500_000_000)
            defer { current += 1 }
            return current
        }
    }
    
    func makeAsyncIterator() -> AsyncIterator {
        AsyncIterator(current: range.lowerBound, end: range.upperBound)
    }
}

// 使用异步序列
Task {
    for await number in AsyncNumberSequence(range: 1...5) {
        print(number)
    }
}

// 5. 实际应用：网络请求
class NetworkManager {
    func fetchURL(_ urlString: String) async throws -> Data {
        guard let url = URL(string: urlString) else {
            throw NetworkError.badURL
        }
        
        let (data, response) = try await URLSession.shared.data(from: url)
        
        guard let httpResponse = response as? HTTPURLResponse,
              (200...299).contains(httpResponse.statusCode) else {
            throw NetworkError.requestFailed
        }
        
        return data
    }
    
    func fetchJSON<T: Decodable>(_ urlString: String, as type: T.Type) async throws -> T {
        let data = try await fetchURL(urlString)
        return try JSONDecoder().decode(T.self, from: data)
    }
}

// 使用
Task {
    let networkManager = NetworkManager()
    do {
        struct Post: Codable {
            let id: Int
            let title: String
        }
        
        let posts = try await networkManager.fetchJSON(
            "https://jsonplaceholder.typicode.com/posts",
            as: [Post].self
        )
        print("Fetched \(posts.count) posts")
    } catch {
        print("Error: \(error)")
    }
}
```

## 6. 实际代码示例
每个部分将附带相应的代码示例及其解释。

## 7. 最佳实践和编码规范

### Swift 编码风格指南

#### 命名规范
```swift
// 1. 类型命名：使用大驼峰命名法（UpperCamelCase）
class UserManager { }
struct NetworkRequest { }
enum HTTPMethod { }
protocol DataSource { }

// 2. 变量和函数命名：使用小驼峰命名法（lowerCamelCase）
var userName: String
func fetchUserData() { }
let maximumLoginAttempts = 3

// 3. 常量命名
let kMaximumNumberOfLoginAttempts = 3  // 避免使用 k 前缀
let MaximumNumberOfLoginAttempts = 3   // 推荐：使用大驼峰

// 4. 枚举命名
enum Direction {
    case north    // 使用小写，不是 North
    case south
    case east
    case west
}

// 5. 布尔值命名：使用 is, has, should 等前缀
var isEnabled: Bool
var hasData: Bool
var shouldRefresh: Bool

// 6. 避免缩写，使用完整单词
var userInfo: [String: Any]  // 好
var usrInf: [String: Any]    // 不好

// 7. 泛型类型参数命名
func map<Element, Result>(_ transform: (Element) -> Result) -> [Result]

// 8. 委托方法命名
protocol TableViewDelegate {
    func tableView(_ tableView: TableView, didSelectRowAt index: Int)
}
```

#### 代码组织
```swift
// 1. 使用 MARK 注释组织代码
class ViewController {
    
    // MARK: - Properties
    private var data: [String] = []
    
    // MARK: - Lifecycle
    override func viewDidLoad() {
        super.viewDidLoad()
        setupUI()
    }
    
    // MARK: - Setup
    private func setupUI() {
        // UI 设置代码
    }
    
    // MARK: - Actions
    @objc private func buttonTapped() {
        // 按钮点击处理
    }
    
    // MARK: - Private Methods
    private func fetchData() {
        // 数据获取逻辑
    }
}

// 2. 使用扩展分离功能
class DataManager {
    var data: [String] = []
}

// MARK: - Data Operations
extension DataManager {
    func addData(_ item: String) {
        data.append(item)
    }
    
    func removeData(at index: Int) {
        data.remove(at: index)
    }
}

// MARK: - Networking
extension DataManager {
    func fetchDataFromServer() async throws -> [String] {
        // 网络请求代码
        return []
    }
}

// 3. 协议一致性使用扩展
struct User {
    let name: String
    let age: Int
}

extension User: Equatable {
    static func == (lhs: User, rhs: User) -> Bool {
        return lhs.name == rhs.name && lhs.age == rhs.age
    }
}

extension User: CustomStringConvertible {
    var description: String {
        return "\(name), age \(age)"
    }
}
```

#### 代码风格
```swift
// 1. 缩进：使用 4 个空格，不使用 Tab
func example() {
    if condition {
        // 代码
    }
}

// 2. 大括号位置：K&R 风格
if condition {
    // 代码
} else {
    // 代码
}

// 3. 空格使用
let result = a + b       // 操作符周围有空格
let array = [1, 2, 3]    // 逗号后有空格
func method(param: Int)  // 冒号后有空格

// 4. 行长度：建议不超过 120 字符
let longString = "This is a very long string that should be broken " +
                 "into multiple lines for better readability"

// 5. 空行使用：相关代码组之间添加空行
func method1() {
    // 实现
}

func method2() {
    // 实现
}

// 6. 避免不必要的括号
if isValid {  // 好
    // 代码
}

if (isValid) {  // 不必要的括号
    // 代码
}

// 7. 尾随闭包
// 好
numbers.map { $0 * 2 }

// 不好
numbers.map({ $0 * 2 })
```

#### 类型推断和显式类型
```swift
// 1. 利用类型推断
let name = "John"           // 好：类型推断
let name: String = "John"   // 不必要的显式类型

// 2. 集合类型推断
let numbers = [1, 2, 3]     // 好
let numbers: [Int] = [1, 2, 3]  // 不必要

// 3. 空集合需要显式类型
var emptyArray: [Int] = []  // 必须
var emptyDict: [String: Int] = [:]  // 必须

// 4. 返回值类型始终显式声明
func calculateSum(a: Int, b: Int) -> Int {
    return a + b
}

// 5. 复杂表达式使用显式类型
let result: Double = Double(intValue) * 1.5 + offset
```

#### 可选值处理
```swift
// 1. 优先使用可选绑定
// 好
if let name = optionalName {
    print(name)
}

// 不好
if optionalName != nil {
    print(optionalName!)
}

// 2. 使用 guard 提前返回
func process(name: String?) {
    guard let name = name else {
        return
    }
    // 使用 name
}

// 3. 使用 nil 合并操作符
let userName = optionalName ?? "Guest"

// 4. 避免强制解包，除非确定不为 nil
let array = [1, 2, 3]
let first = array.first!  // 不好，可能崩溃
let first = array.first ?? 0  // 好

// 5. 可选链
let firstCharacter = optionalString?.first

// 6. 隐式解包可选值：仅在确定场景使用
class ViewController: UIViewController {
    @IBOutlet var label: UILabel!  // IB 连接可以使用
}
```

#### 访问控制
```swift
// 1. 默认使用最严格的访问级别
private var internalData: [String] = []

// 2. 公开 API 使用 public 或 open
public class NetworkManager {
    public func fetchData() { }
}

// 3. internal 是默认访问级别（可省略）
class InternalClass { }  // 默认 internal

// 4. 使用 fileprivate 限制在文件内访问
fileprivate func helperFunction() { }

// 5. 扩展中的访问控制
public struct User {
    private var name: String
    
    public init(name: String) {
        self.name = name
    }
}

extension User {
    public func greet() {
        print("Hello, \(name)")
    }
}
```

#### 错误处理最佳实践
```swift
// 1. 定义清晰的错误类型
enum NetworkError: Error {
    case invalidURL
    case noConnection
    case timeout
    case serverError(code: Int)
    case decodingFailed
}

// 2. 使用 do-catch 处理错误
func fetchData() {
    do {
        let data = try loadData()
        process(data)
    } catch NetworkError.invalidURL {
        print("Invalid URL")
    } catch NetworkError.noConnection {
        print("No connection")
    } catch {
        print("Unexpected error: \(error)")
    }
}

// 3. 使用 try? 当不关心错误时
let data = try? loadData()

// 4. 使用 try! 仅当确定不会失败时
let config = try! loadConfiguration()  // 应用启动时加载，失败就应该崩溃

// 5. 在函数签名中明确标注 throws
func processData() throws -> ProcessedData {
    // 可能抛出错误的代码
}
```

#### 内存管理
```swift
// 1. 避免循环引用：使用 weak 和 unowned
class ViewController {
    var onComplete: (() -> Void)?
    
    func setupClosure() {
        // 好：使用 weak self
        onComplete = { [weak self] in
            guard let self = self else { return }
            self.handleCompletion()
        }
        
        // 或使用 unowned（确定不会为 nil）
        onComplete = { [unowned self] in
            self.handleCompletion()
        }
    }
    
    func handleCompletion() { }
}

// 2. 委托使用 weak
protocol DataDelegate: AnyObject {
    func didReceiveData()
}

class DataManager {
    weak var delegate: DataDelegate?
}

// 3. 值类型优先
struct User {  // 值类型，自动管理内存
    var name: String
    var age: Int
}

// 4. 使用 deinit 清理资源
class DatabaseConnection {
    deinit {
        // 关闭数据库连接
        closeConnection()
    }
    
    func closeConnection() { }
}
```

### 常见错误及解决方法

#### 1. 可选值相关错误
```swift
// 错误：强制解包 nil 值
var name: String?
// print(name!)  // 崩溃！

// 解决方案：
if let name = name {
    print(name)
}

// 或使用 guard
guard let name = name else {
    print("Name is nil")
    return
}
print(name)

// 或使用 nil 合并
print(name ?? "Default Name")
```

#### 2. 数组越界
```swift
// 错误：
let array = [1, 2, 3]
// let item = array[5]  // 崩溃！

// 解决方案：安全访问
extension Collection {
    subscript(safe index: Index) -> Element? {
        return indices.contains(index) ? self[index] : nil
    }
}

let item = array[safe: 5] ?? 0
```

#### 3. 循环引用导致内存泄漏
```swift
// 错误：
class Parent {
    var child: Child?
}

class Child {
    var parent: Parent?  // 强引用循环
}

// 解决方案：
class Child {
    weak var parent: Parent?  // 使用 weak
}
```

#### 4. 在后台线程更新 UI
```swift
// 错误：
DispatchQueue.global().async {
    // self.label.text = "Updated"  // 崩溃或未定义行为
}

// 解决方案：
DispatchQueue.global().async {
    // 后台工作
    let result = processData()
    
    DispatchQueue.main.async {
        self.label.text = result  // 在主线程更新 UI
    }
}

// 或使用 MainActor
Task {
    let result = await processDataInBackground()
    await MainActor.run {
        self.label.text = result
    }
}
```

#### 5. 字典和数组的值类型语义
```swift
// 错误理解：
var dict1 = ["key": "value"]
var dict2 = dict1
dict2["key"] = "newValue"
// print(dict1["key"])  // "value" 而不是 "newValue"

// 说明：值类型会复制，不共享数据
```

#### 6. 闭包中的自引用
```swift
// 错误：
class ViewModel {
    var data: String = ""
    
    func loadData() {
        fetchData { result in
            self.data = result  // 可能的循环引用
        }
    }
}

// 解决方案：
func loadData() {
    fetchData { [weak self] result in
        self?.data = result
    }
}
```

#### 7. 异步操作的错误处理
```swift
// 错误：忽略异步错误
Task {
    let data = try await fetchData()  // 如果失败会崩溃
}

// 解决方案：
Task {
    do {
        let data = try await fetchData()
        // 处理数据
    } catch {
        print("Error: \(error)")
        // 错误处理
    }
}
```

#### 8. 字符串索引错误
```swift
// 错误：
let str = "Hello"
// let char = str[2]  // 编译错误

// 解决方案：
let index = str.index(str.startIndex, offsetBy: 2)
let char = str[index]

// 或创建扩展
extension String {
    subscript(offset: Int) -> Character {
        self[index(startIndex, offsetBy: offset)]
    }
}

let char = str[2]  // 'l'
```

#### 9. 类型转换错误
```swift
// 错误：强制类型转换
let obj: Any = "Hello"
// let str = obj as! Int  // 崩溃

// 解决方案：条件转换
if let str = obj as? String {
    print(str)
} else {
    print("Type conversion failed")
}

// 或使用 guard
guard let str = obj as? String else {
    print("Not a string")
    return
}
```

#### 10. SwiftUI 状态管理错误
```swift
// 错误：在视图中修改常量
struct ContentView: View {
    var count = 0  // 不会触发更新
    
    var body: some View {
        Button("Increment") {
            count += 1  // 编译错误
        }
    }
}

// 解决方案：使用 @State
struct ContentView: View {
    @State private var count = 0
    
    var body: some View {
        Button("Increment") {
            count += 1  // 正确
        }
    }
}
```

### 性能优化建议

#### 1. 集合操作优化
```swift
// 不好：多次遍历
let numbers = Array(1...1000)
let evenNumbers = numbers.filter { $0 % 2 == 0 }
let doubled = evenNumbers.map { $0 * 2 }
let sum = doubled.reduce(0, +)

// 好：链式调用，减少中间集合
let sum = numbers
    .filter { $0 % 2 == 0 }
    .map { $0 * 2 }
    .reduce(0, +)

// 更好：使用 lazy 避免中间集合
let sum = numbers
    .lazy
    .filter { $0 % 2 == 0 }
    .map { $0 * 2 }
    .reduce(0, +)
```

#### 2. 字符串拼接优化
```swift
// 不好：多次拼接
var result = ""
for i in 1...1000 {
    result += "Number \(i)\n"
}

// 好：使用数组 join
let result = (1...1000)
    .map { "Number \($0)" }
    .joined(separator: "\n")
```

#### 3. 视图优化
```swift
// SwiftUI 视图优化
struct OptimizedListView: View {
    let items: [Item]
    
    var body: some View {
        List {
            // 使用 LazyVStack 延迟加载
            LazyVStack {
                ForEach(items) { item in
                    ItemRow(item: item)
                        .id(item.id)  // 帮助 SwiftUI 识别视图
                }
            }
        }
    }
}

// 提取子视图避免重复计算
struct ItemRow: View {
    let item: Item
    
    var body: some View {
        HStack {
            Text(item.name)
            Spacer()
            Text("\(item.value)")
        }
    }
}
```

#### 4. 避免不必要的计算
```swift
// 不好：每次都计算
struct ContentView: View {
    var body: some View {
        Text("Total: \(calculateExpensiveValue())")
    }
    
    func calculateExpensiveValue() -> Int {
        // 复杂计算
        return (1...1000).reduce(0, +)
    }
}

// 好：缓存计算结果
struct ContentView: View {
    private let expensiveValue = (1...1000).reduce(0, +)
    
    var body: some View {
        Text("Total: \(expensiveValue)")
    }
}
```

### 代码审查清单

- [ ] 命名是否清晰且遵循规范
- [ ] 是否有不必要的强制解包
- [ ] 是否正确处理了可选值
- [ ] 是否有潜在的循环引用
- [ ] 访问控制是否合适
- [ ] 是否正确处理了错误
- [ ] 代码是否有适当的注释
- [ ] 是否遵循 DRY 原则（Don't Repeat Yourself）
- [ ] 函数是否单一职责
- [ ] 是否有单元测试覆盖
- [ ] 性能是否可以接受
- [ ] 是否考虑了边界情况
- [ ] UI 更新是否在主线程
- [ ] 资源是否正确释放

## 8. 现代特性
### 宏
宏是 Swift 中的一种新特性。

### 观察框架
观察框架用于处理数据变化。