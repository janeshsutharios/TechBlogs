# ⛓️ Chain Of Responsibility(Behavioral)
Decouples request senders from receivers by allowing multiple handlers to process a request sequentially. Each handler decides to act or pass it down the chain.

## Example - Expense Approval System 
A Swift implementation of the **Chain of Responsibility** behavioral design pattern for handling multi-level expense approvals in a corporate workflow.
Define Expenses -> Build the Chain -> Submit for Approval
## Features
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
