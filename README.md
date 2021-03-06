# Singlepage-Jekyll

A simple Jekyll plugin to make content load dynamically using pagify.js.

## Description

Pagify.js is a great jQuery plugin to make simple one-page websites, with content loading dynamically. The only problem with it is that you have to define every page you want to load manually. This is fine for a static page, but it get's in the way when you're hosting a website with regularly updated content. This plugin aims to solve that. 

It generates a JSON file of all your pages, which you can pass to pagify.js.

## Usage

### Files

Place "singlepage-jekyll.rb" in _plugins, "root" in _includes, and jquery-min.js and pagify.js in your website root. Install ruby-json:

```
gem install json
```

### Setup

Create a layout in _layouts, such as default.html. Load Pagify and jQuery:

``` html
<script src="jquery.min.js" type="text/javascript"></script>
<script src="pagify.js" type="text/javascript"></script>
```

Then go on and add the following:

```html
<body>
{% include root %}
{{ content }}
</body>
```

Create a page with the layout default. Create a div that will contain page content:

``` html
<div id='page_holder' />
```

Call __pagify__ on the aforementioned div and pass in options. _The only required option is `pages`._

``` js
$.getJSON('html.json', function(data) {
   $('#page_holder').pagify({ 
       pages: data, 
       default: 'home'
   }); 
});
```

Link to other pages by linking to hashes of their page names:

``` html
<a href='#contact'>Contact</a>
<a href='#about'>About</a>
```
Or like this:

```html
{% for post in site.posts %}
<a href="#{{ post.id }}">{{ post.title }}</a>
{% endfor %}
```

All the pages you want to call don't need a layout, as their content will just be loaded within a div on the page. To learn more about the options of pagify.js, check out [it's Github page](http://github.com/cmPolis/Pagify).

### Everything else

This is just a first version. Feel free to improve and send a pull request.

Made by [Jacob Klapwijk](http://jcbk.me).

MIT licensed.
