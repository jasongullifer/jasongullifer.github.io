---
title: New site updates!
author: Jason Gullifer
tag: 
tags: [jekyll, "paper repository", "web development", blog]
layout: post
---

I made some new changes to my academic website. 

- Added a blog so I can post additional thoughts and musings. With any luck, I'll keep it updated (and typo-free). 
- Added a somewhat automatic academic paper repository so that I can make (free) preprints of papers available to anyone who wants to read them. 
- I changed around some of the underlying site structure.

I thought I'd make a record of some of these changes, so that I remember what I did in the future. Maybe someone else will be interested in creating something similar. 

My website is written with [Jekyll](https://jekyllrb.com/) using the [skeleton]( http://getskeleton.com/) design/theme. It's hosted on [github](https://github.com/jasongullifer/jasongullifer.github.io).

__Jekyll__ is a tool for generating static websites, and it has all the functionality you need to create a blog and a collection of papers. __Skeleton__ is a fluid page design, so it's adaptable to many different screen sizes (including mobile). A full tutorial on these is beyond the scope of this post, so for now, I'm assuming that you already have a Jekyll site. 

# Creating my blog with Jekyll

## Making blog posts
With Jekyll, you write each blog post as a markdown file, and you save them in your ```_posts/``` directory. Filenames should be in the format ```YYYY-MM-DD-title-of-your-post.md```. When you upload to your host (e.g., GitHub), each markdown post will be converted to HTML and appear in your website's root (by default). 

For example, you can see the markdown for my first post on bilingualism [here](https://github.com/jasongullifer/jasongullifer.github.io/blob/master/_posts/2021-11-26-what-is-bilingualism.md?plain=1).

If you want some additional structure for your blog (i.e., besides a bunch of HTML files created in your site root), you can add a permalink line your ```_config.yml``` file. E.g., this line

```
permalink: /blog/:categories/:year/:month/:day/:title/
```

stores posts under ```your-site-root.com/blog/category/YYYY/MM/DD/title-of-your-post```.

## Making the blog landing page

Now you have blog posts! But you still need a landing page that organizes all the posts. You create this as a normal Jekyll page. You can see my blog.html page [here](https://github.com/jasongullifer/jasongullifer.github.io/blob/master/blog.html). The page contains some  Jekyll code that loops over each blog post in ```_posts/```, adding it to the page. You can loop over tags, categories, etc. so that you can further categorize your blog entries.

E.g. this code will order posts by date, then categorize posts by tag. (This code is in an image format because I could not get the code block working!)

<img src="/images/blog/jekyll_blog_page_code.png" alt="blog landing page code" width="700">

That's basically it! Now you just write your blog posts and put them in ```_posts/```. They will then show up on the blog landing page. Draft posts can be added to ```_drafts/``` and they won't be published. 

# Creating an academic paper repository with Jekyll collections

There's probably multiple ways to create a paper repository in Jekyll. I used Jekyll ```collections```. Collections group related pieces of content. I created a papers collection, and added code to loop over every paper in my collection. Here are the steps I took:

- I created a ```files/preprints/``` directory to house all of my preprint PDF files.
- I created a ```_papers/``` directory to hold markdown files that house the metadata for each paper (one ```md``` file per paper). The metadata is stored as YAML front matter, with keys e.g. ```id``` (i.e., Zotero id), ```date```, ```title```, ```authors```, etc. There's also a key for ```filename``` which refers to the filename within the ```files/preprints/``` directory. 
  - I exported my papers from Zotero to ```Better CSL YAML``` format, and then I just manually grabbed the relevant keys from that file. In the future, I should write a python script to create my markdown files automatically. Or, maybe a more sensible option would be to store this YAML file in the ```_data/``` directory and parse loop through that instead.
- I added a ```papers``` collection to my ```_config.yml```. This collection corresponds to the ```_papers/``` directory above. I also added a key to sort the collection by ```year```. See the following code:

```
collections:
  papers:
    sort_by: year
```

- I wrote a ```papers.html``` page. It has code to loop through each paper in the ```_papers/``` directory and print out the keys in a quasi-apa format that includes links to the PDF files. Code is [here](https://github.com/jasongullifer/jasongullifer.github.io/blob/master/papers.html).

Next steps will be to make the paper markdown generation more automatic!