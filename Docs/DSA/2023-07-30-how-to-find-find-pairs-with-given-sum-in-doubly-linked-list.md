---
title: "How to find find pairs with given sum in doubly linked list"
date: 2023-07-30 03:30:45
categories: ['LinkedList']
layout: post
---

<!-- wp:paragraph -->
<a href="https://www.geeksforgeeks.org/find-pairs-given-sum-doubly-linked-list/" target="_blank" rel="noopener" title="">: </a>Given a sorted doubly linked list of positive distinct elements, Find pairs in a doubly-linked list whose sum is equal to given value k, without using any extra space? 


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<strong><em>#Approach.</em></strong> Using two pointer


<!-- /wp:paragraph -->

<!-- wp:list {"ordered":true} -->
<ol><!-- wp:list-item -->
<li>Initialize two pointer variables, Initialize <strong>first</strong> with the start of the doubly linked list i.e; <strong>firstPointer=head</strong> and initialize <strong>second</strong> with the last node of the doubly linked list i.e; <strong>secondPointer=lastNode</strong>.</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>If current sum of <strong>first</strong> and <strong>second</strong> is less than k, then we move <strong>first</strong> in forward direction. If current sum of <strong>first</strong> and <strong>second</strong> element is greater than k, then we move <strong>second</strong> in backward direction.</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>Loop termination conditions are also different from arrays. The loop terminates when two pointers cross each other (<strong>secondPointer</strong>.next = <strong>firstPointer</strong>), or they become the same (<strong>firstPointer</strong> == secondPointer).</li>
<!-- /wp:list-item --></ol>
<!-- /wp:list -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func pairSumEqualK( _ head: DoublyLinkedListNode<Int>?, _ k: Int) {
    var firstPointer = head, secondPointer = head
    while secondPointer?.next != nil {
        secondPointer = secondPointer?.next
    }
    
    while firstPointer !== secondPointer && secondPointer?.next !== firstPointer {
        // pair found
        if firstPointer!.item + secondPointer!.item == k {
            print("pointers--- > ",firstPointer!.item, secondPointer!.item)// Output 1,4, 2,3
            // move first in forward direction
            firstPointer = firstPointer?.next
            // move second in backward direction
            secondPointer = secondPointer?.previous
            
        } else {
            if  firstPointer!.item + secondPointer!.item < k {
                firstPointer = firstPointer?.next
            } else {
                secondPointer = secondPointer?.previous
            }
        }
    }
}

var pairLinkedList = DoublyLinkedList<Int>()
pairLinkedList = 

pairSumEqualK(pairLinkedList.head, 5)// Output printed in function
</code></pre>
<!-- /wp:code -->