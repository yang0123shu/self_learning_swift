# SwiftUI 基础教程

## 1. SwiftUI 概述
SwiftUI 是一个声明式的用户界面框架，可以让我们以简单的方式构建复杂的用户界面。它与 Swift 语言紧密集成，使得构建应用变得更加高效。

## 2. 视图（Views）
### 2.1 Text
```swift
Text("Hello, SwiftUI!") // 显示文本
```

### 2.2 Image
```swift
Image("exampleImage") // 显示图片
```

### 2.3 Button
```swift
Button(action: {
    print("Button tapped!")
}) {
    Text("Tap me") // 按钮文本
}
```

### 2.4 TextField
```swift
@State private var userInput: String = ""

TextField("Enter something", text: $userInput) // 输入文本框
```

### 2.5 List
```swift
List { 
    Text("Item 1")
    Text("Item 2")
} // 列表显示
```

## 3. 布局（Layout）
### 3.1 VStack
```swift
VStack {
    Text("First")
    Text("Second")
} // 竖直布局
```

### 3.2 HStack
```swift
HStack {
    Text("Left")
    Text("Right")
} // 水平布局
```

### 3.3 ZStack
```swift
ZStack {
    Image("background")
    Text("Foreground")
} // 叠加布局
```

### 3.4 Grid
```swift
LazyVGrid(columns: [GridItem(), GridItem()]) {
    Text("Grid Item 1")
    Text("Grid Item 2")
} // 网格布局
```

## 4. 状态管理（State Management）
### 4.1 @State
```swift
@State private var count: Int = 0 // 管理视图状态
```

### 4.2 @Binding
```swift
struct ChildView: View {
    @Binding var value: String
}
```

### 4.3 @StateObject
```swift
class Model: ObservableObject {
    @Published var data: String = ""
}

@StateObject var model = Model() // 创建可观察对象
```

### 4.4 @ObservedObject
```swift
struct ContentView: View {
    @ObservedObject var model: Model
}
```

### 4.5 @EnvironmentObject
```swift
class UserSettings: ObservableObject {
    @Published var username: String = ""
}

@EnvironmentObject var settings: UserSettings // 共享状态
```

## 5. 修饰符（Modifiers）
```swift
Text("Hello, World!")
    .font(.largeTitle) // 应用字体修饰符
    .foregroundColor(.blue) // 应用颜色修饰符
```

## 6. 导航模式（Navigation Patterns）
```swift
NavigationView {
    NavigationLink(destination: DetailView()) {
        Text("Go to Detail")
    }
}
```

## 7. 表单（Forms）
```swift
Form {
    TextField("Username", text: $username)
    SecureField("Password", text: $password)
    Button("Submit") {
        // 提交动作
    }
}
```

## 8. 带搜索和过滤的列表（Lists with Search and Filter）
```swift
@State private var searchText: String = ""

List(filteredItems) { item in
    Text(item)
}
.searchable(text: $searchText)
```

## 9. 自定义组件（Custom Components）
```swift
struct CustomButton: View {
    var body: some View {
        Button(action: {}) {
            Text("Custom Button")
        }
    }
}
```

## 10. 真实世界示例（Real-World Examples）
### 10.1 登录表单（Login Form）
```swift
struct LoginView: View {
    @State private var username: String = ""
    @State private var password: String = ""

    var body: some View {
        Form {
            TextField("Username", text: $username)
            SecureField("Password", text: $password)
            Button("Login") {
                // 登录逻辑
            }
        }
    }
}
```

### 10.2 用户资料（User Profile）
```swift
struct ProfileView: View {
    @State private var name: String = ""

    var body: some View {
        VStack {
            TextField("Name", text: $name)
            // 更多用户资料
        }
    }
}
```

### 10.3 购物清单（Shopping List）
```swift
struct ShoppingListView: View {
    @State private var items: [String] = []

    var body: some View {
        List {
            ForEach(items, id: \.self) { item in
                Text(item)
            }
        }
    }
}
```

### 10.4 设置屏幕（Settings Screen）
```swift
struct SettingsView: View {
    @State private var notificationsEnabled: Bool = true

    var body: some View {
        Toggle(isOn: $notificationsEnabled) {
            Text("Enable Notifications")
        }
    }
}
```

---
以上是一个全面的 SwiftUI 基础教程，涵盖了多种视图、布局、状态管理等内容，并附有真实世界的示例和详细的中文注释。