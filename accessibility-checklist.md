Accessibility Checklist
=======================

*Initial thoughts on an Accessibility checklist for the Money Advice Service.*

This checklist is aimed at helping the Money Advice Service build accessible websites and applications. It is based on the WCAG 2.0 standard and seeks to ensure that all websites and applications are:

 - perceivable
 - operable
 - understandable
 - robust
 
### Perceivable
All non-text content on a web page (images, inputs fields, audio and video content) must be available to the user in a way that is visible to them, in their way. 

It cannot be invisible to all their senses. 

For example:

If a user is deaf then there must be a text alternative, i.e. the website must be "readable". If a user is blind then the website should be structured to allow a screen reader easy access and translation of text into audio.

### Operable
Page features, links, navigation and controls must be operable by all users. Specifically, everything must be keyboard accessible and include activation and deactivation so it does not "trap" the user.

Reducing animations and flashes to avoid inducing seizures in users. 

Ensure the website is though, navigable.

### Understandable
To be properly accessible the page and what it contains must be understandable, or in other words, readable. 

Ensure the content has an attached language declaration to aid a screen reader. Write the content with readability in mind and avoid jargon, or verbose phraseology that would confuse. Write in plain English.

Additionally, ensure that navigation and key features work as a user would expect and that errors need to be displayed clearly with instructions on how to resolve a problem.

### Robust
This means that users must be able to access the content as technologies advance (as technologies and user agents evolve, the content should remain accessible). A website or application should not rely on a non-standards based or proprietary technology or assistive device.

## Checklist

### HTML and Formatting
Using semantic and well structured HTML5 tags should take precedence over employing ARIA roles.

- Validate HTML5 as semantic.
- Check that the headings are ordered correctly.
- Check that all "read more" links have a visually hidden extended description.
- Check that alt text is included in image tags that require a description and omitted on images with an accompanying caption.

### WAI ARIA
By way of a summary, WAI-ARIA (Web Accessibility Initiative - Accessible Rich Internet Applications) is a draft technical specification published by the World Wide Web Consortium that specifies how to increase the accessibility of dynamic content and user interface components.


- Add WAI-ARIA attributes (role="search") to the HTML.
- Check that WAI-ARIA attribute is not replicating an available HTML5 tag.
- Add WAI-ARIA states (aria-selected="true | false | undefined") to the HTML.
- Add WAI-ARIA properties, such as live regions (aria-live=”polite | assertive | off”), to the HTML.
- Check that when you tab through the page the focus state is clearly visible.


### Visual Accessibility

### Auditory Accessibility
- Check that the HTML include the correct language tag.
- Ensure that any embedded video content has an accompanying transcript, subtitles or sign language.

### Physical Accessibility


### Cognitive Accessibility
- Ensure that all content is written mindfully in plain English (avoiding jargon).
- Check that any CSS animation will not induce a seizure in a user (an is appropriate to the feature).

### Auditory Accessibility


### Accessibile Info-graphics

- use the "longdesc" attribute to connect an image to a long description(targetted for depreciation in HTML5).

@TODO - needs to be a better way to code an accessible infographic than a depreciated attribute or lesser used ARIA labelledby or 

- add a description of the info-graphic on the page and set it to visually hidden