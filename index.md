Andrew is an experienced technical consultant and developer with over 13 years of experience. Throughout his career, Andrew has worked across disciplines which include Consulting, Web Development, Cyber Security, IT Support, Project Management, and Game Design.

[LinkedIn](https://www.linkedin.com/in/andrew-dickinson-8a78a623/)

## Posts

<ul>
    {% for post in site.posts %}
    <li>
        <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
        <p>{{ post.date | date_to_long_string }}</p>
        <p>{{ post.excerpt }}</p>
    </li>
    {% endfor %}
</ul>