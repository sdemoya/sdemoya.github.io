---
title: "Technical Writing"
permalink: /tech-writing/
header:
  image: "/images/banner-pineapple-1704339_1920.jpg"
---
Pardon my dust and typos while I build out this portfolio. With time you'll be able to see a collection of technical writing, python projects and cloud infrastructure know-how. <br/>
<br/>
Special thanks to Michael Rose for the template. mademistakes.com @mmistakes <br/>
Special thanks to pineapplesupplyco & Alexas_Fotos on pixabay.com for the photos. <br/>

{% include base_path %}
{% include group-by-array collection=site.posts field="tags" %}

{% for tag in group_names %}
  {% assign posts = group_items[forloop.index0] %}
  <h2 id="{{ tag | slugify }}" class="archive__subtitle">{{ tag }}</h2>
  {% for post in posts %}
    {% include archive-single.html %}
  {% endfor %}
{% endfor %}
