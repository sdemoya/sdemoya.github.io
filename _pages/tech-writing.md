---
title: "Technical Writing"
permalink: /tech-writing/
header:
  image: "/images/banner-pineapple-1704339_1920.jpg"
---

## [Build a Serverless Website using AWS Lambda, API Gateway, S3 and Route53](https://sdemoya.github.io/Build-a-Serverless-Site-with-Dynamic-Content/)

{% include base_path %}
{% include group-by-array collection=site.posts field="tags" %}

{% for tag in group_names %}
  {% assign posts = group_items[forloop.index0] %}
  <h2 id="{{ tag | slugify }}" class="archive__subtitle">{{ tag }}</h2>
  {% for post in posts %}
    {% include archive-single.html %}
  {% endfor %}
{% endfor %}