+++
title = "Doom Emacs, Hunspell, and MacOs"
author = ["Roberto Zoia"]
date = 2021-04-08
draft = false
+++

Doom Emacs uses [`spell-fu`](https://gitlab.com/ideasman42/emacs-spell-fu) as the default highlighter for spellchecking. `spell-fu` can use several options like `aspell`, `hunspell`, `enchant`, etc. for the actual spellchecking. I prefer to use [Hunspell](https://hunspell.github.io/).

The process to install and configure `hunspell` to work for Doom Emacs is simple:

- Use [homebrew](https://brew.sh/) to install `hunspell`:

<!--listend-->

```bash
$ brew install hunspell
```

- `hunspell` doesn't install dictionaries. Download them from the [aspell](http://wordlist.aspell.net/dicts/) webpage and store them in `~/Library/Spelling`. Check that `hunspell` is recognizing your dictionaries.

<!--listend-->

```bash
$ hunspell -D
```

- Tell Doom Emacs you are using `hunspell` in your `init.el` file:

<!--listend-->

```emacs-lisp
(...)
:checkers
    (spell +hunspell)       ; tasing you for misspelling mispelling
```

- While Doom will take care of telling Emacs which spell checker you are using, _you need to specify a default dictionary_. Otherwise you will go crazy wondering why `spell-fu` is marking every word in your documents as incorrect. (This applies not only for `hunspell` but also for `aspell` and `enchant`.)

  You can get a list of valid dictionary names by changing the dictionary manually within Emacs, i.e. `M-x` `ispell-change-dictionary`.

<!--listend-->

```list
(setq ispell-dictionary "english")
```
