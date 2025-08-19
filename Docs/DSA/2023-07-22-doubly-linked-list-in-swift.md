---
title: "Doubly Linked List in swift"
date: 2023-07-22 14:19:21
categories: ['LinkedList']
layout: post
---

<!-- wp:paragraph -->
Here is example of Doubly Link list in swift


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">//: # Doubky Linked Lists in Swift

// Doubly Link list have previous & next pointer address.

///  DoublyLinkedListNode's Node class declaration
///
public class DoublyLinkedListNode<T> {
    var item: T
    var next: DoublyLinkedListNode?
    weak var previous: DoublyLinkedListNode?
    
    public init(item: T) {
        self.item = item
    }
}

public final class DoublyLinkedList<T> {
    
    /// The head of the DoublyLinkedList List
    private(set) var head: DoublyLinkedListNode<T>?
    
    /// Get last node
    public var last: DoublyLinkedListNode<T>? {
        guard var node = head else {
            return nil // Means Doubly link list is empty
        }
        
        while let next = node.next {
            node = next
        }
        return node
    }
    
    ///  To check is list empty ?
    public var isEmpty: Bool {
        return head == nil
    }
    
    /// Count number of nodes
    public var count: Int {
        guard var node = head else {
            return 0
        }
        
        var count = 1
        while let next = node.next {
            node = next
            count += 1
        }
        return count
    }
    
    /// Default initializer
    public init() {}
    
    
    /// Subscript function to return the node at a specific index
    ///
    /// - Parameter index: Integer value of the requested value's index example linkedList = x 
    public subscript(index: Int) -> T? {
        let node = self.node(at: index)
        return node?.item
    }

    public func node(at index: Int) -> DoublyLinkedListNode<T>? {
        if index <= 0, head == nil {
            return nil
        }
        if index == 0 {
            return head
        } else {
            var node = head?.next
            for _ in 1..<index {
                node = node?.next
                if node == nil {
                    break
                }
            }
            return node
        }
    }
    
    /// Append a value to the end of the list
    ///
    /// - Parameter value: The data value to be appended
    public func append(_ item: T) {
        let newNode = DoublyLinkedListNode<T>(item: item)
        append(newNode)
    }
    
    /// Append a copy of a DoublyLinkedListNode to the end of the list.
    ///
    /// - Parameter node: The node containing the value to be appended
    public func append(_ node: DoublyLinkedListNode<T>) {
        let newNode = node
        if let lastNode = last {
            newNode.previous = lastNode
            lastNode.next = newNode
        } else {
            head = newNode
        }
    }
    
    /// Append a copy of a LinkedList to the end of the list.
    ///
    /// - Parameter list: The list to be copied and appended.
    public func append(_ list: DoublyLinkedList) {
        var nodeToCopy = list.head
        while let node = nodeToCopy {
            append(node.item)
            nodeToCopy = node.next
        }
    }
    
 
    public func insert(_ item: T, at index: Int) {
        let newNode = DoublyLinkedListNode<T>(item: item)
        insert(newNode, at: index)
    }

    public func insert(_ newNode: DoublyLinkedListNode<T>, at index: Int) {
        if index == 0 {
            newNode.next = head
            head?.previous = newNode
            head = newNode
        } else {
            let prev = node(at: index - 1)
            let next = prev?.next
            newNode.previous = prev
            newNode.next = next
            next?.previous = newNode
            prev?.next = newNode
        }
    }
    
    /// Insert a copy of a LinkedList at a specific index. Crashes if index is out of bounds (0...self.count)
    ///
    /// - Parameters:
    ///   - list: The LinkedList to be copied and inserted
    ///   - index: Integer value of the index to be inserted at
    public func insert(_ list: DoublyLinkedList, at index: Int) {
        if list.isEmpty { return }
        
        if index == 0 {
            list.last?.next = head
            head = list.head
        } else {
            let prev = node(at: index - 1)
            let next = prev?.next
            
            prev?.next = list.head
            list.head?.previous = prev
            
            list.last?.next = next
            next?.previous = list.last
        }
    }
    
    public func removeAll() {
        head = nil
    }
    
    /// Function to remove a specific node This is Doubly Link List special feature which is not available in singly linked list
    ///
    /// - Parameter node: The node to be deleted
    /// - Returns: The data value contained in the deleted node.
    @discardableResult public func remove(node: DoublyLinkedListNode<T>) -> T {
        let prev = node.previous
        let next = node.next
        
        if let prev = prev {
            prev.next = next
        } else {
            head = next
        }
        next?.previous = prev
        
        node.previous = nil
        node.next = nil
        return node.item
    }
    
    /// Function to remove the last node/value in the list. Crashes if the list is empty
    ///
    /// - Returns: The data value contained in the deleted node.
    @discardableResult public func removeLast() -> T? {
        if let lastNode = last {
            return remove(node: lastNode)
        }
        return nil
    }
    
    /// Function to remove a node/value at a specific index. Crashes if index is out of bounds (0...self.count)
    ///
    /// - Parameter index: Integer value of the index of the node to be removed
    /// - Returns: The data value contained in the deleted node
    @discardableResult public func remove(at index: Int) -> T? {
        if let node = self.node(at: index) {
            return remove(node: node)
        }
        return nil
    }
}

//: Some Doubly Link List helper functions..

// MARK: - Extension to enable the standard conversion of a list to String
// To be change from Singly Linked List
extension DoublyLinkedList: CustomStringConvertible {
    public var description: String {
        var s = "["
        var node = head
        while let nd = node {
            s += "\(nd.item)"
            node = nd.next
            if node != nil { s += " <- -> " }
        }
        return s + "]"
    }
}

// MARK: - Reverse Doubly linked list
extension DoublyLinkedList {
    public func reverse() {
        var node = head
        while let currentNode = node {
            node = currentNode.next
            swap(&currentNode.next, &currentNode.previous)
            head = currentNode
        }
    }
    // Method 2
    public func reverseLinkList() {
      //  tail = head
        var prev = head
        var current = head?.next
        prev?.next = nil
        
        while current != nil {
            let next = current?.next
            current?.next = prev
            prev = current
            current = next
        }
        head = prev
    }
}

// MARK: - Implement High order functions in Doubly link list like 'map' & 'filter' functions
extension DoublyLinkedList {
    // Example Usage: list.map { obj in obj.count }
    public func map<U>(transform: (T) -> U) -> DoublyLinkedList<U> {
        let result = DoublyLinkedList<U>()
        var node = head
        while let nd = node {
            result.append(transform(nd.item))
            node = nd.next
        }
        return result
    }
    // Example usage:--> list.filter { obj in obj.count > 5 }
    public func filter(predicate: (T) -> Bool) -> DoublyLinkedList<T> {
        let result = DoublyLinkedList<T>()
        var node = head
        while let nd = node {
            if predicate(nd.item) {
                result.append(nd.item)
            }
            node = nd.next
        }
        return result
    }
}

// MARK: - Extension to enable initialization from an Array
extension DoublyLinkedList {
    // For using let arrrayLit = LinkedList(array: Array(repeating: 0, count: 10))
    convenience init(array: Array<T>) {
        self.init()
        array.forEach { append($0) }
    }
}

// MARK: - Extension to enable initialization from an Array Literal
// For using let arrayLiteralInitInfer: LinkedList = 
extension DoublyLinkedList: ExpressibleByArrayLiteral {
    public convenience init(arrayLiteral elements: T...) {
        self.init()
        elements.forEach { append($0) }
    }
}

// MARK: - Collection
extension DoublyLinkedList: Collection {
        
    /// The position of the first element in a nonempty collection.
    ///
    /// - Complexity: O(1)
    public var startIndex: DoublyLinkedListIndex<T> {
        get {
            return DoublyLinkedListIndex<T>(node: head, tag: 0)
        }
    }
    
    /// The collection's "past the end" position---that is, the position one
    /// greater than the last valid subscript argument.
    /// - Complexity: O(n), where n is the number of elements in the list. This can be improved by keeping a reference
    ///   to the last node in the collection.
    public var endIndex: DoublyLinkedListIndex<T> {
        get {
            if let h = self.head {
                return DoublyLinkedListIndex<T>(node: h, tag: count)
            } else {
                return DoublyLinkedListIndex<T>(node: nil, tag: startIndex.tag)
            }
        }
    }
    
    public subscript(position: DoublyLinkedListIndex<T>) -> T? {
        get {
            return position.node?.item
        }
    }
    
    public func index(after idx: DoublyLinkedListIndex<T>) -> DoublyLinkedListIndex<T> {
        return DoublyLinkedListIndex<T>(node: idx.node?.next, tag: idx.tag + 1)
    }
}

// MARK: - Collection Index
/// Custom index type that contains a reference to the node at index 'tag'
public struct DoublyLinkedListIndex<T>: Comparable {
    
    fileprivate let node: DoublyLinkedListNode<T>?
    fileprivate let tag: Int
    
    public static func==<T>(lhs: DoublyLinkedListIndex<T>, rhs: DoublyLinkedListIndex<T>) -> Bool {
        return (lhs.tag == rhs.tag)
    }
    
    public static func< <T>(lhs: DoublyLinkedListIndex<T>, rhs: DoublyLinkedListIndex<T>) -> Bool {
        return (lhs.tag < rhs.tag)
    }
}
//: Some examples
let list = DoublyLinkedList<String>()
list.isEmpty                  // true
list.head                    // nil
list.last                     // nil

list.append("Car")
list.isEmpty                  // false
list.head?.item             // "Car"
list.last?.item              // "Car
list.count                    // 1

list.append("DSA is EASY")
list.head?.item             // "Car""
list.last?.item              // "DSA is EASY"
list.count                    // 2

list.head?.previous          // nil
list.head?.next?.item       // "DSA is EASY"
list.last?.previous?.item    // "Car"
list.last?.next               // nil

list.node(at: 0)?.item    // "Car"
list.node(at: 1)?.item    // "DSA is EASY"
//list.node(at: 2)           // crash!

list     // "Car"
list     // "DSA is EASY"
//list   // crash!

let list2 = DoublyLinkedList<String>()
list2.append("Append Goodbye")
list2.append("Append World")
list.append(list2)            // 
list2.removeAll()             // 
list2.isEmpty                 // true
list.removeLast()             // "Added World"
list.remove(at: 2)       // "Append Goodbye"

print("reversed LinkList-->", list2.description)


list.insert("Janesh Suthar", at: 1)
list     // "Car"
list     // "Janesh Suthar"
list     // "DSA is EASY"
print(list)

//list.reverse()   // 
list.reverseLinkList()

list.node(at: 0)?.item = "Toyota" // changing values in doubly link list
list.node(at: 1)?.item = "Maruti"
let m = list.map { s in s.count }
m    // 
let f = list.filter { s in s.count > 5 }
f    // 

list.remove(node: list.head!) // "Toyota"
list.count                     // 2
list                        // "Maruti"
list                        // "Hello"

list.count                     // 2
list.removeLast()              // "Hello"
list.head?.item
list.count                     // 1
list                        // "Maruti"

list.remove(at: 0)        // "Maruti"
list.count                     // 0

let list3 = DoublyLinkedList<String>()
list3.insert("2", at: 0) // 
list3.count                   // 1
list3.insert("4", at: 1) // 
list3.count                   // 2
list3.insert("5", at: 2) // 
list3.count                   // 3
list3.insert("3", at: 1) // 
list3.insert("1", at: 0) // 

let list4 = DoublyLinkedList<String>()
list4.insert(list3, at: 0) // 
list4.count                     // 5

let list5 = DoublyLinkedList<String>()
list5.append("0")                // 
list5.insert("End", at:1)   // 
list5.count                      // 2
list5.insert(list4, at: 1)  // 
list5.count                      // 7


let linkedList: DoublyLinkedList<Int> =  // 
linkedList.count               // 4
linkedList                  // 1

// Array example: -
let listArrayLiteral2: DoublyLinkedList = 
listArrayLiteral2.count        // 4
listArrayLiteral2           // "Hello"
listArrayLiteral2.removeLast()  // "You"


// Conformance to the Collection protocol
let collection: DoublyLinkedList<Int> = 
let collection2: DoublyLinkedList<Int> = 
print(" is same ?", collection.first == collection2.first)
let index2 = collection.index(collection.startIndex, offsetBy: 2)
let item = collection // 3

collection.reverseLinkList()
print("printing collection--> ", collection)
// Find sum from doubly Link List Iterating in a for loop, since the Sequence protocol allows this.
var sum = 0
for element in collection {
    sum += element ?? 0
}
sum //15

// Get Sum of Doubly Link List though 'reduce', another method defined in an extension of Sequence. Collections are Sequences.
let sumOfElements = collection.reduce(0) {$0 + $1!} // 15




</code></pre>
<!-- /wp:code -->