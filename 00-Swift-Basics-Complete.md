# Swift Basics Tutorial

## 1. 变量和常量
在Swift中，变量用`var`声明，而常量用`let`声明。示例如下：

```swift
let pi = 3.14 // 常量，圆周率
var radius: Double = 5.0 // 变量，半径
```

## 2. 数据类型
Swift支持多种数据类型，包括`Int`、`Double`、`String`等。以下是一些实际使用案例：

### 字符串操作
```swift
let userInput: String = "123"
if let number = Int(userInput) {
    print("用户输入的数字是：\(number)")
} else {
    print("无效的输入")
}
```

### 数字格式化
```swift
let price: Double = 19.99
let formattedPrice = String(format: "%.2f", price)
print("价格：$\(formattedPrice)")
}
```

### 集合管理
```swift
var fruits: [String] = ["苹果", "香蕉", "橘子"]
fruits.append("桃子")
print(fruits)
```

## 3. 运算符
运算符用于执行数学计算和逻辑判断。以下是一个简单的计算器应用示例：

```swift
func calculate(_ a: Double, _ b: Double, operation: (Double, Double) -> Double) -> Double {
    return operation(a, b)
}

let result = calculate(5, 3, operation: +)
print("结果：\(result)") // 输出：结果：8.0
```

## 4. 控制流
控制流语句用于控制程序的执行。以下是一个身份验证逻辑的示例：

```swift
let username = "user"
let password = "password"

if username == "user" && password == "password" {
    print("登录成功")
} else {
    print("登录失败")
}
```

## 5. 函数
函数是执行特定任务的代码块。以下是一个API助手的示例：

```swift
func fetchData(url: String, completion: @escaping (Data?) -> Void) {
    let url = URL(string: url)! 
    let task = URLSession.shared.dataTask(with: url) { data, response, error in
        completion(data)
    }
    task.resume()
}

fetchData(url: "https://api.example.com/data") { data in
    // 处理数据
}
```

## 6. 闭包
闭包是一种自包含的代码块，可以在代码中传递和使用。以下是网络请求回调和UI事件处理的示例：

```swift
let completionHandler: (String) -> Void = { result in
    print("结果：\(result)")
}

completionHandler("成功")
```

## 7. 可选类型
可选类型用于处理可能缺失的值。以下是安全数据处理模式的示例：

```swift
var optionalName: String? = "John"
if let name = optionalName {
    print("名字是：\(name)")
} else {
    print("没有名字")
}
```

## 8. 枚举
枚举类型用于定义一组相关值。以下是应用状态管理的示例：

```swift
enum AppState {
    case active
    case inactive
    case background
}

var currentState = AppState.active
```

## 9. 结构体与类
结构体和类用于定义数据模型。以下是模型示例：

```swift
struct User {
    var name: String
    var age: Int
}

let user = User(name: "Alice", age: 30)
print("用户：\(user.name), 年龄：\(user.age)")
```

## 10. 属性
属性用于存储对象的状态。以下是验证逻辑的示例：

```swift
class Product {
    var price: Double {
        didSet {
            if price < 0 {
                price = 0
            }
        }
    }
    init(price: Double) {
        self.price = price
    }
}

let product = Product(price: 10.0)
product.price = -5.0 // 价格将被设置为0
```

## 11. 方法
方法是结构体和类内部的函数。以下是业务逻辑示例：

```swift
class Calculator {
    func add(_ a: Double, _ b: Double) -> Double {
        return a + b
    }
}

let calculator = Calculator()
print("结果：\(calculator.add(5, 3))") // 输出：结果：8.0
```

## 12. 初始化
初始化用于创建对象。以下是依赖注入的示例：

```swift
class Service {
    init() {}
}

class ViewModel {
    var service: Service
    init(service: Service) {
        self.service = service
    }
}
```

## 13. 错误处理
错误处理用于处理运行时错误。以下是网络请求的示例：

```swift
enum NetworkError: Error {
    case badURL
    case requestFailed
}

func fetch(url: String) throws {
    guard let _ = URL(string: url) else {
        throw NetworkError.badURL
    }
    // 网络请求逻辑
}
```

