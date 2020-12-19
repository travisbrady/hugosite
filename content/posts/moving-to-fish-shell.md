---
title: "Moving from Zsh to Fish"
date: 2020-12-18T17:37:29-06:00
tags: [fish, shell, linux, zsh, bash]
draft: false
---

# Moving from Zsh to Fish 🐠

{{< figure class="avatar" src="https://fishshell.com/assets/img/Terminal_Logo2_CRT_Flat.png" >}}

I recently began experimenting with [Fish](https://fishshell.com/) after a long time using [zsh](https://www.zsh.org/) and [oh my zsh](https://ohmyz.sh/).
Thus far it's been a good experience so thought I'd share why I did it, how I tweaked my setup and my thoughts on Fish so far.  I also share some of the many mistakes I made in trying to configure `fish` to behave a bit like a faster `zsh`. If nothing else writing this is helpful so I remember next time I need to set this up.

## Why
I've always liked zsh since being introduced to it while working at the mighty [Mochi Media](https://en.wikipedia.org/wiki/Mochi_Media) and have had maybe too much fun customizing my prompt over the years. But the persistent performance issues really began to bother me over the last year or two. Indeed there is a [whole](https://blog.mattclemente.com/2020/06/26/oh-my-zsh-slow-to-load.html) [genre](https://blog.jonlu.ca/posts/speeding-up-zsh) [of](https://htr3n.github.io/2018/07/faster-zsh/) [blog](https://medium.com/@dannysmith/little-thing-2-speeding-up-zsh-f1860390f92) [posts](http://sangsoonam.github.io/2019/08/05/why-zsh-is-slow-for-git-repos.html) spun up focused on addressing this issue. Specifically starting up a new shell is often painfully slow. I haven't measured the latency but anecdotally it often seems to be >5 seconds just to get a new zsh prompt. So I experimented a bit with fish to compare and have yet to notice any such lag or latency.

## My Arguably Unreasonable Requirements
Ok so now comes the hard part. Specifically I need fish to be fast as mentioned previously, but I also need it to be easy to use and behave more or less like zsh.

So my requirements are simple but arguably silly:
#### 1. Speed
Zsh has always been laggy for me and at times I've hacked on my `.zshrc` to try to speed it up, but it just never felt **snappy**.

#### 2. Fancy customizable prompt
I don't care if this is silly fluff. I like it and I'm keeping it.

So far I would call this prompt sufficiently fancy and just the right amount of unnecessarily shiny.
{{< figure width="360" src="/omf_prompt.png" >}}

#### 3. ctrl+r based history search
By default fish has its own style of last command substitution using up arrow key but after having used it a bit my fingers prefer plain old ctrl-r.

#### 4. bash/zsh-style Command Substitution
`!!`and `!$` last command substitution. This one is tough, it's very un-fish-like

<hr >

## What I did

#### 1. Install fish
Do the easy thing on Mac:
```bash
$ brew install fish
$ fish --version
fish, version 3.1.2
```
I should say as well that I'm using iTerm2 (3.4.0 beta12) with patched Powerline fonts (MesloLGS NF).

#### 2. Install oh-my-fish aka omf
[oh-my-fish](https://github.com/oh-my-fish/oh-my-fish) is apparently the most popular fish plugin manager and works as expected if you're familiar with oh-my-zsh.
I know `curl` piping to source thing is terrible and makes security people cringe but I used it anyway.

```bash
$ curl -L https://get.oh-my.fish | fish
$ omf version
Oh My Fish version 7
```

#### 3. Install fisher
Fisher is a popular fish plugin manager. But why two plugin managers? Fisher is necessary to install fzf.fish
```bash
$ curl -sL https://git.io/fisher | source && fisher install jorgebucaran/fisher
```

#### 4. Install fzf.fish
FZF really supercharges history search and comes with Ctrl-r as default so I installed [fzf.fish](https://github.com/PatrickF1/fzf.fish)

```bash
$ fisher install PatrickF1/fzf.fish
```
Example of using FZF via Ctrl-r in fish.
{{< figure width="500" src="/fzf_screen.png" >}}

#### 5. Emulate Bash Command Substitution
My fingers are used to `!!` and `!$` (shorthand for last command and last argument of last command respectively) and emit them almost automatically at this point. So I'm skeptical that I could ever learn a new style.
By following along with this [StackOverflow thread](https://superuser.com/questions/719531/what-is-the-equivalent-of-bashs-and-in-the-fish-shell) and [this page](https://github.com/fish-shell/fish-shell/wiki/Bash-Style-Command-Substitution-and-Chaining-(!!-!%24-&&-%7C%7C)) on the fish wiki I was able to get both bangbang and bangdollar to work.

I created the file `~/.config/fish/config.fish` and pasted functions `bind_bang`, `bind_dollar` and `fish_user_key_bindings` in and it works great.

<hr >

## Mistakes I Made Along The Way
1. Mucking around with too many plugins at once
2. Misunderstanding fish's "interactive first" mindset
3. Having omf and [tide](https://github.com/IlanCosman/tide) collide and breaking my prompt
4. Expecting fish to be equivalent to zsh out-of-the-box
5. Making some changes in interactive mode and others in config files
6. This goes for everything ever but: not fully reading the docs. I simply scan them and then copy/paste something

## One Last Bit
The only snag remaining is an issue I encountered when trying to change my default shell to fish. Specifically after making the change in `/etc/shells` and with `chsh` the look of my `bobthefish` based prompt changes and lacks the colors and icons I like in the screenshot above.

## Further Reading
- [Why Aren't You Using Fish and Oh-My-Fish?](https://www.realjenius.com/2020/05/30/oh-my-fish/) Great recent article on fish configuration
- [Fish and iTerm2](https://lobster1234.github.io/2017/04/08/setting-up-fish-and-iterm2/)
- [Fish vs. Zsh vs. Bash and Why You Should Switch to Fish](https://medium.com/better-programming/fish-vs-zsh-vs-bash-reasons-why-you-need-to-switch-to-fish-4e63a66687eb)
- [Fish Themes](https://github.com/oh-my-fish/oh-my-fish/blob/master/docs/Themes.md) (I'm using and happy with [bobthefish](https://github.com/oh-my-fish/theme-bobthefish))
- [Configure Fish with ‘bobthefish’ and ‘nerd fonts’ on Mac](https://denbeke.be/blog/mac/configure-fish-with-bobthefish-and-nerd-fonts-on-mac/)
