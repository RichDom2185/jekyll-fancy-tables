# Jekyll Pure Liquid Fancy Tables

> View the demo [here](https://richdom2185.github.io/jekyll-fancy-tables).

GitHub Pages only allows a specific set of [plugins](https://pages.github.com/versions/) to run, hence, additional plugins like [jeffreytse/jekyll-spaceschip](https://github.com/jeffreytse/jekyll-spaceship) cannot work.

Inspired by that plugin, and the approach used in [allejo/jekyll-toc](https://github.com/allejo/jekyll-toc), I wanted to add support for fancy tables in Pure Liquid.

Benefits:

* Fully compatible with GitHub Pages
* Easily customisable to your needs

## Add it to your site

Simply include it in any of the layouts you want to add support for:

**Recommended:** Reassign the layout's `content` variable. This approach ensures compatibility should you want to include additional features:

```html
{% capture content %}{% include fancy-tables.liquid html=content %}{% endcapture %}
<!-* Some other stuff... -->
{{ content }}
```

**Alternative:** Replace `{{ content }}` directly:

* Before:

  ```html
  <!-* Some other stuff... -->
  {{ content }}
  ```

* After:

  ```html
  <!-* Some other stuff... -->
  {% include fancy-tables.liquid html=content %}
  ```

## Usage

Simply wrap your existing table in a fenced code block with the custom language called `table`. Example:

    ```table
    | Fruits | Vegetables | Meat    |
    |--------|------------|---------|
    | Apple  | Potato     | Chicken |
    ```

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

<table>
  <tbody>
    <tr>
      <td colspan="1" rowspan="1" data-nth-cell="1" align="left">Sometimes</td>
      <td colspan="1" rowspan="1" data-nth-cell="2" align="left">you</td>
      <td colspan="1" rowspan="1" data-nth-cell="3" align="left">don’t</td>
      <td colspan="1" rowspan="1" data-nth-cell="4" align="left">want</td>
      <td colspan="1" rowspan="1" data-nth-cell="5" align="left">them</td>
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
