---
title: "How to Create ProgressBar in swiftUI ?"
date: 2022-09-14 10:42:33
categories: ['circular progress in iOS', 'gauge view ios swift', 'iOS', 'SwiftUI', 'swiftui gauge view', 'swiftui progress bar', 'swiftui speedometer']
layout: post
---

<!-- wp:paragraph -->
In this article we will discuss about creating Gauge or Progress bar in iOS Application by using   <code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">Gauge(</mark></code><br>1. Making Horizontal progressBar<br>2. Creating Circular progressBar 


<!-- /wp:paragraph -->

<!-- wp:heading {"level":5} -->
<h5> 1. Making Horizontal progressBar</h5>
<!-- /wp:heading -->

<!-- wp:image {"id":1394,"width":865,"height":216,"sizeSlug":"full","linkDestination":"none"} -->
<figure class="wp-block-image size-full is-resized">![](/TechBlogs/Assets/Website/2022/09/SwiftUI-Horizontal-progressBar.png)</figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
We will create a simple progress bar where <code>currentProgress</code> shows fraction completion of the bar


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">struct ContentView: View {
    @State private var currentProgress = 0.8
    var body: some View {
        Gauge(value: currentProgress) {
            Text("Progress")
        }
        .padding()
    }
}</code></pre>
<!-- /wp:code -->

<!-- wp:image {"id":1395,"width":864,"height":281,"sizeSlug":"full","linkDestination":"none"} -->
<figure class="wp-block-image size-full is-resized">![](/TechBlogs/Assets/Website/2022/09/progress-bar-2-swiftui.png)</figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
For adding min max values use <code>currentValueLabel</code> <code>minimumValueLabel maximumValueLabel</code>


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">struct ContentView: View {
    @State private var currentProgress = 20.0
    private let startValue = 0.0
    private let endValue = 100.0
    var body: some View {
        Gauge(value: currentProgress, in: startValue...endValue) {
            Text("Progress")
        }
    currentValueLabel: {
        Text(currentProgress.formatted())
    } minimumValueLabel: {
        Text(startValue.formatted())
    } maximumValueLabel: {
        Text(endValue.formatted())
    }
    .padding()
    }
}</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":5} -->
<h5><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">2. Creating Circular progressBar </mark></h5>
<!-- /wp:heading -->

<!-- wp:image {"id":1397,"width":865,"height":336,"sizeSlug":"full","linkDestination":"none"} -->
<figure class="wp-block-image size-full is-resized">![](/TechBlogs/Assets/Website/2022/09/circular-progressbar-SwiftUI-1.png)</figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
Use <code>.gaugeStyle(.accessoryCircularCapacity)</code> & Optionally you can use <code>.scaleEffect(3)</code> to increase the circle.


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">struct ContentView: View {
    @State private var currentProgress = 0.5
    var body: some View {
        Gauge(value: currentProgress) {
            //Text("Downloading..")
        } currentValueLabel: {
            Text(currentProgress.formatted(.percent))
        }
        .gaugeStyle(.accessoryCircularCapacity)
        .tint(.red)
        .scaleEffect(3)// Optional for Extra size of Gauge
        .padding()
    }
}</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
Reference - <a href="https://developer.apple.com/documentation/swiftui/gauge" target="_blank" rel="noopener">https://developer.apple.com/documentation/swiftui/gauge</a>


<!-- /wp:paragraph -->