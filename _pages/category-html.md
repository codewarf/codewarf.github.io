 ---
 title: "HTML"
 layout: archive
 permalink: /categories/html
 author_profile: true
 type: posts
 sidebar:
   nav: "main-sidebar"
 ---

 {% assign posts = site.categories['html'] %}
 {% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}