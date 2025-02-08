# HTML and CSS coding guidelines
This document defines formatting and style rules for HTML and CSS. It aims at improving collaboration, code quality, and enabling supporting infrastructure. In this guidelines we are following the google team rules, not entirely but a lot of it. 

## 1 General
### 1.1 Protocol
Use HTTPS for embedded resources where possible.

Always use HTTPS (https:) for images and other media files, style sheets, and scripts, unless the respective files are not available over HTTPS.
```html
<!-- Not recommended: omits the protocol -->
<script src="//ajax.googleapis.com/ajax/libs/jquery/3.4.0/jquery.min.js"></script>

<!-- Not recommended: uses HTTP -->
<script src="http://ajax.googleapis.com/ajax/libs/jquery/3.4.0/jquery.min.js"></script>
```

```html
<!-- Recommended -->
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.0/jquery.min.js"></script>
```

### 1.2 Indentation
Indent by 4 spaces at a time. It is much easier to quickly scan for what braces match and where blocks end and begin.

Don’t use tabs or mix tabs and spaces for indentation.

### 1.3 Capitalization
Use only lowercase.

All code has to be lowercase: This applies to HTML element names, attributes, attribute values, CSS selectors, properties, and property values (with the exception of strings).
```html
<!-- Not recommended -->
<A HREF="/">Home</A>

<!-- Recommended -->
<img src="google.png" alt="Google">
```

```css
/* Not recommended */
color: #E5E5E5;

/* Recommended */
color: #e5e5e5;
```

### 1.4 Comments
Explain code as needed, where possible.

Use comments to explain code: What does it cover, what purpose does it serve, why is respective solution used or preferred?

(This item is optional as it is not deemed a realistic expectation to always demand fully documented code. Mileage may vary heavily for HTML and CSS code and depends on the project’s complexity.)

### 1.5 Quotation Marks
When quoting attributes values, use double quotation marks.

Use double ("") rather than single quotation marks ('') around attribute values.
```
<!-- Not recommended -->
<a class='maia-button maia-button-secondary'>Sign in</a>

<!-- Recommended -->
<a class="maia-button maia-button-secondary">Sign in</a>
```

### 1.6 ID and Class Naming
Use meaningful or generic ID and class names.

Instead of presentational or cryptic names, always use ID and class names that reflect the purpose of the element in question, or that are otherwise generic.

Names that are specific and reflect the purpose of the element should be preferred as these are most understandable and the least likely to change.

Generic names are simply a fallback for elements that have no particular or no meaning different from their siblings. They are typically needed as “helpers.”

Using functional or generic names reduces the probability of unnecessary document or template changes.

```css
/* Not recommended: meaningless */
#yee-1901 {}

/* Not recommended: presentational */
.button-green {}
.clear {}
```

```css
/* Recommended: specific */
#gallery {}
#login {}
.video {}

/* Recommended: generic */
.aux {}
.alt {}
```

### 1.7 ID and Class Name Style
Use ID and class names that are as short as possible but as long as necessary.

Try to convey what an ID or class is about while being as brief as possible.

Using ID and class names this way contributes to acceptable levels of understandability and code efficiency.

```css
/* Not recommended */
#navigation {}
.atr {}

/* Recommended */
#nav {}
.author {}
```

## 2 HTML
### 2.1 HTML Validity
Use valid HTML where possible.

Use valid HTML code unless that is not possible due to otherwise unattainable performance goals regarding file size.

Use tools such as the W3C HTML validator to test.

Using valid HTML is a measurable baseline quality attribute that contributes to learning about technical requirements and constraints, and that ensures proper HTML usage.

```html
<!-- Not Recommended -->
<ul id="list_of_links">
    <a>Link1</a>
    <a>Link2</a>
    <a>Link3</a>
</ul>

<!-- Recommended -->
<ul id="list_of_links">
    <li><a>Link1</a></li>
    <li><a>Link2</a></li>
    <li><a>Link3</a></li>
</ul>
```

### 2.2 Semantics
Use HTML according to its purpose.

Use elements (sometimes incorrectly called “tags”) for what they have been created for. For example, use heading elements for headings, p elements for paragraphs, a elements for anchors, etc.

Using HTML according to its purpose is important for accessibility, reuse, and code efficiency reasons.
```html
<!-- Not recommended -->
<div onclick="goToHomePage();">Homepage</div>

<!-- Recommended -->
<a href="homepage/">Homepage</a>
```

### 2.3 Multimedia Fallback
Provide alternative contents for multimedia.

For multimedia, such as images, videos, animated objects via canvas, make sure to offer alternative access. For images that means use of meaningful alternative text (alt) and for video and audio transcripts and captions, if available.

Providing alternative contents is important for accessibility reasons: A blind user has few cues to tell what an image is about without @alt, and other users may have no way of understanding what video or audio contents are about either.

(For images whose alt attributes would introduce redundancy, and for images whose purpose is purely decorative which you cannot immediately use CSS for, use no alternative text, as in alt="".)
```html
<!-- Not recommended -->
<img src="spreadsheet.png">

<!-- Recommended -->
<img src="spreadsheet.png" alt="Spreadsheet screenshot.">
```

### 2.4 Entity References
Do not use entity references.

There is no need to use entity references like `&mdash;`, `&rdquo;`, or `&#x263a;`, assuming the same encoding (UTF-8) is used for files and editors as well as among teams.

The only exceptions apply to characters with special meaning in HTML (like < and &) as well as control or “invisible” characters (like no-break spaces).


```html
<!-- Not recommended -->
The currency symbol for the Euro is &ldquo;&eur;&rdquo;.

<!-- Recommended -->
The currency symbol for the Euro is “€”.
```

### 2.5 `type` Attributes
Omit type attributes for style sheets and scripts.

Do not use type attributes for style sheets (unless not using CSS) and scripts (unless not using JavaScript).

Specifying type attributes in these contexts is not necessary as HTML5 implies text/css and text/javascript as defaults. This can be safely done even for older browsers.


```html
<!-- Not recommended -->
<link rel="stylesheet" href="https://www.google.com/css/maia.css"
    type="text/css">
<!-- Recommended -->
<link rel="stylesheet" href="https://www.google.com/css/maia.css">

<!-- Not recommended -->
<script src="https://www.google.com/js/gweb/analytics/autotrack.js"
    type="text/javascript"></script>
<!-- Recommended -->
<script src="https://www.google.com/js/gweb/analytics/autotrack.js"></script>
```

### 2.6 General Formatting
Use a new line for every block, list, or table element, and indent every such child element.

Independent of the styling of an element (as CSS allows elements to assume a different role per `display` property), put every block, list, or table element on a new line.

Also, indent them if they are child elements of a block, list, or table element.

(If you run into issues around whitespace between list items it’s acceptable to put all `li` elements in one line. A linter is encouraged to throw a warning instead of an error.)


### 2.7 HTML Line-Wrapping
Break long lines.

While there is no column limit recommendation for HTML, you may consider wrapping long lines if it significantly improves readability.

When line-wrapping, each continuation line should be indented at least 4 additional spaces from the original line.

```HTML
<!-- Not recommended -->
<md-progress-circular md-mode="indeterminate" class="md-accent"
    ng-show="ctrl.loading" md-diameter="35">
</md-progress-circular>

<!-- Recommended -->
<md-progress-circular
    md-mode="indeterminate"
    class="md-accent"
    ng-show="ctrl.loading"
    md-diameter="35">
</md-progress-circular>
```

## 3 CSS

### 3.1 CSS Validity
Use valid CSS where possible.

Unless dealing with CSS validator bugs or requiring proprietary syntax, use valid CSS code.

Use tools such as the [W3C CSS validator](https://jigsaw.w3.org/css-validator/) to test.

Using valid CSS is a measurable baseline quality attribute that allows to spot CSS code that may not have any effect and can be removed, and that ensures proper CSS usage.

### 3.2 Type Selectors
Avoid using tag names in selectors as this prevents re-use in other contexts.

```css
/* Cannot use this class on an <ol> or <div> element */
ul.dataset-item {}
Also ids should not be used in selectors as it makes it far too difficult to override later in the cascade.

/* Cannot override this button style without including an id */
.btn#download {}
```

### 3.3 Shorthand Properties
Use shorthand properties where possible.

CSS offers a variety of [shorthand](https://www.w3.org/TR/CSS21/about.html#shorthand) properties (like font) that should be used whenever possible, even in cases where only one value is explicitly set.

Using shorthand properties is useful for code efficiency and understandability.

```css
/* Not recommended */
border-top-style: none;
font-family: palatino, georgia, serif;
font-size: 100%;
line-height: 1.6;
padding-bottom: 2em;
padding-left: 1em;
padding-right: 1em;
padding-top: 0;

/* Recommended */
border-top: 0;
font: 100%/1.6 palatino, georgia, serif;
padding: 0 1em 2em;
```

### 3.4 Hexadecimal Notation
Use 3 character hexadecimal notation where possible.

For color values that permit it, 3 character hexadecimal notation is shorter and more succinct.

```css
/* Not recommended */
color: #eebbcc;

/* Recommended */
color: #ebc;
```

### 3.5 Declaration Order
Alphabetize declarations.

Put declarations in alphabetical order in order to achieve consistent code in a way that is easy to remember and maintain.

Ignore vendor-specific prefixes for sorting purposes. However, multiple vendor-specific prefixes for a certain CSS property should be kept sorted (e.g. -moz prefix comes before -webkit).

For VS code user there is a plugin that can automaticall arrange the order using certain commands. Check it [here](https://marketplace.visualstudio.com/items?itemName=ue.alphabetical-sorter).

```css
background: fuchsia;
border: 1px solid;
-moz-border-radius: 4px;
-webkit-border-radius: 4px;
border-radius: 4px;
color: black;
text-align: center;
text-indent: 2em;
```

### 3.6 Block Content Indentation
Indent all block content.

Indent all [block content](https://www.w3.org/TR/CSS21/syndata.html#block), that is rules within rules as well as declarations, so to reflect hierarchy and improve understanding.

### 3.7 Declaration Stops
Use a semicolon after every declaration.

End every declaration with a semicolon for consistency and extensibility reasons.
```css
/* Not recommended */
.test {
  display: block;
  height: 100px
}

/* Recommended */
.test {
  display: block;
  height: 100px;
}
```

### 3.8 Property Name Stops
Use a space after a property name’s colon.

Always use a single space between property and value (but no space between property and colon) for consistency reasons.
```css
/* Not recommended */
h3 {
  font-weight:bold;
}

/* Recommended */
h3 {
  font-weight: bold;
}
```

### 3.9 Declaration Block Separation
Use a space between the last selector and the declaration block.

Always use a single space between the last selector and the opening brace that begins the [declaration block](https://www.w3.org/TR/CSS21/syndata.html#rule-sets).

The opening brace should be on the same line as the last selector in a given rule.

### 3.10 Selector and Declaration Separation
Separate selectors and declarations by new lines.

Always start a new line for each selector and declaration.
```css
/* Not recommended */
a:focus, a:active {
  position: relative; top: 1px;
}

/* Recommended */
h1,
h2,
h3 {
  font-weight: normal;
  line-height: 1.2;
}
```

### 3.11 Section Comments
Group sections by a section comment (optional).

If possible, group style sheet sections together by using comments. Separate sections with new lines.

```css
/* Header */

#adw-header {}

/* Footer */

#adw-footer {}

/* Gallery */

.adw-gallery {}
```