# SwiftUI 基础完整教程

## 1. 介绍
SwiftUI 是 Apple 提供的用于构建用户界面的框架，它具有声明式语法，易于学习。

## 2. 视图
### Text
```swift
Text("Hello, SwiftUI!")
    .font(.largeTitle) // 设置字体为大标题
    .foregroundColor(.blue) // 设置字体颜色为蓝色
```

### Image
```swift
Image("exampleImage")
    .resizable() // 使图片可调整大小
    .scaledToFit() // 保持图片比例
```

### Button
```swift
Button(action: {
    print("Button tapped")
}) {
    Text("Click Me")
}
```

### TextField
```swift
@State private var name: String = ""

TextField("Enter your name", text: $name)
    .padding()
    .border(Color.gray)
```

## 3. 布局
### VStack
```swift
VStack {
    Text("Hello")
    Text("World")
}
```

### HStack
```swift
HStack {
    Text("Left")
    Spacer()
    Text("Right")
}
```

### ZStack
```swift
ZStack {
    Image("background")
    Text("Hello, SwiftUI!").foregroundColor(.white)
}
```

### Spacer
```swift
HStack {
    Text("Start")
    Spacer()
    Text("End")
}
```

### Divider
```swift
Divider()
    .padding()
```

## 4. 状态管理
### @State
```swift
@State private var count: Int = 0

Button(action: {
    count += 1
}) {
    Text("Count: \(count)")
}
```

### @Binding
```swift
struct ChildView: View {
    @Binding var value: String
}
```

### @StateObject
```swift
class ViewModel: ObservableObject {
    @Published var data: String = ""
}

@StateObject var viewModel = ViewModel()
```

### @ObservedObject
```swift
struct ContentView: View {
    @ObservedObject var viewModel: ViewModel
}
```

### @EnvironmentObject
```swift
struct ParentView: View {
    @EnvironmentObject var viewModel: ViewModel
}
```

## 5. 列表和导航
```swift
List(0..<5) { index in
    Text("Item \(index)")
}
```

## 6. 表单和输入
```swift
Form {
    TextField("Name", text: $name)
}
```

## 7. 修饰符和样式
```swift
Text("Styled Text")
    .font(.headline)
    .padding()
```

## 8. 动画
```swift
withAnimation {
    self.isVisible.toggle()
}
```

## 9. 手势
```swift
.onTapGesture {
    print("Tapped!")
}
```

## 10. 警告和表单
```swift
.alert(isPresented: $showAlert) {
    Alert(title: Text("Alert"))
}
```

## 11. TabView 和 NavigationView
### TabView
```swift
TabView {
    Text("First Tab")
        .tabItem { Text("Tab 1") }
}
```

### NavigationView
```swift
NavigationView {
    NavigationLink(destination: Text("Detail View")) {
        Text("Go to Detail")
    }
}
```

## 12. 总结
SwiftUI 提供了强大的功能来构建现代应用程序，鼓励开发者使用声明式编程。