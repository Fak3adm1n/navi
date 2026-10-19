{% for chapter in chapters %}
{% for highlight in chapter.highlights %}
{{ highlight.quotePageBlock }}

{% endfor %}
{% endfor %}
