---
title: "How to add 1 number to a number represented linked list"
date: 2023-07-29 17:53:42
categories: ['LinkedList']
layout: post
---

<!-- wp:paragraph -->
<a href="https://www.geeksforgeeks.org/add-1-number-represented-linked-list/" target="_blank" rel="noopener" title="">: </a>Number is represented in linked list such that each digit corresponds to a node in linked list. Add 1 to it. For example 1999 is represented as (1-> 9-> 9 -> 9) and adding 1 to it should change it to (2->0->0->0) 


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<strong><em>#Approach:</em></strong> 


<!-- /wp:paragraph -->

<!-- wp:list {"ordered":true} -->
<ol><!-- wp:list-item -->
<li>Reverse linked list. For example, 1-> 9-> 9 -> 9 is reversed to 9-> 9 -> 9 ->1.</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>Start traversing linked list from leftmost node and add 1 to it. If there is a carry, move to the next node. Keep moving to the next node while there is a carry.</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>Reverse modified linked list and return head.</li>
<!-- /wp:list-item --></ol>
<!-- /wp:list -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func addOneUtil(_ head: ListNode?) -> ListNode? {
    let res = head // res is head node of the resultant list
    var temp: ListNode?
    var headCopy = head
    var carry = 1, sum = 0
    
    while headCopy != nil {
        // Calculate value of next digit in resultant list. The next digit is sum of following things (i) Carry (ii) Next digit of head list (if there is a next digit)
        sum = carry + headCopy!.val
        
        // update carry for next calculation
        carry = (sum >= 10) ? 1 : 0
        
        // update sum if it's greater than 10
        sum = sum % 10
        
        // Create a new node with sum as data
        headCopy?.val = sum
        
        // Move head and second pointers to next nodes
        temp = headCopy
        headCopy = headCopy?.next
    }
    
    // if some carry is still there, add a new node to result list. example 999+1 = 1000 where 0 is new node.
    if carry > 0 {
        temp?.next = ListNode(carry)
    }
    return res// return head of the resultant list
}

// This function mainly uses addOneUtil().
func addOne(_ head: ListNode?) -> ListNode? {
    var headCopy = head
    // Reverse linked list
    headCopy = reverseList2(headCopy)
    // Add one from left to right of reversed list
    headCopy = addOneUtil(headCopy)
    // Reverse the modified list
    return reverseList2(headCopy)
}

var linkListForAddOne =  ListNode(9, ListNode(9, ListNode(9)))
let addedOneList = addOne(linkListForAddOne)
//print("addedOne to the linkedList  --", addedOneList!)// 1->0->0->0</code></pre>
<!-- /wp:code -->