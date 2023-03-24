---
creation date: 2023-03-22 10:38
modification date: Wednesday, 22nd March 2023, 10:38:37
tags: today_i_leaned, engineering/shell/scriptin
---

# Prompting for confirmation in a script

```bash
confirm() {
    # call with a prompt string or use a default
    read -r -p "${1:-Are you sure? [y/N]} " response
    case "$response" in
        [yY][eE][sS]|[yY]) 
            true
            ;;
        *)
            false
            ;;
    esac
}
```

```bash
confirm "Would you really like to do a push?" && hg push ssh://..
```

```bash
confirm && hg push ssh://..
```
