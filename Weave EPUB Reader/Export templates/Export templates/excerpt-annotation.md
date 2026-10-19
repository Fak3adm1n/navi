{% for chapter in chapters %}
{% for highlight in chapter.highlights %}
{{ highlight.quoteBlock }}

{% endfor %}
{% endfor %}
