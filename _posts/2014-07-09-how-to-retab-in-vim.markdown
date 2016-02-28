---
layout: post
title:  "How to :retab in vim"
date:   2014-07-09 12:00:00
categories: Programming
---

Today I was working with a file that used Tabs as indentation. At [Monterail](http://monterail.com/) two spaces indentation is our convention (the proper one) so I wanted to use `:retab` to change indentation and… suprisingly it didn’t work.

It took me a while and some wiki reading to finally find (almost) working command:

```
:set et|retab
```

The caveat is that it will change all tabs into spaces, so I could write `s/\t/ /g` as well. Fortunately vim wiki has a better command defined:

```
# ~/.vimrcVim
:command! -range=% -nargs=0 Tab2Space execute '<line1>,<line2>s#^\t\+#\=repeat(" ", len(submatch(0))*' . &ts . ')'
```

that converts only leading whitespace.

Please note you should paste it to `~/.vimrc` and then call it in file with `:Tabs2Space`. You can use `:set list` to show whitespace characters and see that this function definitely works as intended.

If you’re interested in my full `.vimrc` file you can find it [on GitHub](https://github.com/hodak/dotfiles/blob/master/vimrc)

Source: [http://vim.wikia.com/wiki/Converting_tabs_to_spaces](https://github.com/hodak/dotfiles/blob/master/vimrc)
