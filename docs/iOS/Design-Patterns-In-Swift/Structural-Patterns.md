# 🔌 Adapter (Structural)

The **Adapter** pattern allows incompatible interfaces to work together by converting the interface of one class into an interface expected by the client. It's like a power plug adapter that lets a U.S. charger work in a European socket.

---

### ✅ When to Use

- You want to use an existing class but its interface doesn't match your needs.
- You want to create a reusable class that works with unrelated or legacy classes.
- You want to bridge **incompatible systems** without changing their code.

---

### 💡 Real-World Example

#### 🎧 Audio Player Adapter

```swift
protocol MediaPlayer {
    func play(filename: String)
}

class MP3Player: MediaPlayer {
    func play(filename: String) {
        print("🎵 Playing MP3 file: \(filename)")
    }
}

// Existing incompatible class
class VLCPlayer {
    func playVLC(file: String) {
        print("🎬 Playing VLC file: \(file)")
    }
}

// Adapter that makes VLCPlayer compatible
class VLCAdapter: MediaPlayer {
    private let vlcPlayer = VLCPlayer()
    
    func play(filename: String) {
        vlcPlayer.playVLC(file: filename)
    }
}
````

#### 🧪 Usage

```swift
let mp3 = MP3Player()
mp3.play(filename: "song.mp3")

let vlcAdapter = VLCAdapter()
vlcAdapter.play(filename: "movie.vlc")
```

---

### 🍎 iOS Built-in Usage

iOS uses the Adapter pattern in many places:

* **URLSession vs. Third-party Networking (like Alamofire)**
  You may create an adapter that converts `URLSession` calls to match a common protocol.

* **Bridging Swift with Objective-C classes**
  Swift automatically creates adapters (known as **bridging headers**) to allow compatibility.

* **UICollectionViewDiffableDataSource** adapts legacy data source logic into modern diffable models.

---

### 🧩 Summary

| Component | Role                                               |
| --------- | -------------------------------------------------- |
| `Target`  | The interface the client expects                   |
| `Adaptee` | The existing, incompatible interface               |
| `Adapter` | Translates `Adaptee` methods to `Target` interface |

> 🔌 The Adapter pattern promotes **code reusability** by allowing legacy or third-party code to be reused in modern systems without modification.

---
Here’s the **markdown version** of the 🌉 **Bridge Pattern** using the **Payment Gateway Integrations** example — perfect for your `README.md`:

---

# 🌉 Bridge (Structural)

### 🧠 Intent

The **Bridge Pattern** decouples an abstraction from its implementation so that the two can vary independently. It's especially useful when you have multiple dimensions of variation in your system.

---

### 💡 Real-World Example: **Payment Gateway Integrations**

Suppose you're building an e-commerce app that needs to support:

* Multiple **payment types** (One-time, Subscription, Refunds, etc.)
* Multiple **payment gateways** (Stripe, PayPal, Razorpay)

Hard-coding all combinations leads to a mess.
With the Bridge pattern, we **separate the payment logic (abstraction)** from **gateway implementations**, keeping your system extensible and maintainable.

---

### 🧱 Structure

```swift
// MARK: - Implementation Interface
protocol PaymentGateway {
    func processPayment(amount: Double)
}

// MARK: - Concrete Implementations
class StripeGateway: PaymentGateway {
    func processPayment(amount: Double) {
        print("Processing ₹\(amount) via Stripe.")
    }
}

class PayPalGateway: PaymentGateway {
    func processPayment(amount: Double) {
        print("Processing ₹\(amount) via PayPal.")
    }
}

// MARK: - Abstraction
class Payment {
    let gateway: PaymentGateway

    init(gateway: PaymentGateway) {
        self.gateway = gateway
    }

    func makePayment(amount: Double) {
        gateway.processPayment(amount: amount)
    }
}

// MARK: - Refined Abstractions
class SubscriptionPayment: Payment {
    override func makePayment(amount: Double) {
        print("Handling subscription logic...")
        super.makePayment(amount: amount)
    }
}

class OneTimePayment: Payment {
    override func makePayment(amount: Double) {
        print("Handling one-time payment logic...")
        super.makePayment(amount: amount)
    }
}
```

---

### ✅ Usage

```swift
let stripe = StripeGateway()
let paypal = PayPalGateway()

let monthlySub = SubscriptionPayment(gateway: stripe)
monthlySub.makePayment(amount: 999.0)

// Output:
// Handling subscription logic...
// Processing ₹999.0 via Stripe.

let oneTime = OneTimePayment(gateway: paypal)
oneTime.makePayment(amount: 499.0)

// Output:
// Handling one-time payment logic...
// Processing ₹499.0 via PayPal.
```

---

### 🍎 iOS Usage Analogy

* `UIView` uses a `CALayer` underneath → a form of **bridge** between visual abstraction and rendering engine.
* `NSURLSession` is an abstraction that can delegate network behavior to different `URLProtocol` implementations.
* In SwiftUI, `View` is protocol-based but rendering is handled separately by the system — another subtle bridge.

---
Great — let’s now document the **🌉 Bridge Pattern** using the **File System (Folders & Files)** example in clean **Markdown for a `README.md`**:

---

# 🌉 Bridge (Structural)

The **Bridge Pattern** decouples an abstraction from its implementation so the two can vary independently. It helps avoid a permanent binding between an abstraction and its implementation.

### ✅ Intent

> “Decouple an abstraction from its implementation so that the two can vary independently.” — GoF

---

### 🧠 Real-World Example: **File System (Folders & Files)**

In a file system:

* You can have different file types: `.pdf`, `.jpg`, `.mp4`, etc.
* Files can be stored in different **storage systems**: local disk, cloud, network.
* With the **Bridge Pattern**, we can separate **File Abstraction** from the **Storage Implementation**, enabling flexible combinations.

---

### 🧱 Structure

```text
       Abstraction                 Implementor
     +-------------+           +------------------+
     |   File      |           |  StorageService  |
     +-------------+           +------------------+
           |                            |
     +-------------+        +--------------------------+
     | PDFFile     |        | LocalStorage / CloudStorage |
     +-------------+        +--------------------------+
```

---

### 💻 Swift Code Example

```swift
// Implementor
protocol StorageService {
    func save(fileName: String)
}

// Concrete Implementors
class LocalStorage: StorageService {
    func save(fileName: String) {
        print("💾 Saved '\(fileName)' to Local Disk")
    }
}

class CloudStorage: StorageService {
    func save(fileName: String) {
        print("☁️ Uploaded '\(fileName)' to Cloud")
    }
}

// Abstraction
class File {
    let fileName: String
    let storage: StorageService

    init(fileName: String, storage: StorageService) {
        self.fileName = fileName
        self.storage = storage
    }

    func save() {
        storage.save(fileName: fileName)
    }
}

// Refined Abstraction
class PDFFile: File {}
class ImageFile: File {}
```

---

### 🧪 Usage

```swift
let pdf = PDFFile(fileName: "resume.pdf", storage: LocalStorage())
pdf.save()

let image = ImageFile(fileName: "photo.jpg", storage: CloudStorage())
image.save()
```

#### 🖨️ Output:

```
💾 Saved 'resume.pdf' to Local Disk
☁️ Uploaded 'photo.jpg' to Cloud
```

---

### 🍏 iOS Use Case

UIKit uses Bridge-like concepts:

* `CALayer` is an implementation object.
* `UIView` is an abstraction on top of it.

This lets `UIView` work consistently across different rendering engines while delegating actual rendering to `CALayer`.

---

### ✅ Benefits

* Increases flexibility by separating abstraction and implementation.
* Makes code easier to extend independently (e.g., add new storage types without changing file abstractions).
* Supports open/closed principle.

---


