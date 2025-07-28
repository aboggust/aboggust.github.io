---
layout: home
title: CV
---

<style>
    :root {
        --xxs-padding: 3pt;
        --xs-padding: 5pt;
        --sm-padding: 7pt;
        --md-padding: 15pt;
        --lg-padding: 20pt;
        
        --accent-font-size: 9pt;
        --subfont-size: 10pt;
        --font-size: 12pt;
        --heading-size: 16pt;
        --title-size: 38pt;
        --line-height: var(--font-size);

        --page-width: 8.5in;
        --page-height: 11in;
        --margin: 0.5in;

        --section-date-width: 103px;
        --section-content-width: calc(var(--section-width) - var(--section-date-width));
    }

    /* @page {
        size: var(--page-width) var(--page-height); 
        margin: var(--margin);
    } */

    html { 
        margin: 0;
        width: 100%;
    }

    body {
        width: 100%;
        margin: 0;
        font-family: 'Roboto', sans-serif;
        font-size: var(--font-size);
        color: #000000;
    }

    /* Screen-specific styles */
    @media screen {
        #cv {
            max-width: calc(var(--page-width) + var(--margin));
            margin: 3em 0;
        }
    }

    .award i {
        font-family: 'Font Awesome 5 Free'; /* or the correct version */
        font-weight: 900;
        display: inline-block;
    }

</style>


<div id='cv'>
 <div id='personal-info'>
    <div id='name'>
        <div class='first-name'>ANGIE</div>
        <div class='last-name'>BOGGUST</div>
    </div>
    <div id='contact-info'>
        <div><a href="mailto:aboggust@csail.mit.edu">aboggust@csail.mit.edu</a></div>
        <div><a href="http://angieboggust.com">angieboggust.com</a></div>
        <div><a href="{{site.data.links['twitter'].url}}">@angie_boggust</a></div>
        <div class="address">32-G816, 32 Vassar St. Cambridge, MA 02139</div>
    </div>
</div>
<div id='education' class='cv-section'>
    <div class='cv-section-heading'>EDUCATION</div>
    <div class='cv-section-content'>
        {% for education in site.data.education %}
        <div class='entry'>
            <div class='date'>
                <div>{{education.date | date: "%Y"}}</div>
            </div>
            <div class='content'>
                <p class='title'>{{education.degree}} in {{education.area}}</p>
                <p class='description'>{{education.university}}</p>
                {% for item in education.details %}
                    <p class='context'>
                        <span>{{item.title}}:</span> 
                        {% if site.data.people[item.value] %}<a class='publication-author' href="{{site.data.people[item.value].url}}">{{site.data.people[item.value].name}}</a>{% else %}{{item.value}}{% endif %}{% if item.detail %}, {{item.detail}} {% endif %}
                        </p>
                {% endfor %}
                <div class='context links'>
                    {% for link in education.links %}
                        <a href="{{link.url}}">{{site.data.icons[link.icon]}} {{link.name}}</a>
                    {% endfor %}
                </div>
            </div>
        </div>
        {% endfor %}
    </div>
</div>

<div id='research' class='cv-section'>
    <div class='cv-section-heading'> ACADEMIC RESEARCH</div>
    <div class='cv-section-content'>
    {% assign sorted_research = site.data.experience | sort: 'startdate' | reverse %}
    {% for research in sorted_research %}
    {% if research.type == 'academic' %}
        <div class='entry'>
            <div class='date'>
                    {% assign startyear = research.startdate | date: "%Y" %}
                    {% assign endyear = research.enddate | date: "%Y" %}
                    {% if startyear == endyear %}
                        {% assign startmonth = research.startdate | date: "%b" %}
                        {% assign endmonth = research.enddate | date: "%b" %}
                        {% if startmonth == endmonth %}
                            {{startmonth}}. {{startyear}}
                        {% elsif startmonth == 'May' or startmonth == 'Jun' and endmonth == 'Aug' or endmonth == 'Sep' %}
                            Summer {{startyear}}
                        {% else %}
                            {{startmonth}} &ndash; {{endmonth}} {{endyear}}
                        {% endif %}
                    {% else %}
                        {{startyear}} &ndash;
                        {% if research.enddate %}
                            {{endyear}}
                        {% else %}
                            Present
                        {% endif %}
                    {% endif %}
            </div>
            <div class='content'>
                <p class='title'>{{research.organization}}</p>
                <p class='description'>{{research.role}}, {{research.group}}</p>
                <p class='context'>
                    {% if research.mentors.size == 1 %}Mentor: {% endif %}
                    {% if research.mentors.size > 1 %}Mentors: {% endif %}
                    {% for mentor in research.mentors %}
                    {% assign person = site.data.people[mentor] %}
                    <a class='publication-author' href="{{person.url}}">{{person.name}}</a>{% unless forloop.last %}
                    <span class='publication-author'> • </span>
                    {% endunless %}
                    {% endfor %}
                </p>
                <p class='context'>{{research.description}}</p>
            </div>
        </div>
    {% endif %}
    {% endfor %}
    </div>
</div>

<div id='industry-research' class='cv-section'>
    <div class='cv-section-heading'> INDUSTRY RESEARCH</div>
    <div class='cv-section-content'>
    {% assign sorted_research = site.data.experience | sort: 'startdate' | reverse %}
    {% for research in sorted_research %}
    {% if research.type == 'industry' %}
        <div class='entry'>
            <div class='date'>
                <div>
                    {% assign startyear = research.startdate | date: "%Y" %}
                    {% assign endyear = research.enddate | date: "%Y" %}
                    {% if startyear == endyear %}
                        {% assign startmonth = research.startdate | date: "%b" %}
                        {% assign endmonth = research.enddate | date: "%b" %}
                        {% if startmonth == endmonth %}
                            {{startmonth}}. {{startyear}}
                        {% elsif startmonth == 'May' or startmonth == 'Jun' and endmonth == 'Aug' or endmonth == 'Sep' %}
                            Summer {{startyear}}
                        {% else %}
                            {{startmonth}} &ndash; {{endmonth}} {{endyear}}
                        {% endif %}
                    {% else %}
                        {{startyear}} &ndash;
                        {% if research.enddate %}
                            {{endyear}}
                        {% else %}
                            Present
                        {% endif %}
                    {% endif %}
                </div>
            </div>
            <div class='content'>
                <p class='title'>{{research.organization}}</p>
                <p class='description'>{{research.role}}, {{research.group}}</p>
                <p class='context'>
                    {% if research.mentors.size == 1 %}Mentor: {% endif %}
                    {% if research.mentors.size > 1 %}Mentors: {% endif %}
                    {% for mentor in research.mentors %}
                    {% assign person = site.data.people[mentor] %}
                    <a class='publication-author' href="{{person.url}}">{{person.name}}</a>{% unless forloop.last %}
                    <span class='publication-author'> • </span>
                    {% endunless %}
                    {% endfor %}
                </p>
                <p class='context'>{{research.description}}</p>
            </div>
        </div>
    {% endif %}
    {% endfor %}
    </div>
</div>


<div id='publications' class='cv-section'>
    <div class='cv-section-heading'>PUBLICATIONS</div>
    <div class='cv-section-content'>
    {% assign sorted_pubs = site.pubs | sort: 'date' | reverse %}
    {% assign last_year = "" %}
    {% for pub in sorted_pubs %}
    {% if pub.type == 'conference' %}
    {% assign current_year = pub.date | date: "%Y" %}
        <div class='entry'>
            <div class='date'>
                {% if current_year != last_year %}
                <div>{{pub.date | date: "%Y"}}</div>
                {% assign last_year = current_year %}
                {% endif %}
            </div>
            <div class='content'>
                <p class='title'>{{pub.title}}</p>
                <p class='context'>
                {% for author in pub.authors %}
                    {% assign person = site.data.people[author.key] %}
                    <a class='publication-author' style="{% if person.name == 'Angie Boggust' %} font-weight: bold {% endif %}" href="{{person.url}}">{{person.name}}{% if author.equal %}*{% endif %}</a>{% unless forloop.last %}
                    <span class='publication-author'> • </span>
                    {% endunless %}
                {% endfor %}
                </p>
                <p class='context'>{{site.data.venues[pub.venue].full}} {{pub.date | date: "%Y"}}</p>
                <div class='context links'>
                {% for link in pub.links %}
                    <a href="{{link.url}}">{{site.data.icons[link.icon]}} {{link.name}}</a>
                {% endfor %}
                </div>
                {% if pub.award %}
                <p class='context award'>{{site.data.icons['award']}} {{pub.award}}</p>
                {% endif %}
            </div>
        </div>
    {% endif %}
    {% endfor %}
    </div>
</div>

<div id='workshops' class='cv-section'>
    <div class='cv-section-heading'>WORKSHOPS & DEMOS</div>
    <div class='cv-section-content'>
    {% assign sorted_pubs = site.pubs | sort: 'date' | reverse %}
    {% assign last_year = "" %}
    {% for pub in sorted_pubs %}
    {% if pub.type == 'workshop' or pub.type == 'demo' %}
    {% assign current_year = pub.date | date: "%Y" %}
        <div class='entry'>
            <div class='date'>
                {% if current_year != last_year %}
                <div>{{pub.date | date: "%Y"}}</div>
                {% assign last_year = current_year %}
                {% endif %}
            </div>
            <div class='content'>
                <p class='title'>{{pub.title}}</p>
                <p class='context'>
                {% for author in pub.authors %}
                    {% assign person = site.data.people[author.key] %}
                    <a class='publication-author' style="{% if person.name == 'Angie Boggust' %} font-weight: bold {% endif %}" href="{{person.url}}">{{person.name}}{% if author.equal %}*{% endif %}</a>{% unless forloop.last %}
                    <span class='publication-author'> • </span>
                    {% endunless %}
                {% endfor %}
                </p>
                <p class='context'>{{site.data.venues[pub.venue].full}} {{pub.date | date: "%Y"}}</p>
                <div class='context links'>
                {% for link in pub.links %}
                    <a href="{{link.url}}">{{site.data.icons[link.icon]}} {{link.name}}</a>
                {% endfor %}
                </div>
                {% if pub.award %}
                <p class='context award'>{{site.data.icons['award']}} {{pub.award}}</p>
                {% endif %}
            </div>
        </div>
    {% endif %}
    {% endfor %}
    </div>
</div>


<div id='talks' class='cv-section'>
    <div class='cv-section-heading'>TALKS & PANELS</div>
    <div class='cv-section-content'>
    {% for talk in site.data.talks %}
        <div class='content' style='padding-bottom: 7pt'>
            <div class='title'>{{talk.title}}</div>
            {% assign sorted_talks = talk.talks | sort: 'date' | reverse %}
            {% for instance in sorted_talks %}
            <div class='entry' style='padding-bottom: 0'>
                <div class='date'>{{instance.date | date: "%b %Y"}}</div>
                <div class='description'>
                {% if site.data.venues[instance.venue] %}
                    {{site.data.venues[instance.venue].full}}
                {% else %}
                    {{instance.venue}}
                {% endif %}
                {% if instance.url %}
                    | <a href="{{ instance.url }}">{{ site.data.icons["recording"] }} Talk</a>
                {% endif %}
                </div>
            </div>
            {% endfor %}
        </div>
    {% endfor %}
    </div>
</div>


<div id='press' class='cv-section'>
    <div class='cv-section-heading'>PRESS</div>
    <div class='cv-section-content'>
    {% assign sorted_press = site.data.press | sort: 'date' | reverse %}
    {% for press in sorted_press %}
    <div class='entry'>
        <div class='date'>
            <div>{{press.date | date: "%b %Y"}}</div>
        </div>
        <div class='content'>
            <p class='title'>{{press.title}}</p>
            <p class='description'>{{press.author}}, {{press.publisher}}</p>
            <div class='context links'>
            {% for link in press.links %}
                <a href="{{link.url}}">{{site.data.icons[link.icon]}} {{link.name}}</a>
            {% endfor %}
            </div>
        </div>
    </div>
    {% endfor %}
    </div>
</div>

<div id='awards' class='cv-section'>
    <div class='cv-section-heading'>AWARDS & GRANTS</div>
    <div class='cv-section-content'>
    {% assign sorted_awards = site.data.awards | sort: 'date' | reverse %}
    {% assign last_year = "" %}
    {% for award in sorted_awards %}
        {% assign current_year = award.date | date: "%Y" %}
        <div class='entry'>
            <div class='date'>
                {% if current_year != last_year %}
                <div>{{award.date | date: "%Y"}}</div>
                {% assign last_year = current_year %}
                {% endif %}
            </div>
            <div class='content'>
                <p class='title'>{{award.title}}</p>
                <p class='context'>{{award.description}}</p>
            </div>
        </div>
    {% endfor %}
    </div>
</div>

<div id='teaching' class='cv-section'>
    <div class='cv-section-heading'>TEACHING</div>
    <div class='cv-section-content'>
    {% for course in site.data.teaching %}
        <div class='entry'>
            <div class='date'>
                <div>{{course.semester}}</div>
            </div>
            <div class='content'>
                <p class='title'>{{course.name}}</p>
                <p class='description'>{{course.role}}</p>
                <p class='context'>
                    {% if course.professors.size == 1 %}Professor: {% endif %}
                    {% if course.professors.size > 1 %}Professors: {% endif %}
                    {% for professor in course.professors %}
                    {% assign person = site.data.people[professor] %}
                    <a class='publication-author' href="{{person.url}}">{{person.name}}</a>{% unless forloop.last %}
                    <span class='publication-author'> • </span>
                    {% endunless %}
                    {% endfor %}
                </p>
                <p class='context'>{{course.description}}</p>
                <div class='context links'>
                    {% for link in course.links %}
                        <a href="{{link.url}}">{{site.data.icons[link.icon]}} {{link.name}}</a>
                    {% endfor %}
                </div>
            </div>
        </div>
    {% endfor %}
    </div>
</div>

<div id='service' class='cv-section'>
    <div class='cv-section-heading'>SERVICE</div>
    <div class='cv-section-content'>
    <div class='group'>
        <p class='title offset'>Research Mentor</p>
        {% assign sorted_students = site.data.students | sort: 'graduation-date' | reverse %}
        {% for student in sorted_students %}
        <div class='entry'>
            <div class='date'>
                <div>{{student.duration}}</div>
            </div>
            <div class='content'>
                <p class='description'><a href="{{site.data.people[student.name].url}}">{{site.data.people[student.name].name}}</a></p>
                <p class='context'>
                {{student.school}} {{student.degree}} {{student.graduation-date | date: "%Y"}}
                {% if student.current-position %}
                &#x2192; {{student.current-position}}
                {% endif %}
                </p>
            </div>
        </div>
        {% endfor %}
    </div>
    <div class='group'>
        <p class='title offset'>Organizer</p>
        {% for service in site.data.service %}
        {% if service.role == "organizer" %}
        <div class='entry'>
            <div class='date'>
            </div>
            <div class='content'>
                <p class='description'>
                {{site.data.venues[service.name].full}} 
                {% for year in service.years %}
                    {% if forloop.last and forloop.length > 1 %}and {% endif %}{{ year }}{%if forloop.length > 2 %}{% unless forloop.last %}, {% endunless %}{% endif %}
                {% endfor %}
                </p>
            </div>
        </div>
        {% endif %}
        {% endfor %}
    </div>
    <div class='group'>
        <p class='title offset'>Program Committee</p>
        {% for service in site.data.service %}
        {% if service.role == "program committee" %}
        <div class='entry'>
            <div class='date'>
            </div>
            <div class='content'>
                <p class='description'>
                {{site.data.venues[service.name].full}}
                {% for year in service.years %}
                    {% if forloop.last and forloop.length > 1 %}and {% endif %}{{ year }}{%if forloop.length > 2 %}{% unless forloop.last %}, {% endunless %}{% endif %}
                {% endfor %}
                </p>
            </div>
        </div>
        {% endif %}
        {% endfor %}
    </div>
    <div class='group'>
        <p class='title offset'>Reviewer</p>
        {% for service in site.data.service %}
        {% if service.role == "reviewer" %}
        <div class='entry'>
            <div class='date'>
            </div>
            <div class='content'>
                <p class='description'>
                {{site.data.venues[service.name].full}}
                {% for year in service.years %}
                    {% if forloop.last and forloop.length > 1 %}and {% endif %}{{ year }}{%if forloop.length > 2 %}{% unless forloop.last %}, {% endunless %}{% endif %}
                {% endfor %}
                </p>
            </div>
        </div>
        {% endif %}
        {% endfor %}
    </div>
    <div class='group'>
        <p class='title offset'>Student Volunteer</p>
        {% for service in site.data.service %}
        {% if service.role == "student volunteer" %}
        <div class='entry'>
            <div class='date'>
            </div>
            <div class='content'>
                <p class='description'>
                {{site.data.venues[service.name].full}}
                {% for year in service.years %}
                    {% if forloop.last and forloop.length > 1 %}and {% endif %}{{ year }}{%if forloop.length > 2 %}{% unless forloop.last %}, {% endunless %}{% endif %}
                {% endfor %}
                </p>
            </div>
        </div>
        {% endif %}
        {% endfor %}
    </div>
    <div class='group'>
        <p class='title offset'>Member</p>
        {% for service in site.data.service %}
        {% if service.role == "member" %}
        <div class='entry'>
            <div class='date'>
            </div>
            <div class='content'>
                <p class='description'>
                {{site.data.venues[service.name].full}}
                </p>
            </div>
        </div>
        {% endif %}
        {% endfor %}
    </div>
    {% for item in site.data.volunteer %}
        <div class='entry'>
            <div class='date'>
                {% assign start_year = item.start | date: "%Y" %}
                {% assign end_year = item.end | date: "%Y" %} 
                <div>
                    {% if end_year %}
                        {% if start_year == end_year %}
                            {{start_year}}
                        {% else %}
                            {{start_year}}–{{end_year}}
                        {% endif %}
                    {% else %}
                        {{start_year}}–Present
                    {% endif %}
                </div>
            </div>
            <div class='content'>
                <p class='title'>{{item.name}}</p>
                <p class='description'>{{item.role}}</p>
                <p class='context'>{{item.description}}</p>
            </div>
        </div>
    {% endfor %}

    </div>
</div>

</div>