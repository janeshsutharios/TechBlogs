# ⛓️ Chain Of Responsibility(Behavioral)
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

# 🖥️ Command (Behavioral)

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

# 📜 Interpreter (Behavioral)
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

# 🔁 Iterator(Behavioral)

The Iterator is a behavioral design pattern that provides a way to access elements of a collection sequentially without exposing its underlying representation. It's one of the most fundamental and frequently used patterns in iOS development.
Core Concept

Problem: You need to traverse different collections (arrays, trees, graphs) in a standardized way without coupling your code to their specific implementations.

Solution: The Iterator pattern:

 - Extracts the traversal behavior into a separate object

 - Provides a common interface for accessing elements

 - Keeps track of the current position

iOS/Swift Implementation
1. Native Swift Iterators

Swift has built-in iterator support through two protocols:
```swift
protocol Sequence {
    associatedtype Iterator: IteratorProtocol
    func makeIterator() -> Iterator
}

protocol IteratorProtocol {
    associatedtype Element
    mutating func next() -> Element?
}
````
**Example with Array:**
```swift
let foods = ["Pizza", "Sushi", "Burger"]
var iterator = foods.makeIterator()

while let item = iterator.next() {
    print(item)
}
// Prints: Pizza, Sushi, Burger
````
2. Custom Iterator Example

Let's create an iterator for your FoodApp that filters vegetarian items:
```swift
struct FoodItem {
    let name: String
    let isVegetarian: Bool
    let price: Double
}

struct VegetarianIterator: IteratorProtocol {
    private var iterator: IndexingIterator<[FoodItem]>
    
    init(items: [FoodItem]) {
        self.iterator = items.makeIterator()
    }
    
    mutating func next() -> FoodItem? {
        while let item = iterator.next() {
            if item.isVegetarian {
                return item
            }
        }
        return nil
    }
}

// Usage:
let menu = [
    FoodItem(name: "Pizza", isVegetarian: true, price: 12.99),
    FoodItem(name: "Steak", isVegetarian: false, price: 24.99),
    FoodItem(name: "Salad", isVegetarian: true, price: 8.99)
]

var vegIterator = VegetarianIterator(items: menu)
while let item = vegIterator.next() {
    print("Vegetarian option: \(item.name)")
}
// Prints: Pizza, Salad
````
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


# 📡 Mediator (Behavioral): 
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
