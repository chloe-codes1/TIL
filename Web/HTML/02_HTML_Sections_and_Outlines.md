# HTML Sections and Outlines

<br>

### 1. 구조적 마크업의 이해

- 구조적 마크업은 문서의 구조를 정의
- 표현적 마크업은 문서의 외형을 정의
- 구조적 마크업과 표현적 마크업의 혼용
  - 오래된 HTML은 구조적 마크업과 표현적 마크업을 혼용해 사용
  - 현재 웹 표준에서는 표현적 마크업을 HTML에서 퇴출
  - 문서의 구조는 HTML을 사용, 문서의 표현은 CSS를 사용
- 표현적 마크업 사용의 문제점
  - 표현적 요소의 사용은 접근성을 저해
  - 더 높은 유지비용 발생
  - 문서 크기 비대화
- **블록 레벨 요소와 인라인 레벨 요소**
  - `블록 레벨 요소`: 줄 바꿈이 일어나는 단락 요소
  - `인라인 레벨 요소`: 줄 바꿈이 일어나지 않는 행의 일부 요소

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
  - The header can also be used in other semantic elements such as `<article> `or `<section>` — or section header, containing perhaps the section's heading, author name, etc. `<article>`, `<section>`, `<aside>`, and `<nav>` can have their own `<header>`. 
  - Despite its name, it is not necessarily positioned at the beginning of the page or section.

  <br>

- #### HTML Footer Element (`<footer>`) 

  - defines a page footer which typically contains the copyright, legal notices and sometimes some links — or section footer, containing perhaps the section's publication date, license information, etc. `<article>`, `<section>`, `<aside>`, and `<nav>` can have their own `<footer>`. 
  - Despite its name, it is not necessarily positioned at the end of the page or section.

<br>

<br>

## 3. HTML elements reference from MDN

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

## 



