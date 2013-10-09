# Front-End Code Standards


This document contains guidelines for web pages and applications built by the Money Advice Service development team. It is based on [http://isobar-idev.github.io/code-standards/](http://isobar-idev.github.io/code-standards/) but with amendments, deletions and additions, especially concerning accessibility.

It is a living document that will be continually updated and improved.

This document's primarily aims to achieve: 1) code consistency and establish 2) best practices. By maintaining consistency in coding style and convention, we can ease the burden of legacy code maintenance, and mitigate risk of breakage in the future. By adhering to best practices, we ensure optimised page loading, accessibility, performance and maintainable code.

## Contents

1. [General Guidelines](#general-guidelines)
2. Progressive Enhancement
3. HTML Markup
4. CSS
5. JavaScript
6. Accessibility
7. Performance
8. Browser Testing and Support
9. Search Engine Optimisation
10. Code Reviews


## Core Concepts
* Separation of content, style and behaviour.
* Markup should be clear, concise, semantic and generally valid.
* Javascript should progressively enhance the experience.

## Progressive Enhancement
Where possible follow the principles of [progressive enhancement](https://www.gov.uk/service-manual/making-software/progressive-enhancement.html). Start by making sure your content is in the correct/logical order. Then select the most appropriate HTML elements and wai-aria atributes.

## General Practices

#### Indentation
The Money Advice Service indents all code by 2 spaces. There is no technical reason behind this practice, it simply minimises horizontal whitespace and sets up a standard for the development team to adhere to.

#### Readability vs Compression
We prefer readability over file-size savings when it comes to maintaining existing files. Plenty of whitespace is encouraged where appropriate. There is no need for any developer to purposefully compress HTML or CSS, nor obfuscate JavaScript.

We will use server-side or build processes to automatically minify and gzip all static client-side files, such as CSS and JavaScript.

### Resetting through normalise.scss

Not all projects require the same level of browser reset. However, we have settled on an amended version of the Normalise.scss reset by [Nicolas Gallagher](http://necolas.github.io/normalize.css/).


## HTML Markup
### HTML5
We use the HTML5 Doctype by default and employ HTML5 features when appropriate.

We test our markup against the [W3C validator](http://validator.w3.org/), to ensure that the markup is well formed. 100% valid code is not essential, but validation helps identify possible issues when building maintainable, accessible, robust sites as well as debugging code.

#### Quoting Attributes
The HTML5 specification defines quotes around attributes as optional. For consistency with attributes that accept whitespace, all attributes should be quoted using double quotation marks.

	<p class="line note" data-attribute="106">This is my paragraph of special text.</p>

### Doctype
We use the HTML5 doctype by default.

	<!DOCTYPE html>

This allows us to use WAI-ARIA roles, microdata and validate our pages. This also triggers standards mode in the browser.

### Character Encoding
All markup should be delivered as UTF-8, as it's the most friendly for internationalisation. We specify it in the head of the document

	<meta http-equiv="content-type" content="text/html; charset=UTF-8">

### General Markup Guidelines

The following are general guidelines for structuring your HTML markup. Authors are reminded to always use markup which represents the semantics of the content in the document being created.
Start by making sure your content is in the correct/logical order in your html document.  Then select the most appropriate html elements and wai-aria attributes to mark the content up.

* Specifying the language of content via the lang attribute - e.g `'lang="en-GB"'` which ensures content is read out correctly by screenreaders.
* Each page should have a unique H1 which should be the page or article title.
* Use a hierarchical heading structure to help screen reader users navigate a page.
* Use actual P elements for paragraph delimiters as opposed to multiple BR tags.
* For links use a link `<a>` - a link takes you to content on the same or another page
* For buttons use a `<button>` - a button performs an action such as opening a widget or playing a video/animation
* Use `label` fields to label each form field, the `for` attribute should associate itself with the `id` of the input field, so users can click the labels.
* Do not use the size attribute on your input fields. The size attribute is relative to the font-size of the text inside the input. Instead use css width.
* Tables are not be used for page layout.
* Use microformats and/or microdata where appropriate, specifically hCard and adr.
* Make use of THEAD, TBODY, CAPTIONS and TH tags (and Scope attribute) when marking up tables.
* Always use title-case for headers and titles. Do not use all caps or all lowercase titles in markup, instead apply the CSS property `text-transform:uppercase/lowercase`.
* Utilise the new HTML5 elements such as `header`, `nav`, `section`, `article`, `aside`, `footer` - but ensure you are using a [html5shiv](https://code.google.com/p/html5shiv/) so they can be styled in IE6,7,8
* Keep the DOM as simple as possible
* Use semantic markup.
* Start by making sure your content is in the correct and most logical order in your document before surrounding it with HTML tags. Then select the most appropriate HTML elements and wai-aria attributes to mark up the content.
* Specify the language of content via the lang attribute - e.g `'lang="en-GB"'` which ensures content is read out correctly by screenreaders.
* Use a hierarchical heading structure to help screen reader users navigate a page.
* For links use a link `<a>` - a link takes you to content on the same or another page.
* For buttons use a `<button>` - a button performs an action such as opening a widget or playing a video/animation.

### WAI-ARIA

* Use WAI-ARIA landmark roles to help screen reader users understand and navigate a page.
* Use WAI-ARIA form attributes to help screen reader users to use forms - e.g `aria-required="true"`.
* Use live regions to inform screen reader users of dynamic text changes - e.g `<div aria-live="polite" aria-atomic="true">`
* Follow the [WAI-ARIA 1.0 Authoring Practices](http://www.w3.org/TR/wai-aria-practices/) when implement javascript widgets such as sliders, tooltips and tab panels.


## CSS
### General Coding Principles
* Do not use presentational class names such as 'green'.
* Any style you apply to :hover also apply to :focus so that keyboard users get the same visual cues.
* Do not make your styles too specific - specifity wars are a maintanence nightmare!
* Avoid using IDs (keeps specificity low and promotes reusability)
* Instead of using content semantics for class names (e.g news) use intention and design patterns (e.g promo-box and carousel) to ensure reusability of the object.
* Style classes (.subheading) instead of elements (h2) to promote reusablity and reduce tying design to document structure (which is very brittle).
* *NOTE: these apply to large sites rather than small sites/features*
* @todo: finish this list and add link to video
* Use Sass to make your CSS more maintainable.

 <!-- add something about using .no-js and .js-enhanced classes on the body element to enable contextual styling   -->

### Sass
The Money Advice Service operates a Ruby on Rails environment and as such we write all our CSS using the Sass preprocessor language.

To avoid deviating to far from the normal CSS syntax we use .scss, rather than the .sass variant.

We follow the Sass communities "[Inception Rule](http://thesassway.com/beginner/the-inception-rule)" that advises that you should not nest your SCSS more than four levels deep.

Ideally you should aim for two levels of nesting which gives enough flexibility for selectors and their accompanying pseudo-states (i.e :hover).

Nesting selectors more than three levels deep, while tempting, causes verbose and unwieldly CSS to be constructed on compile.

### B.E.M. Naming Convention

We have started following the BEM (block, element, modifier) naming convention for assigning clear, conscise and semantic classes to our HTML elements.

An explanation of BEM can be found on [CSS Wizardry](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/) - we ave opted for the [SUIT naming convention](https://github.com/suitcss/suit/blob/master/doc/naming-conventions.md):

    .Block{}
    .Block-element{}
    .Block--modifier{}

.Block represents the higher level of an abstraction or component.
.Block-element represents a descendent of .block that helps form the .block object.
.Block--modifier represents a different state or version of .block.

A practical example of this is:

    .SiteSearch{} /* Block */
    .SiteSearch-field{} /* Element */
    .SiteSearch--full{} /* Modifier */

As noted in the CSS Wizardry article HTML elements marked up with the BEM naming convention can appear "ugly" and verbose. However, where they excell is in their readbility and their contribution to maintainable code.

However, please note that the BEM naming style does not need to be used for elements that have no relationship to parent elements or sit on their own. Remember that BEM is used to clarify code, not to be adhered to without question.

<!-- ### Object Oriented CSS

In order to create a scaleable, reusable, and maintainable codebase we have adopted object oriented CSS (OOCSS). OOCSS in its simplest terms reduces CSS to generic objects that can be extracted from one location and reused across a website or application without unnecessary repetition.

"single responsibility principle" - everything should do one thing, one thing only, and one thing well. This allows for a greater combination of...

Utilise [Object Oriented CSS](http://coding.smashingmagazine.com/2011/12/12/an-introduction-to-object-oriented-css-oocss/) (OOCSS) and [Scalable and Module Architecture for CSS](http://smacss.com/) (SMACSS) -->

### Web Typography
The Money Advice Service utilised web fonts in two ways. First, our brand font "Museo Slab" is referenced using the @font-face declaration. Secondly, to avoid unnecessary HTTP requests we encode site-wide and application specific icons in a web font. This allows for scalability without using individual SVG files or image sprites.

It is also compatible with IE8 which we are required to support.

#### Resources
* [In your @font-face](http://fronteers.nl/congres/2011/sessions/in-your-font-face-jake-archibald) by Jake Archibald

## JavaScript
### JavaScript Libraries
Our library of choice is [jQuery](http://jquery.com/)

We should be using the latest version of jQuery 1.x which is currently 1.10.2

*Note: It looks like we are currently using a few (older) versions on the website. We should improve this so they are all using the same CDN'd version, so user have a higher chance of it already being cached in their browser.*

Use [html5shiv](https://code.google.com/p/html5shiv/) to ensure html5 element work in older version of Internet Explorer (pre IE 9)

### General Coding Principles

Touch the DOM as little as possible as it is VERY slow. Instead cache nodelists and insert HTML as few times as possible.

## Accessibility
All web pages and interfaces must comply to [Web Content Accessibility Guidelines](http://www.w3.org/TR/WCAG/) (WCAG) 2.0 AA standard both to the letter and in spirit.

### The four characteristics of accessible web content are:

#### Perceivable
* Provide text alternatives for non-text content.
* Provide captions and other alternatives for multimedia.
* Create content that can be presented in different ways,
including by assistive technologies, without losing meaning.
* Make it easier for users to see and hear content.

#### Operable
* Make all functionality available from a keyboard.
* Give users enough time to read and use content.
* Do not use content that causes seizures.
* Help users navigate and find content.

#### Understandable
* Make text readable and understandable.
* Make content appear and operate in predictable ways.
* Help users avoid and correct mistakes.

#### Robust
* Maximize compatibility with current and future user tools.

### Common accessibility blunders include:

* Content not being in a logical order in the document - as a developer has been concentrating on the visual layout rather then the content heirarchy.
* Not using alternative text ("alt") that conveys the meaning of an image appropriately.
* Not having a text alternative for multimedia content -i.e captions and transcipts.
* Using jargon and complicated language instead of simple and clear language.
* Not using headings correctly. A page should have one single h1 representing the page title. Other headings should be hierachical and allow a screen reader user to get an overview of the content on a page.
* Failing to use the most appropriate semantic elements to mark up content
* Using too many lists and headings  which add aural clutter to screen reader users.
* Failing to mark up forms correctly.
* Communicating information by colour alone which will not be percieved by colour blind users.
* Not having a visual state that shows when a element has focus - i.e not styling :focus the same as :hover.
* Only communicating states and actions visually - e.g selected, open, close. This also needs to be in the content/markup layer.
* Failing to allow a keyboard user to access all content and functionally on a page - usually by using incorrect HTML elements, e.g spans and divs instead of links or buttons or by introducing keyboard traps with javascript.
* Failing to inform a screen reader user when content dynamically updates on a page.
* Failing to set focus when dynamic content is loaded such as a modal box and not enabling a keyboard user to close such content.

*Note: We should be following GOV.UKs lead who have done extensive accessibility testing: [https://www.gov.uk/service-manual/user-centered-design/accessibility](https://www.gov.uk/service-manual/user-centered-design/accessibility)*

### Resources
* [WebAim](http://webaim.org/) - Information, training, resources, guidelines and standards for Web accessibility and disability access to the Web.
* [Draft BBC Mobile Accessibility Guidleines](http://www.bbc.co.uk/guidelines/futuremedia/accessibility/mobile_access.shtml)

## Performance
A slow website results in a poor user experience. Most of web page performance is affected by front-end engineering, that is, the user interface design and development.

### Basics

**Link to styles from the document head.** A browser renders a page progressively in a specific order, and it will not render a page until it has gathered all the required style information.

Therefore if you are linking to the pages stylesheets at the bottom of a page it will not draw the page until this link is reached. Consequently we link to our stylesheets in the head so that the browser can start rendering immediately upon load.

**Link to scripts from the bottom of the document** (before the closing body tag) as JavaScript blocks the browser from downloading assets until it has loaded any required scripts.

A browser normally attempts to download as many assets as it can in parallel. JavaScript interupts this process.

First, the browser assumes that any script being called may alter the page substantially and therefore prioritises loading the script before loading an asset.

Secondly, scripts are downloaded asynchronously in order that a library like jQuery arrives before the script that relies on it (your plugin).

In a nutshell - to render a page as fast as the browser will allow link to your styles in the head and to prevent JavaScript from stalling the rendering process, call scripts from the bottom.

### HTTP Requests

Download less.

Every asset on a page requires a HTTP request to call it to be downloaded and rendered. This involves a DNS lookup, redirects and possible 404 errors for lost assets. Minimising the amount of information the browser has to request is the simplest way of increasing website performance.

Additionally, browsers can only download a set number of assets "in parallel" which can introduce a bottleneck when downloading, for example, large images.

### CDN

A browser is capped on the number of HTTP requests it can make in parallel. Serving assets from multiple domains (especially if they are CDN designed to decrease latency by being physically located near to our web server) can increase the number of assets a browser can download in parallel.

### HTTP requests and DNS Lookups

### DNS Prefetching

### Resource Prefetching

### CSS and Performance

* Never serve your CSS from an asset subdomain as the DNS lookup will delay rendering.
* Link to the stylesheet from the document head.
* Concatenate it.
* Gzip and minify it to further reduce the file size.
* Cache it to avoid continuing HTTP requests.

### Gzipping and Minifying

Using Gzip and minifying CSS are two simple methods of increasing CSS performance. 

Minifying them to remove any comments and whitespace, and gzipping them to compress them down further.

.htaccess files


### Resources

Yahoo's Exceptional Performance team has identified a number of [best practices for making web pages fast](http://developer.yahoo.com/performance/rules.html). The list includes 35 best practices divided into 7 categories. 23 of these can be checked using the [YSlow](http://yslow.org/) tool:

<ol>
<li><a href="http://developer.yahoo.com/performance/rules.html#num_http">Minimize HTTP Requests</a> - use css sprites, data uris and concatenate CSS and JS files</li>
<li><a href="http://developer.yahoo.com/performance/rules.html#cdn">Use a Content Delivery Network</a></li>
<li><a href="http://developer.yahoo.com/performance/rules.html#emptysrc">Avoid empty src or href</a></li>
<li><a href="http://developer.yahoo.com/performance/rules.html#expires">Add an Expires or a Cache-Control Header</a></li>
<li><a href="http://developer.yahoo.com/performance/rules.html#gzip">Gzip Components</a></li>
<li><a href="http://developer.yahoo.com/performance/rules.html#css_top">Put StyleSheets at the Top</a></li>
<li><a href="http://developer.yahoo.com/performance/rules.html#js_bottom">Put Scripts at the Bottom</a></li>
<li><a href="http://developer.yahoo.com/performance/rules.html#css_expressions">Avoid CSS Expressions</a></li>
<li><a href="http://developer.yahoo.com/performance/rules.html#external">Make JavaScript and CSS External</a></li>
<li><a href="http://developer.yahoo.com/performance/rules.html#dns_lookups">Reduce DNS Lookups</a></li>
<li><a href="http://developer.yahoo.com/performance/rules.html#minify">Minify JavaScript and CSS</a></li>
<li><a href="http://developer.yahoo.com/performance/rules.html#redirects">Avoid Redirects</a></li>
<li><a href="http://developer.yahoo.com/performance/rules.html#js_dupes">Remove Duplicate Scripts</a></li>
<li><a href="http://developer.yahoo.com/performance/rules.html#etags">Configure ETags</a></li>
<li><a href="http://developer.yahoo.com/performance/rules.html#cacheajax">Make AJAX Cacheable</a></li>
<li><a href="http://developer.yahoo.com/performance/rules.html#ajax_get">Use GET for AJAX Requests</a></li>
<li><a href="http://developer.yahoo.com/performance/rules.html#min_dom">Reduce the Number of DOM Elements</a></li>
<li><a href="http://developer.yahoo.com/performance/rules.html#no404">No 404s</a></li>
<li><a href="http://developer.yahoo.com/performance/rules.html#cookie_size">Reduce Cookie Size</a></li>
<li><a href="http://developer.yahoo.com/performance/rules.html#cookie_free">Use Cookie-Free Domains for Components</a></li>
<li><a href="http://developer.yahoo.com/performance/rules.html#no_filters">Avoid Filters</a></li>
<li><a href="http://developer.yahoo.com/performance/rules.html#no_scale">Do Not Scale Images in HTML</a> - <i>note: dated due to responsive</i></li>
<li><a href="http://developer.yahoo.com/performance/rules.html#favicon">Make favicon.ico Small and Cacheable</a></li>
</ol>

### jQuery Proven Performance Tips And Tricks

[Slides by Addy Osmani](http://addyosmani.com/jqprovenperformance/)

@todo: summarise slides


### Tools to help you measure and improve performance are:
* [YSlow](http://yslow.org/)
* [jsperf](http://jsperf.com/)
* [boomerang](http://yahoo.github.io/boomerang/doc/) - End user oriented web performance testing and beaconing
* In browser waterfall UI - found in Chrome (best), also Safari, Firebug, IE and Opera
* [Performance Tools](http://www.stevesouders.com/blog/2012/10/09/webperfdays-performance-tools/) - stevesouders.com

## Browser Testing and Support

The Money Advice Service aims to provide the best experience for the widest range of customers, whilst also ensuring efficient and value driven development of features and use of resources. We aim to provide the best experience for the largest number of our core customers.

The Money Advice Service accepts that the nature of the web as a medium is such that not all web pages can be rendered uniformly and consistently across all browsers. The Money Advice Service also accepts that certain variations in the customer's digital experience are inevitable and are acceptable to a certain extent.

The following browser support standards and guidelines seek to address the trade-off between experience, reach and resources.

### Primary Browsers - supported

* All content must be readable and all functionality must work.
* Where variations inevitably occur between browsers:
	* All content must remain readable.
	* Decisions of trade off through development are prioritised to give those that maximise and benefit the majority of customers according to our browser statistics.
* Pages should be produced to maximise the user experience for the browsers used by the largest number of our core and key customers.

| Browser name | Version | Platform  |
| ------ | ------ | -----: |
|  Internet Explorer  |  8, 9  |   Windows  |
|  Firefox  |  17+  |   Mac/Windows  |
|  Chrome  |  23+  |   Mac/Windows  |
|  Safari  |  5.1+  |   Mac  |


### Secondary Browsers - partially supported

* All main content must be readable and navigation must function.
* Any degradation to the user experience must not affect the ability of the user to read content.
* Any degradation to functionality must follow the principal of graceful degradation

| Browser name | Version | Platform  |
| ------ | ------ | -----: |
|  Internet Explorer  |  10  |   Windows  |
|  Opera  |  9.6x, 10  |   Mac/Windows  |


*Note: This needs updating as I believe our content should be usable in older browsers too (even if it doesn't look pretty!) - we should be using Progressive Enhancement rather than gracefull degradation. This will be especially true when we start building a responsive site. IE10 should also be a primary browser. We need to start thinking about mobile browser/device support.*

*We should be following the same approach as GOV.UK, see: [https://www.gov.uk/service-manual/user-centered-design/browsers-and-devices](https://www.gov.uk/service-manual/user-centered-design/browsers-and-devices)*


## Search Engine Optimisation
An essential part of good web design and development is SEO. Well-structured code is the key to ensuring that a web page not only gets properly indexed by search engines, but made accessible to those with limited web capabilities as well.

## Code Reviews
