---
title: "How to convert Decimal to Binary"
date: 2023-04-25 09:52:21
categories: ['binary number list', 'Decimal to Binary', 'Math']
layout: post
---

<!-- wp:paragraph -->
Here are the steps to convert decimal number into binary : - 


<!-- /wp:paragraph -->

<!-- wp:list {"ordered":true} -->
<ol><!-- wp:list-item -->
<li>Divide the given number by 2.</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>Get the integer quotient for the next iteration as seen in below table</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>Get the remainder for the binary digit.</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>Repeat the steps until the quotient is equal to 0. Now the output is Remainder in reverse order</li>
<!-- /wp:list-item --></ol>
<!-- /wp:list -->

<!-- wp:paragraph -->
Convert 4<sub>10</sub> to binary:


<!-- /wp:paragraph -->

<!-- wp:table {"textColor":"ast-global-color-1","className":"is-style-regular"} -->
<figure class="wp-block-table is-style-regular"><table class="has-ast-global-color-1-color has-text-color"><thead><tr><th class="has-text-align-center" data-align="center"><strong>Divide by 2</strong></th><th class="has-text-align-center" data-align="center"><strong>Quotient</strong></th><th class="has-text-align-center" data-align="center"><strong>Remainder</strong></th><th class="has-text-align-center" data-align="center"><strong>Bit </strong>/ count</th></tr></thead><tbody><tr><td class="has-text-align-center" data-align="center">4/2</td><td class="has-text-align-center" data-align="center">2</td><td class="has-text-align-center" data-align="center">0</td><td class="has-text-align-center" data-align="center">0</td></tr><tr><td class="has-text-align-center" data-align="center">2/2</td><td class="has-text-align-center" data-align="center">1</td><td class="has-text-align-center" data-align="center">0</td><td class="has-text-align-center" data-align="center">1</td></tr><tr><td class="has-text-align-center" data-align="center">1/2</td><td class="has-text-align-center" data-align="center">0</td><td class="has-text-align-center" data-align="center">1</td><td class="has-text-align-center" data-align="center">2</td></tr></tbody></table><figcaption class="wp-element-caption"><strong>So 4<sub>10</sub> = 100<sub>2</sub></strong></figcaption></figure>
<!-- /wp:table -->

<!-- wp:paragraph -->
You can try out self <br>Here are list of some binary numbers - 


<!-- /wp:paragraph -->

<!-- wp:table -->
<figure class="wp-block-table"><table><thead><tr><td class="has-text-align-center" data-align="center"><strong>Decimal</strong></td><td class="has-text-align-center" data-align="center"><strong>Binary</strong></td></tr></thead><tbody><tr><td class="has-text-align-center" data-align="center">0</td><td class="has-text-align-center" data-align="center">0</td></tr><tr><td class="has-text-align-center" data-align="center">1</td><td class="has-text-align-center" data-align="center">1</td></tr><tr><td class="has-text-align-center" data-align="center">2</td><td class="has-text-align-center" data-align="center">10</td></tr><tr><td class="has-text-align-center" data-align="center">3</td><td class="has-text-align-center" data-align="center">11</td></tr><tr><td class="has-text-align-center" data-align="center">4</td><td class="has-text-align-center" data-align="center">100</td></tr><tr><td class="has-text-align-center" data-align="center">5</td><td class="has-text-align-center" data-align="center">101</td></tr><tr><td class="has-text-align-center" data-align="center">6</td><td class="has-text-align-center" data-align="center">110</td></tr><tr><td class="has-text-align-center" data-align="center">7</td><td class="has-text-align-center" data-align="center">111</td></tr><tr><td class="has-text-align-center" data-align="center">8</td><td class="has-text-align-center" data-align="center">1000</td></tr><tr><td class="has-text-align-center" data-align="center">9</td><td class="has-text-align-center" data-align="center">1001</td></tr><tr><td class="has-text-align-center" data-align="center">10</td><td class="has-text-align-center" data-align="center">1010</td></tr></tbody></table></figure>
<!-- /wp:table -->