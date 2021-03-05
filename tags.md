---
layout: page
permalink: /archives/
title: Archives
---

<ul class="tag-cloud">
{% for tag in site.tags %}
  <span style="font-size: {{ tag | last | size | times: 100 | divided_by: site.tags.size | plus: 70  }}%">
    <a href="#{{ tag | first | slugize }}">
      {{ tag | first }}
    </a> &nbsp;&nbsp;
  </span>
{% endfor %}
</ul>


<div id="archives">
{% for category in site.categories %}
  {% capture category_name %}{{ category | first }}{% endcapture %}
  <details>
    <summary id="#{{ category_name | slugize }}">{{ category_name }}</summary>
    <a name="{{ category_name | slugize }}"></a>
    {% for post in site.categories[category_name] %}
        <article class="archive-item">
          <h4><a href="{{ site.baseurl }}{{ post.url }}">{{post.title}}</a></h4>
        </article>
    {% endfor %}
  </details>
{% endfor %}
</div>


