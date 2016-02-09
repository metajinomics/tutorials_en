---
layout: post
title:  "Setup github website"
date:   2016-02-09 16:59:12 -0600
categories: jekyll update
---

### 1. set up main page


#### Create a new repository named username.github.io
#### install jekyll
~~~
jekyll new username.github.io
cd username.github.io/
git init
git checkout --orphan gh-pages
git remote add origin https://github.com/username/username.github.io.git
git add --all
git commit -m 'first'
git push --set-upstream origin gh-pages
~~~


### 2. how to post
you need to put this on the top
~~~
---
layout: post
title:  "Setup github website"
date:   2016-02-09 16:59:12 -0600
categories: jekyll update
---
~~~

### 3. set up project page
~~~
jekyll new name_repository
cd name_repository/
git init
git checkout --orphan gh-pages
git remote add origin https://github.com/username/name_repository.git
git add --all
git commit -m 'first'
git push --set-upstream origin gh-pages
~~~
Don't forget you need to change config
