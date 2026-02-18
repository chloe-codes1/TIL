# HTML Sections and Outlines

<br>

### 1. Understanding Structural Markup

- Structural markup defines the structure of a document
- Presentational markup defines the appearance of a document
- Mixing structural and presentational markup
  - Old HTML used a mixture of structural and presentational markup
  - Current web standards have removed presentational markup from HTML
  - HTML is used for document structure, CSS is used for document presentation
- Problems with using presentational markup
  - The use of presentational elements hinders accessibility
  - Higher maintenance costs
  - Document size bloat
- **Block-level elements and inline-level elements**
  - `Block-level elements`: Paragraph elements that cause line breaks
  - `Inline-level elements`: Part-of-line elements that do not cause line breaks

<br><br>

### 2. Section Elements in HTML5

<br>

- #### HTML Navigational Element (`<nav>`)

  - defines a section that contains navigation links that appear often on a site.
  - You can have primary and secondary menus, but you never nest, or put a `<nav>`element inside a `<nav>` element.

  <br>

- #### HTML Article Element (`<article>`)

  - defines a piece of self-contained content.
  - It does not refer to the main content alone and can be used for comments and widgets.

  <br>

- #### HTML Section Element (`<section>`)

  - defines a section of a document to indicate a related grouping of semantic meaning.
  - Utilize the section element providing extra context from the parent element makes sense.

  <br>

- #### HTML Aside Element (`<aside>`)

  - defines a section that, though related to the main element, doesn't belong to the main flow, like an explanation box or an advertisement.
  - It has its own outline, but doesn't belong to the main one.

<br><br>

### Other Semantic HTML elements used in Sectioning

<br>

- #### HTML Body Element (`<body>`)

  - defines all the content of a document.
  - It contains all the content and HTML tags.

  <br>

- #### HTML Header Element (`<header>`)

  - defines a page which typically contains the logo, title, and navigation.
  - The header can also be used in other semantic elements such as `<article>`or `<section>` — or section header, containing perhaps the section's heading, author name, etc. `<article>`, `<section>`, `<aside>`, and `<nav>` can have their own `<header>`.
  - Despite its name, it is not necessarily positioned at the beginning of the page or section.

  <br>

- #### HTML Footer Element (`<footer>`)

  - defines a page footer which typically contains the copyright, legal notices and sometimes some links — or section footer, containing perhaps the section's publication date, license information, etc. `<article>`, `<section>`, `<aside>`, and `<nav>` can have their own `<footer>`.
  - Despite its name, it is not necessarily positioned at the end of the page or section.

<br>

<br>

### 3. HTML elements reference from MDN

<br>

### Main root

| Element                                                      | Description                                                  |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [`<html>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/html) | The **HTML `<html>` element** represents the root (top-level element) of an HTML document, so it is also referred to as the *root element*. All other elements must be descendants of this element. |

<br>

### Document metadata

Metadata contains information about the page. This includes information about styles, scripts and data to help software ([search engines](https://developer.mozilla.org/en-US/docs/Glossary/search_engine), [browsers](https://developer.mozilla.org/en-US/docs/Glossary/Browser), etc.) use and render the page. Metadata for styles and scripts may be defined in the page or link to another file that has the information.

| Element   | Description                                                  |
| :-------- | :----------------------------------------------------------- |
| `<base>`  | The **HTML `<base>` element** specifies the base URL to use for all relative URLs in a document. |
| `<head>`  | The **HTML `<head>` element** contains machine-readable information ([metadata](https://developer.mozilla.org/en-US/docs/Glossary/metadata)) about the document, like its [title](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/title), [scripts](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/script), and [style sheets](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/style). |
| `<link>`  | The **HTML External Resource Link element (`<link>`)** specifies relationships between the current document and an external resource. This element is most commonly used to link to [stylesheets](https://developer.mozilla.org/en-US/docs/Glossary/CSS), but is also used to establish site icons (both "favicon" style icons and icons for the home screen and apps on mobile devices) among other things. |
| `<meta>`  | The **HTML `<meta>` element** represents [metadata](https://developer.mozilla.org/en-US/docs/Glossary/Metadata) that cannot be represented by other HTML meta-related elements, like `<base>`, `<link>`, `<script>`, `<style>`, or `<title>` |
| `<style>` | The **HTML `<style>` element** contains style information for a document, or part of a document. |
| `<title>` | The **HTML Title element** (**`<title>`**) defines the document's title that is shown in a [browser](https://developer.mozilla.org/en-US/docs/Glossary/Browser)'s title bar or a page's tab. |

<br>

```html
<p> : Paragraph, use a more appropriate element when one exists instead of the p element
<blockquote> : A quoted section from another source
If there is a URL for the quoted source, indicate it with the cite attribute
<pre> : Represents a block of preformatted text
<hr> : Separation of topics at the paragraph level, used standalone without a closing element

Lists
- Ordered list: A list where changing the order changes the meaning
Defined by the <ol> element
<li> element defines list items

- Unordered list: List items start with bullet points
Defined by the <ul> element
<li> element defines list items

- Definition list: Used for dictionary-style definitions
<dl> : Definition list element
<dt> : Definition list title element
<dd> : Definition list data (value) element

<figure> : Displays photos, illustrations, videos, etc.
<figcaption> : Caption for figure element content, used inside the <figure> element
<div> : Used to separate content for styling or scripting purposes

Global attributes
- Global attributes that can be used as attributes in most elements
- The id attribute is a unique identifier within the HTML code
- The class attribute can have the same value multiple times within HTML code
- The class attribute is used in CSS or JavaScript to apply the same style or behavior to multiple elements within HTML code
- The title attribute represents advisory information about an element and is displayed as a tooltip in web browsers

Text-related elements: Inline-level elements
<a> Hyperlink

The href attribute specifies the link path
The target attribute determines which window the link opens in
_self : The link opens in the current web browser window
_parent : If there is a parent window of the current web browser window, the link opens there
_top : The link opens in the topmost web browser window
_blank : Creates a new web browser window and opens the link
- Ii, <em> : Emphasizes content
<strong> : Indicates that content is important

<q> : The q element is an inline element representing a quotation
<cite> : Used when mentioning or referencing the title of works such as books, essays, poems, scripts, papers, paintings, plays, movies, etc.
<abbr> : The abbr element represents an abbreviation or acronym

Uses the title attribute to show the full form of the acronym
<i> : Used for indicating other languages or idioms, quotations, taxonomic classifications, etc. that would be italicized in English
<b> : The b element is used to draw attention without adding meaningful importance
<sup>, <sub>
- The sup element represents superscript.
- The sub element represents subscript.
<span> : Serves to separate content at the inline level for applying styles or use in scripts
<br> : Used without a closing element, represents a simple line break rather than a paragraph break
Should not be used as a substitute for <p> elements

<img>
- The img element represents an image.
- The img element is used standalone without a closing element.
- The src attribute specifies the image path.
- The alt attribute is alternative text for the image. Must be used.
```

<br>

<br>

### 4. HTML Table

<br>

#### Precautions When Using HTML Tables

- Tables have poor accessibility, so if there is a better way to present something, do not use tables.
- Tables should not be used for page layout.
- Tables should also be avoided when presenting input forms whenever possible.

<br>

#### Creating HTML Tables

- table
- element: Represents an HTML table.
- tr element: Represents a row of the table.
- th element: Represents a table header cell. Used for title cells.
- td element: Represents a cell of the table.

<br>

#### Cell Merging

- Horizontal cell merging: Use the colspan attribute
- Vertical cell merging: Use the rowspan attribute

<br>

#### Table Structure Elements

> Structuring tables to enhance accessibility and data analysis

- thead element
  - A collection of rows consisting of table headings
  - No more than two **thead** elements should be defined in a table.
- tbody element
  - The body of the table where the content goes
  - Multiple tbody elements can be set
- tfoot element
  - A collection of rows consisting of the table footer
  - Appears at the end of the table regardless of its position.
  - No more than two tfoot elements should be defined in a table
- col element: Structurally represents a single column.
  Set after the caption element and before thead or tbody.
  Use as many col elements as there are columns in the table.
- colgroup element: A group of col elements
  Can be separated into multiple colgroups according to structure.
- scope attribute
  - Specifies the direction of the header cell's influence
  - If the scope value is row or col
  - The header cell is a title for the row or column
  - If the scope value is rowgroup or colgroup, the header cell is a title for a group of rows (multiple rows below) or a group of columns (multiple columns to the right)
- caption element
  - Represents the caption (title) of the table.
  - Must be set first as the first child element of the table element.
  - If the table is the only child element of a figure element, the caption should be displayed with a figcaption element instead of caption.

<br>

<br>

### 5. HTML Form

<br>

#### form element

> Represents an HTML input form

- action attribute: The server file URL where the form is submitted
- method attribute: The method by which the form is transmitted, with values of get or post.

<br>

#### input element

> An input data field with various types
