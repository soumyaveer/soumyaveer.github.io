---
layout: post
title: My first Ruby Gem
date:   2017-01-20 17:50:00
categories: main
banner_image: "binary.jpg"
summary: Creating a Ruby Gem might look like a difficult task, but the fact is that it is a very rewarding experience. In this post, I am sharing with you, my experience of creating a Ruby Gem and a short description of what the gem is about.

---

When I started learning Ruby, I knew that someday I will be creating my own Ruby gems.
But I was not aware that the day will come sooner than I thought. One day I was working
on a project and struggling with the code style-check when my husband came up with the
idea of creating a ruby gem for validating code style, which will  solve two purposes - one,
reducing the struggle of using wrong conventions while coding and second, as a good practice
for me to learn how to create a ruby gem. And hence , one week  after that I was publishing my
very own first gem - **Stylecheck**.


**Stylecheck** , as the name suggests, runs code style check on `Ruby` and `SCSS` files.
For example, while writing in English, you just can't put a full stop anywhere you want,
because if you do that it will be difficult for the readers to understand the context,
to the extent that it might  completely change the meaning of what you are trying to communicate.
In a similar fashion, in the world of coding there are conventions that should be followed by everyone.
This creates consistency in code and makes it easy to read and understand by other programmers.
This is exactly what `stylecheck` does. It checks the code for bad coding styles and informs
you regarding the same.<br><br>


**Stylecheck** has two dependencies  - `gem rubocop` and `gem scss_lint`.
In order to use it, first thing that needs to be done is adding the `gem stylecheck`
to  `GemFile` and install it  by  running `bundle install` . Next comes the configuring of
files `rubocop.yml` and `scss-lint.yml` .


```ruby
rake stylecheck:init
```


This command will create a `stylecheck` folder in the `config` of
the application that is using the gem and will add `rubocop.yml` and `scss-lint.yml` to it.<br><br>


Once this is done you are free to check your `Ruby` and `SCSS` files.

If you want to validate code style on `Ruby` files based on `config/stylecheck/rubocop.yml`,
run the command:

```ruby
 rake stylecheck:ruby
```
<br>



Similarly, if you want to validate the `SCSS` files code style based on `config/stylecheck/scss-lint.yml`
, run command:

```ruby
rake stylecheck:scss
```
<br>

And finally, to validate coding styles in both the files, `Ruby` and `SCSS` together,
all you have to do is execute command:

```ruby
rake stylecheck
```
<br>

So, once you get the errors, you can either correct them or go ahead and change
`rubocop.yml` and `scss-lint.yml` depending on what coding style conventions you are using.

This gem not only solved my problem of validating the coding style,
but also helped me learn a lot regarding creating the gem and the rake tasks.
The journey from planning to publishing this gem was filled with knowledge, fun and excitement.
