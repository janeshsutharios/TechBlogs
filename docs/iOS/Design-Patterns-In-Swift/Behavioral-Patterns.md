# 🏃‍♀️Behavioral Design Pattern
## ⛓️ Chain Of Responsibility(Behavioral)
Decouples request senders from receivers by allowing multiple handlers to process a request sequentially. Each handler decides to act or pass it down the chain.

**Example - Expense Approval System** 
A Swift implementation of the **Chain of Responsibility** behavioral design pattern for handling multi-level expense approvals in a corporate workflow.
Define Expenses -> Build the Chain -> Submit for Approval
**Features**
- **Dynamic Chain**: Approvers (Manager → Director → CFO) forward requests they can't handle.
- **Scalable**: Add new approvers (e.g., `VP`) without changing existing code.
- **Clear Policies**: Each handler enforces its own business rules.
  
```swift
// MARK: - Expense Report Model
/// Represents an expense request submitted for approval.
struct ExpenseReport {
    let id: UUID
    let amount: Double
    let description: String
    let category: String // e.g., "Travel", "Equipment"
}

// MARK: - Handler Protocol
/// Defines the interface for all approval handlers in the chain.
protocol ExpenseApprover: AnyObject {
    var nextApprover: ExpenseApprover? { get set }
    func approve(_ expense: ExpenseReport) -> String
}

// MARK: - Concrete Handlers

/// Manager can approve expenses up to $1,000.
final class Manager: ExpenseApprover {
    var nextApprover: ExpenseApprover?
    private let approvalLimit: Double = 1_000
    
    func approve(_ expense: ExpenseReport) -> String {
        if expense.amount <= approvalLimit {
            return "✅ Manager approved expense #\(expense.id) (\(expense.description))"
        } else {
            return nextApprover?.approve(expense) ?? "❌ Rejected: No higher authority!"
        }
    }
}

/// Director can approve expenses up to $5,000.
final class Director: ExpenseApprover {
    var nextApprover: ExpenseApprover?
    private let approvalLimit: Double = 5_000
    
    func approve(_ expense: ExpenseReport) -> String {
        if expense.amount <= approvalLimit {
            return "✅ Director approved expense #\(expense.id) (\(expense.description))"
        } else {
            return nextApprover?.approve(expense) ?? "❌ Rejected: Requires CFO review!"
        }
    }
}

/// CFO is the final authority with special rules for travel expenses.
final class CFO: ExpenseApprover {
    var nextApprover: ExpenseApprover? = nil
    
    func approve(_ expense: ExpenseReport) -> String {
        if expense.category == "Travel" && expense.amount > 10_000 {
            return "❌ Rejected: Travel expenses cannot exceed $10,000"
        } else {
            return "✅ CFO approved expense #\(expense.id)"
        }
    }
}

// MARK: - Chain Setup & Demo
func buildApprovalChain() -> ExpenseApprover {
    let manager = Manager()
    let director = Director()
    let cfo = CFO()
    
    manager.nextApprover = director
    director.nextApprover = cfo
    
    return manager
}

// Example Usage
let chain = buildApprovalChain()

let expenses = [
    ExpenseReport(id: UUID(), amount: 800, description: "Team lunch", category: "Food"),
    ExpenseReport(id: UUID(), amount: 4_500, description: "Conference tickets", category: "Travel"),
    ExpenseReport(id: UUID(), amount: 12_000, description: "Business class flight", category: "Travel")
]

for expense in expenses {
    print(chain.approve(expense))
}

/* Output:
✅ Manager approved expense #... (Team lunch)
✅ Director approved expense #... (Conference tickets)
❌ Rejected: Travel expenses cannot exceed $10,000
*/
````

## 🖥️ Command (Behavioral)

Example 
Scenario:
A food delivery app (like Uber Eats) needs to handle orders, undo operations (cancel items), queue requests, and remote kitchen workflows. The Command Pattern encapsulates each order as an object, making it easy to execute, queue, or undo operations.
Swift Implementation: Restaurant Order System

(Single-file, scalable, with clear comments)
1. Key Components

    Command Protocol: Defines execute() and undo().

    Concrete Commands: Encapsulate actions like AddToCartCommand, CancelOrderCommand.

    Invoker (OrderManager): Manages command execution, history (for undo), and queuing.

    Receiver (KitchenSystem): Actually performs the actions (e.g., cooks food).
   
```swift

// MARK: - Receiver (Knows HOW to perform actions)
final class KitchenSystem {
    func prepareOrder(_ dish: String) {
        print("🧑‍🍳 Cooking: \(dish)")
    }
    
    func cancelOrder(_ dish: String) {
        print("🚫 Cancelled: \(dish)")
    }
}

// MARK: - Command Protocol
protocol Command {
    func execute()
    func undo()
}

// MARK: - Concrete Commands
final class AddToCartCommand: Command {
    private let kitchen: KitchenSystem
    private let dish: String
    
    init(kitchen: KitchenSystem, dish: String) {
        self.kitchen = kitchen
        self.dish = dish
    }
    
    func execute() {
        kitchen.prepareOrder(dish)
    }
    
    func undo() {
        kitchen.cancelOrder(dish)
    }
}

final class CancelOrderCommand: Command {
    private let kitchen: KitchenSystem
    private let dish: String
    
    init(kitchen: KitchenSystem, dish: String) {
        self.kitchen = kitchen
        self.dish = dish
    }
    
    func execute() {
        kitchen.cancelOrder(dish)
    }
    
    func undo() {
        kitchen.prepareOrder(dish) // Re-add if undone
    }
}

// MARK: - Invoker (Manages commands)
final class OrderManager {
    private var commandQueue = [Command]()
    private var history = [Command]()
    private let kitchen: KitchenSystem
    
    init(kitchen: KitchenSystem) {
        self.kitchen = kitchen
    }
    
    func addCommand(_ command: Command) {
        commandQueue.append(command)
    }
    
    func processCommands() {
        commandQueue.forEach { cmd in
            cmd.execute()
            history.append(cmd) // Track for undo
        }
        commandQueue.removeAll()
    }
    
    func undoLast() {
        guard !history.isEmpty else { return }
        let lastCmd = history.removeLast()
        lastCmd.undo()
    }
}

// MARK: - Usage
let kitchen = KitchenSystem()
let orderManager = OrderManager(kitchen: kitchen)

// User adds items to cart
orderManager.addCommand(AddToCartCommand(kitchen: kitchen, dish: "Burger"))
orderManager.addCommand(AddToCartCommand(kitchen: kitchen, dish: "Pizza"))

// Process all orders
orderManager.processCommands() 
// Output: 
// 🧑‍🍳 Cooking: Burger  
// 🧑‍🍳 Cooking: Pizza

// User cancels last order
orderManager.undoLast() 
// Output: 🚫 Cancelled: Pizza
````

## 📜 Interpreter (Behavioral)
The Interpreter Pattern is used to define a grammar for a language and provide an interpreter to evaluate expressions in that language. It's useful for:

- Domain-Specific Languages (DSLs) (e.g., SQL, regex)
- Rule engines (e.g., business rules, pricing rules)
- Mathematical expressions (e.g., calculators)
  
**Real-World Example: Smart Home Automation Language**
Imagine creating a simple language to control smart home devices:

1. TURN ON LIGHT "Kitchen"
2. SET THERMOSTAT TO 72
3. IF TIME > "18:00" THEN TURN ON "Living Room Lights"

1. Define the Grammar
Our mini-language has:

    Commands: TURN ON/OFF, SET

    Targets: LIGHT, THERMOSTAT

    Conditions: IF...THEN

```swift
// MARK: - Context (Stores variables/state)
class Context {
    var variables: [String: Any] = [:]
    var deviceStatus: [String: Bool] = [:]
    var thermostatTemp: Int = 68
}

// MARK: - Abstract Expression
protocol Expression {
    func interpret(context: Context) -> String
}

// MARK: - Terminal Expressions (Primitive commands)
final class TurnOnCommand: Expression {
    private let device: String
    
    init(device: String) {
        self.device = device
    }
    
    func interpret(context: Context) -> String {
        context.deviceStatus[device] = true
        return "Turned ON \(device)"
    }
}

final class SetThermostatCommand: Expression {
    private let temp: Int
    
    init(temp: Int) {
        self.temp = temp
    }
    
    func interpret(context: Context) -> String {
        context.thermostatTemp = temp
        return "Thermostat set to \(temp)°F"
    }
}

// MARK: - Non-Terminal Expression (Composite)
final class IfThenExpression: Expression {
    private let condition: () -> Bool
    private let thenExpression: Expression
    
    init(condition: @escaping () -> Bool, thenExpression: Expression) {
        self.condition = condition
        self.thenExpression = thenExpression
    }
    
    func interpret(context: Context) -> String {
        if condition() {
            return thenExpression.interpret(context: context)
        }
        return "Condition not met"
    }
}

// MARK: - Client (Interprets the language)
class HomeAutomationInterpreter {
    private var context = Context()
    
    func interpret(command: String) -> String {
        let parts = command.components(separatedBy: " ")
        
        if command.starts(with: "TURN ON") {
            let device = parts[2].replacingOccurrences(of: "\"", with: "")
            return TurnOnCommand(device: device).interpret(context: context)
        }
        else if command.starts(with: "SET THERMOSTAT") {
            let temp = Int(parts[3])!
            return SetThermostatCommand(temp: temp).interpret(context: context)
        }
        else if command.starts(with: "IF") {
            // Example: "IF TIME > \"18:00\" THEN TURN ON \"Living Room\""
            let condition = { return true } // Simplified for demo
            let thenCommand = command.components(separatedBy: "THEN ")[1]
            let thenExpression = interpret(command: thenCommand)
            return IfThenExpression(
                condition: condition,
                thenExpression: TurnOnCommand(device: "Living Room Lights")
            ).interpret(context: context)
        }
        
        return "Unknown command"
    }
}

// MARK: - Usage
let interpreter = HomeAutomationInterpreter()

print(interpreter.interpret(command: "TURN ON \"Kitchen Light\""))
// Output: "Turned ON Kitchen Light"

print(interpreter.interpret(command: "SET THERMOSTAT TO 72"))
// Output: "Thermostat set to 72°F"

print(interpreter.interpret(command: "IF TIME > \"18:00\" THEN TURN ON \"Living Room Lights\""))
// Output: "Turned ON Living Room Lights" (if condition is true)
````
Key Benefits

✅ Extensible Grammar: Easily add new commands (e.g., LOCK DOOR).

✅ Decouples Parsing from Execution: Change interpretation logic without modifying expressions.

✅ Great for Rule-Based Systems: E.g., pricing engines ("IF customer IS premium THEN APPLY 10% DISCOUNT").

### 🔁 Iterator(Behavioral)

The Iterator is a behavioral design pattern that provides a way to access elements of a collection sequentially without exposing its underlying representation. It's one of the most fundamental and frequently used patterns in iOS development.
Core Concept

Problem: You need to traverse different collections (arrays, trees, graphs) in a standardized way without coupling your code to their specific implementations.

Solution: The Iterator pattern:

 - Extracts the traversal behavior into a separate object

 - Provides a common interface for accessing elements

 - Keeps track of the current position

```swift
struct FoodItem: CustomStringConvertible {
    let name: String
    let isVegetarian: Bool
    let price: Double
    
    var description: String {
        return name
    }
}

// ---------------------------------------------------------------------------------------------------------------------

struct Menu {
    private let items: [FoodItem]
    
    init(items: [FoodItem]) {
        self.items = items
    }
}

extension Menu: Sequence {
    // The makeIterator() method needs to return an iterator
    // that knows how to filter for vegetarian items.
    func makeIterator() -> VegetarianIterator {
        return VegetarianIterator(items: self.items)
    }
}

struct VegetarianIterator: IteratorProtocol {
    private var internalIterator: IndexingIterator<[FoodItem]>

    init(items: [FoodItem]) {
        self.internalIterator = items.makeIterator()
    }
    
    mutating func next() -> FoodItem? {
        while let item = internalIterator.next() {
            if item.isVegetarian {
                return item
            }
        }
        return nil
    }
}

// ---------------------------------------------------------------------------------------------------------------------

// Usage:
let menu = Menu(items: [
    FoodItem(name: "Pizza", isVegetarian: true, price: 12.99),
    FoodItem(name: "Steak", isVegetarian: false, price: 24.99),
    FoodItem(name: "Salad", isVegetarian: true, price: 8.99)
])

print("Vegetarian options:")
for item in menu {
    print("- \(item.name) at $\(item.price)")
}
// Prints
//Vegetarian options:
//- Pizza at $12.99
//- Salad at $8.99
```
**Real-World iOS Examples**
   
```swift
 // Core Data NSFetchedResultsController:
let controller: NSFetchedResultsController<FoodItem> = ...
for item in controller.fetchedObjects ?? [] {
    // Iterates through managed objects
}

// File System Enumeration:
let files = FileManager.default.enumerator(atPath: "/path")
while let file = files?.nextObject() as? String {
    print(file)
}

// Combine Publishers:
[1, 2, 3]
    .publisher
    .sink { value in
        print(value) // Implicit iterator
    }
````    
Key Benefits in iOS Development
- Uniform Access: Traverse arrays, dictionaries, trees, and custom collections the same way
- Algorithm Separation: Keep traversal logic separate from business logic
**When to Use**
- Your collection has complex traversal logic
- You need different ways to traverse the same collection
- You want to hide your collection's implementation details
- You're working with tree/graph structures


## 📡 Mediator (Behavioral): 
The Mediator pattern centralizes complex communication between related objects, making them communicate through a single mediator instead of directly. This reduces tight coupling and simplifies maintenance, especially useful in UI frameworks like chat apps or Stock trading app

Example: Stock Trading Platform
**Overview**
Implements a stock exchange where:
- Buyers/Sellers communicate only through the Exchange (mediator)
- The Exchange handles order matching and trade execution
- Traders remain completely decoupled

**Components**
1. `StockExchangeMediator` - Protocol
2. `NYStockExchange` - Concrete mediator
3. `Trader` - Abstract colleague
4. `BuyOrder`/`SellOrder` - Command objects

```swift
import Foundation

// MARK: - Mediator Protocol
protocol StockExchangeMediator {
    func submitBuyOrder(_ order: BuyOrder)
    func submitSellOrder(_ order: SellOrder)
    func registerTrader(_ trader: Trader)
}

// MARK: - Concrete Mediator
final class NYStockExchange: StockExchangeMediator {
    private var traders = [String: Trader]()
    private var buyOrders = [BuyOrder]()
    private var sellOrders = [SellOrder]()
    
    func registerTrader(_ trader: Trader) {
        traders[trader.id] = trader
        print("ℹ️ Registered trader: \(trader.name)")
    }
    
    func submitBuyOrder(_ order: BuyOrder) {
        buyOrders.append(order)
        print("📈 Buy order submitted: \(order.quantity) x \(order.stock) @ \(order.price)")
        tryMatchTrades()
    }
    
    func submitSellOrder(_ order: SellOrder) {
        sellOrders.append(order)
        print("📉 Sell order submitted: \(order.quantity) x \(order.stock) @ \(order.price)")
        tryMatchTrades()
    }
    
    private func tryMatchTrades() {
        for (i, buyOrder) in buyOrders.enumerated() {
            for (j, sellOrder) in sellOrders.enumerated() 
            where buyOrder.stock == sellOrder.stock 
               && buyOrder.price >= sellOrder.price {
                
                let tradePrice = (buyOrder.price + sellOrder.price) / 2
                let quantity = min(buyOrder.quantity, sellOrder.quantity)
                
                print("""
                🟢 TRADE EXECUTED:
                   \(quantity) shares of \(buyOrder.stock) @ \(tradePrice)
                   Buyer: \(buyOrder.traderName)
                   Seller: \(sellOrder.traderName)
                """)
                
                // Update order quantities
                buyOrders[i].quantity -= quantity
                sellOrders[j].quantity -= quantity
                
                // Cleanup filled orders
                if buyOrders[i].quantity == 0 { buyOrders.remove(at: i) }
                if sellOrders[j].quantity == 0 { sellOrders.remove(at: j) }
                
                return
            }
        }
    }
}

// MARK: - Colleagues
class Trader {
    let id: String
    let name: String
    let mediator: StockExchangeMediator
    
    init(id: String, name: String, mediator: StockExchangeMediator) {
        self.id = id
        self.name = name
        self.mediator = mediator
        mediator.registerTrader(self)
    }
}

struct BuyOrder {
    let traderId: String
    let traderName: String
    let stock: String
    var quantity: Int
    let price: Double
}

struct SellOrder {
    let traderId: String
    let traderName: String
    let stock: String
    var quantity: Int
    let price: Double
}

// MARK: - Concrete Traders
final class InstitutionalTrader: Trader {
    func placeBuyOrder(stock: String, quantity: Int, price: Double) {
        let order = BuyOrder(
            traderId: self.id,
            traderName: self.name,
            stock: stock,
            quantity: quantity,
            price: price
        )
        mediator.submitBuyOrder(order)
    }
}

final class RetailTrader: Trader {
    func placeSellOrder(stock: String, quantity: Int, price: Double) {
        let order = SellOrder(
            traderId: self.id,
            traderName: self.name,
            stock: stock,
            quantity: quantity,
            price: price
        )
        mediator.submitSellOrder(order)
    }
}

// MARK: - Usage Example
func demonstrateStockExchange() {
    print("\n=== STOCK EXCHANGE DEMO ===")
    
    let nyse = NYStockExchange()
    
    let hedgeFund = InstitutionalTrader(
        id: "HF-123", 
        name: "Quantum Capital", 
        mediator: nyse
    )
    
    let retailInvestor = RetailTrader(
        id: "R-456", 
        name: "Jane Doe", 
        mediator: nyse
    )
    
    // Place orders
    hedgeFund.placeBuyOrder(stock: "AAPL", quantity: 1000, price: 175.50)
    retailInvestor.placeSellOrder(stock: "AAPL", quantity: 500, price: 175.25)
    
    // Place another sell order (won't fully match)
    retailInvestor.placeSellOrder(stock: "AAPL", quantity: 800, price: 176.00)
}

// Run the demo
demonstrateStockExchange()

/* Expected Output:
=== STOCK EXCHANGE DEMO ===
ℹ️ Registered trader: Quantum Capital
ℹ️ Registered trader: Jane Doe
📈 Buy order submitted: 1000 x AAPL @ 175.5
📉 Sell order submitted: 500 x AAPL @ 175.25
🟢 TRADE EXECUTED:
   500 shares of AAPL @ 175.375
   Buyer: Quantum Capital
   Seller: Jane Doe
📉 Sell order submitted: 800 x AAPL @ 176.0
*/
````
## 💾 Memento (Behavioral)
*Captures and externalizes an object's state for later restoration without breaking encapsulation. Enables undo/redo functionality and snapshots.*  
**Example:** *Text editor undo stack, game save points, or database transactions.*  

iOS System Examples
```swift
let undoManager = UndoManager()
undoManager.registerUndo(withTarget: self) { 
    $0.restore(from: memento) 
}

// Core Data's Rollback
context.rollback() // Reverts to last persisted state
````

**Let's understand with an example - Memento Pattern: State Snapshot System**

**Overview**
Captures and externalizes an object's state for later restoration while maintaining encapsulation.

**Key Components**
1. `Originator` - The object that produces state snapshots
2. `Memento` - Immutable state container  
3. `Caretaker` - Manages memento history

```swift
import Foundation

// MARK: - Originator (Text Editor)
final class TextEditor {
    private var text: String
    private var cursorPosition: Int
    
    init(text: String = "") {
        self.text = text
        self.cursorPosition = text.count
    }
    
    func type(_ char: Character) {
        text.insert(char, at: text.index(text.startIndex, offsetBy: cursorPosition))
        cursorPosition += 1
        printState()
    }
    
    func delete() {
        guard cursorPosition > 0 else { return }
        text.remove(at: text.index(text.startIndex, offsetBy: cursorPosition-1))
        cursorPosition -= 1
        printState()
    }
    
    private func printState() {
        print("📝 [\(cursorPosition)] \(text)")
    }
    
    // MARK: Memento Creation
    func save() -> EditorMemento {
        return EditorMemento(
            text: text,
            cursor: cursorPosition,
            date: Date()
        )
    }
    
    func restore(from memento: EditorMemento) {
        self.text = memento.text
        self.cursorPosition = memento.cursorPosition
        print("⎌ Restored to \(memento.date.formatted()):")
        printState()
    }
}

// MARK: - Memento (State Snapshot)
struct EditorMemento {
    let text: String
    let cursorPosition: Int
    let date: Date
    
    fileprivate init(text: String, cursor: Int, date: Date) {
        self.text = text
        self.cursorPosition = cursor
        self.date = date
    }
}

// MARK: - Caretaker (Undo Manager)
final class UndoHistory {
    private var stack: [EditorMemento] = []
    
    func save(_ memento: EditorMemento) {
        stack.append(memento)
        print("💾 Saved state (\(stack.count) total)")
    }
    
    func undo() -> EditorMemento? {
        guard stack.count > 1 else { return nil }
        _ = stack.popLast()
        return stack.last
    }
    
    func clear() {
        stack.removeAll()
    }
}

// MARK: - Usage Example
func demonstrateTextEditor() {
    let editor = TextEditor()
    let history = UndoHistory()
    
    // Initial save
    history.save(editor.save())
    
    // Edit document
    "Hello".forEach { editor.type($0) }
    history.save(editor.save())
    
    editor.type(" ")
    editor.type("W")
    editor.type("o")
    editor.delete() // Deletes 'o'
    editor.type("r")
    history.save(editor.save())
    
    // Undo last 2 actions
    print("\n--- Undo ---")
    if let memento = history.undo() {
        editor.restore(from: memento)
    }
    
    // Undo again
    if let memento = history.undo() {
        editor.restore(from: memento)
    }
}

// Run the demo
demonstrateTextEditor()

/* Expected Output:
📝 [1] H
📝 [2] He
📝 [3] Hel
📝 [4] Hell
📝 [5] Hello
💾 Saved state (2 total)
📝 [6] Hello 
📝 [7] Hello W
📝 [8] Hello Wo
📝 [7] Hello W
📝 [8] Hello Wr
💾 Saved state (3 total)

--- Undo ---
⎌ Restored to 6/9/24, 3:30 PM:
📝 [6] Hello 

⎌ Restored to 6/9/24, 3:30 PM:
📝 [5] Hello
*/
````

## 👀 Observer (Behavioral):

Establishes a one-to-many dependency between objects so that when one object changes state, all its dependents are notified automatically.

### Comparison with Similar Patterns

| Pattern       | Relation Direction | Communication Style | Use Case Example |
|--------------|--------------------|---------------------|------------------|
| **Observer** | One-to-many (push) | Automatic broadcasts | Weather updates to multiple displays |
| **Mediator** | Many-to-many       | Centralized routing  | Chat room message distribution |
| **Delegate** | One-to-one         | Direct callbacks     | UITableView cell configuration |

### Key Differences:
- **Observer**: Subjects don't know their observers (`@Published` in SwiftUI)
- **Mediator**: All communication goes through middleman (e.g., `UINavigationController`)
- **Delegate**: Tightly coupled 1:1 relationship (`UITableViewDelegate`)
```swift
import Combine

// Observable (Subject)
class WeatherStation {
    @Published var temperature: Double = 20.0 // Auto-publishes changes
}

// Observer
let station = WeatherStation()
var cancellable: AnyCancellable?

// Subscribe to changes
cancellable = station.$temperature
    .sink { newTemp in
        print("🌡️ Temperature now: \(newTemp)°C") 
    }

// Trigger change
station.temperature = 25.0 // Observer prints automatically

/* Output:
🌡️ Temperature now: 25.0°C
*/
````
Key Components:

    @Published property - The observable subject

    $ prefix access - Creates a publisher

    .sink - The observer's subscription

    AnyCancellable - Manages observation lifecycle

This is the modern Swift (Combine) way to implement Observer pattern with:

    Less boilerplate

    Type safety

    Built-in memory management

## 🔄 State (Behavioral)

The **State pattern** allows an object to alter its behavior when its internal state changes — it appears as if the object changed its class. It's useful when an object must change behavior at runtime depending on its current state.

### 🧑‍💻 Swift Code Example

The State pattern is excellent for managing complex logic by encapsulating state-specific behavior into separate objects. This approach makes your code more scalable and easier to maintain than using large `switch` statements or conditional `if/else` logic. A classic example for a scalable app is a **document editor**, which can exist in various states like `Draft`, `Moderation`, and `Published`.

### Context and States

First, we need to define the **context**—the object whose behavior changes based on its state. We also need to define the **state protocol** and the **concrete states**.

```swift
// State Protocol
// This defines the behavior that all concrete states must implement.
protocol DocumentState: AnyObject {
    func publish(in context: Document)
    func approve(in context: Document)
    func reject(in context: Document)
}
```

-----

### Concrete States

Each state class encapsulates the logic for a specific state. The `publish`, `approve`, and `reject` methods behave differently depending on the current state. The `context` (the `Document` instance) is passed so that the state object can change the document's state.

```swift
// Draft State
class DraftState: DocumentState {
    func publish(in context: Document) {
        print("Draft is submitted for moderation.")
        context.state = ModerationState()
    }
    
    func approve(in context: Document) {
        print("Cannot approve a draft. It must be published first.")
    }
    
    func reject(in context: Document) {
        print("Cannot reject a draft. It is not yet in moderation.")
    }
}

// Moderation State
class ModerationState: DocumentState {
    func publish(in context: Document) {
        print("Cannot publish while in moderation. You must approve it first.")
    }
    
    func approve(in context: Document) {
        print("Document is approved and published.")
        context.state = PublishedState()
    }
    
    func reject(in context: Document) {
        print("Document is rejected and sent back to draft.")
        context.state = DraftState()
    }
}

// Published State
class PublishedState: DocumentState {
    func publish(in context: Document) {
        print("Document is already published.")
    }
    
    func approve(in context: Document) {
        print("Document is already published and does not need approval.")
    }
    
    func reject(in context: Document) {
        print("Cannot reject a published document.")
    }
}
```

-----

### The Context Object

The `Document` class is the **context**. It holds a reference to the current state and delegates all actions to it. This decouples the document's main logic from the state-specific behavior.

```swift
class Document {
    var state: DocumentState
    
    init() {
        self.state = DraftState() // Initial state
    }
    
    func publish() {
        state.publish(in: self)
    }
    
    func approve() {
        state.approve(in: self)
    }
    
    func reject() {
        state.reject(in: self)
    }
}
```

### Usage

The client code interacts with the `Document` object without knowing or caring about its internal state machine. The behavior changes automatically based on the current state.

```swift
let myDocument = Document()

// Initial state: Draft
print("Current State: \(type(of: myDocument.state))") // Prints "DraftState"
myDocument.approve() // "Cannot approve a draft..."
myDocument.publish() // "Draft is submitted for moderation."

// State changed to Moderation
print("Current State: \(type(of: myDocument.state))") // Prints "ModerationState"
myDocument.reject() // "Document is rejected..."

// State changed back to Draft
print("Current State: \(type(of: myDocument.state))") // Prints "DraftState"
myDocument.publish() // "Draft is submitted for moderation."

// State changed to Moderation
print("Current State: \(type(of: myDocument.state))") // Prints "ModerationState"
myDocument.approve() // "Document is approved and published."

// Final State: Published
print("Current State: \(type(of: myDocument.state))") // Prints "PublishedState"
myDocument.publish() // "Document is already published."
```

**iOS and Apple frameworks internally use the State pattern**, especially in scenarios where **an object’s behavior changes based on its current state**. Below are real-world examples:

---

### ✅ 1. `URLSessionTask` State Management

Each task (`dataTask`, `uploadTask`, etc.) has a `state`:

```swift
public enum URLSessionTask.State {
    case running
    case suspended
    case canceling
    case completed
}
```

- The behavior of the task changes based on this state.
- You cannot resume a completed task or cancel a suspended one — only allowed transitions are handled.

🧠 **State Pattern:** Each state governs what next action is valid — mimicking the classic pattern.

---

### ✅ 2. `UIViewController` Lifecycle

A `UIViewController` transitions through multiple internal states:

- `viewDidLoad`
- `viewWillAppear`
- `viewDidAppear`
- `viewWillDisappear`
- `viewDidDisappear`

Each of these corresponds to different internal "states" and determines what setup or teardown logic runs.

🧠 **State Pattern:** The controller behaves differently depending on its current stage in the lifecycle.

---

### ✅ 3. `UIButton` States

A `UIButton` can be in:

- `.normal`
- `.highlighted`
- `.disabled`
- `.selected`

```swift
button.setTitle("Submit", for: .normal)
button.setTitle("Submitting...", for: .disabled)
```

Each state defines different behavior and visuals.

🧠 **State Pattern:** UIButton modifies appearance and behavior based on state automatically — internal implementation leverages State-like behavior.

---

### ✅ 4. `AVPlayer`

An `AVPlayer` can be:

- Playing
- Paused
- Stopped
- Buffering

Each of these internal states modifies what actions are allowed (e.g., can't pause a stopped player).

---

### 📋 Summary

| Area         | iOS API                     | Pattern Used |
|--------------|-----------------------------|---------------|
| Networking   | `URLSessionTask.State`       | ✅ State      |
| UI Lifecycle | `UIViewController`           | ✅ State      |
| UI Controls  | `UIButton`, `UISwitch`, etc. | ✅ State      |
| Media        | `AVPlayer`                   | ✅ State      |

---
## 🎯 Strategy (Behavioral)

The **Strategy Pattern** is used to define a family of algorithms, encapsulate each one, and make them interchangeable. It allows the algorithm to vary independently from clients that use it.

---

### ✅ Real-World Analogy

Imagine a **Navigation App** (like Google Maps or Apple Maps). You can choose how you want to reach your destination:

- 🚗 **Fastest Route**
- 🚦 **Least Traffic**
- 🚌 **Public Transport**
- 🚶 **Walking**

Each of these is a *strategy* for navigation. The app lets you switch strategies at runtime without rewriting the logic of the app itself.

---

### 💻 Swift Example

```swift
// MARK: - Strategy Protocol
protocol RouteStrategy {
    func buildRoute(from: String, to: String)
}

// MARK: - Concrete Strategies
struct FastestRoute: RouteStrategy {
    func buildRoute(from: String, to: String) {
        print("🚗 Fastest route from \(from) to \(to)")
    }
}

struct LeastTrafficRoute: RouteStrategy {
    func buildRoute(from: String, to: String) {
        print("🚙 Least traffic route from \(from) to \(to)")
    }
}

struct PublicTransportRoute: RouteStrategy {
    func buildRoute(from: String, to: String) {
        print("🚌 Public transport route from \(from) to \(to)")
    }
}

// MARK: - Context
class NavigationContext {
    private var strategy: RouteStrategy

    init(strategy: RouteStrategy) {
        self.strategy = strategy
    }

    func updateStrategy(_ strategy: RouteStrategy) {
        self.strategy = strategy
    }

    func navigate(from: String, to: String) {
        strategy.buildRoute(from: from, to: to)
    }
}
```

---

### 🧪 Usage

```swift
let nav = NavigationContext(strategy: FastestRoute())
nav.navigate(from: "Home", to: "Work")

nav.updateStrategy(LeastTrafficRoute())
nav.navigate(from: "Home", to: "Work")

nav.updateStrategy(PublicTransportRoute())
nav.navigate(from: "Home", to: "Work")
```

---

### 📦 Benefits

- Promotes **Open/Closed Principle** — add new strategies without modifying existing code.
- Helps separate concerns — algorithm logic is decoupled from usage.
- Easily testable and extendable.

---

### 📱 Where It's Used in iOS

- `UICollectionView` / `UITableView` uses different *layout strategies* (`UICollectionViewFlowLayout`, `UICollectionViewCompositionalLayout`)
- `UIViewControllerTransitioningDelegate` allows different transition *animation strategies*

---
<a id="template-method"></a>
## 📝 Template-Method-(Behavioral)

The **Template Method** pattern defines the *skeleton* of an algorithm in a base class, while allowing subclasses to redefine specific steps without changing the algorithm's overall structure.

This promotes **code reuse**, enforces **consistent workflows**, and allows flexibility in extending behavior where needed.

---

### ✅ When to Use

- When multiple classes share the same algorithm structure but differ in specific steps.
- When you want to avoid code duplication while allowing extensions.

---

### 🚀 Real-World Example

#### 📦 Online Order Processing(test)

```swift
class OrderProcessTemplate {
    func processOrder() {
        selectItems()
        makePayment()
        shipItems()
        sendReceipt()
    }

    func selectItems() {
        print("Items selected")
    }

    func makePayment() {
        fatalError("Subclass must override makePayment()")
    }

    func shipItems() {
        print("Items shipped")
    }

    func sendReceipt() {
        print("Receipt sent")
    }
}

class OnlineOrder: OrderProcessTemplate {
    override func makePayment() {
        print("Paid using UPI")
    }
}

let order = OnlineOrder()
order.processOrder()
````

---

### 🍎 iOS Built-in Example

UIKit uses the Template Method pattern extensively. For example:

#### 🧱 `UITableView`

Apple defines the *structure* of rendering a table, but developers customize *specific steps* via delegate methods:

```swift
func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int

func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell
```

Apple calls the template lifecycle internally, but gives you hooks to override critical steps.

---

### 🧩 Summary

| Role           | Description                                              |
| -------------- | -------------------------------------------------------- |
| Abstract Class | Defines the template method and default steps            |
| Subclass       | Overrides one or more steps to provide specific behavior |

> ✅ Helps maintain algorithm consistency while offering flexibility for customization.

---

## 👣 Visitor (Behavioral)

The **Visitor** pattern allows you to add new operations to a group of objects without changing their classes. Instead of adding logic to the objects, you create a separate visitor that implements the operation.

---

### ✅ When to Use

- You want to **add new behaviors** to a structure of objects **without modifying** the objects.
- You have a **class hierarchy** and need to perform operations across multiple types **in a uniform way**.
- The object structure is **stable**, but new operations are added frequently.

---

### 💡 Real-World Example

#### 📄 Document Exporter

```swift
protocol Document {
    func accept(visitor: DocumentVisitor)
}

class PDFDocument: Document {
    func accept(visitor: DocumentVisitor) {
        visitor.visit(pdf: self)
    }
}

class WordDocument: Document {
    func accept(visitor: DocumentVisitor) {
        visitor.visit(word: self)
    }
}

protocol DocumentVisitor {
    func visit(pdf: PDFDocument)
    func visit(word: WordDocument)
}

class PrintVisitor: DocumentVisitor {
    func visit(pdf: PDFDocument) {
        print("🖨️ Printing PDF Document")
    }

    func visit(word: WordDocument) {
        print("🖨️ Printing Word Document")
    }
}
````

#### 🧪 Usage:

```swift
let documents: [Document] = [PDFDocument(), WordDocument()]
let printer = PrintVisitor()

for doc in documents {
    doc.accept(visitor: printer)
}
```

---

### 🍎 iOS Built-in Usage

While iOS doesn't explicitly use the Visitor pattern, similar behavior can be seen in:

* **File system traversal** using `FileManager.delegate` for performing actions on files/folders.
* **Core Animation** (`CALayer`, `CATextLayer`, `CAShapeLayer`) — traversing view layers and applying logic.
* **UIKit Accessibility** API or Responder Chain — where different UI elements are "visited" and acted upon based on type.

---

### 🧩 Summary

| Role              | Description                                       |
| ----------------- | ------------------------------------------------- |
| `Visitor`         | Declares `visit()` methods for each concrete type |
| `Element`         | Has an `accept(visitor:)` method                  |
| `ConcreteVisitor` | Implements actions to be taken on each element    |

> ✅ The Visitor pattern promotes **open/closed principle** by letting you add new operations without modifying existing classes.

---

