
## Chafa

```cardlink
url: https://hpjansson.org/chafa/gallery/
title: "Chafa: Terminal Graphics for the 21st Century"
description: "Turn pictures and animations into top-notch terminal graphics and ANSI art."
host: hpjansson.org
favicon: https://hpjansson.org/fav-1.gif
image: https://hpjansson.org/chafa/img/chafa-logo-still.png
```

Terminal graphics for the 21st century.

Useful to display image inside a terminal.

## Atuin

Atuin replaces your shell history with an SQLite database and records additional context for your commands. With this context, Atuin gives you a faster and better search of your shell history!

Additionally, Atuin (optionally) syncs your shell history between your machines! Fully end-to-end encrypted, of course.

You may use either the server I host or host your own! Or don't use sync at all. As all history sync is encrypted, I couldn't access your data even if I wanted to. And I don't want to.

### In .zshrc file
```zshrc
eval "$(atuin init zsh --disable-up-arrow)"
bindkey '^r' _atuin_search_widget

# depends on terminal mode
bindkey '^[[A' _atuin_search_widget
bindkey '^[OA' _atuin_search_widget
```

---
#### references

```cardlink
url: https://atuin.sh/docs/guide
title: "Getting Started | Atuin"
description: "Atuin replaces your existing shell history with a SQLite database, and records"
host: atuin.sh
favicon: /img/favicon.ico
```
