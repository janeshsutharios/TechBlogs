---
title: "How to Sort a Stack using Recursion"
date: 2023-08-03 11:18:24
categories: ['Recursion', 'StacksQueues']
layout: post
---

<!-- wp:paragraph -->
<a href="https://www.geeksforgeeks.org/sort-a-stack-using-recursion/" target="_blank" rel="noopener" title="">: </a>Given a <strong>stack</strong>, the task is to sort it using recursion.<br>I<strong>nput</strong><em>: elements present in stack from top to bottom -3 14 18 -5 30</em><br><strong>Output</strong><em>: 30 18 14 -3 -5</em><br><em><strong>Explanation: </strong>The given stack is sorted know<strong> 30 > 18 > 14 > -3 > -5</strong></em>


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// Stack Definition Starts
public struct Stack<Element> {
    
    private var storage:  = 
    
    public init() { }
}

extension Stack: CustomDebugStringConvertible {
    
    public var debugDescription: String {
    """
    ----top----
    \(storage.map { "\($0)" }.reversed().joined(separator: "\n"))
    -----------
    """
    }
    
    public mutating func push(_ element: Element) {
        storage.append(element)
    }
    
    @discardableResult
    public mutating func pop() -> Element? {
        storage.popLast()
    }
    
    public func peek() -> Element? {
        storage.last
    }
    
    public var isEmpty: Bool {
        peek() == nil
    }
    
}
// Stack Defination Ends


// Swift program to sort a Stack using recursion
// Note that here predefined Stack class is used  for stack operation

// Recursive Method to insert an item x in sorted way
func sortedInsert(_ s: inout Stack<Int>, _ item: Int) {
    // Base case: Either stack is empty or newly inserted item is greater than top (more than all existing)
    if s.isEmpty || item > s.peek()! {
       // print("Peek & item is ----------- ",s.peek(), item)
        s.push(item)
        return
    }
    // If top is greater, remove the top item and recur
    let temp = s.pop()
    //print(" Insert Poped Item in stack---- ",temp!)
    sortedInsert(&s, item);
   // print("Recursion Call Now Add back temp------- ",temp!)
    // Put back the top item removed earlier
    s.push(temp!)
}

// Method to sort stack
func sortStack(_ s: inout Stack<Int>) {
    // Base case If stack is empty return
    if s.isEmpty { return }
    // Remove the top item
    let topItem = s.pop()
    // Sort remaining stack
    sortStack(&s)
    // Push the top item back in sorted stack
    sortedInsert(&s, topItem!)
}

var stackInput = Stack<Int>()
stackInput.push(-3)
stackInput.push(30)
stackInput.push(-5)
//stackInput.push(18)
stackInput.push(14)
print("Input---->", stackInput)
/**
 Input----> ----top----
 14
 -5
 30
 -3
 */
sortStack(&stackInput);
print("Output--->", stackInput)
/**
 Output---> ----top----
 30
 14
 -3
 -5
 -----------
 */
</code></pre>
<!-- /wp:code -->

<!-- wp:image {"id":2130,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large">![](/TechBlogs/Assets/Website/2023/08/Sort-stack-using-recursion-925x1024.jpg)</figure>
<!-- /wp:image -->