---
layout: learningmaterial
title: CSS 3
---

<section id="box-sizing">
<h1 class="section-title">Box-sizing</h1>
<p>Some of you might remember the bad days, the days of IE6 and below. You might remember the IE box model and how it differed from the modern W3C compliant browsers, well it turns out that Microsoft got it right. It might not have been right at the time but we've since come to realize that it had its advantages over the W3C box model that is now the default on the web.</p>
<p>As you probably know, the normal CSS2.1 box model is calculated as follows <code>Width + Padding + Border = rendered width</code>, you might argue that the <code>Margin</code> property belongs here to, but it isn't part of the actual box model, it's just closely related. This also applies to height but we're mostly concerned with the width.</p>
<p>CSS3 reintroduces the old model with the <code>box-sizing: border-box</code> property value. This changes the calculation to <code>Width = rendered width</code>, cool huh? This is extremely helpful when moving away from fixed width layouts as it allows us to use percentage based widths with fixed value paddings/borders without adding extra markup elements.</p>
<p>A common style rule is to change every element to use this box model:</p>
<pre>
*, *:before, *:after {
	box-sizing: border-box;
}
</pre>
<p>The performance hit because of doing this is extremely negligent as the * selector by itself is incredibly fast because of the way that CSS selectors are parsed.</p>
<h2 class="section-subtitle">Browser support</h2>
<p>The <code>box-sizing: border-box;</code> is supported in IE8 and up, Safari below 5.1 requires <code>-webkit-box-sizing</code> and Firefox still requires <code>-moz-box-sizing</code> for all versions.</p>
</section>

<section id="pseudo-elements">
<h1 class="section-title">Pseudo elements</h1>
<h2 class="section-subtitle">:after and :before</h2>
<p>These pseudo elements might be some of the best additions to CSS3, they are almost as important as the new box model rendering. They are simply put, elements that are inserted into the element that you target, not before or after it, but inside and before or after the elements content. These elements can also be styled and positioned in the same way that any other element can. This means that you can use it to create simple directional arrows for dropdown menus or ascending/descending headers without extra markup, you can also use it for pretty overlays of images with cool effects, and even more advanced CSS alchemy. Creating cross browser semi-transparent backgrounds can be a pain, RGBA isn't supported everywhere and opacity effects every child element/content on the element that has it, you can solve this with the :before element by setting it to cover the whole element and setting the opacity of the pseudo-element, this will leave the actual element/content untouched. The sky is the limit with pseudo-elements, you just have to remember to set the <code>content:</code> property to atleast an empty string for the element to be rendered. There is also a IE bug when combining pseudo-elements with pseudo-classes such as <code>:hover</code>.</p>
<p>pseudo-elements are supported in all major browsers, IE8 and up.</p>
</section>

<section id="transitions">
<h1 class="section-title">Transitions</h1>
<p>Long gone are the days when we performed animations using javascript that ran on the CPU and were never that smooth. This is were CSS transitions come in, they are defined in CSS and render on the GPU if the system supports it. Transitions simply let us animate most CSS properties such as width, padding, color and position properties, they will be triggered whenever a selector "hits" an element:</p>
<pre>
.transitionable {
	transition: all 0.3s ease-in-out 0.5s;
	height: 100px;
}
.transitionable:hover, .transitionable.active {
	height: 200px;
}
</pre>
<p>This simple example demonstrates a class that will animate to its new height if it's hovered or gains/loses the <code>.active</code> class. Saying that it will animate its height isn't the whole story though, it will actually animate any new css property since we've specified "all" as the <code>transition-property</code> value, this is also true for properties added/lost in the elements style attribute. We've set the <code>transition-duration</code> to 0.3 seconds meaning that this is the time the animation will take from start to finish, we've also applied the <code>transition-timing-function ease-in-out</code> meaning that the animation speed won't be linear. The last value that we've applied is the <code>transition-delay</code> value that simply tells the animation to wait the specified intervall after a change has occured before running the animation, this is useful for hover animations that shouldn't run if the user just drags over an element without stopping. You might have noticed that we have two interval values, the order is always duration followed by delay which can be omitted.</p>
 <p>Animations are one of those things that aren't necessary, they definately have their place in UX and design but we should simply omit them instead of using hacks to get them to display in browsers that doesn't support native transitions (mileage may vary). Transitions are supported in IE10 and up and in all other modern browsers.</p>
</section>