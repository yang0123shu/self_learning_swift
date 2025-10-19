# Todo List App - SwiftUI Example Project

## Project Overview
A fully functional todo list app that demonstrates state management, lists, navigation, and data manipulation in SwiftUI.

## What You'll Learn
- @State and @StateObject
- List with ForEach
- Navigation
- Add, delete, and edit operations
- Custom data models
- Form handling

## Complete Code

```swift
import SwiftUI

// MARK: - Data Model
struct TodoItem: Identifiable, Codable {
    let id = UUID()
    var title: String
    var isCompleted: Bool
    var createdDate: Date
    var priority: Priority
    
    enum Priority: String, Codable, CaseIterable {
        case low = "Low"
        case medium = "Medium"
        case high = "High"
        
        var color: Color {
            switch self {
            case .low: return .green
            case .medium: return .orange
            case .high: return .red
            }
        }
    }
}

// MARK: - ViewModel
class TodoViewModel: ObservableObject {
    @Published var todos: [TodoItem] = []
    
    init() {
        // Load sample data
        loadSampleData()
    }
    
    func loadSampleData() {
        todos = [
            TodoItem(title: "Buy groceries", isCompleted: false, createdDate: Date(), priority: .medium),
            TodoItem(title: "Walk the dog", isCompleted: true, createdDate: Date(), priority: .low),
            TodoItem(title: "Finish project", isCompleted: false, createdDate: Date(), priority: .high)
        ]
    }
    
    func addTodo(_ todo: TodoItem) {
        todos.insert(todo, at: 0)
    }
    
    func deleteTodo(at indexSet: IndexSet) {
        todos.remove(atOffsets: indexSet)
    }
    
    func toggleComplete(_ todo: TodoItem) {
        if let index = todos.firstIndex(where: { $0.id == todo.id }) {
            todos[index].isCompleted.toggle()
        }
    }
    
    var activeTodos: [TodoItem] {
        todos.filter { !$0.isCompleted }
    }
    
    var completedTodos: [TodoItem] {
        todos.filter { $0.isCompleted }
    }
}

// MARK: - Main View
struct TodoListView: View {
    @StateObject private var viewModel = TodoViewModel()
    @State private var showingAddTodo = false
    
    var body: some View {
        NavigationView {
            List {
                // Active Todos
                if !viewModel.activeTodos.isEmpty {
                    Section(header: Text("Active")) {
                        ForEach(viewModel.activeTodos) { todo in
                            TodoRowView(todo: todo, viewModel: viewModel)
                        }
                    }
                }
                
                // Completed Todos
                if !viewModel.completedTodos.isEmpty {
                    Section(header: Text("Completed")) {
                        ForEach(viewModel.completedTodos) { todo in
                            TodoRowView(todo: todo, viewModel: viewModel)
                        }
                        .onDelete(perform: viewModel.deleteTodo)
                    }
                }
                
                if viewModel.todos.isEmpty {
                    Section {
                        Text("No todos yet")
                            .foregroundColor(.gray)
                            .italic()
                    }
                }
            }
            .navigationTitle("My Todos")
            .toolbar {
                ToolbarItem(placement: .navigationBarTrailing) {
                    Button(action: {
                        showingAddTodo = true
                    }) {
                        Image(systemName: "plus")
                    }
                }
                
                ToolbarItem(placement: .navigationBarLeading) {
                    EditButton()
                }
            }
            .sheet(isPresented: $showingAddTodo) {
                AddTodoView(viewModel: viewModel)
            }
        }
    }
}

// MARK: - Todo Row View
struct TodoRowView: View {
    let todo: TodoItem
    @ObservedObject var viewModel: TodoViewModel
    
    var body: some View {
        HStack {
            Button(action: {
                viewModel.toggleComplete(todo)
            }) {
                Image(systemName: todo.isCompleted ? "checkmark.circle.fill" : "circle")
                    .foregroundColor(todo.isCompleted ? .green : .gray)
                    .font(.title3)
            }
            .buttonStyle(PlainButtonStyle())
            
            VStack(alignment: .leading, spacing: 4) {
                Text(todo.title)
                    .strikethrough(todo.isCompleted)
                    .foregroundColor(todo.isCompleted ? .gray : .primary)
                
                HStack {
                    Label(todo.priority.rawValue, systemImage: "flag.fill")
                        .font(.caption)
                        .foregroundColor(todo.priority.color)
                    
                    Spacer()
                    
                    Text(todo.createdDate, style: .date)
                        .font(.caption)
                        .foregroundColor(.gray)
                }
            }
        }
        .padding(.vertical, 4)
    }
}

// MARK: - Add Todo View
struct AddTodoView: View {
    @ObservedObject var viewModel: TodoViewModel
    @Environment(\.dismiss) var dismiss
    
    @State private var title = ""
    @State private var priority: TodoItem.Priority = .medium
    
    var body: some View {
        NavigationView {
            Form {
                Section(header: Text("Todo Details")) {
                    TextField("What needs to be done?", text: $title)
                    
                    Picker("Priority", selection: $priority) {
                        ForEach(TodoItem.Priority.allCases, id: \.self) { priority in
                            HStack {
                                Image(systemName: "flag.fill")
                                    .foregroundColor(priority.color)
                                Text(priority.rawValue)
                            }
                            .tag(priority)
                        }
                    }
                }
                
                Section {
                    HStack {
                        Image(systemName: "info.circle")
                            .foregroundColor(.blue)
                        Text("Set priority to organize your tasks")
                            .font(.caption)
                            .foregroundColor(.gray)
                    }
                }
            }
            .navigationTitle("New Todo")
            .navigationBarTitleDisplayMode(.inline)
            .toolbar {
                ToolbarItem(placement: .cancellationAction) {
                    Button("Cancel") {
                        dismiss()
                    }
                }
                
                ToolbarItem(placement: .confirmationAction) {
                    Button("Add") {
                        let newTodo = TodoItem(
                            title: title,
                            isCompleted: false,
                            createdDate: Date(),
                            priority: priority
                        )
                        viewModel.addTodo(newTodo)
                        dismiss()
                    }
                    .disabled(title.isEmpty)
                }
            }
        }
    }
}

// MARK: - Preview
struct TodoListView_Previews: PreviewProvider {
    static var previews: some View {
        TodoListView()
    }
}
```

## How to Use

1. Create a new SwiftUI project in Xcode
2. Replace the content of `ContentView.swift` with the code above
3. Run the app in the simulator

## Features

### Core Features
- **Add Todos**: Tap the + button to add new todos
- **Complete Todos**: Tap the circle to mark as complete
- **Delete Todos**: Swipe left on completed todos to delete
- **Priority Levels**: Set priority (Low, Medium, High) with color coding
- **Organized Sections**: Separate active and completed todos
- **Date Tracking**: Shows when each todo was created

### Priority System
- 🟢 Low Priority (Green)
- 🟠 Medium Priority (Orange)
- 🔴 High Priority (Red)

## Exercises to Extend This App

1. **Add Persistence**: Save todos to UserDefaults or Core Data
2. **Add Due Dates**: Include date pickers for deadlines
3. **Add Categories**: Group todos by category (Work, Personal, etc.)
4. **Add Search**: Implement search functionality
5. **Add Filters**: Filter by priority or completion status
6. **Add Sorting**: Sort by date, priority, or alphabetically
7. **Add Notifications**: Remind users about pending todos
8. **Add Edit**: Allow editing existing todos
9. **Add Statistics**: Show completion rate and analytics
10. **Add Themes**: Implement light/dark mode or custom themes

## Architecture

### MVVM Pattern
This app uses the Model-View-ViewModel pattern:
- **Model**: `TodoItem` struct
- **View**: `TodoListView`, `TodoRowView`, `AddTodoView`
- **ViewModel**: `TodoViewModel` class

### Data Flow
1. User interacts with the View
2. View calls methods on the ViewModel
3. ViewModel updates the @Published property
4. SwiftUI automatically updates all views

## Key Concepts

### ObservableObject
```swift
class TodoViewModel: ObservableObject {
    @Published var todos: [TodoItem] = []
}
```
Makes the class observable and automatically updates views when properties change.

### Identifiable Protocol
```swift
struct TodoItem: Identifiable {
    let id = UUID()
}
```
Allows SwiftUI to uniquely identify items in lists.

### Computed Properties
```swift
var activeTodos: [TodoItem] {
    todos.filter { !$0.isCompleted }
}
```
Provides filtered lists without storing duplicate data.

### Environment Dismiss
```swift
@Environment(\.dismiss) var dismiss
```
Modern way to dismiss sheets and navigation views.

## Common Issues and Solutions

### Issue: Todos not updating
**Solution**: Make sure TodoViewModel is marked with `@StateObject` in the parent view and `@ObservedObject` in child views.

### Issue: List not showing changes
**Solution**: Ensure the model conforms to `Identifiable` and uses `ForEach` correctly.

## Next Steps
After completing this app, try building:
- A notes app with rich text
- A shopping list with quantities
- A habit tracker
- A expense tracker
