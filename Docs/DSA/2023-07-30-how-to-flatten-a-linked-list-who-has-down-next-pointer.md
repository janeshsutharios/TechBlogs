---
title: "How to flatten a linked list who has down & next pointer"
date: 2023-07-30 04:16:33
categories: ['LinkedList']
layout: post
---

<!-- wp:paragraph -->
<a href="https://www.geeksforgeeks.org/flattening-a-linked-list/" target="_blank" rel="noopener" title="">: </a>Given a linked list where every node represents a linked list and contains two pointers of its type: 


<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><!-- wp:list-item -->
<li>Pointer to next node in the main list (we call it ‘right’ pointer in the code below) </li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>Pointer to a linked list where this node is headed (we call it the ‘down’ pointer ). </li>
<!-- /wp:list-item --></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<strong>Condition: </strong>All linked lists are sorted and the resultant linked list should also be sorted


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">public class ListNodeWithDown {
    public var data: Int
    public var right: ListNodeWithDown?
    public var down: ListNodeWithDown?
    public init(_ val: Int) {
        self.data = val
        self.right = nil
        self.down = nil
    }
}
var headOfLL: ListNodeWithDown? // head of list

// An utility function to merge two sorted linked lists
func mergeLinkedList(_ a: ListNodeWithDown?, _ b: ListNodeWithDown?) -> ListNodeWithDown? {
    // if first linked list is empty then second
    // is the answer
    if a == nil {
        return b
    }
    // if second linked list is empty then first
    // is the result
    if b == nil {
        return a
    }
    
    // compare the data members of the two linked lists
    // and put the larger one in the result
    var result:ListNodeWithDown?
    
    if a!.data < b!.data {
        result = a
        result?.down = mergeLinkedList(a?.down, b)
    }
    
    else {
        result = b;
        result?.down = mergeLinkedList(a, b?.down)
    }
    
    result?.right = nil
    return result
}

func flatten(_ root: ListNodeWithDown?) -> ListNodeWithDown? {
    // Base Cases
    if root == nil || root?.right == nil {
        return root
    }
    
    // recur for list on right
    root?.right = flatten(root?.right)
    
    // now merge
    var newRoot = mergeLinkedList(root, root?.right)
    
    // return the root
    // it will be in turn merged with its left
    return newRoot
}

/*
 * Utility function to insert a node at beginning of the linked list
 */
func push(_ headRef: ListNodeWithDown?, _ data: Int) -> ListNodeWithDown? {
    /*
     * 1 & 2: Allocate the Node & Put in the data
     */
    var new_node = ListNodeWithDown(data)
    
    /* 3. Make next of new Node as head */
    new_node.down = headRef
    
    /* 4. Move the head to point to new Node */
    var headCopy = headRef
    headCopy = new_node
    
    /* 5. return to link it back */
    return headCopy
}

func printList() {
    var temp = headOfLL
    while temp != nil {
        print(temp!.data, terminator: ",")
        temp = temp?.down
    }
    
}
/*
 * Let us create the following linked list 5 -> 10 -> 19 -> 28 | | | | V V V V 7
 * 20 22 35 | | | V V V 8 50 40 | | V V 30 45
 */

/*
 5 -> 10 -> 19 -> 28
 |    |     |     |
 V    V     V     V
 7    20    22    35
 |          |     |
 V          V     V
 8          50    40
 |                |
 V                V
 30               45
 */

headOfLL = push(headOfLL, 30);
headOfLL = push(headOfLL, 8);
headOfLL = push(headOfLL, 7);
headOfLL = push(headOfLL, 5);

headOfLL?.right = push(headOfLL?.right, 20);
headOfLL?.right = push(headOfLL?.right, 10);

headOfLL?.right?.right = push(headOfLL?.right?.right, 50);
headOfLL?.right?.right = push(headOfLL?.right?.right, 22);
headOfLL?.right?.right = push(headOfLL?.right?.right, 19);

headOfLL?.right?.right?.right = push(headOfLL?.right?.right?.right, 45);
headOfLL?.right?.right?.right = push(headOfLL?.right?.right?.right, 40);
headOfLL?.right?.right?.right = push(headOfLL?.right?.right?.right, 35);
headOfLL?.right?.right?.right = push(headOfLL?.right?.right?.right, 20);

// flatten the list
headOfLL = flatten(headOfLL);

printList() // 5,7,8,10,19,20,20,22,30,35,40,45,50,</code></pre>
<!-- /wp:code -->