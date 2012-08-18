Ad_man
======

Ad_man is an advertising manager mountable engine.  It allows the user to upload and manage advertising banners, and provides an easy to use helper for inserting the banners on your website.  Also counts the number of times an ad has shown, and the number of times an advertisement has been clicked on.  The user must set a keyword for each ad.

Currently supports two image sizes for advertising: Leaderboard 728 x 90 and Banner 468 x 60. 
TODO: Will implement 9 different sizes as mentioned by google's adwords requirements.

Requires Paperclip 3.1, and requires ImageMagick be running on the server.

## Getting started

Ad_man works with Rails 3.2 onwards. You can add it to your Gemfile with:

```ruby
gem 'ad_man'
```

After you install Ad_man and add it to your Gemfile, you need to run the generator:

```console
rails generate ad_man:install
```

This will install the migrations and a few controller files, then just rake the database:
```console
rake db:migrate
```

See where Ad_man is located by running: 
```console
rake routes
```

In our case, we needed to move the line generated by the install in the routes file to our admin space.  Then add any before_filters to the controllers that were generated.

Make sure to change references to the application using the main_app helper:
```erb
<%= link_to "Home", main_app.root_path %>
<%= link_to "Advertising", main_app.ad_man_path %>
```

## Changing default values

If you need to change the default values set by ad_man, you will need to create an ad_man.rb initializer in your config/initializers folder.  

```ruby
# AdMan Default Values
AdMan.leaderboard_size = "728x90"
AdMan.banner_size = "468x60"
AdMan.max_image_size = 50 # 50Kb maximum image size

# These are configurable dimensions (currently leaderboard default)
AdMan.image_dimensions_width = 728
AdMan.image_dimensions_height = 90

# Configurable content type for advertising
AdMan.content_type = ["image/jpg", "image/bmp", "image/png", "image/gif", "image/jpeg"]

# Configurable max advertising for keyword
AdMan.max_count = 6
```

## Putting an advertisement in the view

To put your advertisement in the view just add:
```erb
<%= link_to_ad %>
```
Currently there are three parameters that can control which ads get shown on your page.  :keyword, :size, and :display_on_all_pages.  
```erb
<%= link_to_ad :keyword => "Your Keyword", :size => "leaderboard", :display_on_all_pages => false %>
```

## Ad_man and Javascript
Ad_man supports inserting an advertisement using jQuery.  It also uses jQuery in the backend when creating new ads.  To use this functionality, include this line in the view:
```erb
<%= javascript_include_tag "ad_man/advertisements.js" %>
```

You can pass the keyword name , size of the advertisement and the id of the `<DIV>` element to show advertisemnet through the showAd(); function.  
```erb
<script>
// showAd(keyword);
AdMan.showAd('keyword', 'size', 'div_id');
</script>
```
Then add a `<DIV>` element with the id you pass to the showAd function where you want the advertisement to show.  
```erb
<div id="advertisement"></div>
```

## Authors
Written by [David Strand](http://www.github.com/wspyder) and [Tyler Hu](http://www.github.com/tylerhu)

## Contributors
[Matenia Rossides](http://www.github.com/matenia)

## Copyright & Licensing

Copyright (c) 2012 [Kudelabs](http://kudelabs.com)

Released under MIT License. 
