---
# recommended 70 chars
title: "Migrating my blog from Ghost to Hugo"
# recommended 156 chars
description: "In this meta post I'll talk about my recent experience of migrating my blog from a self-hosted Ghost to Hugo."
date: 2020-12-13T14:27:00+00:00
tags: ["blogging", "ghost", "hugo", "meta"]
author: "Joao Grassi"
showToc: true
TocOpen: false
draft: false
hidemeta: true
comments: false
slug: "migrating-my-blog-from-ghost-to-hugo"
type: posts

# cover:
#     image: "ghactions-dockercompose-cover.png"
#     relative: true
#     alt: "Octocat + GitHub Action + dotnet bot"
---

In this post I'll talk about my recent experience of migrating this very single blog from [Ghost](https://ghost.org/) to [Hugo](https://gohugo.io/).
More specifically, I want to talk about: Why I decided to migrate; What were the pain points; What were the good points and something about hosting. 

So let's start!

# Why touch something that works?

Isn't this the mantra for us, software ppl? 

Jokes aside, when I first started my blog over in 2018 (2 years already, whoa!) I did some lazy research and Ghost seemed the "cool kid on the block" at the time. I love Markdown and wanted to avoid WordPress so that settled it pretty quickly. Ghost it would be. 

Then it came to the hosting part. Because I'm ~~a cheap bastard~~ very responsible with my personal finances, I wanted to keep the costs as low as possible. After all, the intention of the blog **was and is** not to make a profit. Again, with my lazy research DigitalOcean was the most cheap and easy place where I could get things started. I was using a droplet (how they call VMs) that costed $6,00 USD per month, not bad!

I was happy with the setup. It was **super easy** to post new content. Ghost is a terrific platform and I highly recommend it. I did not decide to migrate it because I had problems with it. In fact I had 0 problems with Ghost per se. What started to annoy me after some time and ultimatelly made me decide to switch was:

 - Costs
 - Maintenance

## Costs

6 bucks is like super cheap right? It was for me and I was hapilly paying it.

Now, I'm very controlled with my personal finances. Growing up with some difficulties really puts you on a different perspective when it comes down to money. After a year or so of having my blog published, the montly bills started to get into my nerves. $6,00 a month is $72,00 a year and to me $72,00 is a lot. I can go on and on why I think it's a lot, but let's leave this to maybe a personal finance blog in the future.

## Maintenance

Since I decided to host everything on my own, I had to be also the sys admin of the blog. In the beginning it was kinda fun and not much work. `ssh` into the box every now and then, run some `apt update` to update stuff. But there was more.

I also did backups frequently (do your backup's ppl, bad things happen). I ultimatelly developed a script that would do everything (zip the ghost relevant folders, generate a backup from MySQL and ship it to some place else). But again, that took time and effort.

In the end I was just kind of tired of doing this sys admin work. I was there for the content and somewhat got in the middle of this other.. stuff. A few minutes per week adds up in a year. 

Only if there was another easier option out there.. :thinking:


# Overchoice - The static site generator saga

I started to notice on Twitter more and more people talking about static site generators. I knew about them and what they were there for, but nothing any deeper than this. At this point I had already decided to change my blog to a static site generator. I just needed to pick which one. 

One hard requirement I had was: **it must be simple**. I don't want it to become a labor.

After some research, I narrow it down to these options: [Gatsby](https://www.gatsbyjs.com/), [Jekill](https://jekyllrb.com/) and [Hugo](https://gohugo.io/).


## Gatsby 

I ruled out Gatsby pretty soon. After reading a bit on foruns and so on, I found out a lot of people complaining of it being very slow. It uses React which I never had the time to learn. Not yet decided, I read some more tutorials on how to setup things and my god it all seemed so over complicated. So, yeah it was a no for Gatsby very quickly. I might be wrong and my research was just crap? 

## Jekill

I was pretty close to chosing it. The only downside was that, at the time, I was still using Windows as my OS and setting everything up was not great. I ran into a lot of erros and had to keep spending time researching solutions. This is mostly because Ruby development on Windows is not great. And then, also the fact that I know 0 about Ruby. Not sure though how much one need to know, maybe 0. But since the setup was not awesome.. I decided to stop and continuing shopping.

## Hugo

I was immediately happy with it. Hugo is written in Go with support for multiple platforms and they offer pre-built binaries that you just need to drop somewhere, add to your `PATH` and boom, it works! +1 for easy of instalation.

I quickly looked into their documentation and although not everyting is awesome I found it relatively easy to get started with. I also reached out in their forum when I got stuck later on and I was very well welcomed by others. +1 for docs and community support. 

Getting down into business: Basically you have some markdown files for your content, run a local server with auto refresh while writting it, and when you are ready to publish, just run `hugo` and you are done. +1 for easy of writing new content.

They also say on their website that Hugo is *"The world’s fastest framework for building websites"*. To be honest that is bit over the top if you ask me, so I did some reading about why is that so, and I came across some very impressive benchmarks like [this](https://www.youtube.com/watch?v=CdiDYZ51a2o&feature=emb_title) and [this](https://forestry.io/blog/hugo-vs-jekyll-benchmark/). +1 for performance.

After all this research, seemed Hugo was the winner. :grin:


# Not everything is perfect - A few bumps along the way


## Everything starts with a good theme (or not)


## Backwards compat and URL hell

 - Not break existing URLs (what are the options)
 - RSS - how to keep the same url (/rss, no extension)
 - Not break existing social media post images (open graph/twitter meta tags)

# Hosting

## GitHub pages - how does hosting works

 - Already existing github pages on my root domain
 - Add the blog as a github pages for project
 - Cloudflare as DNS manager (and for nice caching)

## Why not deploy to Netlify?

 - Basically because I did not want to pay
 - Does not play well with Cloudflare caching (netlify already have their own cache with conflicts with cloudflare)
 - If my blog gets super popular (or attacked?) and I exceed the quota on Netlify, I will need to pay and there's no way to block it
 - So I want to avoid surprises
 - Didn't want to have to manage DNS entries in two places (already have everything on cloud flare)

 # Summary