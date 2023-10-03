---
layout: layout
title: John Stechschulte
---

I'm a robotics perception scientist. You can find me on [LinkedIn](https://linkedin.com/in/johnstechschulte) and
[GitHub](http://github.com/JStech). I am available for consulting.

In 2008 I bicycled from Baltimore to Laguna Beach, and kept a [journal](bike_tour) on the way. In 2015 I bicycled from
Vancouver to San Diego (and did not keep a journal).

  <h3>Posts</h3>
  <div class="related">
    <ul>
      {% for post in site.posts %}
        {% unless post.pres %}
          <li>
          <span>{{ post.date | date: "%B %e, %Y" }}</span> &mdash; <a href="{{ post.url }}">{{ post.title }}</a>
          </li>
        {% endunless %}
      {% endfor %}
    </ul>
  </div>
