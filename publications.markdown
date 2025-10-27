---
layout: home
---

<div id='publications' class='section'>
  <h2 class='section-title'>Publications</h2>
  {% assign sorted_pubs = site.pubs | sort: 'date' | reverse %}
  {% for pub in sorted_pubs %}
    <div class='publication'>
      <div class='publication-image'>
        <a href="{{pub.links[0].url}}">
          <img class='publication-img' src="/assets/imgs/thumbs/{{pub.slug}}.jpg" alt="{{pub.slug}} thumbnail image.">
        </a>
      </div>
      <div class='publication-info'>
        <div class='publication-detail'>
          <p class='publication-title'>{{pub.title}}</p>
          <p class='publication-authors'>
            {% for author in pub.authors %}
              {% assign person = site.data.people[author.key] %}
              <a class='publication-author' style="{% if person.name == 'Angie Boggust' %} font-weight: bold {% endif %}" href="{{person.url}}">{{person.name}}{% if author.equal %}*{% endif %}</a>{% unless forloop.last %}
              <span class='publication-author'> • </span>
              {% endunless %}
            {% endfor %}
          </p>
          <p class='publication-venue'>
            {% if pub.underreview == true %}Under Review at{% endif %}
            {{site.data.venues[pub.venue].full}} {{pub.date | date: "%Y"}}
            {% if pub.award %}
            <p class='publication-award'>{{site.data.icons['award']}} {{pub.award}}</p>
            {% endif %}
          </p>
        </div>
        <div class='publication-links row'>
          {% for link in pub.links %}
            <div class='button'>
              <a class='publication-link icon-button' href="{{link.url}}">
                <div>{{site.data.icons[link.icon]}}</div>
                <div>{{link.name}}</div>
              </a>
            </div>
          {% endfor %}
        </div>
      </div>
    </div>
  {% endfor %}
</div>
