# ⛓️ Chain Of Responsibility(Behavioral)
## Expense Approval System (Chain of Responsibility Pattern)

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
