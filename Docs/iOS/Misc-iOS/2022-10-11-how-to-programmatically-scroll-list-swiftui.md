---
title: "How to programmatically scroll list SwiftUI ?"
date: 2022-10-11 09:54:48
categories: ['iOS', 'SwiftUI', 'swiftui scroll list programmatically', 'swiftui scroll to item', 'swiftui scrollviewreader']
layout: post
---

<!-- wp:paragraph -->
<code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">iOS14 * </mark></code>if we want to scroll the List programmatically in iOS We can use  <code>scrollTo(..</code> function where we can pass the specific index for jump to the List. for example if we need to scroll to last of list we can use <code>customArray.endIndex - 1</code><br>likewise you can pass your desired index for example 4,5 etc. Below code explains  for scrolling the list to bottom, try it yourself.


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">struct ContentView: View {
    var countries:  = 
    
    var body: some View {
        ScrollViewReader { scrollView in
            List{
                ForEach(countries, id: \.self) { countryName in
                    Text(countryName)
                        .padding(.all, 50)
                }
                .onAppear {
                    scrollView.scrollTo(countries)
                }
            }
        }
    }
}</code></pre>
<!-- /wp:code -->