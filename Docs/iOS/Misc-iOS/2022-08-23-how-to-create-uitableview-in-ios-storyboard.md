---
title: "How to create UITableView in iOS storyboard"
date: 2022-08-23 05:40:34
categories: ['ios', 'iOS', 'Swift', 'swift', 'uitableview']
layout: post
---

<!-- wp:paragraph -->
To populate a list of items in the iPhone you can use <code>UITableView</code> which provides vertical scrolling over the items. In this article we will <code>UITableView</code> in iOS with <code>storyboard</code> and add some items to it.


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
Let’s Code


<!-- /wp:paragraph -->

<!-- wp:image {"id":1111,"sizeSlug":"full","linkDestination":"none"} -->
<figure class="wp-block-image size-full">![](/TechBlogs/Assets/Website/2022/08/UItableView.png)</figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<strong>Step 1:</strong> Create New Xcode Project & jump towards <code>Main.StoryBoard</code>


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<strong>Step 2:</strong> Click on + icon(Object Library) & Drag <code>UITableView</code> to <code>StoryBoard</code>


<!-- /wp:paragraph -->

<!-- wp:image {"id":1108,"sizeSlug":"full","linkDestination":"none"} -->
<figure class="wp-block-image size-full">![](/TechBlogs/Assets/Website/2022/08/objectlibrary.png)</figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
Step 3: Add<code> leading, trailing top bottom </code>constraints to the <code>tableView</code>, deselect the Constraint to margin Option.


<!-- /wp:paragraph -->

<!-- wp:image {"id":1109,"sizeSlug":"full","linkDestination":"none"} -->
<figure class="wp-block-image size-full">![](/TechBlogs/Assets/Website/2022/08/constraints.png)</figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<strong>Step 4:</strong>  Create a <code>IBOutlet</code> of <code>UITableView</code>. By clicking right click on<code> UITableView </code>& drag the line to<code> ViewController.swift f</code>ile


<!-- /wp:paragraph -->

<!-- wp:image {"id":1110,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large">![](/TechBlogs/Assets/Website/2022/08/iboutlet-1024x513.png)</figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<strong>Step 5</strong>: To link Data/Array to the UItableView we have Make dataSource conformance to self Means The current ViewController class will adopt the methods of UITableViewDataSouce & we can provide data objects to the UITableView


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
– <code>numberOfRowsInSection</code> used for how many rows to present in <code>UITableView</code> 


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
–<code>cellForRowAt</code><strong> </strong>used for designing the cell items 


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<strong>Step 6</strong>: To listen click events of UITableView we have Make delegate conformance to self


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
The Complete Code is here -


<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code lang="swift" class="language-swift">import UIKit

class ViewController: UIViewController {

    @IBOutlet weak var customTableView: UITableView!
    
    var programmingLanguagesArray = 
    
    override func viewDidLoad() {
        super.viewDidLoad()
        setUpUItableView()
    }

    // Setting UItableview 
    func setUpUItableView() {
        customTableView.dataSource = self
        customTableView.delegate = self
        customTableView.estimatedRowHeight = 80// To make resizable cells
        customTableView.rowHeight = UITableView.automaticDimension
        //To register Fresh cell to the TableView
        customTableView.register(UITableViewCell.self, forCellReuseIdentifier: "cell")
    }

}

// MARK: UITableViewDataSource
extension ViewController: UITableViewDataSource {
    
    // Return a list of item in array
    func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        return programmingLanguagesArray.count
    }
    
    // return a cell for specific row
    func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        guard let cell = tableView.dequeueReusableCell(withIdentifier: "cell") else {
            return UITableViewCell()
        }
        var content = cell.defaultContentConfiguration()
        content.text = programmingLanguagesArray
        cell.contentConfiguration = content
        return cell
    }
}

// MARK: UITableViewDelegate
extension ViewController: UITableViewDelegate {
    
    func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath) {
        print("Clicked on row -->", indexPath.row)
    }
}</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
Here is<a href="https://developer.apple.com/documentation/uikit/uitableview"> Apple reference </a>


<!-- /wp:paragraph -->

<!-- wp:paragraph -->
A complete <a href="https://github.com/janeshsutharios/iOS_Tutorials/tree/main/UITableView_Example_Swift">Source code is Here </a>: )


<!-- /wp:paragraph -->