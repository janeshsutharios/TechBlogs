# 💍 Singleton(Creational)
Purpose: Ensure a class has only one instance with global access
# ✅ Singleton in Swift

A **Singleton** is a design pattern that ensures a class has only **one instance** and provides a **global access point** to it.

Swift’s `static let` ensures thread-safety and lazy initialization, making it ideal for singletons.

---
## 🧩 Basic Implementation

```swift
final class MySingleton {
    static let shared = MySingleton()
    
    private init() {
        // Prevent external initialization
    }

    func doSomething() {
        print("Doing something...")
    }
}
// Usage:
MySingleton.shared.doSomething()

````
🔐 Why Use `private init()?`
To prevent accidental instantiation from other parts of the code:
Use final to prevent subclassing	Avoid overusing singletons

iOS Examples:

```swift
- UIApplication.shared 
- FileManager.default
- UserDefaults.standard
- URLSession.shared
- NotificationCenter.default
````

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



# 🏭 Factory Method(Creational)
It provides a way to delegate the instantiation of objects to subclasses.
Instead of calling a constructor directly, the client calls a method that returns an instance of a product, allowing the code to remain flexible and loosely coupled.

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

Purpose: Delegate object creation to subclasses

iOS Examples:
```swift
- UIFont.systemFont(ofSize:) vs UIFont.boldSystemFont(ofSize:)
- UIButton(type: .system) (Creates different button types)
- NSNumber(value:) (Creates number objects for different types)
````


# 🏗️ Abstract Factory(Creational)
 **Abstract Factory** is a creational design pattern that lets you produce families of related objects without specifying their concrete classes. It provides an interface for creating a group of related products, ensuring that they work well together.


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
iOS Examples:
```swift
- UIFontDescriptor with different styles (e.g., .preferredFont(forTextStyle:))
- NSCollectionLayoutSection in Compositional Layouts
- UIViewControllerTransitioningDelegate for custom transitions
````

| Feature           | Factory Method                         | Abstract Factory                                 |
| ----------------- | -------------------------------------- | ------------------------------------------------ |
| **Purpose**       | Create one product                     | Create **families** of related products          |
| **Product Count** | One type of product                    | Multiple related products                        |
| **Inheritance**   | Relies on subclass to override factory | Uses composition to create families              |
| **Flexibility**   | Less flexible                          | More flexible, decouples product families        |
| **Example**       | Create `PushNotification`              | Create UI kits: Button + Label for iOS and macOS |

