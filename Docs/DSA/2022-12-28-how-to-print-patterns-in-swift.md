---
title: "How to print Patterns in swift ?"
date: 2022-12-28 08:33:55
categories: ['Array-Strings']
layout: post
---

<!-- wp:paragraph {"fontSize":"medium"} -->
<p class="has-medium-font-size">Below are the example code for various type of patterns in swift language.


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">/*
 // Question 1: print a square based on input integer.
***
***
***
------------
 */
func printSquare(_ n: Int) {
    for _ in 1...n {
        for _ in 1...n {
            print("*", terminator: "")
        }
        print("", terminator: "\n")// Helps for printing new line
    }
}
printSquare(3)</code></pre>
<!-- /wp:code -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">/*
 // Question 2: print a ladder star pattern.
*
**
***
****
------------
 */
func printLadderStar(_ n: Int) {
    for i in 0..<n {
        print("*", terminator: "")
        for _ in 0..<i {
            print("*", terminator: "")
        }
        print("", terminator: "\n")// Helps for printing new line
    }
}
printLadderStar(4)</code></pre>
<!-- /wp:code -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift"> // Question 3: print a ladder numbers pattern.
 1
 1 2
 1 2 3
 1 2 3 4
 1 2 3 4 5
------------
 */
func printLadderNumber(_ n: Int) {
    for i in 1...n {
        for j in 1...i {
            print(j, terminator: "")
        }
        print("", terminator: "\n")// Helps for printing new line
    }
}
printLadderNumber(4)</code></pre>
<!-- /wp:code -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">/*
 // Question 4: print a ladder same numbers pattern 
 1
 2 2
 3 3 3
 4 4 4 4
 5 5 5 5 5
------------
 */
func printLadderSameNumber(_ n: Int) {
    for i in 1...n {
        for _ in 1...i {
            print(i, terminator: "")
        }
        print("", terminator: "\n")// Helps for printing new line
    }
}
printLadderSameNumber(5)</code></pre>
<!-- /wp:code -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">/*
 // Question 5: print a reverse Ladder start pattern
 * * * * *
 * * * *
 * * *
 * *
 *
------------
 */
func printReverseLadderStar(_ n: Int) {
    for i in 1...n {
        for _ in i...n {
            print("*", terminator: "")
        }
        print("", terminator: "\n")// Helps for printing new line
    }
}
printReverseLadderStar(5)</code></pre>
<!-- /wp:code -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">/*
 // Question 6: print a reverse Ladder Numbers pattern
 1 2 3 4 5
 1 2 3 4
 1 2 3
 1 2
 1
------------
 */

func printReverseLadderNumers(_ n: Int) {
    for i in 1...n {
        for j in i...n {
            print(j, terminator: "")
        }
        print("", terminator: "\n")// Helps for printing new line
    }
}
printReverseLadderNumers(5)</code></pre>
<!-- /wp:code -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">/*
 // Question 6(b): print a reverse Ladder same Numbers pattern
 11111
 2222
 333
 44
 5
------------
 */

func printReverseLadderSameNumers(_ n: Int) {
    for i in 1...n {
        for _ in i...n {
            print(i, terminator: "")
        }
        print("", terminator: "\n")// Helps for printing new line
    }
}
printReverseLadderSameNumers(5)</code></pre>
<!-- /wp:code -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">/*<br>  Question 7: print a cone shape pattern/ Print Pyramids<br>     *<br>    ***<br>   *****<br> */<br>func printPattern(rows: Int) {<br>    for i in 0..<rows {<br>        let spacesCount = rows - i - 1<br>        let starsCount = 2 * i + 1<br>        <br>        // Print spaces<br>        for _ in 0..<spacesCount {<br>            print(" ", terminator: "")<br>        }<br>        <br>        // Print stars<br>        for _ in 0..<starsCount {<br>            print("*", terminator: "")<br>        }<br>        <br>        print("") // Move to the next line after each row<br>    }<br>}<br><br>let n = 3 // number of rows<br>printPattern(rows: n)<br></code></pre>
<!-- /wp:code -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">/*
 // Question 8: print reverse cone
 *********
  *******
   *****
    ***
     *
 ---------------
 */

func printReverseConeStar(_ n: Int) {
    
    for i in stride(from: n, to: 0, by: -1) {

        for _ in 1..<(n - i) + 1 {
            print(" ", terminator: "")
        }

        for _ in 1..<(2 * i - 1) + 1{
            print("*", terminator: "")
        }
        print("", terminator: "\n")// Helps for printing new line
    }
                
}
printReverseConeStar(5)</code></pre>
<!-- /wp:code -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">/*
// Question 9 : print diamond
  *
 ***
*****
 ***
  *
---------------
*/

func printDiamond(_ n: Int) {
   
    for i in 0..<n {
        for _ in i..<n-1 {
            print(" ", terminator: "")
        }
        print("*", terminator: "")
        for _ in 0..<i {
            print("**", terminator: "")
        }
        print("", terminator: "\n")// Helps for printing new line
    }
    
    for i in stride(from: n-1, to: 0, by: -1) {
        for _ in 1..<(n - i) + 1 {
            print(" ", terminator: "")
        }
        for _ in 1..<(2 * i - 1) + 1{
            print("*", terminator: "")
        }
        print("", terminator: "\n")// Helps for printing new line
    }
}
 printDiamond(3)</code></pre>
<!-- /wp:code -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">/*
// Question 10 : print Triangle
 *
 **
 ***
 ****
 ***
 **
 *
---------------
*/

func printTriangle(_ n: Int) {
    for i in 0..<n {
        print("*", terminator: "")
        for _ in 0..<i {
            print("*", terminator: "")
        }
        print("", terminator: "\n")// Helps for printing new line
    }
    for i in 1...n-1 {
        for _ in i...n-1 {
            print("*", terminator: "")
        }
        print("", terminator: "\n")// Helps for printing new line
    }
}
printTriangle(3)</code></pre>
<!-- /wp:code -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">/*
// Question 11 : Binary digits Right Angle triangle.
1
01
101
0101
10101
---------------
*/

func printBinaryTriangle(_ n: Int) {
    for i in 0..<n {
        print(i%2 == 0 ? 1 : 0, terminator: "")
        for j in 0..<i {
            print((i+j)%2 == 0 ? 0 : 1, terminator: "")
        }
        print("", terminator: "\n")// Helps for printing new line
    }
}

printBinaryTriangle(5)</code></pre>
<!-- /wp:code -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">/*
// Question 12 : Print M Star pattern..
 
 1                 1
 1 2             2 1
 1 2 3         3 2 1
 1 2 3 4     4 3 2 1
 1 2 3 4 5 5 4 3 2 1
---------------
*/

func printMPattern(_ n: Int) {
    for i in 1...n {
        for j in 1...i {
            print(j, terminator: "")
        }
        for _ in stride(from: n, to: i, by: -1) {
             print("  ", terminator: "")
         }
        for l in stride(from: i, to: 0, by: -1) {
            print(l, terminator: "")
        }

        print("", terminator: "\n")// Helps for printing new line
    }
}

printMPattern(4)</code></pre>
<!-- /wp:code -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">/*
// Question 13 : Triangle with increment numbers
 
 1
 2 3
 4 5 6
 7 8 9 10
 11 12 13 14 15
---------------
*/

func printTriangleWithIncrementNumbers(_ n: Int) {
    var count = 1
    for i in 1...n {
        for j in 1...i {
            print(count, terminator: " ")
            count+=1
        }
        print("", terminator: "\n")// Helps for printing new line
    }
}
printTriangleWithIncrementNumbers(5)</code></pre>
<!-- /wp:code -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">/*
// Question 14 : Inclined Triangle with ABCD
 A
 AB
 ABC
 ABCD
 ABCDE
---------------
*/

func printInclinedTriangleABCD(_ n: Int) {
    for i in 1...n {
        var ascii = 65
        for _ in 1...i {
            print(String(UnicodeScalar(ascii)!), terminator: " ")
            ascii+=1
        }
        print("", terminator: "\n")// Helps for printing new line
    }
}

printInclinedTriangleABCD(5)</code></pre>
<!-- /wp:code -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">/*
// Question 15 : Inverted Triangle with ABCD
 ABCDE
 ABCD
 ABC
 AB
 A
---------------
*/

func printInvertedTriangleABCD(_ n: Int) {
    for i in 1...n {
        var ascii = 65
        for _ in i...n {
            print(String(UnicodeScalar(ascii)!), terminator: " ")
            ascii+=1
        }
        print("", terminator: "\n")// Helps for printing new line
    }
}

printInvertedTriangleABCD(5)</code></pre>
<!-- /wp:code -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">/*
// Question 16 : Inclined Triangle with ABCD Repetative
 
 A
 BB
 CCC
 DDDD
 EEEEE
---------------
*/

func printInclinedTriangleABCDRepetative(_ n: Int) {
    var ascii = 65
    for i in 1...n {
        for _ in 1...i {
            print(String(UnicodeScalar(ascii)!), terminator: "")
        }
        ascii+=1
        print("", terminator: "\n")// Helps for printing new line
    }
}

printInclinedTriangleABCDRepetative(5)</code></pre>
<!-- /wp:code -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">/*
// Question 17 : Inclined Triangle with ABCD Repetative
    A
   ABA
  ABCBA
 ABCDCBA
---------------
*/

func printTriangleABCDRepetative(_ n: Int) {
    var ascii = 65
    for i in 1...n {
        for j in 1...n+i-1 {
            if(j<n-i+1){
                print(" ", terminator: "")
            }
            else if(j>=n-i+1&&j<n){
                print(String(UnicodeScalar(ascii)!), terminator: "")
                ascii+=1
            }
            else if(j==n){
                print(String(UnicodeScalar(ascii)!), terminator: "")
            }
            else if(j>n&&j<=n+i-1){
                ascii-=1
                print(String(UnicodeScalar(ascii)!), terminator: "")
            }
        }
      //  ascii+=1
        print("", terminator: "\n")// Helps for printing new line
    }
}

printTriangleABCDRepetative(4)</code></pre>
<!-- /wp:code -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">/*
// Question 18 : print reverse ABCD on triangle
 E
 E D
 E D C
 E D C B
 E D C B A
---------------
*/

func printReverseABCD(_ n: Int) {
    var ascii = 65
    for i in 0..<n {
        for j in 0..<i+1 {
            print(String(UnicodeScalar(ascii+n-1-j)!), terminator: " ")
        }
        print("", terminator: "\n")// Helps for printing new line
    }
}

printReverseABCD(5)</code></pre>
<!-- /wp:code -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">/*
// Question 19 : print Triangle With Hole
 *******
 *** ***
 **   **
 *     *
 **   **
 *** ***
 *******
---------------
*/

func printTriangleHole(_ n: Int) {
    var a = n
    var b = n
    for _ in 1..<n {
        for j in 1..<2*n {
            if(j>a && j<b){
                print(" ", terminator: "")
            } else {
                print("*", terminator: "")
            }
        }
        print("", terminator: "\n")
        a=a-1;
        b=b+1;
    }
    a=1;
    b=2*n;
    b-=1
    for _ in 0..<n {
        for j in 1..<2*n {
            if(j>a && j<b){
                print(" ", terminator: "")
            } else {
                print("*", terminator: "")
            }
        }
        print("", terminator: "\n")
        a=a+1;
        b=b-1;
    }
}
printTriangleHole(4)</code></pre>
<!-- /wp:code -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">/*
// Question 20 : print ButterFly
 *      *
 **    **
 ***  ***
 ********
 ***  ***
 **    **
 *      *
---------------
*/

func printButterFly(_ n: Int) {
    for i in 1...2*n {
        for j in 1...2*n {
            if(i<=n){
                if((j<=i)||(j>2*n-i)){
                    print("*", terminator: "")
                }else{
                    print(" ", terminator: "")
                }
            }
            else if(i>n){
                if((j <= 2*n - i) || j > i ){
                    print("*", terminator: "")
                } else{
                    print(" ", terminator: "")
                }
            }
        }
        print("", terminator: "\n")// Helps for printing new line
    }
}

printButterFly(4)</code></pre>
<!-- /wp:code -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">/*
// Question 21 : print Square with Hole
 ****
 *  *
 *  *
 ****
---------------
*/

func printSquaresWithHole(_ n: Int) {
    for i in 1...n {
        for j in 1...n {
            if (i==1 || i==n || j==1 || j==n) {
                print("*", terminator: "")
            } else {
                print(" ", terminator: "")
            }
        }
        print("", terminator: "\n")// Helps for printing new line
    }
}

printSquaresWithHole(4)</code></pre>
<!-- /wp:code -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">/*
// Question 22 : print Square with decreasing values
 4 4 4 4 4 4 4
 4 3 3 3 3 3 4
 4 3 2 2 2 3 4
 4 3 2 1 2 3 4
 4 3 2 2 2 3 4
 4 3 3 3 3 3 4
 4 4 4 4 4 4 4 
---------------
*/

func printSquaresWithNumbers(_ n: Int) {
    for i in 1..<2*n {
        for j in 1..<2*n {
            // cout << max(abs(n-i) + 1,abs(n-j) + 1) << " ";
            print(max(abs(n-i) + 1,abs(n-j) + 1), terminator: " ")
        }
        print("", terminator: "\n")// Helps for printing new line
    }
}

printSquaresWithNumbers(4)</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
<a href="https://takeuforward.org/strivers-a2z-dsa-course/must-do-pattern-problems-before-starting-dsa/" target="_blank" rel="noopener" title="">Reference Link: Take You Forward</a>


<!-- /wp:paragraph -->