# Front-end Code Standards &amp; Best Practice


This document contains guidelines for web pages and applications built by the Money Advice Service development team. It is inspired/based on [http://isobar-idev.github.io/code-standards/](http://isobar-idev.github.io/code-standards/) but with amends, deletions and additions, especially around accessibility. It is a living document that will be continually updated and improved.

This document's primary motivation is two- fold: 1) code consistency and 2) best practices. By maintaining consistency in coding styles and conventions, we can ease the burden of legacy code maintenance, and mitigate risk of breakage in the future. By adhering to best practices, we ensure optimized page loading, accessibility, performance and maintainable code.

## General Guidelines
### Pillars of Front-end Development
* Separation of presentation, content, and behavior.
* Markup should be well-formed, semantically correct and generally valid.
* Javascript should progressively enhance the experience.

Where possible follow the principles of [progressive enhancement](https://www.gov.uk/service-manual/making-software/progressive-enhancement.html). Start by making sure your content is in the correct/logical order.  Then select the most appropriate html elements and wai-aria atributes to mark the content up and ensure that core functionality works using HTTP (i.e links and forms). Then add images and apply css styles taking care to not introduce accessibility barriers. Finally add javascript and ensure you allow full keyboard access and keep screen reader users informed of what is being communicated to sighted users (e.g state and dynamic content changes). Where progressive enhancement isn't possible or pramatic it is still important to use semantic markup and to ensure that javascript is made accessible.

### General Practices

#### Indentation
To be discussed

#### Readability vs Compression
We prefer readability over file-size savings when it comes to maintaining existing files. Plenty of whitespace is encouraged where appropriate. There is no need for any developer to purposefully compress HTML or CSS, nor obfuscate JavaScript.

We will use server-side or build processes to automatically minify and gzip all static client-side files, such as CSS and JavaScript.


## Markup
### HTML5
We use the HTML5 Doctype and HTML5 features when appropriate.

We test our markup against the [W3C validator](http://validator.w3.org/), to ensure that the markup is well formed. Valid html helps to write more maintainable, accessible, robust sites as well as debugging code.

#### Quoting Attributes
The HTML5 specification defines quotes around attributes as optional. For consistency with attributes that accept whitespace, all attributes should be quoted.

	<p class="line note" data-attribute="106">This is my paragraph of special text.</p>

#### Doctype
We use the HTML5 doctype. 
	
	<!DOCTYPE html>

This means we can use WAI-ARIA and mirodata and validate our pages. This also triggers standards mode in your browser.

### Character Encoding
All markup should be delivered as UTF-8, as its the most friendly for internationalization.
We specify it in the head of the document

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
* Use microformats and/or Microdata where appropriate, specifically hCard and adr.
* Make use of THEAD, TBODY, CAPTIONS and TH tags (and Scope attribute) when marking up tables.
* Always use title-case for headers and titles. Do not use all caps or all lowercase titles in markup, instead apply the CSS property `text-transform:uppercase/lowercase`.
* Utilise the new HTML5 elements such as `header`, `nav`, `section`, `article`, `aside`, `footer` - but ensure you are using a [html5shiv](https://code.google.com/p/html5shiv/) so they can be styled in IE6,7,8
* Keep the DOM as simple as possible

### WAI-ARIA

* User WAI-ARIA landmark roles to help screen reader users understand and navigate a page
* Use WAI-ARIA form attributes to help screen reader users to use forms - e.g `aria-required="true"`
* Use live regions to inform screen reader users of dynamic text changes - e.g `<div aria-live="polite" aria-atomic="true">`
* Follow the [WAI-ARIA 1.0 Authoring Practices](http://www.w3.org/TR/wai-aria-practices/) when implement javascript widgets such as sliders, tooltips and tab panels


## CSS
### General Coding Principles
* Do not use presentational class names such as 'green'
* Any style you apply to :hover also apply to :focus so that keyboard users get the same visual cues
* Utilise learnings from [Object Oriented CSS](http://coding.smashingmagazine.com/2011/12/12/an-introduction-to-object-oriented-css-oocss/) (OCSS) and [Scalable and Module Architecture for CSS](http://smacss.com/) (SMACSS)
	* Do not make your styles too specific - specifity wars are a maintanence nightmare!
	* Don't style IDs, style classes instead (keeps specificty low and promotes reusability)
	* Instead of using content semantics for class names (e.g news) uses intention and design patterns semantics (e.g promo-box and carousel) to ensure reusability
	* Style classes (.subheading) instead of elements (h2) to promote reusablity and reduce tying design to document structure (which is very brittle)
	* *NOTE: these apply to large sites rather than small sites/features*
	* @todo: finish this list and add link to video
* Use Sass to make your CSS more maintainable
 
 <!-- add something about using .no-js and .js-enhanced classes on the body element to enable contextual styling   -->
	

### Web Typography
content coming soon

#### Resouces
* [In your @font-face](http://fronteers.nl/congres/2011/sessions/in-your-font-face-jake-archibald) by Jake Archibald

## JavaScript
### JavaScript Libraries
Our library of choice is [jQuery](http://jquery.com/)

We should be using the latest version of jQuery 1.x which is currently 1.10.2

*Note: It looks like we are currently using a few (older) versions on the website.  We should improve this so they are all using the same CDN'd version, so user have a higher chance of it already being cached in there browser.*

Use [html5shiv](https://code.google.com/p/html5shiv/) to ensure html5 element work in older version of Internet Explore (pre IE 9)

### General Coding Principles

* Touch the DOM as little as possible as it is VERY slow - instead cache nodelists and insert html as few times as possible

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

### Common accessibility blunders are:

* Content not being in the a logical order in the document - as developer has been concentrating on the visual layout
* Not using alternative text that conveys the meaning of an image appropriately
* Not having text alternative for multiplemedia content -i.e captions and transcipts
* Using duplicated link text that makes no sense out of content - e.g read more, click here
* Using jargon and complicated language instead of simple language.
* Not using headings correctly.  The single h1 one of the page should be the page title. Other headings should be hierachical and allow a screen reader user to get an overview of the content on a page
* Failing to use the most appropriate semantic elements to mark up content
* Having duplicate links in close proximity - e.g wrapping an image and some text in different links that go to the same destination. Use a single link instead.
* Using too many lists and headings  which add aural clutter to screen reader users
* Failing to mark up forms correctly
* Communicating information by colour alone  which will not be percieved by colour bind users.
* Not having a visual state that shows when a element has focus - i.e not styling :focus the same as :hover
* Only communicating states and actions visually - e.g selected, open, close. This also needs to be in the content/markup layer.
* Failing to allow a keyboard user to access all content and functionally on a page - usually by using incorrect html elements, e.g spans and divs instead of links or buttons or by introducing keyboard traps with javascript
* Failing to inform a screen reader user when content dynamically updates on a page
* Failing to set focus when dynamic content is loaded such as a modal box and not enabling a keyboard user to close such content.
 
*Note: We should be following GOV.UKs lead who have done extensive accessibility testing: [https://www.gov.uk/service-manual/user-centered-design/accessibility](https://www.gov.uk/service-manual/user-centered-design/accessibility)*

### Resources
* [WebAim](http://webaim.org/) - Information, training, resources, guidelines and standards for Web accessibility and disability access to the Web.
* [Draft BBC Mobile Accessibility Guidleines](http://www.bbc.co.uk/guidelines/futuremedia/accessibility/mobile_access.shtml)

## Performance
A slow website results in a poor user experience. Most of web page performance is affected by front-end engineering, that is, the user interface design and development.

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

The MAS aims to provide the best experience for the widest range of customers, whilst also ensuring the efficient and value driven development of features and use of resources. We aim to provide the best experience for the largest number of our core and key customers.
 
The MAS accepts that the nature of the web medium is such that not all web pages can be produced uniformly and consistently across all browsers. The MAS also accepts that certain variations in the customer digital experience are inevitable and are acceptable with limits. 

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

