---
title: "How to Reverse a Stack using Recursion ?"
date: 2023-08-03 11:36:41
categories: ['Recursion', 'StacksQueues']
layout: post
---

<!-- wp:paragraph -->
<a href="https://www.geeksforgeeks.org/reverse-a-stack-using-recursion/" target="_blank" rel="noopener" title=""></a> Write a program to reverse a stack using recursion.<br><strong>Input</strong>: elements present in stack from top to bottom 1 2 3 4 <br><strong>Output</strong>: 4 3 2 1 


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
    
}</code></pre>
<!-- /wp:code -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">
func reverseStackUsingRecursion(_ st: inout Stack<Int>) {
    if !st.isEmpty {
        // Hold all items in Function Call Stack until we reach end of the stack
        var peekElement = st.peek()
        st.pop()
        reverseStackUsingRecursion(&st)
        // Insert all the items held in Function Call Stack one by one from the bottom
        // to top. Every item is inserted at the bottom insert_at_bottom(x);
        insertAtBottom(&st, peekElement!)
    }
}

func insertAtBottom(_ st: inout Stack<Int>, _ item: Int) {
    if st.isEmpty {
        st.push(item)
    } else {
        // All items are held in Function Call Stack until we reach end of the stack. When the stack becomes
        // empty, the st.size() becomes 0, the above if part is executed and the item is inserted at the bottom
        let a = st.peek()!
        st.pop()
        insertAtBottom(&st, item)
        // push all the items held in Function Call Stack once the item is inserted at the bottom
        st.push(a)
    }
}

var stackInput2 = Stack<Int>()
stackInput2.push(1)
stackInput2.push(2)
stackInput2.push(3)
stackInput2.push(4)
print("Input---->", stackInput2)// 4 3 2 1
reverseStackUsingRecursion(&stackInput2)
print("Output---->", stackInput2) // 1 2 3 4</code></pre>
<!-- /wp:code -->