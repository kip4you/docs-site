---
layout: single
classes: wide
permalink: /people
title: "People"
excerpt: "Our smart people."
sidebar:
  nav: "docs"
---

<table style="width:100%">

{% for person in site.data.people %}

<tr>
  <td>
   <b>{{ person.name }}</b>
   <a href="https://www.linkedin.com/in/{{ person.linkedin }}">
    <i class="fab fa-fw fa-linkedin" aria-hidden="true"></i>
  </a> <p />
    {{ person.affiliation }}

  </td>
</tr>

{% endfor %}

</table>
