---
title: "Return all possible subset from an array"
date: 2022-11-24 10:19:37
categories: ['Array-Strings', 'Recursion', 'subset of array']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/subsets-ii/description/" target="_blank" rel="noopener" title=""></a>: Given an integer array that may contain duplicates, find all possible subsets (the power set). No duplicates allowed in answer. Solution in any order allowed.<br>


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Input:</strong> nums = 
<strong>Output:</strong>        </pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<br>


<!-- /wp:paragraph -->

<!-- wp:image {"id":2155,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large">![](/TechBlogs/Assets/Website/2023/08/Subset-tree-recursion-1-1024x490.jpg)</figure>
<!-- /wp:image -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">class Solution {
    func subsetsWithDup(_ nums: ) -> ] {
      guard nums.count > 0 else { return  }
        
        var output = ]()
        var candidates = ()
        let startIndex = 0
        let sorted = nums.sorted()
        
        uniqueSet(&output, &candidates, startIndex, sorted)
        return output
    }
    
    // This is kind of simillar to the "inorder traversal"
    private func uniqueSet(_ output: inout ], _ candidates: inout , _ startIndex: Int, _ nums: ) {
        //Entering valid values store each case("node")'s value
        output.append(candidates)
        
        // try to find if it has "children", if no "child", we done
        for i in startIndex..<nums.count {
            // filter out cases which may cause duplicate subsets
            guard i == startIndex || nums != nums else { continue }

            // update candidates to next level's value(child's value)
            candidates.append(nums)

            // startIndex + 1, go next level(go to its child)
            uniqueSet(&output, &candidates, i+1, nums)

            // update candidates to previous level's value(parent's value)
            candidates.removeLast()
        }
    }
}
// ex: ; assume it is like a tree(inorder traversal), "*" indicates duplicated case
//                     
//              /       \       \
//                       
//           /   \       |
//         
//         /
//     

// output: , , , , , ]</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
<strong>Approach #2: Using Bitwise Operator<br></strong><em>Question: Power Set: Print all the possible subsequences of the String<br></em> To check whether the ith bit is set or not.If n&(1<<i) != 0,then the i-th bit is set.<br>First, write down all the numbers from 0 to 2^(n)-1 and their bit representation. <br>0 -> no-pick , and 1-pick


<!-- /wp:paragraph -->

<!-- wp:image {"id":2151,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large">![](/TechBlogs/Assets/Website/2023/08/Generate-subset-1024x739.jpg)</figure>
<!-- /wp:image -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: (2^n X n) FirstLoop X Second Loop
// SC: O(n)// for saving output

func generateAllSequence(input: String) -> {
    var n = input.count
    var output: = 
    
    for num in 0..<(1 << n) {
        var sub = "";
        for i in 0..<n {
            if (num & (1 << i)) != 0 {//check if the ith bit is set or not
               let index =  input.index(input.startIndex, offsetBy: i)
                sub += String(input)
            }
        }
        if !sub.isEmpty {
            output.append(sub);
        }
    }
    return output;
}

let subSet = generateAllSequence(input: "abc")
print("generateAllSequence using BitOperator--->", subSet)
// </code></pre>
<!-- /wp:code -->