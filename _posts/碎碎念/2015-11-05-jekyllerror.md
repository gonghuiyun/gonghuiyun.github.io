---
layout: post
title: 执行jekyll serve出现的几个错误以及解决方法
category: 碎碎念
tags: git
keywords: 
description:
---
###**1、提示jekyll未安装**
这个问题我郁闷了好久，重新安装了jekyll仍出现这样的提示。试着执行了`ruby -v`，却看不到已经安装的ruby的版本。于是执行`rvm use 2.0.0`
可是又出现了如下错误提示：  

``` c
RVM is not a function, selecting rubies with 'rvm use ...' will not work.
```

经过一番搜索，先执行`bash -login`之后再执行`rvm use 2.0.0`就成功了。再查看ruby的版本，是正确的。然而...
执行`jekyll serve`却又出现如下错误：  

``` c
jekyll 3.0.0 | Error:  Permission denied @ rb_sysopen
```
再一检查，发现是因为不是root用户。于是切换root后，重新执行`bash -login`之后再执行`rvm use 2.0.0`就好了。

###**2、出现如下提示：**
```
error > Deprecation: You appear to have pagination turned on, but you haven’t included the jekyll-paginate gem. Ensure you have gems: [jekyll-paginate] in your configuration file.
```
谷歌了好久，有的说是将jekyll-paginate这个插件加到_config.yml中，即在_config.yml里面加一句: gems: [jekyll-paginate]，然而问题并没有解决。于是想出了一个馊主意：将配置文件_config.yml中用于实现分页功能的语句`paginate: 10`暂时注释掉，再执行`jekyll serve`,终于成功了！此时再将注释符号去掉，保存，OK！虽然这不是好的办法，但凑合着先用吧。
