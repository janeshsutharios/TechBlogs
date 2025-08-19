---
title: "How to add UIScrollView Constraints"
date: 2022-08-21 11:36:06
categories: ['ios', 'iOS', 'Scroll list', 'Swift', 'swift', 'UISCrollView']
layout: post
---

<ol>
<li>Drag <em>UIScrollView</em> to <em>storyboard</em></li>
<li>Add<em> leading, trailing, top, bottom</em> of <em>UIScrollView</em></li>
<li>Add UIView Inside <em>UIScrollView</em> & Rename it to <em>scrollContainerView</em></li>
<li>Add <em>leading, trailing, top, bottom</em> of <em>UIScrollView</em> with parent <em>UIScrollView</em></li>
<li>Add Equal Width content of <em>scrollContainerView</em> with respect to <em>UIScrollVIew</em></li>
<li>Add objects to the <em>scrollContainerView</em> - i have added two button make sure <em>leading trailing top & bottom</em> is set with respect to the <em>scrollContainerView</em></li>
<li>Make sure the to add last item(<em>UIButton</em>) constraint to bottom of the <em>scrollContainerView</em></li>
</ol>
<blockquote>
The <a href="https://github.com/janeshsutharios/iOS_Tutorials/tree/main/UIScrollView_iOS_Demo">Source code is here </a>


Note: If you need horizontal scroll make  scrollContainerView equal height constraint with UIScrollView


</blockquote>
Here is the Youtube video of the same process. --



<!-- wp:embed {"url":"https://www.youtube.com/watch?v=4zG1hvwJ7G8","type":"video","providerNameSlug":"youtube","responsive":true,"className":"wp-embed-aspect-16-9 wp-has-aspect-ratio"} -->
<figure class="wp-block-embed is-type-video is-provider-youtube wp-block-embed-youtube wp-embed-aspect-16-9 wp-has-aspect-ratio"><div class="wp-block-embed__wrapper">
https://www.youtube.com/watch?v=4zG1hvwJ7G8
</div></figure>
<!-- /wp:embed -->

<!-- wp:paragraph -->



<!-- /wp:paragraph -->