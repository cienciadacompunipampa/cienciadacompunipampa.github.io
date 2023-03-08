---
layout: default
---

<section class="hero is-light is-medium">
  <div class="hero-body">
    <div class="container has-text-centered">
      <img id="logo" src="/assets/img/logo.png" alt="Page logo">
    </div>
  </div>

  <div class="hero-foot">
    <nav class="tabs is-boxed is-fullwidth">
      <div class="container">
        <ul>
          <li>
            <a href="/">Links</a>
          </li>
          <li>
            <a href="/faq">Dúvidas</a>
          </li>
          <li class="is-active">
            <a href="/votes">Representação</a>
          </li>
        </ul>
      </div>
    </nav>
  </div>
</section>

<div id="page" class="container content mt-6 mb-6">
{% assign reps = site.data.votes | sort_natural: "startdate" | reverse %}
{% for rep in reps %}
  <h3 class="title">{{ rep.name }}</h3>
  <p class="subtitle">Representante Discente</p>
  <hr>
  {% assign votes = rep.votes | sort_natural: "date" | reverse %}
  {% for vote in votes %}
    <h4 class="title">{{ vote.topic }}</h4>
    <p class="subtitle">{{ vote.date | date: "%d de %b, %Y" }}</p>
    <div class="mt-4"><b>ARGUMENTO:</b></div>
    <div>{{ vote.considerations.summary }}</div>
    {% for point in vote.considerations.points %}
      {% if point.pro %}
        <div class="pl-5"><span class="has-text-success"><b>PRO</b></span>&nbsp;—&nbsp;{{ point.pro }}</div>
      {% elsif point.con %}
        <div class="pl-5"><span class="has-text-danger"><b>CON</b></span>&nbsp;—&nbsp;{{ point.con }}</div>
      {% endif %}
    {% endfor %}
    <div class="mt-3"><b>MANIFESTO:</b></div>
    {% assign tempstr = "FAVORÁVEL" %}
    {% if vote.position.favorable == true %}
    <article class="message is-success mt-4">
    {% else %}
    {% assign tempstr = "DESFAVORÁVEL" %}
    <article class="message is-danger mt-4">
    {% endif %}
      <div class="message-body">
        <p><b>{{ tempstr }}</b>&nbsp;&nbsp;&nbsp;&nbsp;{{ vote.position.opinion }}</p>
      </div>
    </article>
    <hr>
  {% endfor %}
{% endfor %}

</div>

{% include foot.html %}
