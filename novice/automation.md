---
layout: post
title:  "Automation in bash shell"
date:   2016-01-26 02:16:12 -0600
categories: jekyll update
---

<div class="panel panel-warning">
  <div class="panel-heading">
    
    <h4 class="panel-title"><span class="glyphicon glyphicon-exclamation-sign" aria-hidden="true"></span> Prerequisites </h4>
  </div>
  <div class="panel-body">
   This lesson guides you through the basics of file systems and the shell. If you have stored files on a computer at all and recognize the word “file” and either “directory” or “folder” (two common words for the same thing), you’re ready for this lesson.
  </div>
</div>

### before start,
here is the data http://swcarpentry.github.io/shell-novice/shell-novice-data.zip 

Download, copy into your Desktop, unzip.

I expect you use Mac.

To move into your foler type
```
cd ~/Desktop/data-shell
```
## 1. for loop
Let's learn for loop. To print what files are in you forder /data/pdb, you can try this 
~~~
echo "My file name is aldrin.pdb"
~~~

to automate,

~~~
for x in data/pdb/*.pdb ; do echo "My File name is $x";done
~~~

## 2. use shell script
pick up your favorate editor (eg. emacs, vim)

~~~
emacs auto.sh
~~~

type this

~~~
#!/bin/bash
cd ~/Desktop/data-shell
for x in data/pdb/*.pdb ; do echo "My File name is $x";done
~~~

to run this

```
bash auto.sh
```

## 3. make file
make, make all, etc. 
This will be described later