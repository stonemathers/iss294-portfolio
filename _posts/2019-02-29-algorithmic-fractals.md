---
layout: post
title:  "Algorithmic Fractals"
date:   2019-02-19
categories: blogs
---

![Fractals Piece 1](/assets/images/fractals1.png "Fractals Piece 1")

{% for post in site.posts %}
    {% if post.title == "Blog Post - New Media Artists II" %}
The idea for this piece was inspired by LIA's Tentasho, which I discuss in <a href="{{ post.url }}">{{ post.title }}</a>. Of course, my version is quite simplified, but still uses the interplay of a flowing brushes and emerging fractals. Unlike LIA's piece, I wanted to add a level of interactivity with the fractals once they are created. In addition, I play with color blend properties to allow users to easily create intricate and stunning visuals. At any point, the user can claim they are finished, or with a few simple inputs create an entirely different piece.
    {% endif %}
{% endfor %}

![Fractals Piece 2](/assets/images/fractals2.png "Fractals Piece 2")

To interact with this piece, click and drag in empty space to begin drawing. On release, a fractal is drawn. This fractal can then be used as a "brush", either dragging it around the screen, or rotating it by holding the 'a' key or space bar while dragging. The 'a' key will slowly rotate the fractal, while the space bar will cause a much more sporadic rotation. The 'r' key can be pressed to reset the canvas.

Try it out [here](https://stonemathers.github.io/iss294-algorithms/)!