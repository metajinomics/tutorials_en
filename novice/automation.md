---
layout: post
title:  "Automation in bash shell"
date:   2016-01-26 02:16:12 -0600
categories: jekyll update
---

<div class="panel panel-warning">
  <div class="panel-heading">
    
    <h4 class="panel-title"><span class="glyphicon glyphicon-exclamation-sign" aria-hidden="true"></span> Learning Objectives </h4>
  </div>
  <div class="panel-body">
    Panel content
    *   Go through the modify-add-commit cycle for single and multiple files.
    *   Explain where information is stored at each stage of Git commit workflow.
  </div>
</div>


automation. Download data. 

## 1. for loop 
~~~
python something.py input output
~~~

to automate,

~~~
for x in globus/*hof/somthing*.fa ; do python something.py $x $x.output;done
~~~

## 2. use shell script
pick up your favorate editor (eg. emacs, vim)

~~~
emacs auto.sh
~~~

type this

~~~
for x in globus/*hof/somthing*.fa ; do python something.py $x $x.output;done
~~~

## 3. make file
make, make all, etc. 
