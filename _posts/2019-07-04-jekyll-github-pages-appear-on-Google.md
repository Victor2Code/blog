---
layout: post
title: Make your Jekyll Github Pages appear on Google search result (2 steps)
tags: Jekyll
comments: true
last-modified: 2019-07-06 00:47:00 +0800
---

There is no point to make a website if it can not be indexed on Google, so lets take a look at how to make your site and pages appear on Google search result.

## Google search console
You need to use this system provided by Google to accomplish this task. Simply log in to [this system](https://search.google.com/search-console/about) with your Google account, and click "Start now".

## Owner verification
The first step is to let Google know you are the owner of a site, which is identified as a property here. Obviously, you can have a lot of properties.

* Select `URL prefix` as your property type, and input your website address, e.g. `https://victor2code.github.io/blog/`  

  ![select property type]({{ "/images/select_property_type.png" | relative_url }})

  The address you put here should be the root folder of your website, which is the place your `index.html` resides. If you have multiple sites under your github pages, you can register one property for each of them.

* Choose one of the method the website provides to do the verification.  

  The first option would be the easiest way to do that, all you need to do is to download an html file and upload to your website root folder. But unfortunately I tried many times to do the uploading, google failed to identify the file, even though I can access it via url.  

  So I use the second option to accomplish the verification. The goal is to add an html tag to your homepage `<head>` tag. Below steps apply to **minima** theme.

  * Copy `_includes/head.html` from github to your website if it is not there

  * Edit `head.html` to add the tag provided by google in between the `<head>` tag like below
{% raw %}
  ```html
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    {%- seo -%}
    <link rel="stylesheet" href="{{ "/assets/css/style.css" | relative_url }}">
    {%- feed_meta -%}
    {%- if jekyll.environment == 'production' and site.google_analytics -%}
      {%- include google-analytics.html -%}
    {%- endif -%}
    <meta name="google-site-verification" content="P5JvIrpAzGuAYMCBT3_-1TEpWsUUoQAaYK3B6hgaauA" />
  </head>
  ```
  {% endraw %}

  * Click **verify** button, and you are done with it. It may take few minutes for the meta data to take effect, so be a little patient.

  ![owner verification success]({{ "/images/verify_success.png" | relative_url }})

  * It may take hours to few days until you can see the performance about your website in the console


## Site Map
Okay, Google is aware of the existence of your website now. Next, you need to tell Google what your website hierarchy is, which is achieved by a file called **sitemap**.

**Sitemap** stores the structure of your site, like how many pages are there, and what is the url for each of them, something like that.

Github Pages can generate a site map automatically for your site, just simply follow this official [instruction](https://github.com/jekyll/jekyll-sitemap):

* add `gem: jekyll-sitemap` to `gemfile` file

* add  `plugins: - jekyll-sitemap` to your `_config.yml` file

* run `bundle exec jekyll serve`

* a file named `sitemap.xml` will generate automatically at the root folder of your site, such as `https://victor2code.github.io/blog/sitemap.xml` for this site. You shall be able to check it out via this url in browser

Then, you can submit the address of your sitemap file to Google Search Engine, prompting the Googlebot to analyze your site for indexing.

For my case, I could not search my site via site name until **2 days** after I submit the sitemap file. It takes some patience.

## URL Inspection
Yes! If everything goes smoothly, you site can be found via Google now, that is exciting.

But even you have submitted your sitemap to Google, certain pages just can not be indexed on Google search result. You can submit the url of the page to this URL Inspection tool, and Google will show you why your page can not be indexed, and how to solve the problem.

Follow the tips from Google and you shall be all covered.
