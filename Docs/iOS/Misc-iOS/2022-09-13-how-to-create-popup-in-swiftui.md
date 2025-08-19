---
title: "How to create popup in SwiftUI ?"
date: 2022-09-13 06:52:03
categories: ['iOS', 'ios custom popup dialog iOS', 'ios custom popup dialog swiftUI', 'swift popup view programmatically', 'SwiftUI']
layout: post
---

<!-- wp:media-text {"mediaId":1383,"mediaType":"image","mediaWidth":57} -->
<div class="wp-block-media-text alignwide is-stacked-on-mobile" style="grid-template-columns:57% auto"><figure class="wp-block-media-text__media">![](/TechBlogs/Assets/Website/2022/09/Popup-view-SwiftUI.png)</figure><div class="wp-block-media-text__content"><!-- wp:paragraph {"placeholder":"Content…"} -->
From <strong>iOS 16</strong> onwards you can create a popup with inbuilt Apple's API. i.e. <code><mark>.presentationDetents(</mark></code>..


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
Here i have passed values    <mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color"><code>.presentationDetents()</code></mark> Means it will show as medium height first then by dragging it it will cover the full height.


<!-- /wp:paragraph --></div></div>
<!-- /wp:media-text -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">struct ContentView: View {
    @State var isPresentedPopUp: Bool = false
    var body: some View {
        Button {
            self.isPresentedPopUp.toggle()
        } label: {
            Text("Present half sheet")
        }
        .sheet(isPresented: $isPresentedPopUp) {
            PopUpView()
                .presentationDetents()
        }
    }
}

struct PopUpView: View {
    var body: some View {
        Text("Pop Up View")
    }
}</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":6} -->
<h6><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">Setting of custom height of Popup</mark> -</h6>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">    .presentationDetents() // use Your value here</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":6} -->
<h6><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">Percentage height of view </mark>- use .fraction(0.8)</h6>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">.presentationDetents() // 80 Percent of view height</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":6} -->
<h6><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color"><code>Set Custom Indents </code></mark></h6>
<!-- /wp:heading -->

<!-- wp:paragraph -->
You can create your own detents so that you can set Min height & Max  Height of the Popup. See the <strong><code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">FromDetent & ToDetent</mark></code></strong>


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">struct ContentView: View {
    @State var isPresentedPopUp: Bool = false
    var body: some View {
        Button {
            self.isPresentedPopUp.toggle()
        } label: {
            Text("Present half sheet")
        }
        .sheet(isPresented: $isPresentedPopUp) {
            PopUpView()
                .presentationDetents()
        }
    }
}

struct PopUpView: View {
    var body: some View {
        Text("Pop Up View")
    }
}

struct FromDetent: CustomPresentationDetent {
    static func height(in context: Context) -> CGFloat? {
        return 100
    }
}

struct ToDetent: CustomPresentationDetent {
    static func height(in context: Context) -> CGFloat? {
        return 200
    }
}</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
<mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-3-color">Any suggestion ? You can write Comments  👇🏽</mark>


<!-- /wp:paragraph -->