---
title: "How to add Radio Buttons in SwiftUI"
date: 2022-09-05 09:54:49
categories: ['custom radio button swiftui', 'iOS', 'list with radio button swiftui', 'SwiftUI', 'swiftui picker', 'swiftui selection button']
layout: post
---

<!-- wp:paragraph -->



<!-- /wp:paragraph -->

<!-- wp:media-text {"mediaId":1360,"mediaType":"image"} -->
<div class="wp-block-media-text alignwide is-stacked-on-mobile"><figure class="wp-block-media-text__media">![](/TechBlogs/Assets/Website/2022/09/SwiftUI-RadioButtton-1.png)</figure><div class="wp-block-media-text__content"><!-- wp:paragraph {"placeholder":"Content…"} -->
Let's create a List with Radio Buttons in SwiftUI for iOS Application. We will use Image with SFSymbol for radio buttons & based on the user selection image will change dynamically. So by use of closure we will get the selected values. 


<!-- /wp:paragraph --></div></div>
<!-- /wp:media-text -->

<!-- wp:heading {"level":5} -->
<h5>1. Create Radio Button View</h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
We are picking up Button & contents of button taken in <code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">HStack</mark></code>.  The last element inside is <code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">Spacer()</mark></code> for filling up the area.<br><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color"><code>callbackForSelection</code></mark> is used for getting selected values which invokes on button click. And we are passing data through <code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">init( </mark></code>function. I kept it simple, but you can use your custom modifiers 


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">struct RadioButtonView: View {
    
    let currentRadioValue: String
    let callbackForSelection: (String)->()
    let prevselectedValue : String
    
    init(
        _ id: String,
        callback: @escaping (String)->(),
        selectedID: String
    ) {
        self.currentRadioValue = id
        self.prevselectedValue = selectedID
        self.callbackForSelection = callback
    }
    
    var body: some View {
        Button(action:{
            self.callbackForSelection(self.currentRadioValue)
        }) {
            HStack(alignment: .center, spacing: 10) {
                Image(systemName: self.prevselectedValue == self.currentRadioValue ? "largecircle.fill.circle" : "circle")
                    .renderingMode(.original)
                    .resizable()
                    .aspectRatio(contentMode: .fit)
                    .frame(width: 18, height: 18)
                Text(currentRadioValue)
                Spacer()
            }
        }
    }
}</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":5} -->
<h5>2. Create a List for Radio Buttons</h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
Embedding the Radio  button is SwiftUI's <mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color"><code>List</code></mark>, Here <code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">items</mark></code> represents the radio button list & <code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">selectedId</mark></code> is current selected Radio button String and callbackForSelection for getting selected radio button value. The example code is below- 


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">struct RadioButtons: View {
    
    let items : 
    let callbackForSelection: (String) -> ()
    @State var selectedId: String = ""
    
    var body: some View {
        List {
            ForEach(0..<items.count, id: \.self) { index in
                RadioButtonView(self.items,
                                callback: self.radioGroupCallback,
                                selectedID: self.selectedId)
            }

        }.listStyle(PlainListStyle())
        
    }
    
    func radioGroupCallback(id: String) {
        selectedId = id
        callbackForSelection(id)
    }
}</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":5} -->
<h5>3. Create Content View</h5>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">objectsArray</mark></code> is example array which used for radio item listing and you can use default selection by using <code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">selectedRadioButton</mark></code> & VStack contains Text with Radio button listing. The example code is below -


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">struct ContentView: View {
    
    @State var objectsArray = 
    @State var selectedRadioButton = "India"
    
    var body: some View {
        VStack {
            Text("Select Country")
                .font(Font.largeTitle)
                .foregroundColor(.red)
            RadioButtons(items: objectsArray,
                         callbackForSelection:  { selectedVal in
                print("Selected Value  -- : \(selectedVal)")
                selectedRadioButton = selectedVal
            },selectedId: selectedRadioButton)
            Text("Selected --:  \(selectedRadioButton)")
            Spacer()
        }
    }
}</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
That's it : ) <br><a href="https://github.com/janeshsutharios/iOS_Tutorials/tree/main/RadioButton_SwiftUI" target="_blank" rel="noopener" title="">Source  code is here </a>


<!-- /wp:paragraph -->