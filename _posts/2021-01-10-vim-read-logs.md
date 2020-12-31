---
layout: post
title:  Effectively read logs using vanilla vim
date:   2021-01-10
tags: vim software
---
## TL;DR
Glance over the gifs below for tips.

## Preface
As with the motivation for my [previous post]({{ site.baseurl }}{% link _posts/2020-12-13-5-lines-in-vimrc.md %}), I often need to read logs in remote machines or containers. Rather than trying to copy the files to my local computer, it's easier to open and browse them directly in the remote shell using vim.

This article showcases some vanilla vim features (i.e. without custom plugins) that I find useful while navigating logs. The goal is to provide you intuition on how the features work, so that you can adopt them in your own workflows. Before proceeding, I recommend that you first set the [5 configs]({{ site.baseurl }}{% link _posts/2020-12-13-5-lines-in-vimrc.md %}) mentioned in the previous post.

Below is the example log I'll be using.  Feel free to save the content to a file and follow along:
```
2021-01-02 00:00:01,000 - handlers.py[DEBUG]: start: task 1
2021-01-02 00:00:02,000 - util.py[DEBUG]: Running command ['ip', 'link', 'set', 'dev', 'eth0', 'up'] with allowed return codes [0] (shell=False, capture=True)
2021-01-02 00:00:04,000 - handlers.py[DEBUG]: finish: task 1, took 3 seconds
2021-01-02 00:00:10,000 - handlers.py[DEBUG]: start: task 2
2021-01-02 00:00:20,000 - handlers.py[DEBUG]: start: task 3
2021-01-02 00:00:21,000 - util.py[DEBUG]: Running command ['/var/tmp/cloud-init/cloud-init-dhcp-x4y__t7z/dhclient', '-1', '-v', '-lf', '/var/tmp/cloud-init/cloud-init-dhcp-x4y__t7z/dhcp.leases', '-pf', '/var/tmp/cloud-init/cloud-init-dhcp-x4y__t7z/dhclient.pid', 'eth0', '-sf', '/bin/true'] with allowed return codes [0] (shell=False, capture=True)
2021-01-02 00:00:22,000 - util.py[DEBUG]: Running command ['systemd-detect-virt', '--quiet', '--container'] with allowed return codes [0] (shell=False, capture=True)
2021-01-02 00:00:30,000 - handlers.py[DEBUG]: finish: task 2, took 20 seconds
2021-01-02 00:05:00,000 - handlers.py[DEBUG]: finish: task 3, took 280 seconds
```

## 1. Line wrap
Sometimes, log lines are longer than the width of your terminal. You can use `:set wrap` to enable line wrap, `:set nowrap` to disable it, or `:set wrap!` to toggle.
<figure>
<video autoplay loop muted playsinline src="/assets/images/2021-01-10-vim-read-logs/wrap.mp4"></video>
<figcaption markdown=span>Use `:set wrap!` to toggle line wrap</figcaption>
</figure>

## 2. Search
You can search within a file using `/`. What makes it more interesting though is that search supports regular expression - just make sure to escape special characters.
<figure>
<video autoplay loop muted playsinline src="/assets/images/2021-01-10-vim-read-logs/find.mp4"></video>
<figcaption markdown=span>Search for multiple keywords with regex symbol `|`</figcaption>
</figure>
And having regular expression means you can be increasingly creative. Here's an example to match numbers with at least 2 digits (references: [character classes](http://www.rexegg.com/regex-quickstart.html#classes), [quantifiers](http://www.rexegg.com/regex-quickstart.html#quantifiers)):
<figure>
<video autoplay loop muted playsinline src="/assets/images/2021-01-10-vim-read-logs/find2.mp4"></video>
<figcaption markdown=span>Find tasks that took at least 10 seconds</figcaption>
</figure>

## 3. Filter
The [global command](https://vim.fandom.com/wiki/Power_of_g), `:g`, comes very handy when dealing with verbose or repetitive logs. I use it most often to filter out unneeded log lines:
<figure>
<video autoplay loop muted playsinline src="/assets/images/2021-01-10-vim-read-logs/filter.mp4"></video>
<figcaption markdown=span>`:g//d` to delete matching lines, `:g!//d` to delete non-matching lines</figcaption>
</figure>
Or if you want to do the search and filter in one step, put the query between the slashes, e.g. `:g/running command/d`.

But be careful to not save! You can run `vim -R` to start vim in read-only mode. To save the filtered results, copy them into a new buffer:
<figure>
<video autoplay loop muted playsinline src="/assets/images/2021-01-10-vim-read-logs/filter2.mp4"></video>
<figcaption markdown=span>Save the filtered results into a new buffer, and undo the changes in the original file</figcaption>
</figure>
Breakdown of commands in the previous gif:
1. `gg` to jump to top of the file
2. `V` to visually select entire lines
3. `G` to jump to bottom of the file while in visual mode, thereby selecting all lines
4. `y` to copy the selected text
5. `:tabe` to open a new blank buffer
6. `p` to paste the copied text
7. `gt` to navigate to the next (i.e. first) tab
8. `uu` to undo the 2 `:g` filters

## 4. Substitute
If a lot of information is logged in a delimited format, you can use vim's [search and replace](https://vim.fandom.com/wiki/Search_and_replace) feature to replace the delimiters with new lines, for ease of reading:
<figure>
<video autoplay loop muted playsinline src="/assets/images/2021-01-10-vim-read-logs/substitute.mp4"></video>
<figcaption markdown=span>`:%s//\r/g` to replace matched results with new lines</figcaption>
</figure>
Deconstructing the syntax:
- `%` means to perform substitute on all lines (instead of only the current line)
- the "search" and "replace" portions are surrounded by slashes (in the gif, we left "search" blank because we already had search results)
- `\r` (carriage return) represents new line in vim
- `g` means to substitute all occurrences in a line (instead of only the first occurrence)

## Discussion

Discuss this post on [HN](https://news.ycombinator.com/item?id=25720188).
