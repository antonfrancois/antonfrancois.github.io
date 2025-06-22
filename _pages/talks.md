---
title: "Talks"
layout: gridlay
sitemap: false
permalink: /talks/
---
<div class="talks">

{% for talk in site.data.talks %}
- **{{ talk.title }}**, {{ talk.conference }}, {{ talk.date }} – [Slides]({{ talk.slides }})
{% endfor %}

</div>