---
title: "Remove Nth Node From End of LinkedList"
date: 2023-07-22 16:13:28
categories: ['LinkedList']
layout: post
---

<!-- wp:paragraph -->
: Given the <code>head</code> of a linked list, remove the <code>n<sup>th</sup></code> node from the end of the list and return its head.<br>


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Input:</strong> head = , n = 4
<strong>Output:</strong> </pre>
<!-- /wp:preformatted -->

<!-- wp:heading {"level":5} -->
<h5 class="wp-block-heading">#Approach Two pointer</h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
Step: 1 Move fast pointer till count<br>Step: 2 Increment fast pointer till we get fast?.next == nil if we got nil just remove mid pointer...


<!-- /wp:paragraph -->

<!-- wp:image {"id":2062,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large">![](/TechBlogs/Assets/Website/2023/07/Remove-last-nth-node-LinkedList-1024x790.jpg)</figure>
<!-- /wp:image -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func removeNthFromEnd(_ head: ListNode?, _ n: Int) -> ListNode? {
    var fast = head
    var slow = head
    var count = n
    
    while count > 0 {
        count -= 1
        fast = fast?.next
    }
    if fast == nil { return head?.next }
    
    while slow != nil && fast != nil {
        if fast?.next == nil {
            slow?.next = slow?.next?.next
        }
        slow = slow?.next
        fast = fast?.next
    }
    
    return head
}

var aLinkList2 =  ListNode(1, ListNode(2, ListNode(3,ListNode(4, ListNode(5)))))
let afterDeletingLL = removeNthFromEnd(aLinkList2, 2)// Remove second last
print("removeNthFromEnd------", afterDeletingLL) //  1 -> 2 -> 3 -> 5</code></pre>
<!-- /wp:code -->