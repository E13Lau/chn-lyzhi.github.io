
---
layout: post
title:  "jekyll + GitHub 博客搭建"
date:   2015-07-10 10:32
categories: jekyll update
tags: other
---

`_config.yml`文件

```
# Site settings
title: 非生物
# email: chn.lyzasd(@)gmail.com
description: > # this means to ignore newlines until "baseurl:"
   闻道有先后
baseurl: "" # the subpath of your site, e.g. /blog/
url: "http://yourdomain.com" # the base hostname & protocol for your site
github_username:  chn-lyzhi

# Build settings
markdown: redcarpet

# 分页 0为不分页
paginate: 50
```

其中需要修改title、description、github_username、markdown

文章名格式
`yyyy-MM-DD-文件名`


参考：
－ <http://jekyllcn.com/docs/assets/>
－ <http://www.devtalking.com/articles/git-gitHub-markdown-jekyll/>
- <http://dylanninin.com/blog/2013/11/02/free_blogs.html>