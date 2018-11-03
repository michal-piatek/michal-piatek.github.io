<ul>
  {% for post in site.posts %}
    <li>
      {{ post.excerpt }}
      <a href="{{ post.url }}">More ...</a>
    </li>
  {% endfor %}
</ul>
