---
layout: default
permalink: /
---

# bio

Dimitar Atanasov has half a decade of experience in Cloud Engineering and Automation, specializing in the creation and maintenance of secure and reliable infrastructure. In the physical world he repetitively lifts heavy things and puts them back down.

# portfolio

<div class="section-block">
{% for post in site.portfolio reversed %}
{% include portfolio-item.html %}

<hr>
{% endfor %}
</div>

{% if site.positions and site.positions.size > 0 %}

# career

<div class="section-block positions-timeline">
{% for position in site.positions %}
{% include position-timeline-item.html position=position %}
{% endfor %}
</div>
{% endif %}
