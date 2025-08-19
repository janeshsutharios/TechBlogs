---
title: "How to use MARK: in iOS Swift ?"
date: 2022-08-20 08:35:26
categories: ['coderedablility', 'ios', 'iOS', 'Markdown', 'markup', 'Swift', 'swift']
layout: post
---


<!-- wp:paragraph -->
We can write code annotation so that when we see the Minimap, it will list out functions & vars of the project in sectioned manner. This will speedup to jump the desired piece of code.<br>At Minimum we can apply the <strong>// MARK:  -- ViewLifeCycle</strong> It will look like below image


<!-- /wp:paragraph -->

<!-- wp:image {"id":1060,"sizeSlug":"full","linkDestination":"none"} -->
<figure class="wp-block-image size-full">![](/TechBlogs/Assets/Website/2022/08/XCode-swift-mark-2.png)</figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
For the Code


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">    //MARK:  -- ViewLifeCycle

    override func viewDidLoad() {
        super.viewDidLoad()
        // Do any additional setup after loading the view.
    }


}
// MARK:  -- UITableViewDataSource
extension ViewController : UITableViewDataSource {
    func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        return 0
    }
    
    func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        return UITableViewCell()
    }
}

// MARK: Here is -- UITableViewDelegate
extension ViewController: UITableViewDelegate {
    
}

//TODO: - To do block A TODO  reminder ...
extension ViewController {
    func makeAPICall() {}
}


//FIXME: - Bug fix block... A bug fix reminder ...
extension ViewController {
    func bugfix() {}
}
</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
So we can also use additional markup based upon need like //TODO: To do block //FIXME: - Bug fix block.


<!-- /wp:paragraph -->
