---
permalink: /lab-challenges/
title: "Lab Challenges"
layout: single
author_profile: false
classes: wide
---

Hands-on networking and security labs from the Cyber Shujaa Cloud and Network Security track, plus HackTheBox Academy and TryHackMe modules. New entries are added as I publish them.

<div class="grid__wrapper">
{% for post in site.categories.labs %}
  {% include archive-single.html type="grid" %}
{% endfor %}
</div>