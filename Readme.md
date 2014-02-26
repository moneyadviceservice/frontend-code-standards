# Front-End Code Standards


This document contains guidelines for web pages and applications built by the Money Advice Service development team. It is based on [http://isobar-idev.github.io/code-standards/](http://isobar-idev.github.io/code-standards/) but with amendments, deletions and additions, especially concerning accessibility.

It is a living document that will be continually updated and improved.

This document's primarily aims to achieve: 
1) code consistency and establish 
2) best practices. 

By maintaining consistency in coding style and convention, we can ease the burden of legacy code maintenance, and mitigate risk of breakage in the future. By adhering to best practices, we ensure optimised page loading, accessibility, performance and maintainable code.

## Contents

1. [General Guidelines](#general-guidelines)
2. [Progressive Enhancement](#progressive-enhancement)
3. [HTML Markup](#html-markup)
4. [CSS](#css)
5. [JavaScript](#javascript)
6. [Accessibility](#accessibility)
7. [Performance](#performance)
8. [Browser Support](#browser-support)


## General Guidelines

### Core Concepts
* Separation of content, style and behaviour.
* Markup should be clear, concise, semantic and generally valid.
* Javascript should progressively enhance the experience.

### General Practices

#### Indentation
The Money Advice Service indents all code by 2 spaces. There is no technical reason behind this practice, it simply minimises horizontal whitespace and sets up a standard for the development team to adhere to.

#### Readability vs Compression
We prefer readability over file-size savings when it comes to maintaining existing files. Plenty of whitespace is encouraged where appropriate. There is no need for any developer to purposefully compress HTML or CSS, nor obfuscate JavaScript.

All static client-side files, such as CSS and JavaScript, are automatically minified as part of the Ruby on Rails asset pipeline.

## Progressive Enhancement
Follow the principles of [progressive enhancement](https://www.gov.uk/service-manual/making-software/progressive-enhancement.html). Start by making sure your content is in the correct/logical order. Then select the most appropriate HTML elements and wai-aria atributes. Enhanced layout is then provided by externally linked CSS. Enhanced behaviour is provided by unobtrusive, externally linked JavaScript.

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
* Keep the DOM as simple as possible - although extra markup can be used to make code more scalable, reusable and maintainable.


### WAI-ARIA

* Use [WAI-ARIA landmark roles](http://blog.paciellogroup.com/2013/02/using-wai-aria-landmarks-2013/) to help screen reader users understand and navigate a page i.e
  * `role="banner"`
  * `role="complementary" `
  * `role="contentinfo"`
  * `role="form"`
  * `role="main"`
  * `role="navigation"`
  * `role="search"`
* Use WAI-ARIA form attributes to help screen reader users to use forms - e.g `aria-required="true"`.
* Use live regions to inform screen reader users of dynamic text changes - e.g `<div aria-live="polite" aria-atomic="true">`
* Follow the [WAI-ARIA 1.0 Authoring Practices](http://www.w3.org/TR/wai-aria-practices/) when implement javascript widgets such as sliders, tooltips and tab panels.


## CSS
### General Coding Principles
* Add CSS through external files, minimizing the # of files, if possible. It should always be in the HEAD of the document.
* Use the LINK tag to include, never the @import.
* Don't include styles inline in the document, either in a style tag or on the elements. It's harder to track down style rules.
* Use [normalize.css](http://necolas.github.io/normalize.css/) to make rendering more consistent across browsers. This is automatically included as part of mas-assets (our gem containing shared client side assets).
* Do not use presentational class names such as 'green'.
* Any style you apply to :hover also apply to :focus so that keyboard users get the same visual cues.
* Do not make your styles too specific - specifity wars are a maintanence nightmare!
* Avoid using IDs (keeps specificity low and promotes reusability)
* Instead of using content semantics for class names (e.g news) use intention and design patterns (e.g promo-box and carousel) to ensure reusability of the object.
* Consider styling classes (.heading-secondary) instead of elements (h2) to promote reusablity and reduce tying design to document structure (which is very brittle). If directly styling elements inside components use child selectors where possible to reduce the depth of applicability - this is ensures that styles do not affect other unintended elements.
* Use Sass to make your CSS more maintainable (see below).
 <!-- add something about using .no-js and .js-enhanced classes on the body element to enable contextual styling   -->

### B.E.M. Naming Convention
We have started following the BEM (block, element, modifier) naming convention for assigning clear, conscise and semantic classes to our HTML elements.

An explanation of BEM can be found on [CSS Wizardry](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/) - we ave opted for the [SUIT naming convention](https://github.com/suitcss/suit/blob/master/doc/naming-conventions.md):

    .block{}
    .block__element{}
    .block--modifier{}

.block represents the higher level of an abstraction or component.

.block__element represents a descendent of .block that helps form the .block object.

.block--modifier represents a different state or version of .block.

A practical example of this is:

    .site-search{} /* Block */
    .site-search__submit{} /* Element */
    .site-search--full{} /* Modifier */

As noted in the CSS Wizardry article HTML elements marked up with the BEM naming convention can appear "ugly" and verbose. However, where they excell is in their readbility and their contribution to maintainable code.

However, please note that the BEM naming style does not need to be used for elements that have no relationship to parent elements or sit on their own. Remember that BEM is used to clarify code, not to be adhered to without question.


### Sass
The Money Advice Service operates a Ruby on Rails environment and as such we write all our CSS using the Sass preprocessor language.

To avoid deviating to far from the normal CSS syntax we use .scss, rather than the .sass variant.

We follow the Sass communities "[Inception Rule](http://thesassway.com/beginner/the-inception-rule)" that advises that you should not nest your SCSS more than four levels deep.

Ideally you should aim for no more than two levels of nesting which gives enough flexibility for selectors and their accompanying pseudo-states (i.e :hover).

Nesting selectors more than three levels deep, while tempting, causes verbose and unwieldly CSS to be constructed on compile.

Avoid using @mixins to reuse static snippets of code as it can result in bloated css. Instead use placeholder selectors in @extends (see: [Mastering Sass extends and placelholders](http://8gramgorilla.com/mastering-sass-extends-and-placeholders/)). Mixins should just be used when code changes due to a variable being passed in.

The directory structure that we use for our Sass files is:

	/base
	/blocks
	/global
	  _functions.css.scss
	  _mixins.css.scss
	  _placeholders.css.scss
	  _variables.css.scss
	/layout

**global** directory contains all of the non printing styles - your tool chest - all of your functions, mixins, placeholders and variables.

**base** directory contains all of the visual styles that are not layout or are specfic to a component/module/block - this includes font-face and default element styles

**blocks** directory a file for each component/module/block. The name of the file is the same as the name of the block

**layout** directory contains styles that are used to lay blocks out on the page which includes grids and columns

### Web Typography
The Money Advice Service utilises web fonts in two ways. First, our brand font "Museo Slab" is referenced using the @font-face declaration and is available in mas-assets. Secondly, to avoid unnecessary HTTP requests we encode site-wide and application specific icons in a web font. This allows for scalability without using individual SVG files or image sprites.


## JavaScript
### JavaScript Libraries
Our library of choice is [jQuery](http://jquery.com/). We currently use jQuery 1.8.1 which is provided by Ruby on Rails.

Use [html5shiv](https://code.google.com/p/html5shiv/) to ensure html5 element work in older version of Internet Explorer (pre IE 9) which is also provided as part of mas-assets


### General Coding Principles

Touch the DOM as little as possible as it is VERY slow. Instead cache nodelists and insert HTML as few times as possible.

We have recently decided to follow the [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript)


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

In a nutshell - to render a page as fast as the browser will allow link to your styles in the head and to prevent JavaScript from stalling the rendering process, call scripts from the bottom. An excpetion is when creating contextual classes that are used for layout such as .js - these need to be in the head to prevent a flash of unstyled content.

### HTTP Requests

Download less.

Every asset on a page requires a HTTP request to call it to be downloaded and rendered. This involves a DNS lookup, redirects and possible 404 errors for lost assets. Minimising the amount of information the browser has to request is the simplest way of increasing website performance.

Additionally, browsers can only download a set number of assets "in parallel" which can introduce a bottleneck when downloading, for example, large images.


### Tools to help you measure and improve performance are:
* [YSlow](http://yslow.org/)
* [jsperf](http://jsperf.com/)
* [boomerang](http://yahoo.github.io/boomerang/doc/) - End user oriented web performance testing and beaconing
* In browser waterfall UI - found in Chrome (best), also Safari, Firebug, IE and Opera
* [Performance Tools](http://www.stevesouders.com/blog/2012/10/09/webperfdays-performance-tools/) - stevesouders.com
* [Google PageSpeed Insights](http://developers.google.com/speed/pagespeed/insights/)

## Browser Support

We accept that the nature of the web is such that not all web pages can be produced uniformly and consistently across all browsers. The following browser support guidelines seek to address the trade-off between experience, reach and resources.

### Primary Browsers - supported
All content must be readable and all functionality must work.

| Browser name | Version | Platform  |
| ------ | ------ | -----: |
|  Internet Explorer  |  8,9,10 |   Windows  |
|  Firefox  |  Latest version  |   Mac/Windows  |
|  Chrome  |  Latest version |   Mac/Windows  |
|  Safari  |  5.1+  |   Mac  |

### Secondary Browsers - partially supported
All content must be readable must be readable and core functionality must work.

| Browser name | Version | Platform  |
| ------ | ------ | -----: |
|  Internet Explorer  |  7  |   Windows  |
|  Opera  |  10+  |   Mac/Windows  |


### Mobile browsers - supported as secondary browsers
Follow secondary browser standards of performance and user experience.

| Browser name | Version | Platform  |
| ------ | ------ | -----: |
|  Safari for iOS  |  6+  |   iOS iPad, iPhone  |
|  Chrome for iOS  |  Latest version  |   iOS iPad, iPhone  |
|  Android Webkit  |  2.x and 4.x  |   Android  |

**Latest version** - Where latest version is listed, it means the latest major stable version plus one major version back, as these browsers regularly self-update.
