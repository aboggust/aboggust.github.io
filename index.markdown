---
layout: home
---
<div id='intro'>
  <h1 id='intro-title'>Hello, I'm Angie Boggust</h1>
  <h2 id='intro-subtitle'>I'm an MIT PhD candidate studying AI + HCI</h2>
  <div id='intro-description'>
    <div id='intro-text-wrapper'>
      <p>
      I work with <a href="{{site.data.people['arvindsatya'].url}}">{{site.data.people['arvindsatya'].name}}</a> in the <a href='http://www.mit.edu/'>MIT</a> <a href='https://www.csail.mit.edu/'>CSAIL</a> <a href='http://vis.mit.edu/'>Visualization Group</a>.

      My research focuses on improving <b>human-AI alignment</b> by designing systems that reveal model representations and methods to shift them toward human expectations.
      </p>
      <p>
      Previously, I graduated with my SB and MEng in Computer Science from MIT, where I worked with <a href="{{site.data.people['jimglass'].url}}">{{site.data.people['jimglass'].name}}</a> and <a href="{{site.data.people['daveharwath'].url}}">{{site.data.people['daveharwath'].name}}</a> in the <a href='http://groups.csail.mit.edu/sls/'>Spoken Language Systems Group</a>. Throughout my PhD, I have been fortunate to spend summers as a research intern at <a href="https://machinelearning.apple.com/">Apple</a> with <a href="{{site.data.people['fredhohman'].url}}">{{site.data.people['fredhohman'].name}}</a> and at <a href='https://research.ibm.com/'>IBM Research</a> with <a href="{{site.data.people['hendrikstrobelt'].url}}">{{site.data.people['hendrikstrobelt'].name}}</a>.
      </p>
      <p>
      I am honored to have had my research supported by the MIT John Jarve Fellowship and the <a href="https://machinelearning.apple.com/updates/apple-scholars-aiml-2024">Apple Scholars in AI/ML PhD Fellowship</a>.
      </p>
    </div>
    <div id='intro-headshot-wrapper'>
      <img id='intro-headshot' src="/assets/imgs/people/angieboggust.jpg" alt="Angie Boggust headshot">
      <div class='row intro-links'>
        {% for link_dict in site.data.links %}
          {% assign link = link_dict[1] %}
          {% assign url = link.url %}
          {% unless link.url contains '://' %}
            {% assign url = link.url | prepend: site.url %}
          {% endunless %}
          <a class='button' href="{{url}}">
            <div>{{site.data.icons[link.icon]}}</div>
          </a>
        {% endfor %}
      </div>
      <div class='row intro-links'>
          <a class='button' id='email' href="mailto:aboggust@csail.mit.edu">
            <div>aboggust@csail.mit.edu</div>
          </a>
      </div>
    </div>
  </div>
</div>

<div id='news' class='section'>
  <h2 class='section-title'>News</h2>
  {% assign sorted_news = site.data.news | sort: 'date' | reverse %}
  {% for news in sorted_news %}
    <div class='news'>
      <div class='news-date'>{{news.date | date: "%B %-d, %Y"}}</div>
      <div class='news-title'>{{news.title}} {{site.data.icons[news.icon]}}</div>
    </div>
  {% endfor %}
</div>

<div id='publications' class='section'>
  <h2 class='section-title'>Featured Publications</h2>
  {% assign sorted_pubs = site.pubs | sort: 'date' | reverse %}
  {% for pub in sorted_pubs %}
  {% if pub.venue != 'arxiv' and pub.type == 'conference' %}
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
          <p class='publication-venue'>{{site.data.venues[pub.venue].short}} {{pub.date | date: "%Y"}}
          {% if pub.award %}
          <p class='publication-award'>{{site.data.icons['award']}} {{pub.award}}</p>
          {% endif %}
          </p>
        </div>
        <div class='publication-links row'>
          {% for link in pub.links %}
            <div class='button'><a class='publication-link' href="{{link.url}}">{{site.data.icons[link.icon]}} {{link.name}}</a></div>
          {% endfor %}
        </div>
      </div>
    </div>
  {% endif %}
  {% endfor %}
</div>