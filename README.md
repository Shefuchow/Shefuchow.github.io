# Jekyll Startup ReadMe
### Author: Sefath

## Requirements 
> - Need Ruby -> comes installed on mac -> check with `ruby -v` -> I'm using Version 2.6.3
> - Need Gems -> package manager for ruby -> check `gem -v` -> I'm using Version 3.0.3
> - Need Jekyll Framework -> use `gem install jekyll bundler` -> check with `jekyll -v`

---
## Code Scaffold
run `jekyll new <blogName>`
```
.
├── 404.html
├── Gemfile
├── Gemfile.lock
├── _config.yml
├── _posts
│   └── 2019-12-18-welcome-to-jekyll.markdown
├── about.markdown
└── index.markdown

.
├── 404.html
├── Gemfile *All Gem Dependancies*
├── Gemfile.lock
├── _config.yml *Site Settings*
├── _posts
│   └── *All Posts*
├── _site *Final Outputted Site*
│   ├── 404.html
│   ├── about
│   │   └── index.html
│   ├── assets
│   ├── feed.xml
│   ├── index.html
│   └── jekyll
├── about.markdown
└── index.markdown
```

## Serve up Boiler Plate
run `cd <blog>` and then `bundle exec jekyll serve`

---
## Front Matter
Front matter is information about our blog post 
example:
```
---
layout: post
title:  "Welcome to Jekyll!"
date:   2019-12-18 13:43:06 -0500
categories: jekyll update
---
```
Front Matter can be written in YAML or JSON -> both of these languages really just store key value pairs for specified fields. Above is just the default front matter, you can add your own -> ex:\ "Author: Mastershefu" \
Even all pages have frontmatter in ex: index.markdown / about.markdown files. \
https://jekyllrb.com/docs/front-matter/ \
One front matter variable that I would Highly reccomend is Permalink -> defining permalinks in the beginning can very useful when you have dependance page/posts structures and you change one post, and the link is permanent so jekyll won't auto update and break your existing links \
You can also set default front matter that you want to create with any new page or post generation, so you dont have to manually add those fields everytime. You do this in the config.yml file, aka your "Jekyll site settings" \
Example: \
```
# Build settings
markdown: kramdown
theme: minima
plugins:
  - jekyll-feed
defaults: 
  - 
    scope:
      path: "" 
      type: "post"
    values:
      #values
      layout: "post"
```

---
## Writing Posts
Under the _posts folder, each new post would be titled in this format: \
year-month-day-title-hyphenated.markdown \
ex: \
2019-08-13-hey-whats-up.markdown \
Each post must have front matter, and thats how Jekyll would know how to style the post, and add the correct metadata \
\
You can even create new directories to organize post by directory or category or however you choose \
\
You can also create a `_draft` directory to have draft posts that you dont want to post yet
and you can see how everything looks with `jekyll serve --draft` 

## Creating Pages
Creating Pages is similar to creating posts. We can take a look at about.markdown for an example in the root directory of the project. \
Page contents example: \
`helloWorld.md`
```
---
layout: page
---
Some content
```

## Jekyll Themes
https://rubygems.org/search?utf8=%E2%9C%93&query=jekyll-theme
http://jekyllthemes.org/
http://jekyllthemes.org/themes/jekyll-theme-prologue/
https://jekyller.github.io/jasper2/
http://artemsheludko.com/bef/
http://artemsheludko.com/adam-blog/
https://nrandecker.github.io/particle/
http://jekyllthemes.org/themes/frisco/
https://portfolio-central.github.io/jekyll-instagram-portfolio-theme/
http://jekyllthemes.org/themes/moon/ ***
http://jekyllthemes.org/themes/siera/
http://knaman2609.github.io/clean/
https://liabogoev.com/?s=hello
https://github.com/thesowah/GridGallery

## Layouts
In your front matter, you noticed layouts, and those are generally tied with layouts in a _layouts directory right under your root directory. \
An example layout can be: \
`post.html` 
```
<h1 style="background-color: aqua;">This is a post</h1>

<hr style="background-color: burlywood;"> {{ content }}
```
This would be to customize an existing layout. But you can also make custom layouts such as: \
`photoCardForAPost.html`
```
<div class="col-md-4 probootstrap-animate" data-animate-effect="fadeIn">
    <a href="photos.html" class="img-bg" style="background-image: url(img/image_001.jpg);">
        <div class="probootstrap-photo-details">
            <h2>Titile</h2>
            <hr> {{ content }}
        </div>
    </a>
</div>
```
You can use the {{ curley braces }} to access variables, loop through data, use conditionals, etc. \
Jekyll also supports layout inhertance, so layouts can inherit the properties of a parent layout. \
#### Variables
You can access layout level variables -> page level variables -> site level variables

#### Includes
You can inject html into your site page with includes (use cases are like a header, footer, navigation menu (hamburger menu) \
You do this in an _includes folder in  the root directory of your project folder \ 
and include it in your layouts with -> ` {% include header.html %}`
you can even put variables to access from that include statement from your layout file -> `{% include header.html color="blue" %}`

#### Loops
Loop through all your blog posts
```
{% for post in site.posts %}
  //do something
  //example
  {{ post.url }} <br>
{% endfor %}
```
//or
```
<ul class="social-buttons">
{% for social in site.socials %}
    <a href="{{ social.link }}"><i class="fab fa-{{ social.name }}"> &NonBreakingSpace;</i></a>
{% endfor %}
<ul>
```

#### Conditionals
```
{% if //conditions and //condition or //condition %}
{% elsif %}
{% endif %}
```
example building active link in navigation bar
```
{% for post in site.posts %}
  <li><a class={% if page.url == post.url %}"active"{% endif %}>{{ post.url }}</a></li>
{% endfor %}
```

#### Data Files
if you wanted to simulate a database -> you can create a _data directory in the root directory \
you can create YAML files in here that have data you might need to constantly reference, such as: \
`team.yaml`
```
- name: "Batman"
  occupation: "Billionaire" 

- name: "Superman"
  occupation: "Alien"

- name: "Ezio Auditore"
  occupation: "Assassin"  
```
Then you access this information on Jekyll layouts: \
`Team.html`
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Team Page</title>
</head>
<body>
    <h1> This is our team </h1>
    <ul>
    {% for person in site.data.team %}
      <li> Meet {{ person.name }}, a full time {{ person.occupation }} </li>
    {% endfor %}
    </ul>
</body>
</html>
```

#### Static Files
Static files as far as Jekyll is concerned is any file that doesn't have front matter, that includes javascript files, css files, images, etc. \
You can create an assets folder in the root directory and utilize it for static files. \
example: \
```
Assets
├── catMeme.jpeg
├── awesomeLogo.png
└── Resume.pdf
```
You can loop through this in any layout with 
```
{% for file in static.static_files %} 
  {{ file.path }} <br> //file.name file.ext file.basename
{% endfor %}
````
You can also configure front matter for your assets like for example: \
if you make an img folder under assets, and that img folder hold all your images, you can give front matter to all your images -> in _config.yml \
```
defaults:
  - scope: 
      path: "/assets/img"
    values: 
      image: true
```
anytime you edit the _config.yml file, you want to run the `bundle exec jekyll serve` command \
you can then display all your images like this:
```
{% for file in static.static_files %} 
  {% if file.image %}
    <img src = "{{file.path}}" alt="{{file.name}}">
  {% endif %}
{% endfor %}
```




#### Content Management Software
https://www.siteleaf.com/

#### Comparing Jekyll vs Hugo
https://forestry.io/blog/hugo-and-jekyll-compared/
