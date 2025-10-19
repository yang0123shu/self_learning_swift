# Swift and SwiftUI Tutorial

## Introduction
This tutorial provides a comprehensive guide to Swift and SwiftUI, with extensive real-world examples and best practices for building production-ready iOS applications.

## 1. Network Requests with URLSession and Async/Await
使用 `URLSession` 进行网络请求，并使用 `async/await` 来处理异步操作。

```swift
import Foundation

func fetchData() async throws -> Data {
    let url = URL(string: "https://api.example.com/data")!
    let (data, _) = try await URLSession.shared.data(from: url)
    return data
}
```

## 2. JSON Parsing with Codable
使用 `Codable` 进行 JSON 数据解析。

```swift
struct User: Codable {
    let id: Int
    let name: String
}

func parseJSON(data: Data) throws -> User {
    let decoder = JSONDecoder()
    return try decoder.decode(User.self, from: data)
}
```

## 3. Image Loading and Caching
使用 `URLSession` 加载图像并进行缓存。

```swift
class ImageLoader: ObservableObject {
    @Published var image: UIImage?
    private var cancellables = Set<AnyCancellable>()

    func load(from url: URL) {
        URLSession.shared.dataTaskPublisher(for: url)
            .map { $0.data }
            .map(UIImage.init)
            .replaceNil(with: UIImage(systemName: "photo")!)
            .receive(on: DispatchQueue.main)
            .assign(to: &$image)
    }
}
```

## 4. Form Validation
通过 SwiftUI 表单验证用户输入。

```swift
struct ContentView: View {
    @State private var email: String = ""
    @State private var isValidEmail: Bool = false

    var body: some View {
        Form {
            TextField("Email", text: $email)
                .onChange(of: email) { newValue in
                    isValidEmail = isValidEmail(newValue)
                }
            if !isValidEmail {
                Text("Invalid email address").foregroundColor(.red)
            }
        }
    }

    func isValidEmail(_ email: String) -> Bool {
        // Email validation logic
    }
}
```

## 5. User Authentication Flow
实现用户认证流程。

```swift
func login(username: String, password: String) async throws {
    // Authentication logic here
}
```

## 6. Local Data Persistence with UserDefaults, FileManager, CoreData
���用 `UserDefaults`, `FileManager`, 和 `CoreData` 进行本地数据持久化。

```swift
// UserDefaults example
UserDefaults.standard.set("value", forKey: "key")

// CoreData example
let context = persistentContainer.viewContext
// Add your CoreData logic here
```

## 7. List with Search, Filter, and Pagination
实现带有搜索、过滤和分页的列表。

```swift
struct ContentView: View {
    @State private var searchText: String = ""
    @State private var items: [Item] = []

    var body: some View {
        List {
            ForEach(items.filter { $0.name.contains(searchText) || searchText.isEmpty }) { item in
                Text(item.name)
            }
        }
        .searchable(text: $searchText)
    }
}
```

## 8. Navigation Patterns (NavigationStack, Sheets, Alerts)
使用 `NavigationStack`、模态视图和警报进行导航。

```swift
NavigationView {
    NavigationLink(destination: DetailView()) {
        Text("Go to Detail")
    }
}
```

## 9. Custom Reusable Components
创建可重用的自定义组件。

```swift
struct CustomButton: View {
    var title: String
    var action: () -> Void

    var body: some View {
        Button(action: action) {
            Text(title)
        }
    }
}
```

## 10. MVVM Architecture Pattern
实现 MVVM 架构模式。

```swift
class ViewModel: ObservableObject {
    @Published var data: [Item] = []

    func fetchData() {
        // Fetch data logic
    }
}
```

## 11. Combine Publishers and Subscribers with Practical Examples
使用 Combine 进行数据流处理。

```swift
import Combine

class DataFetcher {
    var cancellables = Set<AnyCancellable>()

    func fetchData() {
        URLSession.shared.dataTaskPublisher(for: URL(string: "https://api.example.com")!)
            .map { $0.data }
            .sink(receiveCompletion: { print($0) }, receiveValue: { print($0) })
            .store(in: &cancellables)
    }
}
```

## 12. Error Handling Best Practices
处理错误的最佳实践。

```swift
enum NetworkError: Error {
    case badURL
    case requestFailed
}

func performRequest() throws {
    throw NetworkError.requestFailed
}
```

## 13. Unit Testing Examples
编写单元测试的示例。

```swift
import XCTest
@testable import YourApp

class YourAppTests: XCTestCase {
    func testExample() {
        XCTAssertEqual(2 + 2, 4)
    }
}
```

## 14. Performance Optimization Techniques
性能优化技术。

```swift
// Example of using Instruments for optimization
```

## 15. Real-world App Examples (Todo App, Weather App, etc.)
提供真实应用的示例，如待办事项应用、天气应用等。

```swift
// Example code for Todo app
```

---

以上是 Swift 和 SwiftUI 的完整教程，包含了许多实用的例子和最佳实践。