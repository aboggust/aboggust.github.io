---
layout: home
---

<div id='news' class='section'>
  <h2 class='section-title'>News</h2>
  {% assign sorted_news = site.data.news | sort: 'date' | reverse %}
  {% for news in sorted_news%}
    <div class='news'>
      <div class='news-date'>{{news.date | date: "%B %-d, %Y"}} </div>
      <div class='vertical-line'></div>
      <p class='news-title'>{{news.title}} {{site.data.icons[news.icon]}}</p>
    </div>
  {% endfor %}
</div>