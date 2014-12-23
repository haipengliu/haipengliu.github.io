---
layout: post
title: "How to Use Octopress to write blog"
date: 2014-12-23 20:45:48 +0800
comments: true
categories: [Octopress, Blog]
---
Author: Haipeng Liu <A href="mailto:pliu1981@gmail.com">email to me</A></br>
keywords: Octopress</br>

#Install Octopress

``` 
git clone git://github.com/imathis/octopress.git octopress
cd octopress

```
## Installing Ruby With Rbenv

### Install Rbenv

```
cd
git clone git://github.com/sstephenson/rbenv.git .rbenv
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bash_profile
echo 'eval "$(rbenv init -)"' >> ~/.bash_profile
git clone git://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build
source ~/.bash_profile
```
<--! more -->

### Install Ruby 1.9.3
```
rbenv install 1.9.3-p0
rbenv local(/global) 1.9.3-p0 
rbenv rehash
```
### Install dependencies

```
gem install bundler
rbenv rehash    # If you use rbenv, rehash to be able to run the bundle command
bundle install
```
### Install the default Octopress theme.
```
rake install
```
# Write A Blog

```
rake new_post['<your_post_title>']
```
In your octopress path **octopress/source/_posts**, open the post just created and edit as fowllows:
```
---
layout: post
title: "<your_title>"
date: 2014-11-15 08:55:38 +0800
comments: true
categories: [<tag_1>, <tag_2>]
---
Author: 
keywords: 

```
# Deploy Your Blog

## Preview
```
rake install
rake generate
rake preview
```
Now you can see your blog preview at <localhost>:4000

## Publish
```
rake deploy
```
# Back Up your Blogsite onto Github
```
git add .
git commit -m “your message”
git push origin source
```
Finished.