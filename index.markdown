---
layout: home
---
<div id='intro'>
  <div id='intro-headshot-wrapper' class='intro-column'>
    <img id='intro-headshot' class='intro-item' src="/assets/imgs/people/angieboggust.jpg" alt="Angie Boggust headshot">
    <div class='column intro-item' id='job-market'>
      <p id='job-market-tag-line'><b>I'm on the academic and industry job markets!</b></p>
      <div class='statement-links'>
        {% for statement in site.data.statements %}
          <a class='button icon-button' href="{{statement.link}}">
            <div style='width:18px'>{{site.data.icons[statement.type]}}</div>
            <div>{{statement.name}}</div>
          </a>
        {% endfor %}
      </div>
    </div>
  </div>
  <div id='intro-text-wrapper' class='intro-column'>
    <div id='intro-header' class='intro-item'>
      <h1 id='intro-title'>ANGIE BOGGUST</h1>
      <h2 id='intro-subtitle'>MIT PhD candidate studying HCI + AI</h2>
      <div class='row intro-links'>
        {% for link_dict in site.data.links %}
          {% assign link = link_dict[1] %}
          {% assign url = link.url %}
          {% unless link.url contains '://' %}
            {% assign url = link.url | prepend: site.url %}
          {% endunless %}
          <a class='button' href="{{url}}" style='width:25px'>
            <div>{{site.data.icons[link.icon]}}</div>
          </a>
        {% endfor %}
        <a class='button icon-button' href="mailto:aboggust@csail.mit.edu">
            <div>{{site.data.icons['email']}}</div>
            <div>aboggust@csail.mit.edu</div>
          </a>
      </div>
    </div>
    <div id='intro-text' class='intro-item'>
      <p>
      Hi, I'm Angie! I'm a final-year PhD candidate at MIT CSAIL advised by <a href="{{site.data.people['arvindsatya'].url}}">{{site.data.people['arvindsatya'].name}}</a> in the <a href='http://vis.mit.edu/'>Visualization Group</a>.
      My research focuses on improving <b>human-AI alignment</b> by designing systems that reveal model representations and methods to shift them toward human expectations.
      I am honored to have my research supported by the <a href='https://science.mit.edu/seed-funding-helps-science-researchers/'>MIT John Jarve Fellowship</a> and <a href="https://machinelearning.apple.com/updates/apple-scholars-aiml-2024">Apple Scholars in AI/ML PhD Fellowship</a>.
      </p>
      <p>
      Previously, I received my SB and MEng in computer science from MIT, where I worked with <a href="{{site.data.people['jimglass'].url}}">{{site.data.people['jimglass'].name}}</a> and <a href="{{site.data.people['daveharwath'].url}}">{{site.data.people['daveharwath'].name}}</a> in the <a href='http://groups.csail.mit.edu/sls/'>Spoken Language Systems Group</a>. Throughout my PhD, I've interned at <a href="https://machinelearning.apple.com/">Apple Research</a> with <a href="{{site.data.people['fredhohman'].url}}">{{site.data.people['fredhohman'].name}}</a> and <a href='https://research.ibm.com/'>IBM Research</a> with <a href="{{site.data.people['hendrikstrobelt'].url}}">{{site.data.people['hendrikstrobelt'].name}}</a>.
      </p>
    </div>
  </div>
</div>

<div id='news' class='section'>
  <h2 class='section-title'>Recent News</h2>
  {% assign sorted_news = site.data.news | sort: 'date' | reverse %}
  {% for news in sorted_news limit:7%}
    <div class='news'>
      <div class='news-date'>{{news.date | date: "%B %-d, %Y"}} </div>
      <div class='vertical-line'></div>
      <p class='news-title'>{{news.title}} {{site.data.icons[news.icon]}}</p>
    </div>
  {% endfor %}
  <!-- <a class='button icon-button' href='/news'>
    <div>{{ site.data.icons['plus'] }}</div>
    <div>View All News</div>
  </a> -->
</div>

<div id='publications' class='section'>
  <h2 class='section-title'>Publications</h2>
  {% assign sorted_pubs = site.pubs | sort: 'date' | reverse %}
  {% for pub in sorted_pubs %}
  {% if pub.featured == true %}
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
            {{site.data.venues[pub.venue].short}} {{pub.date | date: "%Y"}}
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
  {% endif %}
  {% endfor %}
  <a class='button icon-button' href="/publications">
    <div>{{ site.data.icons['plus'] }}</div>
    <div>View All Publications</div>
  </a>
</div>

<!-- <div id='news' class='section'>
  <h2 class='section-title'>News</h2>
  {% assign sorted_news = site.data.news | sort: 'date' | reverse %}
  {% for news in sorted_news limit:7%}
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
</div> -->