---
title: "How to rotate linked list with K-th places ?"
date: 2023-07-30 04:11:51
categories: ['LinkedList']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/rotate-list/description/" target="_blank" rel="noopener" title="">: </a>Given the <code>head</code> of a linked list, rotate the list to the right by <code>k</code> places.<br>Example: -


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Input:</strong> head = , k = 2
<strong>Output:</strong> </pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<strong><em>#Approach</em></strong> <br>Step: 1 Create <code>tail</code> node which moves till ends<br>Step: 2 Create <code>curr</code> the tail node is the (len-k)-th node (1st node is head)<br>Step: 3 Reorder linked list


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func rotateRight(_ head: ListNode?, _ k: Int) -> ListNode? {
    // Base case
    guard head?.next != nil, k > 0 else { return head }
    
    // Find length and tail
    var tail = head, length = 1
    while tail?.next != nil {
        tail = tail?.next
        length += 1
    }
    
    // Reduce k
    var k = k % length// because if 5%5 encounters it gives 0(Not to rotate.)
    if k == 0 { return head }
    
    // Find the pivot
    var curr = head
    for _ in 0..<length - k - 1 {
        curr = curr?.next// the tail node is the (len-k)-th node (1st node is head)
    }
    // Reorder the list
    let newHead = curr?.next
    curr?.next = nil
    tail?.next = head
    //        print("head ----->", head)
    //        print("curr ----->", curr)
    //        print("tail ----->", tail)
    //        print("newHead -->", newHead)
    
    return newHead
}

let rotateLinkListInput = ListNode(1, ListNode(2, ListNode(3,ListNode(4, ListNode(5)))))
let rotateLinkListOutput = rotateRight(rotateLinkListInput, 2)
//print("Output of rotateLinkListOutput is ---", rotateLinkListOutput!)// 4 5 1 2 3
</code></pre>
<!-- /wp:code -->