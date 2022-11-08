# Jekyll Pure Liquid Fancy Tables

> View the demo [here](https://richdom2185.github.io/jekyll-fancy-tables).

GitHub Pages only allows a specific set of [plugins](https://pages.github.com/versions/) to run, hence, additional plugins like [jeffreytse/jekyll-spaceschip](https://github.com/jeffreytse/jekyll-spaceship) cannot work.

Inspired by that plugin, and the approach used in [allejo/jekyll-toc](https://github.com/allejo/jekyll-toc), I wanted to add support for fancy tables in Pure Liquid.

Benefits:

* Fully compatible with GitHub Pages
* Easily customisable to your needs

## Usage

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
