---
title: "How to read a JSON File Using Swift"
date: 2022-10-07 11:03:00
categories: ['iOS', 'read json file swift 5', 'SwiftUI']
layout: post
---

<!-- wp:paragraph {"align":"left"} -->
<p class="has-text-align-left">JSON stands for JavaScript Object Notation which is <strong>a standard text-based format for representing structured data based on JavaScript object syntax</strong>, we can use that in Swift, If you don't have the JSON file you can create one<em> Xcode->New->File->Strings</em><br>later you can rename .<code>strings to .json</code> & make sure it contains pure JSON only without any comments or markup.


<!-- /wp:paragraph -->

<!-- wp:heading {"level":5} -->
<h5><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">#</mark>demoJSONFile look like below</h5>
<!-- /wp:heading -->

<!-- wp:paragraph {"align":"left"} -->
<p class="has-text-align-left"><code>{  <br> "country": "India"<br>}</code><br><strong><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">1. To load JSON file from Bundle,  use <code>Bundle.main.url(forResource</code> <br>2. To convert into decode object use <code>JSONDecoder</code><br>3. The Json is converted into swift model using <code>CodableModel</code></mark></strong>


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">struct CodableModel: Decodable {
    var country: String
}
if let url = Bundle.main.url(forResource: "demoJSONFile", withExtension: "json") {
    do {
        let data = try Data(contentsOf: url)
        let decoder = JSONDecoder()
        let jsonModel = try decoder.decode(CodableModel.self, from: data)
        print(jsonModel.country)
      } catch {
           // Block for error handling
      }
}</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
The <a href="https://github.com/janeshsutharios/iOS_Tutorials/tree/main/ReadingJSONInSwift" target="_blank" rel="noopener">Source code is here ..</a> That's All 😊


<!-- /wp:paragraph -->