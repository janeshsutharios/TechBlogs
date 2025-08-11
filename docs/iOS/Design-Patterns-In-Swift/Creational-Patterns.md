# 🛠 Creational Design Pattern

## 🏗️ Abstract Factory(Creational)
 **Abstract Factory** is a creational design pattern that lets you produce families of related objects without specifying their concrete classes. It provides an interface for creating a group of related products, ensuring that they work well together.

iOS Examples:
```swift
- UIFontDescriptor with different styles (e.g., .preferredFont(forTextStyle:))
- NSCollectionLayoutSection in Compositional Layouts
- UIViewControllerTransitioningDelegate for custom transitions
````

```swift
// MARK: - Abstract Product Protocols

protocol Chair {
    func sitOn()
}

protocol Sofa {
    func lieOn()
}

protocol Table {
    func placeItems()
}

// MARK: - Concrete Product Implementations

// Victorian
class VictorianChair: Chair {
    func sitOn() {
        print("Sitting on a Victorian Chair")
    }
}

class VictorianSofa: Sofa {
    func lieOn() {
        print("Lying on a Victorian Sofa")
    }
}

class VictorianTable: Table {
    func placeItems() {
        print("Items placed on a Victorian Table")
    }
}

// Modern
class ModernChair: Chair {
    func sitOn() {
        print("Sitting on a Modern Chair")
    }
}

class ModernSofa: Sofa {
    func lieOn() {
        print("Lying on a Modern Sofa")
    }
}

class ModernTable: Table {
    func placeItems() {
        print("Items placed on a Modern Table")
    }
}

// MARK: - Abstract Factory

protocol FurnitureFactory {
    func createChair() -> Chair
    func createSofa() -> Sofa
    func createTable() -> Table
}

// MARK: - Concrete Factories

class VictorianFurnitureFactory: FurnitureFactory {
    func createChair() -> Chair {
        VictorianChair()
    }

    func createSofa() -> Sofa {
        VictorianSofa()
    }

    func createTable() -> Table {
        VictorianTable()
    }
}

class ModernFurnitureFactory: FurnitureFactory {
    func createChair() -> Chair {
        ModernChair()
    }

    func createSofa() -> Sofa {
        ModernSofa()
    }

    func createTable() -> Table {
        ModernTable()
    }
}

// MARK: - Client Code

func setupRoom(with factory: FurnitureFactory) {
    let chair = factory.createChair()
    let sofa = factory.createSofa()
    let table = factory.createTable()

    chair.sitOn()
    sofa.lieOn()
    table.placeItems()
}

// Usage
let modernFactory = ModernFurnitureFactory()
setupRoom(with: modernFactory)

let victorianFactory = VictorianFurnitureFactory()
setupRoom(with: victorianFactory)
````

Purpose: Create families of related objects

| Feature           | Factory Method                         | Abstract Factory                                 |
| ----------------- | -------------------------------------- | ------------------------------------------------ |
| **Purpose**       | Create one product                     | Create **families** of related products          |
| **Product Count** | One type of product                    | Multiple related products                        |
| **Inheritance**   | Relies on subclass to override factory | Uses composition to create families              |
| **Flexibility**   | Less flexible                          | More flexible, decouples product families        |
| **Example**       | Create `PushNotification`              | Create UI kits: Button + Label for iOS and macOS |

🧱 Real-World Analogy
Factory Method:
Think of a Coffee Machine that can make either an Espresso or a Cappuccino, depending on how it's subclassed.

Abstract Factory:
Think of a Furniture Set Factory. It produces a chair, a sofa, and a table — all of the same style (e.g., Victorian or Modern).

## 🏭 Factory-Method(Creational)
It provides a way to delegate the instantiation of objects to subclasses.
Instead of calling a constructor directly, the client calls a method that returns an instance of a product, allowing the code to remain flexible and loosely coupled.

Purpose: Delegate object creation to subclasses

iOS Examples:
```swift
- UIFont.systemFont(ofSize:) vs UIFont.boldSystemFont(ofSize:)
- UIButton(type: .system) (Creates different button types)
- NSNumber(value:) (Creates number objects for different types)
````


```swift
// MARK: - Product
protocol Coffee {
    var name: String { get }
    func prepare()
}

// MARK: - Concrete Products
class Espresso: Coffee {
    var name: String { "Espresso" }
    
    func prepare() {
        print("Grinding fine coffee beans...")
        print("Brewing \(name)... ☕️")
    }
}

class Cappuccino: Coffee {
    var name: String { "Cappuccino" }
    
    func prepare() {
        print("Grinding coffee beans...")
        print("Adding steamed milk...")
        print("Brewing \(name)... ☕️")
    }
}

// MARK: - Creator (Factory)
protocol CoffeeMachine {
    func createCoffee() -> Coffee
    func serveCoffee()
}

extension CoffeeMachine {
    func serveCoffee() {
        let coffee = createCoffee()
        print("Starting the machine...")
        coffee.prepare()
        print("Serving your \(coffee.name)! ✅")
    }
}

// MARK: - Concrete Creators
class EspressoMachine: CoffeeMachine {
    func createCoffee() -> Coffee {
        return Espresso()
    }
}

class CappuccinoMachine: CoffeeMachine {
    func createCoffee() -> Coffee {
        return Cappuccino()
    }
}

// MARK: - Usage
let espressoMachine = EspressoMachine()
espressoMachine.serveCoffee()

print("\n---\n")

let cappuccinoMachine = CappuccinoMachine()
cappuccinoMachine.serveCoffee()
````

## 👷 Builder(Creational)
- Constructs complex objects step by step.
- Useful when an object needs to be constructed with many configuration options (e.g., URL requests, form data).

iOS Examples:      
```swift
- URLComponents (Builds URLs incrementally)
- UIAlertController with added actions
- NSAttributedString with NSAttributedString.Builder (iOS 15+)
- SwiftUI's ViewBuilder (e.g., @ViewBuilder closures)
````

Real world example with URLComponents builder 
```swift
class RequestBuilder {
    private var urlComponents = URLComponents()
    private var method: String = "GET"
    private var headers: [String: String] = [:]
    private var body: Data?
    
    init(baseURL: String) {
        urlComponents.scheme = "https"
        urlComponents.host = baseURL
    }
    
    func setPath(_ path: String) -> RequestBuilder {
        urlComponents.path = path
        return self
    }
    
    func setMethod(_ method: String) -> RequestBuilder {
        self.method = method
        return self
    }
    
    func addQueryItem(name: String, value: String) -> RequestBuilder {
        if urlComponents.queryItems == nil {
            urlComponents.queryItems = []
        }
        urlComponents.queryItems?.append(URLQueryItem(name: name, value: value))
        return self
    }
    
    @discardableResult
    func addHeader(key: String, value: String) -> RequestBuilder {
        headers[key] = value
        return self
    }
    
    func setJSONBody<T: Encodable>(_ model: T) -> RequestBuilder {
        let encoder = JSONEncoder()
        self.body = try? encoder.encode(model)
        self.addHeader(key: "Content-Type", value: "application/json")
        return self
    }
    
    func build() -> URLRequest? {
        guard let url = urlComponents.url else { return nil }
        
        var request = URLRequest(url: url)
        request.httpMethod = method
        request.httpBody = body
        for (key, value) in headers {
            request.setValue(value, forHTTPHeaderField: key)
        }
        
        return request
    }
}
struct LoginPayload: Codable {
    let email: String
    let password: String
}


let request = RequestBuilder(baseURL: "api.myapp.com")
    .setPath("/v1/login")
    .setMethod("POST")
    .setJSONBody(LoginPayload(email: "john@example.com", password: "123456"))
    .build()

// Now use it with URLSession
if let request = request {
    URLSession.shared.dataTask(with: request) { data, response, error in
        // Handle response
    }.resume()
}
````

## ♾️ Monostate(Creational)
Shared State Pattern: All instances of a class share the same internal state (static variables), making them behave like a singleton.
Bonus: Unlike Singleton (one instance), Monostate allows multiple "fake" instances with shared data. 🎭

| Feature       | Singleton         | Monostate                   |
|---------------|-------------------|-----------------------------|
| Instantiation | One only (shared) | Many, but share state       |
| Global Access | Yes               | No (needs passing instances)|
| Testability   | Harder            | Easier                      |
| Subclassing   | Restrictive       | Flexible                    |


```swift
final class AppConfiguration: Sendable {
    private static let lock = NSLock()
    private static var _environment: Environment = .production
    private static var _featureToggles: [String: Bool] = [:]
    
    var environment: Environment {
        get {
            Self.lock.lock()
            defer { Self.lock.unlock() }
            return Self._environment
        }
        set {
            Self.lock.lock()
            defer { Self.lock.unlock() }
            Self._environment = newValue
        }
    }
    
    var featureToggles: [String: Bool] {
        get {
            Self.lock.lock()
            defer { Self.lock.unlock() }
            return Self._featureToggles
        }
        set {
            Self.lock.lock()
            defer { Self.lock.unlock() }
            Self._featureToggles = newValue
        }
    }
    
    func isFeatureEnabled(_ key: String) -> Bool {
        Self.lock.lock()
        defer { Self.lock.unlock() }
        return Self._featureToggles[key] ?? false
    }
    
    func setFeature(_ key: String, enabled: Bool) {
        Self.lock.lock()
        defer { Self.lock.unlock() }
        Self._featureToggles[key] = enabled
    }
}

enum Environment: Sendable {
    case staging, production
}
let config1 = AppConfiguration()
config1.environment = .staging
config1.setFeature("NewOnboarding", enabled: true)

let config2 = AppConfiguration()
print(config2.environment) // .staging
print(config2.isFeatureEnabled("NewOnboarding")) // true
````
## 🖨️ Prototype Pattern (Creational)

### Context:
Purpose: Clone objects instead of creating new ones
In a scalable iOS app (like a design tool or a visual editor), users can create reusable "design elements" (buttons, cards, labels, etc.) and duplicate them easily. Each duplicated item should be an independent copy (not just a reference), preserving the current state but allowing customization afterward.

This is where the Prototype pattern shines.

---

### When to Use:
- You need to duplicate complex objects efficiently.
- Object creation is costly (lots of setup/configuration).
- You want to decouple instantiation from the object type.

---

### 🔧 Example: UI Component Prototyping System

We’ll create a base `DesignComponent` protocol that requires `clone()`.

### 1. Component Protocol

```swift
protocol DesignComponent: AnyObject {
    func clone() -> DesignComponent
}
```

---

### 2. Concrete Components

```swift
final class ButtonComponent: DesignComponent {
    var title: String
    var backgroundColor: String
    var cornerRadius: Double

    init(title: String, backgroundColor: String, cornerRadius: Double) {
        self.title = title
        self.backgroundColor = backgroundColor
        self.cornerRadius = cornerRadius
    }

    func clone() -> DesignComponent {
        return ButtonComponent(title: self.title, backgroundColor: self.backgroundColor, cornerRadius: self.cornerRadius)
    }
}

final class CardComponent: DesignComponent {
    var heading: String
    var bodyText: String
    var imageURL: String

    init(heading: String, bodyText: String, imageURL: String) {
        self.heading = heading
        self.bodyText = bodyText
        self.imageURL = imageURL
    }

    func clone() -> DesignComponent {
        return CardComponent(heading: self.heading, bodyText: self.bodyText, imageURL: self.imageURL)
    }
}
```

---

### 3. Usage in the App (Cloning Components)

```swift
let originalButton = ButtonComponent(title: "Submit", backgroundColor: "#FF5733", cornerRadius: 8.0)
let clonedButton = originalButton.clone() as! ButtonComponent

if let clonedButton = originalButton.clone() as? ButtonComponent {
    clonedButton.title = "Cancel" // Independent copy
}
```

---

### 💡 Benefits:
- Allows runtime duplication without knowing the exact class.
- Helps isolate state between cloned instances.
- Makes UI building tools and design systems very flexible.

---

### 📦 Real-world Analogy:
Like duplicating slides in Keynote or Figma components — you want the same base, but modifiable independently.

---

### 🧠 Related Concepts in iOS:
- `NSCopying` protocol is a native equivalent of the Prototype pattern.
- Used in copy-on-write implementations like `Array`, `String`, `Data` (for performance).

---

### 📱 Example Extension: Component Library

You can extend this system with a registry of default components and use `.clone()` to offer base templates to users in a design editor.

---
### iOS Examples
---

### ✅ 1. UICollectionViewCell — `dequeueReusableCell`
`UICollectionViewCell — dequeueReusableCell(withIdentifier:)`
Concept: Instead of creating new cells from scratch each time, iOS reuses a "prototype cell" (often registered via a nib or class), and dequeues a copy of it for display.

Why it's Prototype: The system maintains a pool of cells, and returns a copy-like reused cell instance — mimicking the Prototype pattern where new instances are created from existing ones.

Note: It's not a literal `copy()` under the hood, but the concept of reusing object instances is inspired by the same goal of reducing object creation overhead.
```swift
class ProductCell: UICollectionViewCell {
    static let reuseIdentifier = "ProductCell"

    override init(frame: CGRect) {
        super.init(frame: frame)
        contentView.backgroundColor = .lightGray
    }

    required init?(coder: NSCoder) {
        fatalError("init(coder:) has not been implemented")
    }

    func configure(with product: String) {
        // Set up the cell's data
    }
}

class ProductViewController: UICollectionViewController {
    let products = ["iPhone", "iPad", "MacBook"]

    override func viewDidLoad() {
        super.viewDidLoad()
        collectionView.register(ProductCell.self, forCellWithReuseIdentifier: ProductCell.reuseIdentifier)
    }

    override func collectionView(_ collectionView: UICollectionView, numberOfItemsInSection section: Int) -> Int {
        return products.count
    }

    override func collectionView(_ collectionView: UICollectionView,
                                 cellForItemAt indexPath: IndexPath) -> UICollectionViewCell {
        let cell = collectionView.dequeueReusableCell(withReuseIdentifier: ProductCell.reuseIdentifier, for: indexPath) as! ProductCell
        cell.configure(with: products[indexPath.item])
        return cell
    }
}
```

> Reuses prototype instances — iOS keeps a pool of cells and clones them with new configurations.

---

### ✅ 2. UIView Copying via `NSCopying`
UIView.copy() via NSCopying
Concept: Classes that conform to NSCopying allow creating clones of an instance using `copy()` or `mutableCopy()`.

Why it's Prototype: This is a direct use of the Prototype pattern — duplicating an object via a defined copying method rather than instantiating a new one from scratch.

Example: Custom views or models that implement `copy(with:)` method to make independent copies.
```swift
class CustomLabel: UILabel, NSCopying {
    var customStyle: String = ""

    func copy(with zone: NSZone? = nil) -> Any {
        let copy = CustomLabel()
        copy.text = self.text
        copy.textColor = self.textColor
        copy.customStyle = self.customStyle
        return copy
    }
}

// Usage
let original = CustomLabel()
original.text = "Original"
original.textColor = .blue
original.customStyle = "Header"

let cloned = original.copy() as! CustomLabel
cloned.text = "Cloned"
```

> Allows you to duplicate view configurations — true **Prototype** behavior.

---

### ✅ 3. Codable — Decoding JSON Templates

 Codable objects decoded from JSON
Concept: When you decode a JSON payload into Swift objects, you're essentially cloning data into a model structure.

Why it's similar to Prototype: You're not using an existing object to copy(), but the idea is close — you are replicating a known structure repeatedly from the same schema (like a prototype template).

Caveat: Not a textbook Prototype, but shares the idea of repeated structured instantiation from a template-like format.

```swift
struct User: Codable {
    var name: String
    var age: Int
}

// JSON Data
let jsonData = """
[
    {"name": "Alice", "age": 30},
    {"name": "Bob", "age": 24}
]
""".data(using: .utf8)!

do {
    let users = try JSONDecoder().decode([User].self, from: jsonData)
    users.forEach { print($0.name, $0.age) }
} catch {
    print("Decoding failed: \(error)")
}
````
## 💍 Singleton(Creational)
Purpose: Ensure a class has only one instance with global access

A **Singleton** is a design pattern that ensures a class has only **one instance** and provides a **global access point** to it.

Swift’s `static let` ensures thread-safety and lazy initialization, making it ideal for singletons.

iOS Examples:
```swift
- UIApplication.shared 
- FileManager.default
- UserDefaults.standard
- URLSession.shared
- NotificationCenter.default
````

---
### 🧩 Basic Implementation

```swift
// Thread Safe Singleton
actor Singleton {
    static let shared = Singleton()
    private init() {}
    
    private var _data: String = "Default"
    
    // Isolated access to mutable state
    func setData(_ value: String) {
        _data = value
    }
    
    func getData() -> String {
        _data
    }
}
// Usage:-
Task {
    await Singleton.shared.setData("NewValue")  // Thread-safe
    let data = await Singleton.shared.getData()
}
````
🔐 Why Use `private init()?`
To prevent accidental instantiation from other parts of the code:
Use final to prevent subclassing	Avoid overusing singletons

Example #
Reference [Apple](https://developer.apple.com/documentation/coredata/setting-up-a-core-data-stack)
```swift
// Define an observable class to encapsulate all Core Data-related functionality.
class CoreDataStack: ObservableObject {
    static let shared = CoreDataStack()
    
    // Create a persistent container as a lazy variable to defer instantiation until its first use.
    lazy var persistentContainer: NSPersistentContainer = {
        
        // Pass the data model filename to the container’s initializer.
        let container = NSPersistentContainer(name: "DataModel")
        
        // Load any persistent stores, which creates a store if none exists.
        container.loadPersistentStores { _, error in
            if let error {
                // Handle the error appropriately. However, it's useful to use
                // `fatalError(_:file:line:)` during development.
                fatalError("Failed to load persistent stores: \(error.localizedDescription)")
            }
        }
        return container
    }()
        
    private init() { }
}
````

📚 Common Use Cases
- App-wide logger
- Analytics tracker
- Core Data stack
- User session manager
- Theme/Appearance manager

