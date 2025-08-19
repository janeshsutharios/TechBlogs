---
title: "How to Sort Linked List ?"
date: 2023-07-29 17:39:32
categories: ['LinkedList']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/sort-list/" target="_blank" rel="noopener" title="">: </a>Given Head of singly linked list return a sorted linkedlist head(<em><strong>ascending order</strong></em>.)<br>Criteria: -TC should O(n) SC: O(1)


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Input:</strong> head = 
<strong>Output:</strong> </pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<strong><em>#Approach </em></strong>: We can use merge sort: which work on divide & conquer 


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func sortList(_ head: ListNode?) -> ListNode? {
    if head?.next == nil { return head }
    
    var slow = head
    var fast = head?.next
    while fast != nil && fast?.next != nil {
        slow = slow?.next
        fast = fast?.next?.next
    }
    
    let leftHalf = head
    let rightHalf = slow?.next
    
    slow?.next = nil// to make exact left half(break link list into two parts.)
    
    var currLeft = sortList(leftHalf)
    var currRight = sortList(rightHalf)
    
    let answer = ListNode(-1)
    var curr: ListNode? = answer
    
    while currLeft != nil || currRight != nil {
        if currLeft?.val ?? Int.max <= currRight?.val ?? Int.max {
            curr?.next = currLeft
            currLeft = currLeft?.next
        } else {
            curr?.next = currRight
            currRight = currRight?.next
        }
        
        curr = curr?.next
    }
    return answer.next
}

let unsortedLinkList = ListNode(5, ListNode(11, ListNode(10,ListNode(1, ListNode(5)))))
let afterSort = sortList(unsortedLinkList)!
//print("After sort LinkList cycle is--- ", afterSort)// 1->5->5->10->11</code></pre>
<!-- /wp:code -->