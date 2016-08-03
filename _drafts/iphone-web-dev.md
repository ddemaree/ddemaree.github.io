---
title: How I manage a Jekyll-powered web site from my phone
---

# iPhone cloud development

The secret sauce to making web software from an iOS device is pretty simple: do all the real work on another computer. In my case, my main development environment is a Linux (Ubuntu 14.04) VM hosted at DigitalOcean, set up with all the same tools and configuration I'm accustomed to from my Mac (Zsh, Vim, Git). One reason I use DigitalOcean for my VM hosting is that their web console is simple, and works well from all my iOS devices. (The AWS console, on the other hand, has some bizarre, failed, semi-responsive UI stuff going on that makes it nearly unusable on small screens.)

## Tips & tricks

To edit posts—including this one—from my iOS devices, I use Working Copy, a lovely Git client with excellent support for iOS's Document Provider extension API, which means I can open Markdown drafts in any text editor that uses document providers. I open and edit drafts in my Markdown writing app of choice, Ulysses, then switch back to Working Copy to commit changes and push them to GitHub.

Images are hosted in an Amazon S3 bucket, and I can upload them from Transmit on iOS. I use Cloudinary to transform them.