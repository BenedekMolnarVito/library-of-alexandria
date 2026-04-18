---
title: "I Ditched Warp. My Free zshrc Does 90% of What It Does."
source: "https://medium.com/vibe-coding/i-ditched-warp-my-free-zshrc-does-90-of-what-it-does-63113669ffe4"
author:
  - "[[Alex Dunlop]]"
published: 2026-04-12
created: 2026-04-18
description: "I replaced Warp with 6 free brew installs and one zshrc file. Here's the exact config I use daily. Autocomplete, fuzzy search, and a clean prompt."
tags:
  - "clippings"
---
## [Vibe Coding](https://medium.com/vibe-coding?source=post_page---publication_nav-413d50faa755-63113669ffe4---------------------------------------)

[![Vibe Coding](https://miro.medium.com/v2/resize:fill:48:48/1*nD0mORiSRPKPztpAByfNdw.png)](https://medium.com/vibe-coding?source=post_page---post_publication_sidebar-413d50faa755-63113669ffe4---------------------------------------)

Vibe Coders is where we share ideas that help shape the future.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*-pxnm3sYF2ZiFQi0XCYSxg.png)

Image made with MidJourney, edited in Figma

## I cancelled Warp after 20 minutes with this config. Here’s the file.

**$18** per month for the **terminal**. *Really think about that.*

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*nkBltlPbTtbJ8Ef-LGO1KQ.png)

Warp pricing model

*Before 2020 engineers would be screaming at that idea.*

Warp features are good though, I’ll give them that. ***Useful autocomplete. AI baked in***. **300,000 developers** use it. But a couple months ago I tried to **replicate warp.** *It took me* ***20 minutes****.*

I’m **sharing** the exact setup, *you don’t have to figure it out yourself*.

*Not a Medium member? Read for free by* [***clicking here***](https://medium.com/vibe-coding/i-ditched-warp-my-free-zshrc-does-90-of-what-it-does-63113669ffe4?sk=ce5c04932837031cb550152e8c9c1de2)*.*

## Your Terminal Shouldn’t Have an Upsell

Warp’s new UI feels like a **mobile game**, *it forgot its place*.

*Panels pushing you to upgrade*. Features **behind** a **paywall**. Your terminal has its own *homepage now*.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*wsJXpexGO_JgDyFyEg48ZQ.png)

Screenshot of mobile ads

I understand, **they’re a business** which needs to **make money**. *However there is something* *wrong* about opening your **sacred** development **environment**, and being **sold something**.

Mobile games did the same thing, *first they were good, then they were free*, and now they are bad.

I have one monitor on my desk. No clutter.

> “A clean space is a clear mind.”

I think your terminal should be the same.

*It should open, wait, get out of your way.*

Warp stopped being that for me.

## A Reader Asked Me This Directly

*A few days ago* I **published** about using [**cmux**](https://medium.com/vibe-coding/i-run-10-claude-code-agents-easily-using-this-app-b1926d7bd83c).

[*Sacha Wharton*](https://medium.com/u/58fac65d9c85?source=post_page---user_mention--63113669ffe4---------------------------------------)

*left an amazing comment.*

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*K58LgCLvJv6z9XSXeG6sjA.png)

Sacha Wharton -Asking about warp

> “Have you tried Warp.dev, I would be interested to hear what you think.”

*Thanks for the comment, this one is for you!*

I used to use Warp. I loved it for a while. *But it started to get in my way*.

> “Why don’t you just upgrade.”

### For what?

- Autocomplete *(should always be free)*.
- AI correction *(I barely used this)*.
- A weird coding alternative IDE?

*No thanks, most of the features are* ***open-source*** *anyway.*

## The 6 Tools That Replace It

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*bAABilrDzDAI2-XV2tE-Mw.png)

My original Claude message.

[**zsh-autosuggestions**](https://github.com/zsh-users/zsh-autosuggestions) replaces Warp’s autocomplete. Suggestions as you type. Free and simple.

```c
brew install zsh-autosuggestions zsh-syntax-highlighting
```

[**fzf**](https://github.com/junegunn/fzf) replaces Warp’s command search. Hit `Ctrl+R` and get a fuzzy searchable history of everything you’ve ever run.

```c
brew install fzf
$(brew --prefix)/opt/fzf/install
```

[**Starship**](https://github.com/starship/starship) replaces Warp’s prompt UI.

```c
brew install starship
```

[**zoxide**](https://github.com/ajeetdsouza/zoxide) replaces Warp’s recent directories. Type `z project` instead of `cd ~/dev/clients/project`. It somewhat learns.

```c
brew install zoxide
```

[**eza**](https://github.com/eza-community/eza) replaces `ls`. Icons, colour, git status inline.

```c
brew install eza
```

[**bat**](https://github.com/sharkdp/bat) replaces `cat`. Syntax highlighting, line numbers, automatic paging.

```c
brew install bat
```

## My Exact File. You Can Use It.

Here is **my actual** `./.zshrc`, not some made up version.

```c
PROMPT='→ '

eval "$(fnm env --use-on-cd --shell zsh)"

# Plugins
# Must come in first
source $(brew --prefix)/share/zsh-autocomplete/zsh-autocomplete.plugin.zsh
source $(brew --prefix)/share/zsh-autosuggestions/zsh-autosuggestions.zsh
source $(brew --prefix)/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh

source <(fzf --zsh)

eval "$(starship init zsh)"
```

You’ll notice zoxide and bat aren’t in there. *I tried them, didn’t think I needed them*.

The point isn’t to install everything, it’s to **install** what you **really need** *(another reason Warp was overkill for me)*.

Feel free to copy it, run `source ~/.zshrc`, open a new terminal window. *That's your 20 minute conversion completed.*

## What I’ll Give Warp Credit For

*Warp is a product good for a type of person.*

If you’re new to the terminal, then Warp is a good start. The AI error explanations, visual command blocks, searchable history, everything works out the box. No config needed, no plugins, just open and you are good.

*I completely understand that.*

However if you’ve been using the terminal for a few years, you don’t need holding, you need **speed and clarity**. *(Personally I do think you should learn terminal basics as a first step)*.

Another thing Warp does well is teams, sharing prompts, shared workflows, notebooks. **However** my **problem** with this is, convincing your whole engineering team in practice to use a certain terminal, is near impossible *(speaking from experience)*.

## Start Here

*If you have* **5 minutes**: Copy my `.zshrc` above and run `source ~/.zshrc`. You will also need to install the plugins *(use AI to help you)*.

*If you have* **15 minutes**: *Run all 6 brew installs. See which ones you like.*

*If you have* **30 minutes**: Customise your Starship prompt.

I personally think your terminal should be **fast, quiet, and free**.

*I am not affiliated with Warp, Starship, or any of the tools mentioned. All thoughts are my own.*

[![Alex Dunlop](https://miro.medium.com/v2/resize:fill:60:60/1*uybQ98Ulg8xZgz9X6V5mBw.jpeg)](https://medium.com/@alexjamesdunlop?source=post_page---post_author_info--63113669ffe4---------------------------------------)[3 following](https://medium.com/@alexjamesdunlop/following?source=post_page---post_author_info--63113669ffe4---------------------------------------)

Engineer at Popp AI. Volunteer at Aruuri. Passionate about learning/collaborating. Trying to leave a positive contribution for the dev community.

## Responses (5)

Benedek Molnar

What are your thoughts?

```c
Working in multi cloud environments I find warp to be far more useful for cli tool calling aws, terraform, az. Etc than for simple terminal commands
```

5

```c
I’ve been using Warp from the beginning and agree, I think they’ve lost their way. I used it mainly for this bash commands, awk one-liners, and a quick ask ai something. I’m 100% bash, and using some of the tools you mentioned. Any reason in your opinion to switch to zsh?
```

8

```c
WOW Alex thank you so much for this post! Great job! This is so helpful!
```

17

[View list](https://medium.com/@molnar.benedictus/list/reading-list?source=post_page---list_recirc--63113669ffe4-----------predefined%3Afb06a7b34edd%3AREADING_LIST----------------------------)