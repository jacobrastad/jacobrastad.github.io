---
layout: post
title: "Getting started with Jekyll on Github with Windows"
categories: jekyll
image: /assets/article_images/2016-03-06-getting-started-with-jekyll-on-github-with-windows/header_jekyll_on_windows.jpg
---

The first post of this blog will be about how to setup the blog itself. A short story about its own creation.

If you haven't already, install Ruby on your machine. Checkout [RubyInstaller.org](http://rubyinstaller.org/){:target="_blank"}, don't forget to install the Ruby devkit too.

## Install Jekyll on Windows
Bring up your terminal and enter the following

{% highlight shell %}
$ gem install jekyll
{% endhighlight %}

Be sure to install the latest version of Jekyll, some older ones have compatibility issues with Windows (e.g [v1.4.3](https://github.com/jekyll/jekyll/issues/1948){:target="_blank"}).

Jekyll have a nice feature that watches for file changes and reloads your site so that you can preview the compiled version directly after editing the file. On windows this requires one additional gem.

{% highlight shell %}
$ gem install wdm
{% endhighlight %}

## Prepare your repository on Github <i class="fa fa-github"></i>

When using Github pages to host your content you need to create a repository called `USERNAME.github.io` for it to work correctly.

![Create Github repo for Jekyll blog](/assets/article_images/2016-03-06-getting-started-with-jekyll-on-github-with-windows/create-github-jekyll-repository.PNG)

After you've created the repo, clone it to your computer.
{% highlight shell %}
$ git clone https://github.com/USERNAME/USERNAME.github.io.git
{% endhighlight %}

## Let's go Jekyll!
While standing in the folder above your newly cloned repo, execute the following command. That way all files created by Jekyll will end up in the root of your repo.

{% highlight shell %}
$ jekyll new USERNAME.github.io
{% endhighlight %}

And in a few seconds Jekyll will have created your new blog.

To see it in action, run this:

{% highlight shell %}
$ cd USERNAME.github.io
$ bundle exec jekyll serve
{% endhighlight %}

And visit http://localhost:4000 in your browser. Wow look at your new fancy Jekyll blog!

Next up, you don't want to keep alot of garbage data in your git repo. Add the following lines to `.gitignore`.

{% highlight shell %}
_site
.sass-cache
.jekyll-metadata
{% endhighlight %}

## Fix your Gemfile

Create a file called `Gemfile` and add the following lines:

{% highlight ruby %}
source 'https://rubygems.org'
gem 'github-pages'
gem 'wdm', '~> 0.1.0' if Gem.win_platform?
gem 'jemoji'
gem 'jekyll-compose', group: [:jekyll_plugins]
{% endhighlight %}

- *Github-pages* is a gem from Github that adds a few default settings to your Jekyll project.
- *Wdm* - Remember that Jekyll needed an extra gem to be able to watch your files for changes? Well this line makes it happen.
- *Jemoji* lets you add emojis supported by Github in your content. If you don't like emojis, you can remove this line.
- *Jekyll-compose* adds a few shortcut commands to generate new posts.

## Commit and push it!

Now would be a good time to make your first commit.

{% highlight shell %}
$ git add .
$ git commit -m "First commit"
$ git push
{% endhighlight %}

After you push it to Github you will be able to see it live on http://USERNAME.github.io.

If you want to know more about the GitHub specific features of Jekyll, you can visit the [GitHub help section](https://help.github.com/categories/customizing-github-pages/){:target="_blank"}.

## I want my blog to look more flashy

If you don't want to style it your self there are alot of nice people that can help you with this. Check out the following Jekyll theme collections:

- [Jekyll's own collection of themes](https://github.com/jekyll/jekyll/wiki/Themes){:target="_blank"}
- [Jekyllthemes.org](http://jekyllthemes.org/){:target="_blank"}
- [Jekyllthemes.io](http://jekyllthemes.io/){:target="_blank"}
- [Jekyll Tips](http://jekyll.tips/templates/){:target="_blank"}
- [JekyllRC.org](http://themes.jekyllrc.org/){:target="_blank"}

## Don't miss Jekyll Compose
If you want to be able to generate new posts easily from the command line, checkout [Jekyll Compose](https://github.com/jekyll/jekyll-compose){:target="_blank"}.

Add the following to your `Gemfile`
{% highlight ruby %}
gem 'jekyll-compose', group: [:jekyll_plugins]
{% endhighlight %}

After you have run `bundle install` you will be able to run the following commands.
{% highlight shell %}
$ bundle exec jekyll page "My New Page"
$ bundle exec jekyll post "My New Post"
$ bundle exec jekyll draft "My new draft"
$ bundle exec jekyll publish _drafts/my-new-draft.md
{% endhighlight %}

And voila, you can now create new posts and pages with ease.