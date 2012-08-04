---
layout: post
title: "Redbox - A rails compatible lightbox"
date: 2006-08-16 03:34
comments: true
categories: 
---
*[Redbox is no longer supported]*

Lightbox, and all it's similarly named siblings, is a colleciton of javascript and css designed to show off some page content, such as an image, or a div, in a floating box in the center of the page, while the rest of the page appears dimmed behind it. 

This is as good a way as any to do the kind of 'modal popup' that if familiar in desktop applications. However, I couldn't find such a library that was fully compatible with rails ajax functionality, and I have a client needing multi-page forms within such a box.

So, I've created one as a rails plugin. Rather predictibly named 'Redbox', this plugin is heavily based on Codey Linley's "Thickbox":http://jquery.com/demo/thickbox/ library.   However, thickbox uses JQuery, which is yet another big javascript library, and I've chosen to use prototype instead for Redbox, as most rails sites already use it.

## Installation

Redbox is a rails plugin. You can install it using:

    script/plugin install svn://rubyforge.org/var/svn/ambroseplugins/redbox

Please not that this copies three files into the appropriate public directories, being redbox.js, redbox.css and redbox_spinner.gif. If you already have files with these names, they will be overridden.

If you are updating an existing redbox installation, or if you accidentally delete those files, you can have them copied into the right spots again by typing the following from within you vendor/plugins/redbox directory

    rake update_scripts

## Setup

All you need to do is include the javascript and css files into your layout. You'll also need to include the default rails javascript files (if you aren't already).

```erb
<%= stylesheet_link_tag 'redbox' %>
<%= javascript_include_tag :defaults %>
<%= javascript_include_tag 'redbox' %>
```

## Usage

Redbox provides three helpers which are used instead of a regular "link_to" helper when linking to a redbox.

```ruby
    link_to_redbox(name, id, html_options = {})
```

This is used if you already have an HTML element in your page (presumably hidden, but it doesn't have to be) and you wish to use it for your redbox. Specify it by it's id, and you're in business.

```ruby
    link_to_component_redbox(name, url_options = {}, html_options = {})
```

This serves essentially the same purpose, but it uses the url_options supplied to load another page from your app into a hidden div on page load. This saves you having to do it yourself, but beware that there are definate performance implications to using components.

```ruby
    link_to_remote_redbox(name, url_options = {}, html_options = {})
```

This waits until the link is clicked on to load the redbox using ajax, and displays loading graphics while it's waiting. 

```ruby
    link_to_close_redbox(name, html_options = {})
```

Allows you to put a link (presumably inside the redbox) to close it. Other way to close it is to refresh the entire page, but obviously closing it with javascript is spiffier.

That's really all there is too it. It's no doubt far from perfect, and it hasn't been tested outside of firefox and safari yet, so I'd welcome any feedback.