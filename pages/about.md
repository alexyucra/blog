---
layout: page
title: Quem sou, o que eu faço, o que eu como, como pode me encontrar...
description: A codificação muda o mundo
keywords: Analista de Dados, Ti, Sistemas, DBA, Desenvolvedor FullStack
comments: true
menu: about
permalink: /about/
---

Analista de Dados | Ti | Sistemas | DBA | Desenvolvedor FullStack 

Ciência de dados | Engenheiro Estatístico | Instrutor Consultor


## Social

<ul>
{% for website in site.data.social %}
<li>{{website.sitename }}：<a href="{{ website.url }}" target="_blank">@{{ website.name }}</a></li>
{% endfor %}
{% if site.url contains 'mazhuang.org' %}
<li>
Like：<br />
<img style="height:192px;width:192px;border:1px solid lightgrey;" src="{{ assets_base_url }}/assets/images/qrcode.jpg" alt="Latin Dev" />
</li>
{% endif %}
</ul>


## Skill Keywords

{% for skill in site.data.skills %}
### {{ skill.name }}
<div class="btn-inline">
{% for keyword in skill.keywords %}
<button class="btn btn-outline" type="button">{{ keyword }}</button>
{% endfor %}
</div>
{% endfor %}
