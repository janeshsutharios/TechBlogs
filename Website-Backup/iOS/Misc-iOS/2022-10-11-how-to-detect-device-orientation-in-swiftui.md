---
title: "How to detect device orientation in swiftUI ?"
date: 2022-10-11 09:29:40
categories: ['how to get current device orientation ios swift', 'iOS', 'ios get device orientation programmatically', 'SwiftUI']
layout: post
---

<!-- wp:paragraph -->
To check current device orientation in iOS application <br>1.  <code>NotificationCenter.default.publisher </code>for detecting device orientation <br>2. <code>.onReceive(</code>...  receive live values from the element on <br>3. <mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">getColor</mark> will return the color based on device orientation  


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">struct ContentView: View {
    
    @State var currentOrientation = UIDevice.current.orientation
    
    let orientationHasChanged = NotificationCenter.default.publisher(for: UIDevice.orientationDidChangeNotification)
        .makeConnectable()
        .autoconnect()
    
    var body: some View {
        Group {
            Text("Hello")
                .background(getColor())
            
        }.onReceive(orientationHasChanged) { _ in
            self.currentOrientation = UIDevice.current.orientation
        }
    }
    
    func getColor() -> Color {
        if self.currentOrientation == .portrait || self.currentOrientation == .portraitUpsideDown {
            return .red
        } else {
            return .yellow
        }
    }
    
}</code></pre>
<!-- /wp:code -->