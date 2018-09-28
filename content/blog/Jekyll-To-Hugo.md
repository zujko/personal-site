+++
categories = ["jekyll","hugo","go","blog","static site"]
comments = false
date = "2017-06-01T18:21:35-07:00"
draft = false
showcomments = true
showpagemeta = true
slug = ""
tags = []
title = "Jekyll To Hugo"

+++
I've used [Jekyll](https://jekyllrb.com/) exclusively for my blog and personal site ever since I started maintaining a site. I used Jekyll because of its relative ease of use and because it's what you had to use for GitHub pages. 

I moved to using [Hugo](https://gohugo.io/) which is an awesome static site engine written in Go. Since to my knowledge you can't use Hugo on GitHub pages, I moved over to Gitlab pages which has support for a bunch of different static site generators.

## Creating a Hugo site
If you're like me and are just looking to use or modify an existing theme, Hugo is easy and flexible. Simply install Hugo and run ```hugo new site <site-name>```. This should create a directory with the following layout.
```
.
|-- archetypes
|-- config.toml
|-- content
|-- data
|-- layouts
|-- static
|-- themes

6 directories, 1 file
```

If you're interested in what these directories are for take a look at the quickstart [here](https://gohugo.io/overview/quickstart/).

I decided to modify a theme called [goa](https://github.com/shenoybr/hugo-goa).

Hugo doesn't come with a default theme, therefore you need to import one into the themes directory. So, simply clone the theme into the directory 

```git clone https://github.com/shenoybr/hugo-goa.git themes```

You then need to setup your config file. Hugo themes usually have an example config in a directory named ```exampleSite```, so just copy that to the root of your project, in my case ```cp themes/hugo-goa/exampleSite/config.toml .```

To override an existing template, all you have to do is copy the file you want to modify from the theme into the root directory, then just edit the copy in the project directory. So for example, I wanted to change the header. All I would do is 

```cp themes/hugo-goa/layouts/partials/header.html layouts/partials```


## Hosting on GitLab Pages
I'm not going to go into a lot of detail about how to host on GitLab. I'll just document my steps. If you'd like more information, there's a great guide [here](https://about.gitlab.com/2016/04/07/gitlab-pages-setup/).

In order to get something running you need a GitLab CI configuration file. What the configuration file does is it tells the GitLab runner what to do. For a basic Hugo setup your configuration file should look something like this.

```
image: alpine

variables:
  HUGO_VERSION: '0.20.7'
  HUGO_SHA: '04f2c7d2f6ea500b0ead4821f035f334b7ac370154509653391bfccec1c4d524'

before_script:
  - apk update && apk add openssl ca-certificates
  - wget -O ${HUGO_VERSION}.tar.gz https://github.com/spf13/hugo/releases/download/v${HUGO_VERSION}/hugo_${HUGO_VERSION}_Linux-64bit.tar.gz
  - echo "${HUGO_SHA}  ${HUGO_VERSION}.tar.gz" | sha256sum -c
  - tar xf ${HUGO_VERSION}.tar.gz && mv hugo* /usr/bin/hugo
  - hugo version

test:
  script:
  - hugo
  except:
  - master

pages:
  script:
  - hugo
  artifacts:
    paths:
    - public
  only:
  - master
``` 

Overall, I've loved Hugo and definitely recommend it.
