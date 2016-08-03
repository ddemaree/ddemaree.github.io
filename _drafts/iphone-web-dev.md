---
title: How I manage a Jekyll-powered web site from my phone
---

# iPhone cloud development

The secret sauce to making web software from an iOS device is pretty simple: do all the real work on another computer. In my case, my main development environment is a Linux (Ubuntu 14.04) VM hosted at DigitalOcean, set up with all the same tools and configuration I'm accustomed to from my Mac (Zsh, Vim, Git). One reason I use DigitalOcean for my VM hosting is that their web console is simple, and works well from all my iOS devices. (The AWS console, on the other hand, has some bizarre, failed, semi-responsive UI stuff going on that makes it nearly unusable on small screens.)

## Setting up

Fortunately for my thumbs, I was starting from a purely static, single page web site. Using the built-in Terminal in Coda I just created a new Jekyll site with `jekyll new`, then copied over my two static HTML & CSS files. 

Though my site is currently bare-bones, one area where templating already comes in handy is managing OpenGraph/Twitter Card `meta` tags, which contain the same information repeated a few times. I created an include template and moved all of that information to my site's `_config.yml`.

I build and preview my site on the server using a combination of `jekyll build -w` and the [Caddy][1] web server (which I find just performs better than the Ruby HTTP server Jekyll uses by default), which I start and stop using [Foreman][2].

Once I'd confirmed everything was working the way I wanted, I created [a new GitHub repository for my web site][3] and pushed everything to the server.

Nearly all of this was done from the Zsh command line, using Coda's built-in terminal. For the bits that required editing files (creating a Twitter Card template, editing my confit and Procfile), I used Coda's excellent editing tools, reading and writing files over SFTP.

## In which we replace Apache with nine kinds of serverless-ish infrastructure

Previously, I'd had one Apache instance handle just about everything, where "everything" included not only serving my web site, but also handling redirects from my short domain (`demar.ee`) to my full one (`demaree.me`) using `mod_rewrite` rules. By moving my site to GitHub, not only could I not set up that kind of seamless redirect, but I can only map one domain at a time to my site.

First, for mapping my main domain to GitHub, I logged into Cloudflare (my DNS provider) and created a CNAME pointing demaree.me to ddemaree.github.io, and added a CNAME file to my repo telling GitHub to change the default domain.

For the redirects from demar.ee, I set up an AWS S3 bucket, turned on static web hosting, and set up the bucket to redirect all requests to demaree.me. Then, because S3 doesn't automatically handle the www subdomain (or any other subdomain), I put AWS CloudFront in front of the bucket, with SSL support and CNAMES for both demar.ee and www.demar.ee.

## Tips & tricks

To edit posts—including this one—from my iOS devices, I use Working Copy, a lovely Git client with excellent support for iOS's Document Provider extension API, which means I can open Markdown drafts in any text editor that uses document providers. I open and edit drafts in my Markdown writing app of choice, Ulysses, then switch back to Working Copy to commit changes and push them to GitHub.

Images are hosted in an Amazon S3 bucket, and I can upload them from Transmit on iOS. I use Cloudinary to transform them.

[1]:	caddyserver.com
[2]:	http://ddollar.github.io/foreman/
[3]:	https://github.com/ddemaree/ddemaree.github.io