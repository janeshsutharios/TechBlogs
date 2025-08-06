# 1💍 Singleton
Purpose: Ensure a class has only one instance with global access
# ✅ Singleton in Swift

A **Singleton** is a design pattern that ensures a class has only **one instance** and provides a **global access point** to it.

Swift’s `static let` ensures thread-safety and lazy initialization, making it ideal for singletons.

---
iOS Examples:

```swift - UIApplication.shared 
- FileManager.default
- UserDefaults.standard
- URLSession.shared
- NotificationCenter.default
````
Example 
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
🔐 Why Use private init()?
To prevent accidental instantiation from other parts of the code:
Use final to prevent subclassing	Avoid overusing singletons

📚 Common Use Cases
- App-wide logger
- Analytics tracker
- Core Data stack
- User session manager
- Theme/Appearance manager
