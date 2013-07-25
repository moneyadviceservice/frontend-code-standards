# Front-end Code Standards &amp; Best Practice


This document contains guidelines for web pages and applications built by the Money Advice Service development team. It is inspired/based on [http://isobar-idev.github.io/code-standards/](http://isobar-idev.github.io/code-standards/) but with amends and additions as we see fit. It is a living document that will is continually updated and improved.

This document's primary motivation is two- fold: 1) code consistency and 2) best practices. By maintaining consistency in coding styles and conventions, we can ease the burden of legacy code maintenance, and mitigate risk of breakage in the future. By adhering to best practices, we ensure optimized page loading, performance and maintainable code.

## General Guidelines
### Pillars of Front-end Development
* Separation of presentation, content, and behavior.
* Markup should be well-formed, semantically correct and generally valid.
* Javascript should progressively enhance the experience.

Where possible follow the principles of progressive enhancement. Start by making sure your content is in the correct/logical order.  Then select the most appropriate html elements and wai-aria attributes to mark the content up.  Then apply css styles taking care to not introduce accessibility barriers. Finally apply javascript and make sure that you do not introduce any keyboard traps.

## Markup
### HTML5
We use the HTML5 Doctype and HTML5 features when appropriate.

We test our markup against the W3C validator, to ensure that the markup is well formed. 100% valid code is not a goal, but validation certainly helps to write more maintainable sites as well as debugging code.

### Doctype
We use the HTML5 doctype
	
	<!DOCTYPE html>

### Character Encoding
All markup should be delivered as UTF-8, as its the most friendly for internationalization.
We specify it in the head of the document

	<meta http-equiv="content-type" content="text/html; charset=UTF-8">

### General Markup Guidelines
* Use html5shiv to ensure html5 element work in IE 6,7,8,9
* Use semantic markup.  Start by making sure your content is in the correct/logical order in your html document.  Then select the most appropriate html elements and wai-aria attributes to mark the content up.
* Use a hierarchical heading structure to help screen reader users navigate a page
* For links use a link `<a>`
* For buttons use a `<button>`
* User WAI-ARIA landmark roles to help screen reader users navigate a page
* Use WAI-ARIA form attributes to help screen reader users to use forms

## CSS
### General Coding Principles
* Do not make your styles too specific
* Do not use presentational class names such as 'green'
* Use Sass to make you CSS more maintainable
* Any style you apply to :hover also apply to :focus

### Web Typography
content coming soon

## JavaScript
### JavaScript Libraries
Our library of choice is [jQuery](http://jquery.com/)

We should be using the latest version of jQuery 1.x which is currently 1.10.2

It looks like we are currently using a few (older) versions on the website.  We should improve this so they are all using the same CDN'd version, so user have a higher chance of it already being cached in there browser.

### General Coding Principles
content coming soon

## Accessibility
All web pages and interfaces must comply to [Web Content Accessibility Guidelines](http://www.w3.org/TR/WCAG/) (WCAG) 2.0 AA standard both to the letter and in spirit.

The four characteristics of web accessibility are:

* Percievable
* Operable
* Understandable
* Robust

14 common accessibility blunders are:

* Content not being in the most logical order in the document
* Not using alternative text that conveys the meaning of an image appropriately
* Not having text alternative for multiplemedia content -i.e captions and transcipts
* Using jargon and complicated language instead of simple language.
* Not using headings correctly.  The single h1 one of the page should be the page title. Other headings should be hierachical and allow a screen reader user to get an overview of the content on a page
* Failing to use the most appropriate semantic elements to mark up content
* Using too many lists and headings  which add aural clutter to screen reader users
* Failing to mark up forms correctly
* Communicating information by colour alone  which will not be percieved by colour bind users.
* Not having a visual state that shows when a element has focus
* Only communicating states and actions visually - e.g selected, open, close. This also needs to be in the markup.
* Failing to allow a keyboard user to access all content and functionally on a page - usually by using incorrect html elements, e.g spans and divs instead of links or buttons or by introducing keyboard traps with javascript
* Failing to inform a screen reader user when content dynamically updates on a page
* Failing to set focus when dynamic content is loaded such as a modal box and not enabling a keyboard user to close such content.
 
We should be following GOV.UKs lead who have done extensive accessibility testing: [https://www.gov.uk/service-manual/user-centered-design/accessibility](https://www.gov.uk/service-manual/user-centered-design/accessibility)

### Resources
* [WebAim](http://webaim.org/) - Information, training, resources, guidelines and standards for Web accessibility and disability access to the Web.
* [Draft BBC Mobile Accessibility Guidleines](http://www.bbc.co.uk/guidelines/futuremedia/accessibility/mobile_access.shtml)

## Performance
Reduce http requests by using sprites or data uris and concatenate css and javascript files

Where possible move your javascript files to the bottom of the page so content can render as quickly as possible.

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


Note: This needs updating as I believe our content should usable in older browsers too (even if it doesn't look pretty!) - we should be using Progressive Enhancement rather than gracefull degradation.  We should be following the same approach as GOV.UK, see: [https://www.gov.uk/service-manual/user-centered-design/browsers-and-devices](https://www.gov.uk/service-manual/user-centered-design/browsers-and-devices)

IE10 should also be a primary browser. We need to start thinking about mobile devices too.


## Search Engine Optimisation
An essential part of good web design and development is SEO. Well-structured code is the key to ensuring that a web page not only gets properly indexed by search engines, but made accessible to those with limited web capabilities as well.

