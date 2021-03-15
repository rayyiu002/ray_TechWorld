## Framework Template

**Carte** is a simple Jekyll based documentation website for APIs. It is designed as a boilerplate to build your own documentation and is heavily inspired from [Swagger](http://swagger.wordnik.com/) and [I/O docs](http://www.mashery.com/product/io-docs). Fork it, add specifications for your APIs calls and customize the theme. <small>Go ahead, see if we care.</small>

## Installation 

1. Clone this repository on your local,
2. [Install Jekyll](https://github.com/mojombo/jekyll/wiki/install),
3. Go at the root of the repository and run ```jekyll serve --watch```,
4. Go to http://localhost:4000,
5. [Great success! High five!](http://www.youtube.com/watch?v=wWWyJwHQ-4E)

## Grouping calls

Adding a category to your YAML header will allows you to group methods in the navigation. It is particularly helpful as you start having a lot of methods and need to organize them. For example:

```
---
category: Stuff
path: '/stuff/:id'
title: 'Delete a thing'
type: 'DELETE'

layout: nil
---
```

## Edit the design

The default UI is mostly described through the `css/style.css` file and a couple short jQuery scripts in the `/_layouts/default.html` layout. Hack it to oblivion.
