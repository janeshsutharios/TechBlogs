---
title: "How to create deep copy of linked list who has random pointer"
date: 2023-07-30 03:52:40
categories: ['LinkedList']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/copy-list-with-random-pointer/" target="_blank" rel="noopener" title="">: </a>Create a <a href="https://en.wikipedia.org/wiki/Object_copying#Deep_copy" target="_blank" rel="noreferrer noopener"><strong>deep copy</strong></a> of the linked list. which consist of exactly <code>n</code> <strong>fresh new</strong> nodes, where each new node has its value set to the value of its corresponding original node. Both the <code>next</code> and <code>random</code> pointer of the new nodes should point to new nodes in the copied list such that the pointers in the original list and copied list represent the same list state. <strong>None of the pointers in the new list should point to nodes in the original list</strong>.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
For example, if there are two nodes <code>X</code> and <code>Y</code> in the original list, where <code>X.random --> Y</code>, then for the corresponding two nodes <code>x</code> and <code>y</code> in the copied list, <code>x.random --> y</code>.


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Input:</strong> head = ,,,,]// with next & random pointers
<strong>Output:</strong> head  ,,,,]</pre>
<!-- /wp:preformatted -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// Question--> Deep of Copy linked list
// Definition for a Node.
public class ListNodeWithRandom {
    public var val: Int
    public var next: ListNodeWithRandom?
    public var random: ListNodeWithRandom?
    public init(_ val: Int) {
        self.val = val
        self.next = nil
        self.random = nil
    }
}

func copyRandomList(_ head: ListNodeWithRandom?) -> ListNodeWithRandom? {
    var iter = head, next = head
    // First round: make copy of each node, and link them together side-by-side in a single list.
    while iter != nil {
        next = iter?.next
        var copyList = ListNodeWithRandom(iter!.val)
        iter?.next = copyList// poiting to New copy Node
        copyList.next = next
        iter = next
    }
    // Second round: assign random pointers for the copy nodes.
    iter = head
    while iter != nil {
        if iter?.random != nil {
            iter?.next?.random = iter?.random?.next
        }
        iter = iter?.next?.next
    }
    iter = head
    var pseudoHead = ListNodeWithRandom(0)
    var newCopy1 = pseudoHead, newCopy2 = pseudoHead
    // Third round: restore the original list, and extract the copy list.
    while iter != nil {
        next = iter?.next?.next
        
        // extract the copy
        newCopy1 = iter!.next!
        newCopy2.next = newCopy1
        newCopy2 = newCopy1
        
        // restore the original list
        iter?.next = next
        
        iter = next
    }
    
    return pseudoHead.next
}</code></pre>
<!-- /wp:code -->