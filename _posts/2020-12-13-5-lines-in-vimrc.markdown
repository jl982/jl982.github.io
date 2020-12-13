---
layout: post
title:  5 lines I put in a blank .vimrc
date:   2020-12-13
tags: vim software
---
## TL;DR
To make a default Vim installation more useful, type the following 5 lines into its `.vimrc` file:

```
set hls
set ic
set is
set nu
set noswf
```

Or if you prefer, copy and paste the spelled out and annotated version:

```
set hlsearch    " highlight all search results
set ignorecase  " do case insensitive search 
set incsearch   " show incremental search results as you type
set number      " display line number
set noswapfile  " disable swapfile
```

For what it's worth, the acronym for the 5 lines is `HIINN`.

Edit: [Multiple people on HN](https://news.ycombinator.com/item?id=25410751){:target="_blank"} [pointed out](https://news.ycombinator.com/item?id=25410742){:target="_blank"} that the 5 lines can be combined into a single line like below. I didn't know about this capability, but will definitely start doing this from now on.

```
set hls ic is nu noswf
```

## Motivation
[Vim](https://www.vim.org/){:target="_blank"} is a powerful text editor for Unix/Linux, and I use it frequently to view and edit files. Unfortunately, Vim's default configurations lack several important usability features compared to popular alternative text editors, such as [VSCode](https://code.visualstudio.com/){:target="_blank"}.

The undesirable defaults are not an issue on my own computer, as I can take the time to configure them. However, often I'd find myself debugging or reading logs on near-fresh Linux installations (eg. virtual machines spun up to do integration testing), where Vim had not yet been configured.

So over time, I distilled the text editor features that I needed the most, and came up with the list above. To set it up, I would run `vim ~/.vimrc`, manually enter those 5 lines in whichever order that I remembered them, then quit and restart Vim to pick up the new configurations.

## Discussion
The first 4 lines are straightforward - most popular modern text editors already come with all of them out of the box. The last one could be controversial, since [swap file](http://vimdoc.sourceforge.net/htmldoc/recover.html#swap-file){:target="_blank"} is designed to help users recover work. In practice though, I find it to be more in the way, due to the additional dialogue that pops up when opening a file that has an existing swap file. The recovery feature itself is also not useful to me, as I more often read logs rather than make edits in those cases.

The next time you find yourself in a similar situation, I recommend you to also try putting those 5 lines into the `.vimrc`. It could make your Vim experience just a bit better.

Discuss this post on [HN](https://news.ycombinator.com/item?id=25410390){:target="_blank"}.
