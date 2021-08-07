---

Title: Self-Hosted Cloud Services

Template: blog-content

Description: The transparency of open-source software is liberating, but open-source cloud services that work as seamlessly as the widely-used Google, Apple, or other services can be a near-impossible feat.

Author: Tim White

Date: 2020-11-11

Robot: noindex,nofollow

Tags: [technical,website,cloud-server,nginx,nextcloud]

---

# Self-Hosted Cloud Services

The transparency of open-source software is liberating, but finding open-source cloud services that operate as seamlessly as mainstream services can be a daunting task.

Today I will introduce the frameworks and services I use, as well as their individual benefits and limitations.

## Virtual Private Server hosting

Over the years, I have worked in a variety of web hosting services including [DigitalOcean Droplets](https://www.digitalocean.com/products/droplets/), [GitHub Pages](https://pages.github.com/), [Google App Engine](https://cloud.google.com/appengine/), and [Amazon EC2/lightsail](https://aws.amazon.com/lightsail/), among others.

After shifting my personal interests from [static site](https://en.wikipedia.org/wiki/Static_web_page) hosting to more intricate cloud service hosting like [NextCloud](https://nextcloud.com/), I discovered other more cost-effective **Virtual Private Server (VPS)** solutions like [Hetzner](https://hetzner.com) (Shout-out to [LowEndBox.com](https://lowendbox.com/)).

Hetzner is an example of a VPS host with aggressively competitive pricing. They offer services that are General Data Protection Regulation (GDPR) Compliance and have affordable & fast SSD expandable storage. I'm not in any way sponsored to do so, but I would greatly recommend their platform.

My main VPS specifications right now are: Ubuntu 20.04.1 LTS (GNU/Linux 5.4.0-48-generic x86_64); 2 vCPU (KVM); 4 GB RAM; 40 GB local SSD + 200 GB block storage. I also backup all of my important data off-site through Backblaze, check out how I do that on my [Backup Strategy for Website & Cloud Data post](https://timwhite.io/blog/backup-strategy).

## Domain name registration

I usually shift between domain name registrars depending on who provides the most affordable service, but lately I have been partial to [Google Domains](https://domains.google.com) and [NameCheap](https://namecheap.com).

In late 2020, I renewed my services with NameCheap for 3-years, and I recommend their platform.

Some people ask why I chose the **[Top-level domain](https://en.wikipedia.org/wiki/List_of_Internet_top-level_domains)**[ (TLD)](https://en.wikipedia.org/wiki/List_of_Internet_top-level_domains) *".io"* in *"timwhite.io"*. The simple reason is that *".io"* is commonly associated with the idea of **[inputs/outputs](https://en.wikipedia.org/wiki/Input/output)**[ (I/O)](https://en.wikipedia.org/wiki/Input/output) when discussing electronic & computing processes.

A variety of tech-industry giants use this TLD, and I figured it could be a subtle marketing tool in my professional career.

## Nginx Web Server

If we move this discussion one layer down from the Ubuntu VPS, (almost) all of the web frameworks and services on timwhite.io are deployed and accessed through an [NGINX web server](https://www.nginx.com/). For some services running in Python, Ruby, or NodeJS, I use [Passenger](https://www.phusionpassenger.com/docs/tutorials/what_is_passenger/) within NGINX.

After a few years using the [Apache HTTP server](https://en.wikipedia.org/wiki/Apache_HTTP_Server), I made the switch to NGINX to learn a new skill. I have found NGINX to be subjectively better performing, and I prefer its virtual host configuration over that of Apache.

### Portfolio Website (www.timwhite.io - this very page)

The content you are reading now is being served and updated by a [Content Management System (CMS)](https://en.wikipedia.org/wiki/Content_management_system) called [PicoCMS](https://github.com/picocms/Pico).

PicoCMS is an open-source framework developed around the [Symfony PHP framework](https://symfony.com/) and [Twig template engine](https://twig.symfony.com/). It compiles [Markdown](https://en.wikipedia.org/wiki/Markdown) pages into developed themes. I would compare it to how large front-end frameworks like [Angular](https://angular.io/guide/component-overview) and [React](https://reactjs.org/docs/components-and-props.html) handle their respective components and modules.

This portfolio site has been through many designs. I have built some versions from scratch, used front-end frameworks like Angular for others, and I am now happily settling in with PicoCMS.

DIY web design has introduced me to modern day [HTML5](https://html.com/html5/), taken me through [flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/), the introduction of [css-grid](https://css-tricks.com/snippets/css/complete-guide-grid/), and onward to more mainstream CSS frameworks like [Bootstrap](https://blog.getbootstrap.com/2020/06/16/bootstrap-5-alpha/) and [Bulma](https://bulma.io/).

This site's purpose is to provide both a casual & professional showcase for anything I feel like writing about. While there isn't an intentional theme to the content I upload, you will find that I tend to focus on the things I enjoy like Travel, Technology, Ethics, Self-Study, Data Analysis & Visualization, and more.

I hope you run into a few of the custom functions I have added onto the PicoCMS framework including:

* Estimated page read times for posts
* Content tagging/sorting for posts
* Web-friendly heading element IDs (as shareable links)
* Custom Lazy-loading image plugin for [Parsedown](https://github.com/erusev/parsedown)
* ...and More to come!

### FreshRSS Feed (rss.timwhite.io)

In the subdomain *rss.timwhite.io*, I host a local clone of the [FreshRSS feed aggregator](https://www.freshrss.org/) framework. In short summary, I have compiled a list of RSS feeds from my favorite news sites that I can view all in one place. It's essentially a daily newspaper curated to my specific interests.

The data is all stored in a locally hosted MariaDB database on my VPS.

Feel free to go poke around on [rss.timwhite.io](https://rss.timwhite.io/) as everything read-only has been made public.

![Screenshot of landing page of rss.timwhite.io](https://cloud.timwhite.io/s/zYFMZEQzKpnE8rw/preview)*Screenshot of landing page of rss.timwhite.io*

![Screenshot of individual news article on rss.timwhite.io](https://cloud.timwhite.io/s/FcbKM5rwbnMxtna/preview)*Screenshot of individual news article on rss.timwhite.io*

### Nextcloud (cloud.timwhite.io)

Do you use Google Docs, Google Drive, Google Photos, or Microsoft Office for your personal or professional record keeping? Do you worry about data leaks or scandals by mainstream services like [this time with Google](https://mashable.com/article/google-photos-videos-glitch/), or [this other time with Google](https://en.wikipedia.org/wiki/2018_Google_data_breach), or [this time with Microsoft](https://en.wikipedia.org/wiki/2021_Microsoft_Exchange_Server_data_breach), or [this time with Facebook](https://en.wikipedia.org/wiki/Facebook%E2%80%93Cambridge_Analytica_data_scandal)?

Self-hosting of these services like file storage & sharing, photo storage & sharing, online .docx editing, etc. can all be accomplished by open-source software like [NextCloud](https://nextcloud.com/) or [OwnCloud](https://owncloud.com).

I have chosen to self-host NextCloud (while taking extra precautions to [backup my data](https://timwhite.io/blog/backup-strategy)). Self-hosting NextCloud is not for everyone; it can be a finicky setup process and, depending on the specifications of your server, it may not be as snappy as services provided by companies like Google with incredible computing power ([at least 180 Petaflops](https://bit.ly/3msn2zm)).

### TrackTWIO (track.timwhite.io)

\-- MariaDB Database -- Collabora Online (self-hosted LibreOffice) -- Two-factor Auth -- Auto-preview generation for photos, videos, files

* FreshRSS -- MariaDB Database
* Sandbox servers for web-app development (currently: track.timwhite.io) -- MariaDB Database

UFW + Fail2Ban,

Off-site Backup services through Rclone, borg, cron scheduling

Self-signed SSL certificates through Letsencrypt (wildcard)

No longer self-hosting email (too much trouble with "please use a valid email" for signups, spam filtering, upkeep)

## Front-End vs. Middle-Ware vs. Back-End

When you type ["timwhite.io"](https://timwhite.io/) into the address bar of your browser, your computer resolves ["timwhite.io"](https://timwhite.io/) into a numerical IP address of a server associated with the domain name. The browser then sends a packet of information to that remote server containing additional information about your request.

The remote cloud server then sends a file or files as a response to your request, and your browser paints them to your screen. The content of those files that are painted to your screen is generally considered **the front-end.**

Middle-ware and back-end services are rarely directly observed. An example can be seen in one of my self-hosted cloud applications, ["rss.timwhite.io"](https://rss.timwhite.io).

Similar to [www.timwhite.io](https://timwhite.io), there is information painted to your screen, but in the case of [rss.timwhite.io](%22https://rss.timwhite.io%22), that information originates from a database alongside settings, login information, and other data.

An executable "middle-ware" service communicates between the front-end and the database (in this case, that "middle-ware" service is FreshRSS; more below). The setup and maintenance of the database in this example would be "the back-end."

There are many nuances to the terminology here, but this can serve as a brief overview.

Someone who develops front-end, middle-ware, and back-end systems, as well as their interactions, is known as a full-stack developer.
