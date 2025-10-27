# State Management in SwiftUI

## Introduction
State management is crucial in SwiftUI. It determines how your app stores and updates data, and how that data flows through your views.

## @State
Used for simple, view-local state that SwiftUI manages.

### Basic @State
```swift
struct CounterView: View {
    @State private var count = 0
    
    var body: some View {
        VStack {
            Text("Count: \(count)")
                .font(.largeTitle)
            
            HStack {
                Button("Increment") {
                    count += 1
                }
                
                Button("Decrement") {
                    count -= 1
                }
            }
        }
    }
}
```

### Multiple State Variables
```swift
struct FormView: View {
    @State private var name = ""
    @State private var age = 18
    @State private var isStudent = false
    
    var body: some View {
        Form {
            TextField("Name", text: $name)
            
            Stepper("Age: \(age)", value: $age, in: 0...120)
            
            Toggle("Student", isOn: $isStudent)
            
            Section {
                Text("Name: \(name)")
                Text("Age: \(age)")
                Text("Student: \(isStudent ? "Yes" : "No")")
            }
        }
    }
}
```

## @Binding
Used to create a two-way connection between views.

### Parent-Child Binding
```swift
struct ParentView: View {
    @State private var isOn = false
    
    var body: some View {
        VStack {
            Text("Switch is \(isOn ? "ON" : "OFF")")
                .font(.title)
            
            ToggleView(isOn: $isOn)
        }
    }
}

struct ToggleView: View {
    @Binding var isOn: Bool
    
    var body: some View {
        Toggle("Toggle Switch", isOn: $isOn)
            .padding()
    }
}
```

### Custom Binding Component
```swift
struct ColorPickerView: View {
    @Binding var selectedColor: Color
    
    let colors: [Color] = [.red, .blue, .green, .yellow, .purple]
    
    var body: some View {
        HStack {
            ForEach(colors, id: \.self) { color in
                Circle()
                    .fill(color)
                    .frame(width: 50, height: 50)
                    .overlay(
                        Circle()
                            .stroke(selectedColor == color ? Color.black : Color.clear, lineWidth: 3)
                    )
                    .onTapGesture {
                        selectedColor = color
                    }
            }
        }
    }
}

struct ColorDemoView: View {
    @State private var backgroundColor = Color.red
    
    var body: some View {
        VStack {
            Rectangle()
                .fill(backgroundColor)
                .frame(height: 200)
                .cornerRadius(10)
            
            ColorPickerView(selectedColor: $backgroundColor)
        }
        .padding()
    }
}
```

## @ObservedObject
Used for external reference types that conform to ObservableObject.

### Basic ObservableObject
```swift
class UserSettings: ObservableObject {
    @Published var username = ""
    @Published var isLoggedIn = false
    @Published var notifications = true
}

struct SettingsView: View {
    @ObservedObject var settings = UserSettings()
    
    var body: some View {
        Form {
            TextField("Username", text: $settings.username)
            Toggle("Logged In", isOn: $settings.isLoggedIn)
            Toggle("Notifications", isOn: $settings.notifications)
        }
    }
}
```

### Shared ObservableObject
```swift
class ShoppingCart: ObservableObject {
    @Published var items: [String] = []
    
    var itemCount: Int {
        items.count
    }
    
    func addItem(_ item: String) {
        items.append(item)
    }
    
    func removeItem(at index: Int) {
        items.remove(at: index)
    }
}

struct ShoppingView: View {
    @ObservedObject var cart = ShoppingCart()
    @State private var newItem = ""
    
    var body: some View {
        VStack {
            HStack {
                TextField("Add item", text: $newItem)
                    .textFieldStyle(RoundedBorderTextFieldStyle())
                
                Button("Add") {
                    cart.addItem(newItem)
                    newItem = ""
                }
                .disabled(newItem.isEmpty)
            }
            .padding()
            
            List {
                ForEach(cart.items.indices, id: \.self) { index in
                    Text(cart.items[index])
                }
                .onDelete { indexSet in
                    indexSet.forEach { cart.removeItem(at: $0) }
                }
            }
            
            Text("Total items: \(cart.itemCount)")
                .font(.headline)
                .padding()
        }
    }
}
```

## @StateObject
Used to create and own an ObservableObject. The view owns the object.

### StateObject vs ObservedObject
```swift
class Timer: ObservableObject {
    @Published var currentTime = Date()
    
    init() {
        Timer.scheduledTimer(withTimeInterval: 1.0, repeats: true) { _ in
            self.currentTime = Date()
        }
    }
}

struct TimerView: View {
    // Use @StateObject when the view creates and owns the object
    @StateObject private var timer = Timer()
    
    var body: some View {
        Text("Current time: \(timer.currentTime)")
    }
}
```

## @EnvironmentObject
Used to share data across many views without passing it explicitly.

### Setting up EnvironmentObject
```swift
class AppState: ObservableObject {
    @Published var isLoggedIn = false
    @Published var username = "Guest"
    @Published var theme = "Light"
}

// In your App file
@main
struct MyApp: App {
    @StateObject private var appState = AppState()
    
    var body: some Scene {
        WindowGroup {
            ContentView()
                .environmentObject(appState)
        }
    }
}

// In any view
struct ContentView: View {
    @EnvironmentObject var appState: AppState
    
    var body: some View {
        VStack {
            Text("Welcome, \(appState.username)")
            
            if appState.isLoggedIn {
                Button("Logout") {
                    appState.isLoggedIn = false
                    appState.username = "Guest"
                }
            } else {
                LoginView()
            }
        }
    }
}

struct LoginView: View {
    @EnvironmentObject var appState: AppState
    @State private var username = ""
    
    var body: some View {
        VStack {
            TextField("Username", text: $username)
                .textFieldStyle(RoundedBorderTextFieldStyle())
                .padding()
            
            Button("Login") {
                appState.username = username
                appState.isLoggedIn = true
            }
        }
    }
}
```

## @Environment
Access system-wide settings and values.

### Common Environment Values
```swift
struct EnvironmentExampleView: View {
    @Environment(\.colorScheme) var colorScheme
    @Environment(\.dismiss) var dismiss
    
    var body: some View {
        VStack {
            Text("Current scheme: \(colorScheme == .dark ? "Dark" : "Light")")
            
            Button("Dismiss") {
                dismiss()
            }
        }
    }
}
```

## Practical Example: Complete App with State Management

```swift
// Data Model
struct Task: Identifiable, Codable {
    let id = UUID()
    var title: String
    var isCompleted: Bool
    var priority: Priority
    
    enum Priority: String, Codable, CaseIterable {
        case low = "Low"
        case medium = "Medium"
        case high = "High"
    }
}

// ViewModel
class TaskManager: ObservableObject {
    @Published var tasks: [Task] = []
    
    func addTask(_ task: Task) {
        tasks.append(task)
    }
    
    func removeTask(at indexSet: IndexSet) {
        tasks.remove(atOffsets: indexSet)
    }
    
    func toggleComplete(for task: Task) {
        if let index = tasks.firstIndex(where: { $0.id == task.id }) {
            tasks[index].isCompleted.toggle()
        }
    }
    
    var incompleteTasks: [Task] {
        tasks.filter { !$0.isCompleted }
    }
    
    var completedTasks: [Task] {
        tasks.filter { $0.isCompleted }
    }
}

// Main View
struct TaskListView: View {
    @StateObject private var taskManager = TaskManager()
    @State private var showingAddTask = false
    
    var body: some View {
        NavigationView {
            List {
                Section(header: Text("Incomplete")) {
                    ForEach(taskManager.incompleteTasks) { task in
                        TaskRowView(task: task, taskManager: taskManager)
                    }
                }
                
                Section(header: Text("Completed")) {
                    ForEach(taskManager.completedTasks) { task in
                        TaskRowView(task: task, taskManager: taskManager)
                    }
                }
                .onDelete(perform: taskManager.removeTask)
            }
            .navigationTitle("Tasks")
            .toolbar {
                Button(action: { showingAddTask = true }) {
                    Image(systemName: "plus")
                }
            }
            .sheet(isPresented: $showingAddTask) {
                AddTaskView(taskManager: taskManager)
            }
        }
    }
}

// Row View
struct TaskRowView: View {
    let task: Task
    @ObservedObject var taskManager: TaskManager
    
    var priorityColor: Color {
        switch task.priority {
        case .low: return .green
        case .medium: return .orange
        case .high: return .red
        }
    }
    
    var body: some View {
        HStack {
            Button(action: {
                taskManager.toggleComplete(for: task)
            }) {
                Image(systemName: task.isCompleted ? "checkmark.circle.fill" : "circle")
                    .foregroundColor(task.isCompleted ? .green : .gray)
            }
            
            VStack(alignment: .leading) {
                Text(task.title)
                    .strikethrough(task.isCompleted)
                
                Text(task.priority.rawValue)
                    .font(.caption)
                    .foregroundColor(priorityColor)
            }
        }
    }
}

// Add Task View
struct AddTaskView: View {
    @ObservedObject var taskManager: TaskManager
    @Environment(\.dismiss) var dismiss
    
    @State private var title = ""
    @State private var priority: Task.Priority = .medium
    
    var body: some View {
        NavigationView {
            Form {
                TextField("Task title", text: $title)
                
                Picker("Priority", selection: $priority) {
                    ForEach(Task.Priority.allCases, id: \.self) { priority in
                        Text(priority.rawValue)
                    }
                }
            }
            .navigationTitle("New Task")
            .toolbar {
                ToolbarItem(placement: .cancellationAction) {
                    Button("Cancel") {
                        dismiss()
                    }
                }
                
                ToolbarItem(placement: .confirmationAction) {
                    Button("Add") {
                        let task = Task(title: title, isCompleted: false, priority: priority)
                        taskManager.addTask(task)
                        dismiss()
                    }
                    .disabled(title.isEmpty)
                }
            }
        }
    }
}
```

## Best Practices
1. Use `@State` for view-local, simple value types
2. Use `@StateObject` when creating and owning an `ObservableObject`
3. Use `@ObservedObject` when observing an object created elsewhere
4. Use `@EnvironmentObject` for app-wide shared state
5. Use `@Binding` to create two-way connections
6. Keep state as minimal as possible
7. Lift state up when multiple views need to share it

## Practice Exercises
1. Create a settings screen with multiple @State variables
2. Build a form that uses @Binding to connect parent and child views
3. Create an ObservableObject for a user profile
4. Build a multi-view app that uses @EnvironmentObject for shared state
