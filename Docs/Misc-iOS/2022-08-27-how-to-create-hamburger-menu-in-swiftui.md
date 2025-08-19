---
title: "How to create Hamburger Menu in SwiftUI"
date: 2022-08-27 12:29:21
categories: ['ios', 'iOS', 'swift', 'SwiftUI', 'swiftUI']
layout: post
---

<!-- wp:paragraph -->
Hey Folks, In this tutorial i will show you Creating SideBar menu or hamburger menu in SwiftUI which supports Gestures as well.


<!-- /wp:paragraph -->

<!-- wp:image {"id":1303,"sizeSlug":"full","linkDestination":"none"} -->
<figure class="wp-block-image size-full">![](/TechBlogs/Assets/Website/2022/08/Side-Menu.001.png)</figure>
<!-- /wp:image -->

<!-- wp:buttons -->
<div class="wp-block-buttons"><!-- wp:button {"backgroundColor":"ast-global-color-1","textColor":"ast-global-color-5"} -->
<div class="wp-block-button"><a class="wp-block-button__link has-ast-global-color-5-color has-ast-global-color-1-background-color has-text-color has-background" href="https://drive.google.com/file/d/1BlXJrl2M213ApN2Hnk8GH5KxqnsIfO-8/view?usp=sharing" target="_blank" rel="noreferrer noopener">Video Link </a></div>
<!-- /wp:button --></div>
<!-- /wp:buttons -->

<!-- wp:paragraph -->
We will Create Three classes <br>1. DashBoardView - Which represents Dashboard of the app with Hamburger Menu.<br>2. ViewModel - For Managing SideBar flag <br>3. SideBarView- The view which invokes when we trigger Hamburger's icon


<!-- /wp:paragraph -->

<!-- wp:heading {"level":5} -->
<h5>1. <code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">DashBoardView.swift</mark></code></h5>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">import SwiftUI

// Dashboard view with Hamburger Menu
struct DashBoardView: View {
    // 1: View Model For managing sideBar flag
    @StateObject var viewModel = ViewModel()
    
    var body: some View {
        
        ZStack {
            NavigationView {
                VStack(alignment:.leading) {
                    List {
                        ForEach((1...130), id: \.self) {
                            Text("Index---> \($0)")
                        }
                    }
                }
                .navigationBarTitle("", displayMode: .inline)
                // Setup Hamburger Icon On NaviationBar
                .toolbar {
                    ToolbarItem(placement: .navigationBarLeading) {
                        Button(action: {
                            self.viewModel.isMenuVisible.toggle()
                        }, label: {
                            HStack {
                                Image(systemName: "sidebar.leading")
                                Text("Home").font(.headline)
                            }
                        })
                        .foregroundColor(.blue) // You can apply colors and other modifiers too
                    }
                }
            }
            
            SideBarView()
                .ignoresSafeArea()
            // .background(Color.clear.edgesIgnoringSafeArea(Edge.Set.all))
            
        }.environmentObject(self.viewModel)
            .gesture(customDrag)
    }
    
    // Adding Drag Gesture - Swipe from Left with edge of $0.location.x < 200
    var customDrag: some Gesture {
        
        return DragGesture(minimumDistance: 5)
            .onEnded {
                if ($0.location.x - $0.startLocation.x) > 0 {
                    //print("rRight Swipe--->", $0.translation.width, self.viewModel.isLeftMenuVisible)
                    if $0.location.x < 200 && !self.viewModel.isMenuVisible {
                        //print("dsdsd",$0.translation.width, $0.location, UIScreen.main.bounds.width)
                        withAnimation {
                            self.viewModel.isMenuVisible.toggle()
                        }
                    }
                } else {
                    //print("Left Swipe ---")
                    if $0.translation.width < -100 && self.viewModel.isMenuVisible {
                        withAnimation {
                            self.viewModel.isMenuVisible.toggle()
                        }
                    }
                }
            }
    }
}
struct ContentView_Previews: PreviewProvider {
    static var previews: some View {
        DashBoardView()
    }
}</code></pre>
<!-- /wp:code -->

<!-- wp:list {"ordered":true} -->
<ol><li>Create <code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">ZStack</mark></code> with <code>NavigationView</code>  as commonly we use to create SwiftUI View</li><li> We will be using <code>toolbar</code> <code>func</code> for designing Hamburger icon on the <code>navigationBa</code>r</li><li>Use <code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">.ignoresSafeArea()</mark></code> to use entire area visible for Sidebar menu</li><li><code>customDrag</code> is used for enable swipe from left to invoke <code>SideBarMenu</code> where <code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color"><strong>if</strong> $0.location.x < 200</mark></code> defines that it will invoke drag only when finger is from<code> 0 to 200 on <mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">x</mark> Axis </code></li><li>To enable Left To right swipe we used  <code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color"><strong>if</strong> ($0.location.x - $0.startLocation.x) > 0 {</mark></code><br>Entertain only when Gesture ends i.e.  <code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-7-color">.onEnded {</mark></code></li></ol>
<!-- /wp:list -->

<!-- wp:heading {"level":5} -->
<h5><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">2. ViewModel.swift</mark></h5>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">class ViewModel: ObservableObject {
    // Indicates Hamburgers visiblity 
    @Published var isMenuVisible:Bool = false
}</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":5} -->
<h5><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">3. SideBarMenu.swift</mark></h5>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">import SwiftUI
// HamburgerView
struct SideBarView:View {
    
    @EnvironmentObject var viewModel:ViewModel
    
    var body: some View {
        
        ZStack {
            if self.viewModel.isMenuVisible {
                Color.black.opacity(0.3)
                    .ignoresSafeArea()
                    .transition(.opacity)
                VStack(alignment: .leading) {
                    Image(systemName: "brain.head.profile")
                        .resizable()
                        .overlay(
                            Circle().stroke(Color.gray, lineWidth: 1))
                        .frame(width: 60, height: 60)
                        .clipShape(Circle())
                    Text("SwiftUI Menu")
                        .font(.largeTitle)
                    Text("You Did It")
                        .font(.caption)
                    Divider()
                    
                    ScrollView {
                        ForEach((1...40), id: \.self) {
                            Text("Side Menu Index---> \($0)")
                        }
                    }
                    Divider()
                    Text("bottom")
                    
                }
                .padding(,50)
                .padding(.leading, 20)
                .frame(maxWidth:.infinity, maxHeight: .infinity)
                .background(Color.white)
                .cornerRadius(5)
                .padding(.trailing,50)
                .transition(
                    .asymmetric(
                        insertion: .move(edge: .leading),
                        removal: .move(edge: .leading)
                    )
                ).zIndex(1)  // to force keep at top 
            }
        }
        .frame(maxWidth: .infinity, maxHeight: .infinity)
        .animation(.default, value: self.viewModel.isMenuVisible)  // << here !!
    }
}</code></pre>
<!-- /wp:code -->

<!-- wp:list {"ordered":true} -->
<ol><li>Here i have created a List with top header icon which most generally used in Hamburgers Menu</li><li><code><strong>if</strong> <strong>self</strong>.viewModel.isMenuVisible {</code> Indicates show menu only id flag is on</li><li><code>transition(</code> is used to define asymmetric for insertion & Removal</li><li><code>.zIndex(1)</code> for managing item at top of hierarchy</li><li>That's All :)</li></ol>
<!-- /wp:list -->

<!-- wp:paragraph -->
Final Code is <a href="https://github.com/janeshsutharios/iOS_Tutorials/tree/main/SideBar_SwiftUI" target="_blank" rel="noopener" title="">Available here </a>


<!-- /wp:paragraph -->