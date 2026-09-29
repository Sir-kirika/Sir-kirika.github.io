---
permalink: /lab-challenges/
title: "Lab Challenges"
layout: single
author_profile: true
---

Hands-on networking and security labs from the Cyber Shujaa Cloud and Network Security track, plus HackTheBox Academy and TryHackMe modules. New entries added weekly — this list updates automatically as new lab posts are published.

---

{% assign labs = site.categories.labs | sort: 'date' | reverse %}
{% for post in labs %}
### [{{ post.title }}]({{ post.url | relative_url }})
{{ post.excerpt }}

{% endfor %}
