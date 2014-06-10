This version forked from [Letterpress](https://github.com/an0/Letterpress) is made for Python 2 and Python 3.

# What's Letterpress?
Letterpress is a minimal, [Markdown](http://daringfireball.net/projects/markdown/) based blogging system written in Python.

# Why Letterpress?
* Letterpress is lighter than WordPress.
* Python is prettier than PHP.
* Static/text is more reliable than dynamic/database.
* Markdown is more human-friendly than HTML.
* Math writing is much easier in ASCIIMathML than in MathML.

# Requirements
1. A Linux kernel with inotify support is required to run Letterpress.
2. [virtualenv](http://www.virtualenv.org) and [pip](http://www.pip-installer.org) are recommended.
3. UTF-8 is assumed. The babel of human languages is bad enough, let's at least use the same encoding.

# Installation
1. Install [pyinotify](https://github.com/seb-m/pyinotify).
	```bash
	pip install pyinotify
	```
2. Copy `code/letterpress.py` to your Python runtime path. 
3. Copy `code/markdown2/lib/markdown2.py` to your Python runtime path.
4. Make a directory to hold your posts — let's call it *press_folder* — and copy `press/*` to it.
5. Make the necessary changes to the templates(title, twitter handle…) and `letterpress.config`.
6. Install [Pygments](http://pygments.org) if you want to embed code(using [GFM](http://github.github.com/github-flavored-markdown/)'s Syntax Highlighting) in your posts.
	```bash
	pip install Pygments
	```

# Usage
```bash
$ python letterpress.py path_to_press_folder
```

# How It Works
After launch, Letterpress monitors Markdown files(recognized by the filename extension specified in `letterpress.config`) in *press_folder*. When an new Markdown file is detected Letterpress generates a new HTML file from that Markdown file. Similarly, when an existing Markdown file is updated or deleted, Letterpress updates or deletes the corresponding HTML file.

Letterpress also monitors templates. If any change is detected in any of the template files, Letterpress rebuilds the whole site.

Letterpress also monitors subfolders and other files in *press_folder* but treat them as assets. It maps them directly into `site_dir`. It means if you make an *assets* folder and put images there you can reference them in your posts, e.g., `![Big Headshot](/assets/big_headshot.jpg)`.

Letterpress builds these indices automatically:

* Home index
* Archive indices
* Monthly indices
* Yearly indices
* Tag indices

Letterpress writes logs into *press_folder* so you can easily review what is going on.

# Writing
You write posts in such a natural format:
```
title: Post Title
date: Publishing date in the format specified in letterpress.config. The default format is 01/31/2013.
excerpt: Summary of the post.
tags: math, web

Content of the post…

### Let's have fun with math & physics

$E=m*c^2$

```

Refer to `press/sample_post.md` for a complete example.

# Naming
The recommended naming scheme for post files is to use post title, directly or shortened. Adding date to file names would result in redundant path segment in permalinks since Letterpress already puts the HTML files under folders named after their publish dates.

# Publishing
You can publish posts by putting them in *press_folder* with whatever method you like, e.g., FTP or rsync. However, I highly recommend [Dropbox](https://www.dropbox.com). This is how you should use Dropbox to publish posts to Letterpress:

1. Of course you must have a Dropbox account. Let's call it *writer's account*.
2. Install Dropbox client on your desktop computer, iPhone, iPad or other devices you write on. Let's call it *writing machine*.
3. Sign in your *writer's account* on your *writing machine*.
4. Have the aforementioned *press_folder* somewhere in Dropbox folder on your *writing machine*.
5. Register another Dropbox account. Let's call it *publisher's account*.
6. Install Dropbox client on your server. Let's call it *publishing  machine*.
7. Sign in your *publisher's account* on your *publishing machine*.
8. Share *press_folder* from your *writer's account* to your *publisher's account*.
9. Now your *writing machine*'s *press_folder* and *publishing machine*'s *press_folder* are in sync. Whenever you put a new post into, edit an existing post in, or delete one from, your *press_folder* on your *writing machine*, Letterpress will generate, update, or delete the corresponding HTML file in *site_dir*(configured in `letterpress.config`) on your *publishing machine*.

# Credits
* Templates and style sheets are derived from [Michiel de Graaf's blog](https://github.com/michieldegraaf/blog).
* [pyinotify](https://github.com/seb-m/pyinotify) by Sebastien Martini.
* [python-markdown2](https://github.com/trentm/python-markdown2) by Trent Mick. My [fork](https://github.com/an0/python-markdown2) is used here because:

	1. Some necessary bug fixes are not merged back yet.
	2. Some extension is required to support ASCIIMathML embedding.
	3. I want to use my inline-styled footnotes.

* [Pygments](http://pygments.org) by Pocoo.
* [MathJax](http://www.mathjax.org) for [ASCIIMathML](http://www1.chapman.edu/~jipsen/mathml/asciimath.html) processing and [MathML](http://www.mathjax.org) rendering.

So I hardly did any thing but glue these awesome things together.

# License
Letterpress is licensed under a BSD-3-clause license. See [LICENSE](https://github.com/an0/Letterpress/blob/master/LICENSE) for details. You are encouraged to keep the "Powered by Letterpress" footer on your site.
