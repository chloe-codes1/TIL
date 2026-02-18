# Python Coding Convention

> Got curious about PEP8, so I looked it up and decided to organize it
>
> References: [Book] Effective Python

<br>

<br>

## What is PEP8?

> Python Enhancement Proposal 8 (PEP8)

- A style guide that tells you how to organize Python code
  - An agreement to write code in a specific format
    - Using a consistent style makes **maintenance** easier and improves **readability**!
- Detailed information is available at [python.org](https://www.python.org/dev/peps/pep-0008/)!

<br>

<br>

## Some Rules from PEP8 That Must Be Followed

<br>

### 1. Whitespace

> In Python, whitespace is syntactically significant
>
> Python programmers are particularly sensitive to the impact of whitespace because of code clarity!

- Indent with **spaces**, not tabs
- Use **4 spaces** for each level of syntactically significant indentation
- Each line should be **79 characters** or less
- When an expression continues to the next line, use **4 additional spaces** beyond the normal indentation level
- `Functions` and `classes` in a file should be separated by **two blank lines**

- Methods within a Class should be separated by a single blank line
- Do **not use spaces** around `list indices`, `function calls`, or `keyword argument assignments`

<br>

### 2. Naming Conventions

> PEP 8 suggests unique naming conventions for different parts of the language
>
> This makes it easy to distinguish the type corresponding to each name when reading code!

- `Functions`, `variables`, and `attributes` follow the **lowercase_underscore** format
- `Protected` instance attributes follow the **_leading_underscore** format
- `Private` instance attributes follow the **__double_leading_underscore** format
- Classes and Exceptions follow the **CapitalizedWord** format
- Module-level constants follow the **ALL_CAPS** format
- The first parameter of a `Class instance` method (which references the object) should be named **self**
- The first parameter of a `Class method` (which references the class) should be named **cls**

<br>

### 3. Expressions and Statements

> The Zen of Python states: "There should be one-- and preferably only one --obvious way to do it"
>
> PEP 8 codifies this style as the standard for expressions and statements

- Use inline negation (`if a is not b`) instead of negation of positive expressions (`if not a is b`)
- Don't check for empty values (`[]` or `''`) by checking the length (`if len(somelist) == 0`)
  - Use `if not somelist` and assume that empty values are implicitly **False**
  - The same approach applies to non-empty values!
    - Non-empty values will make `if somelist` implicitly **True**
- Don't write single-line `if statements`, `for and while loops`, or `except compound statements`
  - Write these statements on multiple lines for clarity!
- Always place import statements at the top of the file
- When **importing modules**, always use the module's absolute name; do not use relative path names based on the current module's path
  - ex) Use `from bar import foo` instead of just `import foo`!
- If you must use relative imports, use explicit syntax: `from . import foo`
- Imports should be organized in the order of `standard library modules`, `third-party modules`, and `your own modules`
  - Within each subsection, import in alphabetical order



<br>

<br>

## How to Check If You're Following PEP8

> Install and use pylint and PEP8!

<br>

### 1. pylint

```bash
$ pip install pylint
```

<br>

### 2. PEP8

```bash
$ pip install pep8
```


