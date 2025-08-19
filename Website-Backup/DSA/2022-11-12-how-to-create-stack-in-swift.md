---
title: "How to create Stack in Swift ?"
date: 2022-11-12 10:50:03
categories: ['DSA', 'Stack in swift']
layout: post
---

<!-- wp:paragraph -->
We will create a stack where we perform push, pop and other operations. Here we have covered question - Print Reverse Stacks <a href="https://github.com/janeshsutharios/DSA_iOS_Swift" target="_blank" rel="noopener" title="">More can be find here </a>


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// Post from www.JaneshSwift.com
// Creating a stack with Array type storage
public struct Stack<Element> {
    
    private var storage:  = 
    
    public init() { }
}

// To express Stack like array literals
extension Stack: ExpressibleByArrayLiteral {
  public init(arrayLiteral elements: Element...) {
    storage = elements
  }
}

// To make iterate over loop conform with sequence protocol
extension Stack: Sequence {
  public func makeIterator() -> AnyIterator<Element> {
    var curr = self
    return AnyIterator {
      return curr.pop()
    }
  }
}

// To print out stack. Because stack is LIFO we just have to reverse the array
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


var stack = Stack<Int>()
stack.push(1)
stack.push(2)
stack.push(3)
stack.push(4)

print("top element-->", stack.peek())

print("stack is -->",stack)

if let poppedElement = stack.pop() {
    assert(4 == poppedElement)
    print("Popped: \(poppedElement)")
}

// Question 1 : Reverse print elements of stacks
func printInReverse<T: Sequence>(stacksData: ) {
    
    var newStack: Stack<T> = 
    
    for value in stacksData {
        newStack.push(value)
     }
    
    while let poppedElement = newStack.pop() {
        print("current popped:--", poppedElement)
    }
}

let stackExample1 :Stack<Int> = 
printInReverse(stacksData: stackExample1)</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":4,"textColor":"ast-global-color-1"} -->
<h4 class="has-ast-global-color-1-color has-text-color">2. Check Balance <a href="https://leetcode.com/problems/longest-valid-parentheses">Parentheses</a>.  </h4>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// Question 2 : Check balance Parathesis in string
// Example: -- (Hello) True  & (Hel False

func checkParentheses(_ string: String) -> Bool {
    var stack = Stack<Character>()
    
    for currentChar in string {
        switch currentChar {
        case "(":
            stack.push(")")
        case ")":
            if stack.pop() == nil {
                return false
            }
        default:
            continue
        }
    }
    return stack.isEmpty
}
print(checkParentheses("(Hello)"))</code></pre>
<!-- /wp:code -->