---

layout: post
title: Gem install problem - could not find gem locally or in a repository
topics: gems
excerpt: Error could not find gem mislav-hanna locally or in a repository. Solution found at...

---

###Error: could not find gem mislav-hanna locally or in a repository

My solution to this problem was found at [http://gems.github.com/](http://gems.github.com/)

When I got this error my gem source was only set to: http://gems.rubyforge.org/

But the gem I was trying to install was housed on github.  So I just needed to add github as a gem source.

<code>$ gem sources -a http://gems.github.com</code>

To find out your gem sources type in

<code>$ gem sources</code>

