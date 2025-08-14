## Swift is often described as a Protocol-Oriented Programming (POP) language. This means Swift emphasizes the use of protocols as a fundamental way to structure and organize code, promoting flexibility and reusability. While Swift also supports object-oriented programming (OOP), POP is a core part of its design philosophy
Here's a **comprehensive set of practical examples** demonstrating all key use cases for protocols in Swift, with complete implementations:

## Here some example by usin protocols
### **1. Heterogeneous Collections (Payment System)**
```swift
protocol PaymentMethod {
    func process(amount: Double)
}

class CreditCard: PaymentMethod {
    func process(amount: Double) {
        print("Charging ₹\(amount) to credit card")
    }
}

struct UPI: PaymentMethod {
    func process(amount: Double) {
        print("Processing UPI payment for ₹\(amount)")
    }
}

let payments: [PaymentMethod] = [CreditCard(), UPI()]
payments.forEach { $0.process(amount: 999) }
```

---

### **2. Dependency Injection (Logger Service)**
```swift
protocol Logger {
    func log(_ message: String)
}

class ConsoleLogger: Logger {
    func log(_ message: String) {
        print("[LOG] \(message)")
    }
}

class ApiService {
    private let logger: Logger
    
    init(logger: Logger = ConsoleLogger()) {
        self.logger = logger
    }
    
    func fetchData() {
        logger.log("Fetching data...")
    }
}

let service = ApiService()  // Uses ConsoleLogger by default
```

---

### **3. Type Constraints (Generic Cache)**
```swift
protocol Cacheable: Codable {
    var cacheKey: String { get }
}

struct UserProfile: Cacheable {
    let id: String
    var cacheKey: String { "user_\(id)" }
}

class CacheManager<T: Cacheable> {
    private var storage = [String: T]()
    
    func cache(_ item: T) {
        storage[item.cacheKey] = item
    }
}
```

---

### **4. Protocol Composition (UI Components)**
```swift
protocol Tappable {
    func handleTap()
}

protocol Swipable {
    func handleSwipe()
}

class ImageView: Tappable, Swipable {
    func handleTap() { print("Image tapped") }
    func handleSwipe() { print("Image swiped") }
}

func configure(interactive: Tappable & Swipable) {
    interactive.handleTap()
}
```

---

### **5. Default Implementations (Renderable Views)**
```swift
protocol Renderable {
    func render()
}

extension Renderable {
    func render() {
        print("Default rendering logic")
    }
}

class PDFDocument: Renderable {}  // Inherits default render()

class VideoPlayer: Renderable {
    func render() {
        print("Custom video rendering")
    }
}
```

---

### **6. Associated Types (Repository Pattern)**
```swift
protocol Repository {
    associatedtype T
    func save(_ item: T)
    func get(id: String) -> T?
}

class UserRepository: Repository {
    typealias T = User
    
    func save(_ item: User) {
        print("Saving user \(item.name)")
    }
    
    func get(id: String) -> User? {
        return User(name: "John")
    }
}
```

---

### **7. Delegation Pattern (Download Manager)**
```swift
protocol DownloadManagerDelegate: AnyObject {
    func downloadDidFinish(fileURL: URL)
}

class DownloadManager {
    weak var delegate: DownloadManagerDelegate?
    
    func startDownload() {
        delegate?.downloadDidFinish(fileURL: URL(string: "file://report.pdf")!)
    }
}

class ReportViewer: DownloadManagerDelegate {
    func downloadDidFinish(fileURL: URL) {
        print("Opening downloaded file at \(fileURL)")
    }
}
```

---

### **8. Conditional Conformance (Premium Content)**
```swift
protocol Premium {
    var isPremium: Bool { get }
}

extension Array: Premium where Element: Premium {
    var isPremium: Bool {
        contains { $0.isPremium }
    }
}

struct Article: Premium {
    var isPremium: Bool
}

let articles = [Article(isPremium: false), Article(isPremium: true)]
print(articles.isPremium)  // true
```

---

### **9. Testing Mocks (Database)**
```swift
protocol Database {
    func getUsers() -> [String]
}

class RealDatabase: Database {
    func getUsers() -> [String] {
        return ["Admin"]  // Real DB call
    }
}

class MockDatabase: Database {
    func getUsers() -> [String] {
        return ["TestUser"]  // Fake data
    }
}

func testUserCount(database: Database) {
    let count = database.getUsers().count
    assert(count > 0)
}
```

---

### **10. Error Handling (Validation)**
```swift
protocol ValidationError: LocalizedError {
    var field: String { get }
}

struct EmailError: ValidationError {
    let field = "email"
    var errorDescription: String? {
        "Invalid \(field) format"
    }
}

func validateEmail(_ email: String) throws {
    if !email.contains("@") {
        throw EmailError()
    }
}
```

---

### **11. Factory Pattern (Themes)**
```swift
protocol Theme {
    var backgroundColor: UIColor { get }
}

struct DarkTheme: Theme {
    let backgroundColor = UIColor.black
}

struct LightTheme: Theme {
    let backgroundColor = UIColor.white
}

enum ThemeFactory {
    static func create(for style: UIUserInterfaceStyle) -> Theme {
        switch style {
        case .dark: return DarkTheme()
        default: return LightTheme()
        }
    }
}
```

---

### **12. Property Wrappers (Validation)**
```swift
protocol Validatable {
    func isValid() -> Bool
}

@propertyWrapper
struct Validated<T: Validatable> {
    private var value: T
    
    var wrappedValue: T {
        get { value }
        set { if newValue.isValid() { value = newValue } }
    }
}

struct Age: Validatable {
    let value: Int
    func isValid() -> Bool { value >= 18 }
}

struct User {
    @Validated var age: Age
}
```

---

### **13. Opaque Return Types (SwiftUI Views)**
```swift
protocol ViewBuilder {
    associatedtype V: View
    func build() -> V
}

struct HomeScreenBuilder: ViewBuilder {
    func build() -> some View {
        Text("Home")
            .padding()
    }
}
```

---

### **Key Takeaways**

| **Pattern**              | **Protocol Benefit**                     | **When to Use**               |
|--------------------------|------------------------------------------|-------------------------------|
| Collections              | Unified interface                        | Payment processors            |
| Dependency Injection     | Swappable implementations               | Testing, Services            |
| Generics                 | Type-safe abstractions                  | Repositories, Caches         |
| Default Implementations  | Code reuse                              | Shared behaviors             |
| Delegation               | Loose coupling                          | UIKit callbacks              |
| Associated Types         | Flexible generic constraints            | Abstract data operations     |

**Golden Rule**: 
- Use protocols when you need **flexibility** ("what it can do" > "what it is")
- Prefer structs for models, classes for shared state, and protocols for behavior
