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
<p> : 문단, p 요소 보다 더 적합한 요소가 있을 때에는 해당 요소를 사용함
<blockquote> : 다른 소스로부터 가져온 인용 섹션
인용된 소스의 URL 주소가 있다면 cite 속성으로 표시
<pre> : 형식화된 텍스트 블록을 표현
<hr> : 문단 레벨에서 주제의 분리, 마침 요소 없이 단독으로 사용

목록
- 순서가 있는 목록: 순서가 바뀌면 의미가 바뀌는 목록
<ol> 요소로 정의
<li> 요소가 목록 아이템을 정의

- 순서가 없는 목록: 목록 아이템이 말머리 기호로 시작
<ul> 요소로 정의
<li> 요소가 목록 아이템을 정의

- 정의 목록: 사전식 정의를 위해 사용
<dl> : 정의 목록 요소
<dt> :정의 목록 제목 요소
<dd> :정의 목록 데이터(값) 요소

<figure> :사진, 일러스트, 비디오 등을 표시
<figcaption> : figure요소 내용에 대한 캡션, <figure> 요소 내부에서 사용
<div> :스타일 또는 스크립트 목적으로 콘텐츠를 분리하기 위해 사용

전역 속성
- 대부분의 요소에서 속성으로 사용 가능한 전역 속성
- id 속성은 HTML 코드 내에 유일한 식별자
- class 속성은 HTML 코드 내에 같은 값을 다수 가질 수 있음
- class 속성은 css 나 자바스크립트에서 HTML 코드 내 여러 요소에 동일한 스타일 또는 작동을 적용
하기 위해 사용
- title 속성은 요소의 조언 정보를 나타내며 웹 브라우저에서 툴팁으로 표시

텍스트 관련 요소 : 인라인 레벨 요소
<a> 하이퍼링크

href 속성으로 링크 경로를 지정
target 속성은 어떤 윈도우에서 링크가 열릴지 결정
_self : 현재의 웹 브라우저 창에서 링크가 열림
_parent : 현재의 웹 브라우저 창의 부모 창이 있다면 그 부모 창에서 링크가 열림
_top : 최상위 웹 브라우저 창에서 링크가 열림
_blank : 새로운 웹 브라우저 창을 생성하고 링크가 열림
- Ii, <em> : 내용을 강조
<strong> : 내용이 중요함을 나타냄

<q> : q 요소는 인용을 나타내는 인라인 요소
<cite> : 책, 수필, 시, 대본, 논문, 그림, 연극, 영화 등과 같은 작품의 제목을 언급하거나 참조 했을
때 사용
<abbr> : abbr 요소는 약어 및 두문자어를 나타냄

title 속성을 이용하여 두문자의 원형을 나타냄
<i> : 다른 언어 표시나 영문에서 이텔릭체로 표현하는 숙어인용, 분류학 등에 사용
<b> :b요소는 의미 있는 중요성을 부가하지 않고 눈에 띄게 하기 위해 사용
<sup>, <sub>
- sup 요소는 위첨자를 나타낸다.
- sub 요소는 아래첨자를 나타낸다.
<span> :인라인 레벨에서 스타일을 적용하거나 스크립트에서 사용하고자 콘텐츠를 분리하는 역할
<br> : 마침 요소 없이 사용되며 문단 분리가 아닌 단순 줄바꿈을 표시
<p> 요소 대용으로 사용하면 안됨

<img>
- img 요소는 이미지를 의미.
- img 요소는 마침 요소가 없이 단독으로 사용.
- src 속성에 이미지의 경로를 지정.
- alt 속성은 이미지를 대체하기 위한 텍스트. 반드시 사용.
```

<br>

<br>

### 4. HTML 표 (Table)

<br>

#### HTML 표의 사용시 주의 점

- 표는 접근성이 떨어지므로 표 이외에 더 좋은 표현 방법이 있다면 표를 사용하지 않아야 한다.
- 표를 페이지 레이아웃에 사용하지 말아야 한다.
- 입력 서식을 나타낼 때도 되도록이면 표를 사용하지 말아야 한다.

<br>

#### HTML 표 작성

- table
- 요소: HTML 표를 의미한다.
- tr 요소: 테이블의 row를 나타낸다.
- th 요소: 테이블 헤더셀을 나타낸다. 제목 셀에 사용한다
- td 요소: 테이블의 셀(칸)을 의미한다.

<br>

#### 셀 병합

- 가로셀 병합: colsapn 속성 사용
- 세로셀 병합: rowspan 속성 사용

<br>

#### 표의 구조화 요소

> 접근성 강화와 데이터 분석을 위해 표를 구조화 한다

- thead 요소
  - 표의 제목으로 구성된 row의 집합
  - 표에 두 개 이상의 **thead**가 정의 되어서는 안된다.
- tbody 요소
  - 표의 몸 부분으로 표의 내용이 들어간다
  - 여러 개의 tbody설정 가능
- tfoot 요소
  - 표의 푸터로 구성된 row의 집합
  - 위치와 상관없이 표 마지막에 나타난다.
  - 표에 두 개 이상의 tfoot이 정의 되어서는 안된다
- col 요소: 구조적으로 하나의 column을 대표한다.
  caption 요소의 뒤에 thead나 tbody의 앞에 설정한다.
  표의 컬럼 갯수 만큼 col 요소를 사용한다.
- colgroup 요소: col 요소의 그룹
  구조에 따라 여러개의 colgroup으로 분리할 수 있다.
- scope 속성
  - 헤더셀의 영향력이 어느쪽으로 향하는지를 지정
  - scope의 값이 row 또는 col이면
  - 헤더셀은row 또는 column에 제목
  - scope의 값이 rowgroup또는 colgroup이면 헤더셀은 row의 그룹(아래에 있는 여러 줄) 또는 col의 그룹(우측에 있는 여러 컬럼들)의 제목
- caption 요소
  - 표의 캡션(제목)을 나타낸다.
  - table 요소의 첫 번째 자식 요소로 가장 먼저 설정되어야 한다.
  - table이 figure 요소의 유일한 자식요소라면 caption 대신 figcaption요소로 캡션을 표시해야 한다.

<br>

<br>

### 5. HTML 시식 (Form)

<br>

#### form 요소

> HTML 입력 서식을 의미한다

- action 속성: 서식이 전송되는 서버 파일 URL
- metho 속성: 폼이 전송되는 방식, get 또는 post 값을 가진다.

<br>

#### input 요소

> 다양한 타입을 가지는 입력 데이터 필드
