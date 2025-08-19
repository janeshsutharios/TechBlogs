---
title: "How to add two numbers in LinkList ?"
date: 2022-11-25 13:33:26
categories: ['DSA', 'LinkedList', 'subset of array']
layout: post
---

<!-- wp:paragraph -->
<strong><a href="https://leetcode.com/problems/add-two-numbers/description/" target="_blank" rel="noopener" title="">: - </a> Add two numbers using the ListList in swift. <br> Ex Input: l1 = , l2 =  Output:  Explanation: 342 + 465 = 807.</strong>


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">//Definition for singly-linked list.
public class ListNode {
    public var val: Int
    public var next: ListNode?
    public init() { self.val = 0; self.next = nil; }
    public init(_ val: Int) { self.val = val; self.next = nil; }
    public init(_ val: Int, _ next: ListNode?) { self.val = val; self.next = next; }
}
extension ListNode: CustomStringConvertible {
    
    public var description: String {
        guard let next = next else {
            return "\(val)"
        }
        return "\(val) -> " + String(describing: next) + " "
    }
}

private var reminderVal = 0
func addTwoNumbers(_ l1: ListNode?, _ l2: ListNode?) -> ListNode? {
    if l1 == nil && l2 == nil && reminderVal == 0 { return nil }
    let sum = (l1?.val ?? 0) + (l2?.val ?? 0) + reminderVal
    reminderVal = sum / 10 // ex 10/10 = 1 so add it two next iteration.
    return .init(sum % 10, addTwoNumbers(l1?.next, l2?.next))
}
let l1 = ListNode(2, ListNode(4, ListNode(3)))
let l2 = ListNode(5, ListNode(6, ListNode(4)))

let result = addTwoNumbers(l1, l2)

print(result.debugDescription)</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
Explanation: # Recursion Approach: Create a sum variable & add two nodes with a previous reminder on the recursive call use modulo operator to use the numerator value (7%10 = 7, 10%10 = 0 , 8%10 = 8)


<!-- /wp:paragraph -->