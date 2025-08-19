---
title: "Recursion examples in swift"
date: 2022-10-28 03:28:31
categories: ['Recursion', 'Recursion examples in swift']
layout: post
---

<!-- wp:paragraph -->
A function which calls itself in the body & solve the problem is called recursion. we will take some example to understand  


<!-- /wp:paragraph -->

<!-- wp:list {"ordered":true} -->
<ol><!-- wp:list-item -->
<li>Print 1 to N</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>Print N to 1</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>Sum of first n numbers</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>Check if String is Palindrome.</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>Create Factorial of a number</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>Get Fibonacci nth Number</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>Calculate Power of two </li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>Calculate Power of four</li>
<!-- /wp:list-item --></ol>
<!-- /wp:list -->

<!-- wp:heading {"level":3} -->
<h3>#1 Print numbers from 1 to N</h3>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func printNumersFromOneToN(_ n: Int) {
    if n <= 0 { return }
    printNumersFromOneToN(n-1)
    print(n, terminator: " ")
}</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
Because Print is before recursion function it will print 1 to n


<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>#2 Print numbers from N to 1</h3>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">func printNumersFromNtoOne(_ n: Int) {
     if n < 1 { return }
    print(n, terminator: " ")
    printNumersFromNtoOne(n-1)
}
printNumersFromNtoOne(5)</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":3} -->
<h3>#3 Sum of first N numbers</h3>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">var sumValue = 0
func sumOfFirstNNumbers(_ n: Int) -> Int {
    if n < 1 { return sumValue }
    sumValue += n
    return sumOfFirstNNumbers(n-1)
}
let op = sumOfFirstNNumbers(5)
print("op", op)// 15</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":3} -->
<h3>#4 Check if string is Palindrome</h3>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// Approach #1
func checkPalindrom(_ str: inout String) -> Bool {
  if str.count < 2 {
    return true
  } else {
    if str.removeFirst() != str.removeLast() {
      return false
    } else {
        return checkPalindrom(&str)
    }
  }
}
var inputStr = "nitin"
let isPalidrom = checkPalindrom(&inputStr)
print("isPalindrom-->", isPalidrom)

// Approach #2

func checkPalindrome<T: StringProtocol>(_ str: T) -> Bool {
    if str.count < 2 {
        return true
    } else {
        if str.first == str.last {
            let start = str.index(str.startIndex,offsetBy: 1)
            let end = str.index(str.endIndex,offsetBy: -1)
            return checkPalindrome(str)
        } else {
            return false
        }
    }
}
checkPalindrom(&inputStr)

// Approach #3: Non recursive
extension StringProtocol {
  subscript(_ offset: Int) -> Element {
      self
  }
}

func isPalindrome(_ word: String) -> Bool {
    let word = word.filter{ $0 != " " }
    for (i, character) in word.enumerated() {
        if character != word {
            return false
        }
    }
    return true
}
isPalindrome("nitin")

// Approach #4 Non recursive

func isPalindrome4(_ word: String) -> Bool {
    let word = word.filter{ $0 != " " }
    for (i, character) in word.enumerated() {
        let lastChar = word.index(word.startIndex, offsetBy: word.count-i-1)
        if character != word {
            return false
        }
    }
    return true
}
isPalindrome4("nitin")</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":3} -->
<h3>#5. Create Factorial of a number</h3>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// Example 2: Factorial : Example - 4! = 4x3x2x1 = 24

func findFactorial(inputNumber: Int) ->Int {
    if inputNumber == 1 {// Base case
        return 1
    }
    return inputNumber * findFactorial(inputNumber: inputNumber - 1)
}
print("findFactorial:")
print(findFactorial(inputNumber: 3))</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
When we write a recursive call base case plays important role. when we dropdown to a lower number we just add a check to stop recursive call. Like here we have base case <code>if inputNumber == 1</code>. So Factorial is calculated as 4 * findFactorial(3)= > 4*3*2*1


<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>#6. Get Fibonacci nth Number</h3>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// Example 3 Get nth Fabonacci number.. : Fibonacci number 0: 1: 1: 2: 3: 5: 8: 13: 21

func fibonacci(num: Int) ->Int {
    if num <= 1 {
        return num
    }
    // print("in function starts")
    let first = fibonacci(num: num - 1)
    let second = fibonacci(num: num - 2)
    //print("first--->", first)
    //print("second--->", second)
    //print("+++", first+second)
    return first + second
}
print("fibonacci(n--->", fibonacci(num: 4))</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
Fibonacci is basically addition of current & Next - Fibonacci number 0: 1: 1: 2: 3: 5: 8: 13: 21 & Base case will be if num <= 1 {


<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>#7. Calculate Power of two </h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
// Example 4: Power of 2... 2p0 =1 -- 2p1 = 2 -- 2p2 = 2 -- 2p3 =8 -- 2p4 = 16 (p stand for power). We can solve it by using two approaches : -


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">// Approach #A
func getPowerOfTwo(num: Int) -> Int {
    if num == 0 {
        return 1
    }
    return 2 * getPowerOfTwo(num: num-1)
}
print("getPowerOfTwo", getPowerOfTwo(num: 3))</code></pre>
<!-- /wp:code -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift"># Approach B using Bitwise operator 
func checkValidPowerOfTwoWithBitwise(num:Int) -> Bool {
    return num > 0 && (num & (num-1) == 0 )
}
print(checkValidPowerOfTwo(num: 1))</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
Bit manipulation :  bit manipulation techniques are usually based on observations from multiple examples


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
Binary form of numbers is - <br>3->0000 0011<br>4->0000 0100<br>5->0000 0101<br>6->0000 0110<br>7->0000 0111<br>8->0000 1000<br>The observation we can conclude is that the number which is a power of two has always compulsory 1 true bit.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
Now consider :-<br>bit representation of 7 -> 0111<br>bit representation of 8 -> 1000<br>bitwise AND of 7 and 8 -> 0000<br>we are gonna use this property for for all numbers which are powers of two<br>Time Complexity : O(1)<br>Space Complexity : O(1)


<!-- /wp:paragraph -->