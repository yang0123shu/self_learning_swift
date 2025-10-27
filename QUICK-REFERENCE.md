# Swift & SwiftUI Quick Reference Guide

A quick reference for common Swift and SwiftUI patterns and syntax.

## Swift Quick Reference

### Variables and Constants
```swift
var changeable = 42          // Variable
let constant = 42            // Constant (preferred)
var explicit: Int = 42       // With type annotation
```

### Common Data Types
```swift
let number: Int = 42
let decimal: Double = 3.14
let text: String = "Hello"
let flag: Bool = true
let items: [String] = ["A", "B", "C"]
let dict: [String: Int] = ["age": 25]
let unique: Set<Int> = [1, 2, 3]
```

### Optionals
```swift
var optional: String? = "value"
var optional: String? = nil

// Unwrapping
if let value = optional {
    print(value)
}

// Nil coalescing
let result = optional ?? "default"

// Force unwrap (use carefully!)
let value = optional!
```

### Control Flow
```swift
// If
if condition {
    // code
} else if otherCondition {
    // code
} else {
    // code
}

// Switch
switch value {
case 1:
    print("One")
case 2...5:
    print("Two to Five")
default:
    print("Other")
}

// For loop
for item in items {
    print(item)
}

for i in 0..<5 {
    print(i)
}

// While
while condition {
    // code
}
```

### Functions
```swift
// Basic function
func greet(name: String) -> String {
    return "Hello, \(name)"
}

// No parameters
func sayHello() {
    print("Hello")
}

// Multiple parameters
func add(_ a: Int, _ b: Int) -> Int {
    return a + b
}

// Default parameters
func greet(name: String = "Guest") {
    print("Hello, \(name)")
}
```

### Classes and Structs
```swift
// Struct (value type)
struct Person {
    var name: String
    var age: Int
    
    func introduce() {
        print("Hi, I'm \(name)")
    }
}

// Class (reference type)
class Animal {
    var name: String
    
    init(name: String) {
        self.name = name
    }
    
    func makeSound() {
        print("Some sound")
    }
}

// Inheritance
class Dog: Animal {
    override func makeSound() {
        print("Woof!")
    }
}
```

### Closures
```swift
// Basic closure
let greet = { (name: String) -> String in
    return "Hello, \(name)"
}

// Array operations
let numbers = [1, 2, 3, 4, 5]
let doubled = numbers.map { $0 * 2 }
let evens = numbers.filter { $0 % 2 == 0 }
let sum = numbers.reduce(0, +)
```

## SwiftUI Quick Reference

### Basic Views
```swift
Text("Hello")
    .font(.title)
    .foregroundColor(.blue)

Image(systemName: "star.fill")
    .font(.largeTitle)

Button("Click Me") {
    // action
}

TextField("Placeholder", text: $text)

Toggle("Switch", isOn: $isOn)

Slider(value: $value, in: 0...100)
```

### Layout
```swift
// Vertical stack
VStack(spacing: 10) {
    Text("First")
    Text("Second")
}

// Horizontal stack
HStack(alignment: .top) {
    Text("Left")
    Text("Right")
}

// Depth stack
ZStack {
    Rectangle()
    Text("On top")
}

// Spacer
HStack {
    Text("Left")
    Spacer()
    Text("Right")
}
```

### State Management
```swift
// Local state
@State private var count = 0

// Binding (parent-child)
@Binding var value: String

// Observable object
class ViewModel: ObservableObject {
    @Published var items: [String] = []
}

@StateObject private var viewModel = ViewModel()
@ObservedObject var viewModel: ViewModel
@EnvironmentObject var appState: AppState
```

### Lists
```swift
List {
    ForEach(items) { item in
        Text(item.name)
    }
    .onDelete(perform: delete)
}

List(items) { item in
    NavigationLink(destination: DetailView()) {
        Text(item.name)
    }
}
```

### Navigation
```swift
NavigationView {
    List {
        NavigationLink("Detail") {
            DetailView()
        }
    }
    .navigationTitle("Main")
}
```

### Common Modifiers
```swift
.padding()
.padding(.horizontal, 20)
.background(Color.blue)
.foregroundColor(.white)
.cornerRadius(10)
.shadow(radius: 5)
.frame(width: 100, height: 100)
.frame(maxWidth: .infinity)
.opacity(0.5)
.offset(x: 10, y: 20)
.rotationEffect(.degrees(45))
.scaleEffect(1.5)
```

### Sheets and Alerts
```swift
.sheet(isPresented: $showSheet) {
    SheetView()
}

.alert("Title", isPresented: $showAlert) {
    Button("OK") { }
}
```

### Conditional Views
```swift
if condition {
    Text("Shown when true")
}

if let value = optional {
    Text(value)
} else {
    Text("No value")
}

condition ? Text("True") : Text("False")
```

## Common Patterns

### MVVM Pattern
```swift
// Model
struct Item: Identifiable {
    let id = UUID()
    var name: String
}

// ViewModel
class ItemViewModel: ObservableObject {
    @Published var items: [Item] = []
    
    func addItem(_ item: Item) {
        items.append(item)
    }
}

// View
struct ItemListView: View {
    @StateObject private var viewModel = ItemViewModel()
    
    var body: some View {
        List(viewModel.items) { item in
            Text(item.name)
        }
    }
}
```

### Async/Await
```swift
func fetchData() async throws -> Data {
    let url = URL(string: "https://api.example.com")!
    let (data, _) = try await URLSession.shared.data(from: url)
    return data
}

// In SwiftUI
.task {
    await viewModel.loadData()
}
```

### Error Handling
```swift
enum NetworkError: Error {
    case invalidURL
    case noData
}

do {
    let data = try fetchData()
} catch {
    print("Error: \(error)")
}
```

## Keyboard Shortcuts (Xcode)

- **⌘ + B** - Build
- **⌘ + R** - Run
- **⌘ + .** - Stop
- **⌘ + /** - Comment/Uncomment
- **⌘ + Shift + L** - Show Library
- **⌘ + Shift + O** - Quick Open
- **⌘ + Click** - Jump to Definition
- **⌥ + Click** - Show Quick Help
- **⌘ + Shift + A** - Show Actions
- **⌘ + Option + [** - Move Line Up
- **⌘ + Option + ]** - Move Line Down

## Debugging Tips

```swift
// Print debugging
print("Value: \(variable)")
dump(complexObject)

// Debug view boundaries
.border(Color.red)

// Debug state changes
.onChange(of: value) { newValue in
    print("Changed to: \(newValue)")
}

// Preview with different states
struct ContentView_Previews: PreviewProvider {
    static var previews: some View {
        Group {
            ContentView()
                .preferredColorScheme(.light)
            ContentView()
                .preferredColorScheme(.dark)
        }
    }
}
```

## Best Practices

### Swift
- Use `let` instead of `var` when possible
- Prefer value types (structs) over reference types (classes)
- Use descriptive names for variables and functions
- Handle optionals safely
- Keep functions small and focused

### SwiftUI
- Extract complex views into separate components
- Use `@State` for simple local state
- Use `@StateObject` for owned objects
- Keep view models separate from views
- Use computed properties for derived state
- Extract repeated code into custom modifiers

## Resources

- [Swift.org Documentation](https://swift.org/documentation/)
- [SwiftUI Documentation](https://developer.apple.com/documentation/swiftui/)
- [Hacking with Swift](https://www.hackingwithswift.com/)
- [Swift Forums](https://forums.swift.org/)

---

This is a quick reference. For detailed explanations, refer to the main tutorial sections.
