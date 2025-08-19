---
title: "How To Scroll To A Position Programmatically In UIScrollView"
date: 2022-10-04 12:14:20
categories: ['horizontalscrollview scroll to position', 'iOS', 'Swift', 'swift scrollview scroll to top', 'uiscrollview scroll to bottom', 'uiscrollview scroll to top']
layout: post
---

<!-- wp:paragraph -->
In general we use<code> UIScrollView, UITableView or UICollectionView</code> & sometimes we have to scroll programmatically to Top or bottom, so we can achieve it by using <code><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">setContentOffset</mark></code> where we set where exactly to scroll


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
Below are 4 helper methods which help in scrolling the Scroll view 


<!-- /wp:paragraph -->

<!-- wp:list {"ordered":true} -->
<ol><li><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">UIScrollView scroll to bottom </mark></li><li><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">UIScrollView scroll to Top </mark></li><li><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">UIScrollView scroll to Right </mark></li><li><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">UIScrollView scroll to Left </mark></li></ol>
<!-- /wp:list -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">//MARK: - Scrolling UIScrollView to possible 4 directions..

extension UIScrollView {
    
    func scrollToBottom() {
        let bottomOffset = CGPoint(x: 0, y: self.contentSize.height - self.bounds.height + self.contentInset.bottom)
        self.setContentOffset(bottomOffset, animated: true)
    }
    
    func scrollToTop() {
        let topOffset = CGPoint.zero
        self.setContentOffset(topOffset, animated: true)
    }
    
    
    func scrollToRightEnd(animated: Bool) {
        if self.contentSize.width < self.bounds.size.width { return }
        let rightOffset = CGPoint(x: self.contentSize.width - self.bounds.size.width, y: 0)
        self.setContentOffset(rightOffset, animated: animated)
    }
    
    func scrollToLeftEnd(animated: Bool) {
        if self.contentSize.width < self.bounds.size.width { return }
        let leftOffset = CGPoint.zero
        self.setContentOffset(leftOffset, animated: animated)
    }
    
}</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":4} -->
<h4><mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-ast-global-color-1-color">Example Usage : </mark></h4>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">DispatchQueue.main.async {
    self.itemsScrollView.scrollToTop()
}</code></pre>
<!-- /wp:code -->

<!-- wp:buttons -->
<div class="wp-block-buttons"></div>
<!-- /wp:buttons -->

<!-- wp:paragraph -->
You can Test on <a href="https://github.com/janeshsutharios/iOS_Tutorials/tree/main/UIScrollView_iOS_Demo" target="_blank" rel="noopener">This ScrollView project:</a> 


<!-- /wp:paragraph -->