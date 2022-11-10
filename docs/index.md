---
layout: demo
---
<!-- markdownlint-disable-file first-line-h1 -->
<!-- markdownlint-disable-file blanks-around-fences -->

> {{ site.description }}
{: style="font-size: 1.5em" }

<!-- markdownlint-disable-next-line blanks-around-headers -->
## Table of Contents
{: .no_toc}

* toc
{:toc}

## Showcase

The following table is written entirely in (extended) Markdown with no HTML!

{% capture table %}
```table
| Check out this _fancy_ :sparkles: table!                                                                                 \\|
|-----------------------|----------------------------------------------------------------------------------------|-----------|
| One                   | Banana 1                                                                               | Orange 1  |
| Three                 \                                                                                        | Orange 3  |
| Four                  | Banana 4                                                                               | ^^        |
| ^^                    | Banana 5                                                                               | Orange 5  |
| Six                   | Banana 6                                                                               | Orange 6  |
| Seven                 \                                                                                        | Orange 7  |
| ^^ hi                 \                                                                                        | Orange 8  |
| Nine                  | Hello,                                                                                 | Orange 9  |
| Ten                   | ^^                                                                                     | Orange 10 |
| Eleven                | ^^ _World?_                                                                            | Orange 11 |
| Twelve                | Banana 12                                                                              | Orange 12 |
| Thirteen              | Some really long text that ought to span multiple lines, and oh, it also has **markdown** styles! \|
```alignment
c
LLL
L r
LL
LL
LLc
c L
L
LLL
L L
L L
lll
lR
```

{% endcapture %}

{{ table }}

{% capture newline %}
{% endcapture %}
Aaand... the markdown code below:

{% assign as_code = '' | split: '' %}
{% assign lines = table | split: newline %}
{% for line in lines %}{% assign padded = line | prepend: '    ' %}{% assign as_code = as_code | push: padded %}{% endfor %}
{{ as_code | join: newline }}

---

## Features

### 1. Headerless Tables

Simply chop off the header line:

Before:

```text
| This      | table | looks | quite | ugly    |
|-----------|-------|-------|-------|---------|
| Sometimes | you   | don't | want  | headers |
```

After:

```text
|-----------|-------|-------|-------|---------|
| Sometimes | you   | don't | want  | headers |
```

Result:

```table
|-----------|-------|-------|-------|---------|
| Sometimes | you   | don't | want  | headers |
```

### 2. Column Span and Row Span

#### Column Span

* Works in table headers and table body
* Simply "break" the column separator to span multiple columns

  ```text
  | OMG, I span 3 columns! \      \      |
  |------------------------|------|------|
  | That's...              | very | nice |
  ```

* Breaks don't have to be aligned to anything

  ```text
  | OMG, I span 3 columns! \\|
  |------------|------|------|
  | That's...  | very | nice |
  ```

* Non-blank cells will be joined together with a space

  ```text
  | OMG, I    \ span \ 3 columns! |
  |-----------|------|------------|
  | That's... | very | nice       |
  ```

The above 3 examples give the same result:

```table
| OMG, I span 3 columns! \\|
|------------|------|------|
| That's...  | very | nice |
```

#### Row Span

* Only works for the table body

* Simply prepend table cells with `^^`

  ```text
  |------------------------|---------|
  | Look, I span two rows! | Looks   |
  | ^^                     | pretty! |
  ```

  Result:

  ```table
  |------------------------|---------|
  | Look, I span two rows! | Looks   |
  | ^^                     | pretty! |
  ```

* Non-blank cells will be joined together with a line break

  ```text
  |---------------|---------|
  | Look, I span  | Looks   |
  | ^^ two rows!  | pretty! |
  ```

  Result:

  ```table
  |---------------|---------|
  | Look, I span  | Looks   |
  | ^^ two rows!  | pretty! |
  ```

### 3. Individual Cell Alignment

* Simply add a section under `` ```alignment `` before closing the code block with `` ``` ``. Specify left, right, or center-aligned using `L`, `R`, or `C` respectively

      ```table
      | _For padding_ | _For padding_ | _For padding_ |
      |---------------|---------------|---------------|
      | left          |    center     |         right |
      |    center     |         right | left          |
      |         right | left          |    center     |
      ```alignment
      CCC
      LCR
      CRL
      RLC
      ```

* Whitespace and capitalization do not matter

      ```table
      | _For padding_ | _For padding_ | _For padding_ |
      |---------------|---------------|---------------|
      | left          |    center     |         right |
      |    center     |         right | left          |
      |         right | left          |    center     |
      ```alignment
      cCClRrCrlrLc
      ```

The above 2 examples give the same result:

```table
| _For padding_ | _For padding_ | _For padding_ |
|---------------|---------------|---------------|
| left          |    center     |         right |
|    center     |         right | left          |
|         right | left          |    center     |
```alignment
cCClRrCrlrLc
```

## Additional styling

Keeping to the spirit of Markdown, in order to not make the syntax too complicated, style-related syntax is limited to table cell alignment only (but you are welcome to request for features in the [issue tracker](https://github.com/RichDom2185/jekyll-fancy-tables/issues)).

Having said that, the file also provides a `data-nth-cell` HTML attribute for each table cell (1-indexed), so you can style each individual cell using CSS/JS that way.
