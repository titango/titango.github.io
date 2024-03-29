---
layout: post
title:  "Running Jekyll on MacOs M1"
date:   2022-03-26 12:00:00 +0300
image:  '/assets/img/language/jekyll.png'
tags:   [blog, coding, web_programming, tech, ruby ,jekyll]
---

( If you don't know what Jekyll is. I recommend checking out their site [here](https://jekyllrb.com/))<br /><br/>
I bought a *new 14-inch Macbook Pro* at late 2021 and spent some times to configure and transferred all my previous files into my new mac machine. I didn't have time to run Jekyll again as I was busy working for a long (and complicated) project at my job.<br/> <br/> 
Later today on weekends, I started pulling Jekyll repo on Github back to make an attempt to write a post about Jest & Testing library with Msw (coming soon! 👌) and I ran into an issue that Jekyll **could't execute bundle and run**.<br/><br/> 
Therefore, I am writing this post in order to help other people to solve the issues as I had earlier so they don't need to go through all the hassles and just get it run 😄.

Without any futher delay, let's get started ! <br/> <br />

<hr />
## Installing new Ruby version

You probably are having the issue at the moment andI cannot remember what exact error was, but apparently we know that jekyll couldn't run.
As I thought the problem was my new Macbook M1 chip, as I searched around. I found out this [post](https://www.shouvikbasak.net/website/jekyll-on-macos-apple-m1-solved/)
here stating that 
> Jekyll is compatible with macOS with ARM64 architecture. However, bundle exec jekyll serve may fail with older version ffi <br/>
> You may need to run bundle update or update ffi to at least 1.14.2 manually.”
<br/>

As it also states in the post that MacOS Big Sur 11.3.0 has inbuilt Ruby version 2.6.3p62 and it's not compatible with Jekyll newer version *(such as 4.2.0)*
And so, we need to install a newer version of Ruby to get started with.

{% highlight bash %}
brew install ruby
{% endhighlight %}


After finish installing, I'd recommend setting **$PATH**, **$GEM_PATH** and **$GEM_HOME** (I'm using `zshell` and put inside `~/.zshrc` but you can also use `bash` and put inside `~/.bash_profile`) the following: 

{% highlight bash %}
...
export PATH="/opt/homebrew/opt/ruby/bin:$PATH"
export GEM_HOME=/opt/homebrew/lib/ruby/gems/3.1.0
export GEM_PATH=/opt/homebrew/lib/ruby/gems/3.1.0
...
{% endhighlight %}

**NOTE:** Make sure you set the right `PATH` indicated after ruby has been installed. In some cases, the message for `PATH` could be like the following:

{% highlight bash %}
...
By default, binaries installed by gem will be placed into:
  /usr/local/lib/ruby/gems/3.1.0/bin

You may want to add this to your PATH.
...
{% endhighlight %}
Then you need to set `GEM_HOME` and `GEM_PATH` to be **/usr/local/lib/ruby/gems/3.1.0**

<hr />
## Installing Ruby ffi

Ruby-FFI is a gem for programmatically loading dynamically-linked native libraries, binding functions within them, and calling those functions from Ruby code.
<br /> <br />
In order to install Ruby ffi, run:

{% highlight bash %}
gem install ffi
{% endhighlight %}

<hr />
## Installing Webrick

I stumbled upon this question when I ran into the issue of trying to set up github pages. It seems that in the latest version of **Ruby** that is installed with `homebrew webrick` is not included by default
<br/> <br/>
Therefore, we need to install it manually with `homebrew`

{% highlight bash %}
bundle update
bundle add webrick
{% endhighlight %}

<hr />
## Running Jekyll
And it's done, we now can try running **Jekyll** with `Live Reload`.

{% highlight bash %}
bundle exec jekyll serve --livereload
{% endhighlight %}

<br />
Hope this post is useful for you and if you have any questions, feel free send an email to me. Cheers.

<!---
SOURCE COMMENT
1. Update Ruby
   1. `brew install ruby`
   2. export PATH="/opt/homebrew/opt/ruby/bin:$PATH"
      export GEM_HOME=/opt/homebrew/lib/ruby/gems/3.1.0
      export GEM_PATH=/opt/homebrew/lib/ruby/gems/3.1.0
2. Install ruby ffi
   1. Ruby-FFI is a gem for programmatically loading dynamically-linked native libraries, binding functions within them, and calling those functions from Ruby code. Moreover, a Ruby-FFI extension works without changes on CRuby (MRI), JRuby, Rubinius and TruffleRuby
   2. `gem install ffi`
3. Update bundle `bundle update`
4. I stumbled upon this question when I ran into the issue of trying to set up github pages. It seems that in the latest version of ruby that is installed with homebrew webrick is not included by default
   1. Install webrick `bundle add webrick`
5. Run serve `bundle exec jekyll serve`
-->