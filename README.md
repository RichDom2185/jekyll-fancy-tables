# Jekyll Pure Liquid Fancy Tables

> View the demo [here](https://richdom2185.github.io/jekyll-fancy-tables).

GitHub Pages only allows a specific set of [plugins](https://pages.github.com/versions/) to run, hence, additional plugins like [jeffreytse/jekyll-spaceschip](https://github.com/jeffreytse/jekyll-spaceship) cannot work.

Inspired by that plugin, and the approach used in [allejo/jekyll-toc](https://github.com/allejo/jekyll-toc), I wanted to add support for fancy tables in Pure Liquid.

Benefits:

* Fully compatible with GitHub Pages
* Easily customisable to your needs

## Add it to your site

### Step 1: Copy the required files

Copy the following files to your site's `_includes` folder:

* `fancy-tables.liquid`: The main parser to generate the tables
* `capturehtml.liquid`: Un-escapes HTML special characters, used to parse HTML tags inside pre-formatted code blocks

### Step 2: Include it in your site

You can render fancy tables in your Jekyll site using one of two, non-mutually-exclusive ways:

#### As a HTML layout

Simply include it in any of the layouts you want to add support for:

**Recommended:** Reassign the layout's `content` variable. This approach ensures compatibility should you want to include additional features:

```html
{% capture content %}{% include fancy-tables.liquid html=content %}{% endcapture %}
<!-- Some other stuff... -->
{{ content }}
```

**Alternative:** Replace `{{ content }}` directly:

* Before:

  ```html
  <!-- Some other stuff... -->
  {{ content }}
  ```

* After:

  ```html
  <!-- Some other stuff... -->
  {% include fancy-tables.liquid html=content %}
  ```

#### As an Include Expression

_See [Advanced Usage: Rendering Individual Tables Only](#rendering-individual-tables-only)._

## Usage

Simply wrap your existing table in a fenced code block with the custom language called `table`. Example:

    ```table
    | Fruits | Vegetables | Meat    |
    |--------|------------|---------|
    | Apple  | Potato     | Chicken |
    ```

This syntax was chosen for a couple reaons:

* Relatively easy parsing
* Prevents most formatters from accidentally breaking the table layout due to the non-standard syntax

## Features

_Note: For all examples below, where not specified, the markup is wrapped with `` ```table `` as per the usage section above._

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

<table>
  <tbody>
    <tr>
      <td colspan="1" rowspan="1" data-nth-cell="1" align="left">Sometimes</td>
      <td colspan="1" rowspan="1" data-nth-cell="2" align="left">you</td>
      <td colspan="1" rowspan="1" data-nth-cell="3" align="left">don’t</td>
      <td colspan="1" rowspan="1" data-nth-cell="4" align="left">want</td>
      <td colspan="1" rowspan="1" data-nth-cell="5" align="left">headers</td>
    </tr>
  </tbody>
</table>

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

<table>
  <thead>
    <tr>
      <th colspan="3" data-nth-cell="1" align="left">OMG, I span 3 columns!</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td colspan="1" rowspan="1" data-nth-cell="2" align="left">That’s…</td>
      <td colspan="1" rowspan="1" data-nth-cell="3" align="left">very</td>
      <td colspan="1" rowspan="1" data-nth-cell="4" align="left">nice</td>
    </tr>
  </tbody>
</table>

#### Row Span

* Only works for the table body

* Simply prepend table cells with `^^`

  ```text
  |------------------------|---------|
  | Look, I span two rows! | Looks   |
  | ^^                     | pretty! |
  ```

  Result:

  <table>
    <tbody>
      <tr>
        <td colspan="1" rowspan="2" data-nth-cell="1" align="left">Look, I span two rows!</td>
        <td colspan="1" rowspan="1" data-nth-cell="2" align="left">Looks</td>
      </tr>
      <tr>
        <td colspan="1" rowspan="1" data-nth-cell="3" align="left">pretty!</td>
      </tr>
    </tbody>
  </table>

* Non-blank cells will be joined together with a line break

  ```text
  |---------------|---------|
  | Look, I span  | Looks   |
  | ^^ two rows!  | pretty! |
  ```

  Result:

  <table>
    <tbody>
      <tr>
        <td colspan="1" rowspan="2" data-nth-cell="1" align="left">Look, I span <br>two rows! </td>
        <td colspan="1" rowspan="1" data-nth-cell="2" align="left">Looks</td>
      </tr>
      <tr>
        <td colspan="1" rowspan="1" data-nth-cell="3" align="left">pretty!</td>
      </tr>
    </tbody>
  </table>

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

<table>
  <thead>
    <tr>
      <th colspan="1" data-nth-cell="1" align="center">
        <em>For padding</em>
      </th>
      <th colspan="1" data-nth-cell="2" align="center">
        <em>For padding</em>
      </th>
      <th colspan="1" data-nth-cell="3" align="center">
        <em>For padding</em>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td colspan="1" rowspan="1" data-nth-cell="4" align="left">left</td>
      <td colspan="1" rowspan="1" data-nth-cell="5" align="right">center</td>
      <td colspan="1" rowspan="1" data-nth-cell="6" align="right">right</td>
    </tr>
    <tr>
      <td colspan="1" rowspan="1" data-nth-cell="7" align="center">center</td>
      <td colspan="1" rowspan="1" data-nth-cell="8" align="right">right</td>
      <td colspan="1" rowspan="1" data-nth-cell="9" align="left">left</td>
    </tr>
    <tr>
      <td colspan="1" rowspan="1" data-nth-cell="10" align="right">right</td>
      <td colspan="1" rowspan="1" data-nth-cell="11" align="left">left</td>
      <td colspan="1" rowspan="1" data-nth-cell="12" align="center">center</td>
    </tr>
  </tbody>
</table>

## Advanced Usage

### Rendering Individual Tables Only

<details>
  <summary><strong>Why would you use this?</strong></summary>

  This can be useful together with some creative tricks like using [text substitution for lists in markdown tables](https://gist.github.com/RichDom2185/26166ba51cf432b90a0afb04993d0640).

</details>

If you only want to render certain tables, the extension also supports rendering directly from markdown. Simply include the following markup in your source file:

    {% capture table %}
    ```table
    | The Do-Re-Mi Song              \\|
    |-----|---------------------|------|
    | Doe | A deer, a female... | Deer |
    ```alignment
    c
    ```
    {% endcapture %}

    {% include fancy-tables.liquid markdown=table %}

Note the use of the `markdown` argument instead of `html`.

Result:

<table>
  <thead>
    <tr>
      <th colspan="3" data-nth-cell="1" align="center">The Do-Re-Mi Song</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td colspan="1" rowspan="1" data-nth-cell="2" align="left">Doe</td>
      <td colspan="1" rowspan="1" data-nth-cell="3" align="left">A deer, a female…</td>
      <td colspan="1" rowspan="1" data-nth-cell="4" align="left">Deer</td>
    </tr>
  </tbody>
</table>

If used together with [the HTML layout](#as-a-html-layout), you will have to wrap the include statement in a `div` element to prevent the markdown preprocessor from parsing it again:

```html
<div markdown="0">{% include fancy-tables.liquid markdown=table %}</div>
```

Note: depending on your Jekyll site configuration, the `markdown="0"` attribute may or may not be needed.

## Others

### Bugs

Feel free to report any bugs in the [issue tracker](https://github.com/RichDom2185/jekyll-fancy-tables/issues).

### Additional styling

Keeping to the spirit of Markdown, in order to not make the syntax too complicated, style-related syntax is limited to table cell alignment only (but you are welcome to request for features in the [issue tracker](https://github.com/RichDom2185/jekyll-fancy-tables/issues)).

Having said that, the file also provides a `data-nth-cell` HTML attribute for each table cell (1-indexed), so you can style each individual cell using CSS/JS that way.

## Planned additions

* [ ] Default column alignment
* [ ] Individual cell alignment: ignore all characters, not just whitespace
* [ ] _??? (suggest a feature [here!](https://github.com/RichDom2185/jekyll-fancy-tables/issues))_
