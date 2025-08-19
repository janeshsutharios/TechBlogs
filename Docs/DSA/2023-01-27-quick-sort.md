---
title: "Quick Sort"
date: 2023-01-27 08:07:13
categories: ['Quick sort in swift', 'Sorting', 'sorting in swift']
layout: post
---

<!-- wp:paragraph -->
Logic: Create a pivot element & arrange elements with two partitions, If the elements are lesser than pivot add it to left partition & if elements bigger than the pivot arrange it to right side of partition & make call recursively with the subarray found with same approach.  <br><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">Time Complexity: <mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">Avg</mark> O(n^2) .. Best: O(n log (n))<br>Space Complexity: O(n)</mark><br>Worst case Time complexity of QuickSort is <mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">O(n^2) </mark>Let say we have sorted array & we applied Quick sort so the recursion will go as -- n , n-1, n-2, n-3..... Which is sum of arithmetic number which is n(n+1)/2 = O(n^2)


<!-- /wp:paragraph -->

<!-- wp:image {"id":1769,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large">![](/TechBlogs/Assets/Website/2023/01/Quick_sort-1-1024x886.jpg)</figure>
<!-- /wp:image -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">//Approach #1 create pivot element & sort elements which are lesser than the pivot to right & bigger on left.
// Here we are taking pivot as last element...
func quickSort(_ arr: inout , _ lowerBound: Int, _ upperBound: Int) {
    if lowerBound < upperBound {
        let pivot = partition(&arr, lowerBound, upperBound)
       // print("pivot is-->", pivot)
        quickSort(&arr, lowerBound, pivot-1)
        quickSort(&arr, pivot+1, upperBound)
    }
}

func partition(_ arr: inout , _ lowerBound: Int, _ upperBound: Int) -> Int {
   // print("part-- lower, upper---->", lowerBound, upperBound)
    let pivot = arr // pivot
    var i = (lowerBound - 1) // Index of smaller element and indicates the right position of pivot found so far
    for j in lowerBound..<upperBound {
        // If current element is smaller than the pivot
        if arr < pivot {
            i+=1 // increment index of smaller element
            arr.swapAt(i, j)
        }
    }
    i+=1
    arr.swapAt(i,upperBound)// Placing the  pivot at right position so xx(lesser elements) Pivot xx(larger elements)
    return i
}
var arr = 
quickSort(&arr, 0, arr.count - 1)
print("Quick Sort-->", arr)</code></pre>
<!-- /wp:code -->