---
layout: post
title: My first Rubygem - Stylecheck
date:   2017-01-23 13:30:00
categories: main
banner_image: "rubygem.jpg"
summary: Stylecheck is the first rubygem created and published recently by me.

---

The **Stylecheck** gem provides a bunch of rake tasks to run code style checks.
Currently it supports `Ruby` (via `rubocop`) and `SCSS` (via `scss-lint`). I will be adding more
languages to it very soon. Typically one would hook it up to CI to run it along with the application tests.
One shortcoming of this approach is that unlike HoundCI it runs checks on all included files, not just the
changed ones.
Check it out [here](https://github.com/soumyaveer/stylecheck).
