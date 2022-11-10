---
layout: demo
---
<!--markdownlint-disable-file first-line-h1 -->
<!-- markdownlint-disable-file blanks-around-fences -->

> {{ site.description }}
{: style="font-size: 1.5em" }

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
