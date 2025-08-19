---
title: "Merge Sort"
date: 2023-01-26 16:34:43
categories: ['merge sort', 'Sorting', 'sorting in swift']
layout: post
---

<!-- wp:paragraph -->
Merge Sort is based on divide & conquer approach, first we divide array into two parts until we got single element then merge the single single element and create a subarray, Now merge two sorted subarray into single array likewise in final we got the final sorted array.   <br>In Conquer approach we have i, j k where i if left subarray, j is right subarray now we are comparing elements right with left & add it to tempArray. k index is used to fill on temp array<br><strong><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">Time Complexity:- O(n log(n))<br>Space Complexity:- O(n) </mark></strong>


<!-- /wp:paragraph -->

<!-- wp:image {"id":1749,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large">![](/TechBlogs/Assets/Website/2023/01/Merge-sort-1024x849.jpg)</figure>
<!-- /wp:image -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// Merge Sort...
func mergeSort(_ arr: inout , _ l: Int, _ r: Int) {
    //print("MS called with ", l,r)
    if (l < r) {
        let mid = (l + r) / 2;
        mergeSort(&arr, l, mid); // left half // Divide
        mergeSort(&arr, mid + 1, r); // right half // Divide
        mergeSortConquer(&arr, l, mid, r); // merging sorted halves// Conquer
    } else {
       // print("Discarded--> ", l,r)
    }
}

func mergeSortConquer(_ arr: inout ,  _ lowerBound: Int,  _ mid: Int,  _ upperBound: Int) {
    var i = lowerBound; // starting index of left half of array
    var j = mid + 1; // starting index of right half of array
    var k = lowerBound; // k is index used to transfer elements in temp array
    var tempArray:  = Array.init(repeating: 0, count: arr.count) // temp array
   // print(lowerBound, upperBound, "entered here for sorting INDEX -->", i, j, upperBound, " -- Respective Values-->", arr, arr)
   // print("entered with", lowerBound ,mid, upperBound)
    // storing elements in the temp array in a sorted manner//
    
    while i <= mid && j <= upperBound {
        if (arr < arr) {
            tempArray = arr;
            i+=1;
        } else {
            tempArray = arr;
            j+=1;
        }
        k+=1;
    }
    // Note:- In below code we are transferring the element from any two subarray 
    // if elements on the left half are still available to insert //
    
    if i > mid {
        while j <= upperBound {
            //print("Left entered in if loop...", arr)
            tempArray = arr;
            k+=1;
            j+=1;
        }
    } else {
        // if elements on the right half are still available to insert  //
        while i <= mid {
            // print("Right entered in if loop...", arr)
            tempArray = arr;
            k+=1;
            i+=1;
        }
    }
    // transferring all elements from temporary to arr //
    for k in lowerBound...upperBound {
        arr = tempArray;
    }
//    print("tempArray---------", tempArray)
}

var arr = 
mergeSort(&arr, 0, arr.count - 1)
print("merge Sort-->", arr)
</code></pre>
<!-- /wp:code -->