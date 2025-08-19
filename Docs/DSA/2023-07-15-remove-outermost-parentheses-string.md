---
title: "Remove Outermost Parentheses || String"
date: 2023-07-15 10:47:58
categories: ['String']
layout: post
---

<!-- wp:paragraph -->
<a href="https://leetcode.com/problems/remove-outermost-parentheses/description/" target="_blank" rel="noopener" title="">: </a> A valid parentheses string is either empty <code>""</code>, <code>"(" + A + ")"</code>, or <code>A + B</code>, where <code>A</code> and <code>B</code> are valid parentheses strings, and <code>+</code> represents string concatenation.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
For example, <code>""</code>, <code>"()"</code>, <code>"(())()"</code>, and <code>"(()(()))"</code> are all valid parentheses strings.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
Return <code>s</code> <em>after removing the outermost parentheses of every primitive string in the primitive decomposition of </em><code>s</code>.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<strong>Example 1:</strong>


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Input:</strong> s = "(()())(())"
<strong>Output:</strong> "()()()"
<strong>Explanation:</strong> 
The input string is "(()())(())", with primitive decomposition "(()())" + "(())".
After removing outer parentheses of each part, this is "()()" + "()" = "()()()".
</pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<strong>Example 2:</strong>


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Input:</strong> s = "(()())(())(()(()))"
<strong>Output:</strong> "()()()()(())"
<strong>Explanation:</strong> 
The input string is "(()())(())(()(()))", with primitive decomposition "(()())" + "(())" + "(()(()))".
After removing outer parentheses of each part, this is "()()" + "()" + "()(())" = "()()()()(())".
</pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<strong>Example 3:</strong>


<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><strong>Input:</strong> s = "()()"
<strong>Output:</strong> ""
<strong>Explanation:</strong> 
The input string is "()()", with primitive decomposition "()" + "()".
After removing outer parentheses of each part, this is  "" + "" = "".</pre>
<!-- /wp:preformatted -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// TC: O(n)
// SC: O(_)
func removeOuterParentheses(_ s: String) -> String {
    var outputStr = ""
    var opened = 0
    for c in s {
        if c == "(" {
            if opened > 0 {
                outputStr.append(c)
            }
            opened+=1
        }
        if c == ")" {
            if opened > 1  {
                outputStr.append(c)
            }
            opened-=1
        }
    }
    return outputStr
}

let parnthString = "(()())(())"
let opRemovedLastParath = removeOuterParentheses(parnthString)
print(" removed last Paranth", opRemovedLastParath) // ()()()</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":5} -->
<h5 class="wp-block-heading">Dry Run:  for (  ( )  ( )  )  (  (  )  )</h5>
<!-- /wp:heading -->

<!-- wp:table -->
<figure class="wp-block-table"><table><tbody><tr><td>Input</td><td>Opened Current</td><td>Opened After</td><td>Output </td></tr><tr><td>( </td><td>0</td><td>1</td><td>“”</td></tr><tr><td>(</td><td>1</td><td>2</td><td>(</td></tr><tr><td>)</td><td>2</td><td>1</td><td>(  ) </td></tr><tr><td>(</td><td>1</td><td>2</td><td>( ) (</td></tr><tr><td>)</td><td>2</td><td>1</td><td>( ) ( )</td></tr><tr><td>)</td><td>1</td><td>0</td><td>( ) ( )</td></tr><tr><td>(</td><td>0</td><td>1</td><td>( ) ( ) </td></tr><tr><td>( </td><td>1</td><td>2</td><td>( ) ( ) ( </td></tr><tr><td>)</td><td>2</td><td>1</td><td>( ) ( )  ( )</td></tr><tr><td>)</td><td>1</td><td>0</td><td>( ) ( )  ( )</td></tr></tbody></table></figure>
<!-- /wp:table -->