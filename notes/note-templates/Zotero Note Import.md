---
title: "{{title | escape}}"
citekey: "{{citekey}}"
authors: "{{authors}}"
year: {{date | format("YYYY")}}
tags: [{% for t in tags %}"{{t.tag}}"{% if not loop.last %}, {% endif %}{% endfor %}]
---

# {{title}}

**Zotero Link:** [Zotero Link]({{desktopURI}}) | **PDF Link:** {{pdfZoteroLink}}

---

## Summary & Notes

{% persist "notes" %} {% if isFirstImport %} Write your personal notes,
summaries, and synthesis here! {% endif %} {% endpersist %}

---

## Annotations

{% persist "annotations" %} {% for annotation in annotations -%}
{% if annotation.tags and annotation.tags.length > 0 -%} _Tags:
{% for t in annotation.tags %}#{{t.tag | replace(" ", "-") |
replace(":","_")}}{% if not loop.last %}, {% endif %}{% endfor %}\_ {%- endif %}
{% if annotation.annotatedText -%} {%- if annotation.colorCategory -%}
<mark class="hltr-{{annotation.colorCategory | lower}}">"{{annotation.annotatedText | safe}}"</mark>
{%- else -%} ==="{{annotation.annotatedText | safe}}"=== {%- endif %}
([Page {{annotation.pageLabel}}](zotero://open-pdf/library/items/{{annotation.attachment.itemKey}}?page={{annotation.pageLabel}}&annotation={{annotation.id}}))
{%- endif %} {% if annotation.comment -%}
<mark class="hltr-{{annotation.colorCategory | lower}}">{{annotation.comment | safe}}</mark>
{%- endif %}

{% endfor -%} {% endpersist %}
