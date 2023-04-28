---
layout: demo
---
<!-- markdownlint-disable-file first-line-h1 -->
<!-- markdownlint-disable-file blanks-around-fences -->

> {{ site.description }}
{: style="font-size: 1.5em" }

For the full guide (usages, etc.), view the project on [GitHub]({{ site.github.repository_url }}).

<!-- markdownlint-disable-next-line blanks-around-headers -->
## Table of Contents
{: .no_toc}

* toc
{:toc}

## Showcase

The following table is written entirely in (extended) Markdown with no HTML!

{% capture table %}
```table
| Check out this _fancy_ :sparkles: table!                                               \\|
|----------|-----------------------------------------------------------------|-------------|
| Doe      | A deer, a female...                                             | Deer        |
| Oh wait, \ this cell spans two columns! Here's an orange :tangerine:       | Two rows!   |
| Four...  | Bananas forever :banana: :banana: :banana:                      | ^^          |
| ^^       | Oops, forgot one more :banana:                                  \             |
| Testing  | This is <strong>HTML bold</strong>, not markdown                | _center_    |
| This row would be center-aligned                                          \| Hello,      |
| ^^ Hey! How are you? :eyes:                                               \| ^^          |
| Sponge?  | Imagination :rainbow:  &#124; ( • ) ( • ) &#124; :rainbow:      | ^^ _world?_ |
| Thirteen | Some text I will break here,<br>and oh, it also has **markdown** styling!    \|
```alignment
c LLL Lr LL L LLc cL   ll lR
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

<!-- markdownlint-disable-next-line no-inline-html -->
_Note: For all examples below, where not specified, the markup is wrapped with <code>```table</code> as per the usage section above._

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

<!-- markdownlint-disable-next-line no-inline-html -->
* Simply add a section under <code>```alignment</code> before closing the code block with <code>```</code>. Specify left, right, or center-aligned using `L`, `R`, or `C` respectively

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
      cCClCrCrlrLc
      ```

The above 2 examples give the same result:

```table
| _For padding_ | _For padding_ | _For padding_ |
|---------------|---------------|---------------|
| left          |    center     |         right |
|    center     |         right | left          |
|         right | left          |    center     |
```alignment
cCClCrCrlrLc
```

## Additional styling

Keeping to the spirit of Markdown, in order to not make the syntax too complicated, style-related syntax is limited to table cell alignment only (but you are welcome to request for features in the [issue tracker](https://github.com/RichDom2185/jekyll-fancy-tables/issues)).

Having said that, the file also provides a `data-nth-cell` HTML attribute for each table cell (1-indexed), so you can style each individual cell using CSS/JS that way.
