---
title: "Talks"
layout: gridlay
sitemap: false
permalink: /talks/
nav: true
nav_order: 4
---
<div class="talks">

{% for talk in site.data.talks %}
- **{{ talk.title }}**, {{ talk.conference }}, {{ talk.date }} – [Slides]({{ talk.slides }})
{% endfor %}

</div>