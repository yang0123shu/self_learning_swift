# Lists and Navigation in SwiftUI

## Introduction
Lists and navigation are fundamental for building apps. Lists display collections of data, while navigation allows users to move between screens.

## Lists

### Basic List
```swift
struct BasicListView: View {
    let items = ["Apple", "Banana", "Orange", "Grape", "Mango"]
    
    var body: some View {
        List {
            ForEach(items, id: \.self) { item in
                Text(item)
            }
        }
    }
}
```

### List with Custom Rows
```swift
struct Fruit: Identifiable {
    let id = UUID()
    let name: String
    let emoji: String
    let color: Color
}

struct FruitListView: View {
    let fruits = [
        Fruit(name: "Apple", emoji: "🍎", color: .red),
        Fruit(name: "Banana", emoji: "🍌", color: .yellow),
        Fruit(name: "Grape", emoji: "🍇", color: .purple),
        Fruit(name: "Orange", emoji: "🍊", color: .orange)
    ]
    
    var body: some View {
        List(fruits) { fruit in
            HStack {
                Text(fruit.emoji)
                    .font(.largeTitle)
                Text(fruit.name)
                    .font(.headline)
                Spacer()
                Circle()
                    .fill(fruit.color)
                    .frame(width: 20, height: 20)
            }
            .padding(.vertical, 5)
        }
    }
}
```

### Sections in Lists
```swift
struct SectionedListView: View {
    var body: some View {
        List {
            Section(header: Text("Fruits")) {
                Text("Apple")
                Text("Banana")
                Text("Orange")
            }
            
            Section(header: Text("Vegetables")) {
                Text("Carrot")
                Text("Broccoli")
                Text("Spinach")
            }
        }
    }
}
```

### List with Delete
```swift
struct DeletableListView: View {
    @State private var items = ["Item 1", "Item 2", "Item 3", "Item 4"]
    
    var body: some View {
        List {
            ForEach(items, id: \.self) { item in
                Text(item)
            }
            .onDelete(perform: deleteItems)
        }
    }
    
    func deleteItems(at offsets: IndexSet) {
        items.remove(atOffsets: offsets)
    }
}
```

### List with Move
```swift
struct MovableListView: View {
    @State private var items = ["First", "Second", "Third", "Fourth"]
    
    var body: some View {
        List {
            ForEach(items, id: \.self) { item in
                Text(item)
            }
            .onMove(perform: moveItems)
        }
        .toolbar {
            EditButton()
        }
    }
    
    func moveItems(from source: IndexSet, to destination: Int) {
        items.move(fromOffsets: source, toOffset: destination)
    }
}
```

## Navigation

### NavigationView and NavigationLink
```swift
struct NavigationExample: View {
    var body: some View {
        NavigationView {
            List {
                NavigationLink("Go to Detail 1") {
                    DetailView(title: "Detail 1")
                }
                
                NavigationLink("Go to Detail 2") {
                    DetailView(title: "Detail 2")
                }
                
                NavigationLink("Go to Detail 3") {
                    DetailView(title: "Detail 3")
                }
            }
            .navigationTitle("Main Menu")
        }
    }
}

struct DetailView: View {
    let title: String
    
    var body: some View {
        Text("This is \(title)")
            .font(.largeTitle)
            .navigationTitle(title)
    }
}
```

### Navigation with Data
```swift
struct Person: Identifiable {
    let id = UUID()
    let name: String
    let age: Int
    let occupation: String
}

struct PeopleListView: View {
    let people = [
        Person(name: "Alice", age: 28, occupation: "Developer"),
        Person(name: "Bob", age: 35, occupation: "Designer"),
        Person(name: "Charlie", age: 42, occupation: "Manager")
    ]
    
    var body: some View {
        NavigationView {
            List(people) { person in
                NavigationLink(destination: PersonDetailView(person: person)) {
                    VStack(alignment: .leading) {
                        Text(person.name)
                            .font(.headline)
                        Text(person.occupation)
                            .font(.subheadline)
                            .foregroundColor(.gray)
                    }
                }
            }
            .navigationTitle("People")
        }
    }
}

struct PersonDetailView: View {
    let person: Person
    
    var body: some View {
        VStack(spacing: 20) {
            Image(systemName: "person.circle.fill")
                .font(.system(size: 100))
                .foregroundColor(.blue)
            
            Text(person.name)
                .font(.largeTitle)
                .bold()
            
            Text("Age: \(person.age)")
                .font(.title2)
            
            Text("Occupation: \(person.occupation)")
                .font(.title3)
                .foregroundColor(.gray)
        }
        .navigationTitle(person.name)
        .navigationBarTitleDisplayMode(.inline)
    }
}
```

### Programmatic Navigation
```swift
struct ProgrammaticNavigationView: View {
    @State private var isShowingDetail = false
    
    var body: some View {
        NavigationView {
            VStack {
                Button("Show Detail") {
                    isShowingDetail = true
                }
                
                NavigationLink(
                    destination: Text("Detail View"),
                    isActive: $isShowingDetail
                ) {
                    EmptyView()
                }
            }
            .navigationTitle("Main")
        }
    }
}
```

## Combining Lists and Navigation

### Master-Detail Pattern
```swift
struct Product: Identifiable {
    let id = UUID()
    let name: String
    let price: Double
    let description: String
    let category: String
}

struct ProductCatalogView: View {
    let products = [
        Product(name: "iPhone", price: 999, description: "Latest smartphone", category: "Electronics"),
        Product(name: "MacBook", price: 1299, description: "Powerful laptop", category: "Electronics"),
        Product(name: "AirPods", price: 199, description: "Wireless earbuds", category: "Audio"),
        Product(name: "Apple Watch", price: 399, description: "Smart watch", category: "Wearables")
    ]
    
    var body: some View {
        NavigationView {
            List(products) { product in
                NavigationLink(destination: ProductDetailView(product: product)) {
                    ProductRowView(product: product)
                }
            }
            .navigationTitle("Products")
        }
    }
}

struct ProductRowView: View {
    let product: Product
    
    var body: some View {
        HStack {
            VStack(alignment: .leading, spacing: 5) {
                Text(product.name)
                    .font(.headline)
                Text(product.category)
                    .font(.caption)
                    .foregroundColor(.gray)
            }
            
            Spacer()
            
            Text("$\(product.price, specifier: "%.2f")")
                .font(.headline)
                .foregroundColor(.blue)
        }
        .padding(.vertical, 5)
    }
}

struct ProductDetailView: View {
    let product: Product
    @State private var quantity = 1
    
    var body: some View {
        ScrollView {
            VStack(alignment: .leading, spacing: 20) {
                // Product image placeholder
                Rectangle()
                    .fill(Color.gray.opacity(0.3))
                    .frame(height: 300)
                    .cornerRadius(10)
                
                VStack(alignment: .leading, spacing: 10) {
                    Text(product.name)
                        .font(.title)
                        .bold()
                    
                    Text(product.category)
                        .font(.subheadline)
                        .foregroundColor(.gray)
                    
                    Text("$\(product.price, specifier: "%.2f")")
                        .font(.title2)
                        .foregroundColor(.blue)
                        .bold()
                    
                    Divider()
                    
                    Text("Description")
                        .font(.headline)
                    
                    Text(product.description)
                        .font(.body)
                        .foregroundColor(.secondary)
                    
                    Divider()
                    
                    // Quantity selector
                    HStack {
                        Text("Quantity:")
                            .font(.headline)
                        
                        Stepper("\(quantity)", value: $quantity, in: 1...10)
                    }
                    
                    Button(action: {
                        // Add to cart action
                    }) {
                        Text("Add to Cart")
                            .font(.headline)
                            .foregroundColor(.white)
                            .frame(maxWidth: .infinity)
                            .padding()
                            .background(Color.blue)
                            .cornerRadius(10)
                    }
                }
                .padding()
            }
        }
        .navigationTitle(product.name)
        .navigationBarTitleDisplayMode(.inline)
    }
}
```

## Search in Lists

### Searchable List
```swift
struct SearchableListView: View {
    @State private var searchText = ""
    
    let items = ["Apple", "Banana", "Orange", "Grape", "Mango", 
                 "Strawberry", "Blueberry", "Raspberry", "Pineapple"]
    
    var filteredItems: [String] {
        if searchText.isEmpty {
            return items
        } else {
            return items.filter { $0.localizedCaseInsensitiveContains(searchText) }
        }
    }
    
    var body: some View {
        NavigationView {
            List(filteredItems, id: \.self) { item in
                Text(item)
            }
            .navigationTitle("Fruits")
            .searchable(text: $searchText, prompt: "Search fruits")
        }
    }
}
```

## Practical Example: Todo List App

```swift
struct Todo: Identifiable {
    let id = UUID()
    var title: String
    var isCompleted: Bool
}

struct TodoListView: View {
    @State private var todos = [
        Todo(title: "Buy groceries", isCompleted: false),
        Todo(title: "Walk the dog", isCompleted: true),
        Todo(title: "Read a book", isCompleted: false)
    ]
    @State private var newTodoTitle = ""
    
    var body: some View {
        NavigationView {
            VStack {
                // Add new todo
                HStack {
                    TextField("New todo", text: $newTodoTitle)
                        .textFieldStyle(RoundedBorderTextFieldStyle())
                    
                    Button(action: addTodo) {
                        Image(systemName: "plus.circle.fill")
                            .font(.title2)
                    }
                    .disabled(newTodoTitle.isEmpty)
                }
                .padding()
                
                // Todo list
                List {
                    ForEach($todos) { $todo in
                        HStack {
                            Button(action: {
                                todo.isCompleted.toggle()
                            }) {
                                Image(systemName: todo.isCompleted ? "checkmark.circle.fill" : "circle")
                                    .foregroundColor(todo.isCompleted ? .green : .gray)
                            }
                            
                            Text(todo.title)
                                .strikethrough(todo.isCompleted)
                                .foregroundColor(todo.isCompleted ? .gray : .primary)
                        }
                    }
                    .onDelete(perform: deleteTodo)
                    .onMove(perform: moveTodo)
                }
            }
            .navigationTitle("Todo List")
            .toolbar {
                EditButton()
            }
        }
    }
    
    func addTodo() {
        let newTodo = Todo(title: newTodoTitle, isCompleted: false)
        todos.append(newTodo)
        newTodoTitle = ""
    }
    
    func deleteTodo(at offsets: IndexSet) {
        todos.remove(atOffsets: offsets)
    }
    
    func moveTodo(from source: IndexSet, to destination: Int) {
        todos.move(fromOffsets: source, toOffset: destination)
    }
}
```

## Practice Exercises
1. Create a list of your favorite movies with navigation to detail views
2. Build a contacts app with searchable list
3. Create a shopping list with add, delete, and mark as purchased features
4. Build a recipe app with categories and detail views
