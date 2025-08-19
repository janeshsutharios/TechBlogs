---
title: "Allocate Books || Binary Search"
date: 2023-07-12 08:49:37
categories: ['BinarySearch']
layout: post
---

<!-- wp:paragraph -->
<a href="https://www.codingninjas.com/studio/problems/allocate-books_1090540" target="_blank" rel="noopener" title=""></a>: Given an array  of integer numbers, ‘arr’ represents the number of pages in the ‘i-th’ book. There are ‘m’ number of students, and the task is to allocate all the books to the students. Allocate books in such a way that: <br>1. Each student gets at least one book. <br>2. Each book should be allocated to only one student. <br>3. Book allocation should be in a contiguous manner. <br>Allocate the book to ‘m’ students such that the maximum number of pages assigned to a student is minimum. <br>If the allocation of books is not possible, return -1.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
Example:


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<strong>let</strong> booksArrayWithPages = <br><strong>var</strong> booksCount = 4<br><strong>var</strong> studentsCount = 2<br>Output: 113


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<strong>Explanation</strong>: All possible ways to allocate the ‘4’ books to '2' students are:<br>12 | 34, 67, 90 - the sum of all the pages of books allocated to student 1 is ‘12’, and student two is ‘34+ 67+ 90 = 191’, so the maximum is ‘max(12, 191)= 191’.<br>12, 34 | 67, 90 - the sum of all the pages of books allocated to student 1 is ‘12+ 34 = 46’, and student two is ‘67+ 90 = 157’, so the maximum is ‘max(46, 157)= 157’.<br>12, 34, 67 | 90 - the sum of all the pages of books allocated to student 1 is ‘12+ 34 +67 = 113’, and student two is ‘90’, so the maximum is ‘max(113, 90)= 113’.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<em>We are getting the minimum in the last case. Hence answer is ‘113’.</em>


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(Nlog(N))
// SC: O(1)
func bookAllocation(_ arr: , _ booksCount: Int, _ studentsCount: Int) ->Int {
    var start = 0
    var sum = 0
    for i in 0..<booksCount {
        sum += arr
    }
    var end = sum // end = sum of all array elements
    var ans = -1    // initialize ans
    
    var mid = start + (end-start)/2
    
    while start<=end {
        if isPossibleToBookAllocate(arr, booksCount, studentsCount, mid) {
            //possible solution, save the ans and move to left to find minimal possilbe solution, coz right of this will also satisfy the condition
            ans = mid
            end = mid-1
        } else {
            //no soln exists, means more no. of students needed than given, so move to right to increase sum
            //lower the search space, bring start infront
            start = mid+1
        }
        mid = start+(end-start)/2
    }
    return ans
}

func isPossibleToBookAllocate(_ arr: , _ booksCount: Int, _ studentCount: Int, _ mid: Int) -> Bool {
    var currentStudentCount = 1
    var pageSum = 0;    //min start with one student, and page sum=0, keep on adding value till it is<mid and rest give to other student and check
    for i in 0..<booksCount {
        if (pageSum + arr) <= mid {
            //a current page sum value, maintain a running count
            pageSum+=arr    //save it || page sum represents the no. of pages alloted to the student in consideration right now
        } else{
            //allocate remaining pages to other student
            currentStudentCount+=1
            //check for no solution case
            if currentStudentCount > studentCount || (arr > mid){
                return false;
                //if student >m and the value of current is greater than mid, stop in these two cases
            } else {
                //we increases student count so new page sum value
//                 pageSum=0;
//                 pageSum+=arr;
//                 we can use above lines also for understanding, if starting from zero no needed for zero + in unary operator
                pageSum = arr;
            }
        }
    }
    return true  
}

let booksArrayWithPages = 
var booksCount = 4
var studentsCount = 2
let minAllocatedBook = bookAllocation(booksArrayWithPages, booksCount, studentsCount)
print("Min allocation-- ", minAllocatedBook)// 113
</code></pre>
<!-- /wp:code -->