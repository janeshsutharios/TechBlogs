---
title: "How to make Multiline TextField in iOS SwiftUI"
date: 2022-09-14 09:54:11
categories: ['iOS', 'resizable text field swiftui', 'SwiftUI', 'swiftui text editor line limit', 'swiftui textfield axis', 'textfield multiline']
layout: post
---

<!-- wp:heading {"level":5} -->
<h5><code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">iOS 16</mark></code></h5>
<!-- /wp:heading -->

<!-- wp:image {"id":1389,"width":863,"height":321,"sizeSlug":"full","linkDestination":"none"} -->
<figure class="wp-block-image size-full is-resized">![](/TechBlogs/Assets/Website/2022/09/MultilineTextField-swiftUI-iOS.png)</figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
 You can use <code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">.lineLimit(5, reservesSpace: true)</mark></code> where first argument denotes the lines required & <code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">reservesSpace</mark></code> means do you need default space for `n` lines.  If you make it false by default single line space will be shown.<br>Just Like A <code>UITextField</code> in <code>UIKit</code> it works as a multiline text entry in iOS application.


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">struct ContentView: View {
    @State var inputText: String = ""
    var body: some View {
        VStack {
            Spacer()
            TextField("Please type your comments here", text: $inputText, axis: .vertical)
                .textFieldStyle(.roundedBorder)
                .lineLimit(5, reservesSpace: true)
                .padding()
            Spacer()
        }
    }
}</code></pre>
<!-- /wp:code -->