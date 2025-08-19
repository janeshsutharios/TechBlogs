---
title: "Reverse Doubly Link List."
date: 2023-07-29 17:18:22
categories: ['LinkedList']
layout: post
---

<!-- wp:paragraph -->
<a href="https://www.geeksforgeeks.org/reverse-a-doubly-linked-list/" target="_blank" rel="noopener" title=""></a> Given a <a href="https://www.geeksforgeeks.org/doubly-linked-list/">Doubly Linked List</a>, the task is to reverse the given Doubly Linked List.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
Here we can can solve by two approach #1 Iterative #2 Recursive 


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">public class DoublyLinkedListNode<T> {
    var item: T
    var next: DoublyLinkedListNode?
    weak var previous: DoublyLinkedListNode?
    
    public init(item: T) {
        self.item = item
    }
}
// MARK: - Reverse Doubly linked list
public func reverse() {
    //        var node = head
    //        while let currentNode = node {
    //            node = currentNode.next
    //            swap(&currentNode.next, &currentNode.previous)
    //            head = currentNode
    //        }
    // Or
    var node = head
    while let currentNode = node {
        node = currentNode.next
        let nxt = currentNode.next
        let pvs = currentNode.previous
        currentNode.next = pvs
        currentNode.previous = nxt
        head = currentNode
    }
}

func reverseListRecursive(_ head: DoublyLinkedListNode<T>?) -> DoublyLinkedListNode<T>? {
    if head == nil || head?.next == nil {
        return head
    }
    let temp = reverseListRecursive(head?.next)
    head?.next?.next = head
    head?.previous = head?.next
    head?.next = nil
    return temp
}
</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
For information about usage visit my <a href="https://github.com/janeshsutharios/DSA_iOS_Swift/tree/main/Topics_Playground/DoublyLinkList.playground" target="_blank" rel="noopener" title="">Githhub Page</a>


<!-- /wp:paragraph -->