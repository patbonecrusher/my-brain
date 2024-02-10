---
creation date: 2024-02-06 21:52
modification date: Tuesday, 6th February 2024, 21:52:36
tags:
  - today_i_leaned
  - computer/raspberry_pi
---

```zsh
❯ cat ~/.zshrc
##
# ⚠️ WARNING: Don't manually `source` your .zshrc file! This can have unexpected
# side effects.
# Instead, to apply changes, open a new terminal or restart your shell.
#

[[ -r ~/.zshenv/znap/znap.zsh ]] ||
    git clone --depth 1 -- https://github.com/marlonrichert/zsh-snap.git ~/.zshenv/znap

##
# Source Znap at the start of your .zshrc file.
#
source ~/.zshenv/znap/znap.zsh

export LANG=en_US.UTF-8
export LC_ALL=en_US.UTF-8

znap source sorin-ionescu/prezto modules/{environment,history,ssh}
znap source ohmyzsh/ohmyzsh plugins/asdf

# `znap prompt` makes your prompt visible in just 15-40ms!
#znap prompt sindresorhus/pure
# The same goes for any other kind of custom prompt:
#znap eval starship 'starship init zsh --print-full-init'
#znap prompt
eval "$(starship init zsh)"

#znap prompt ohmyzsh/ohmyzsh themes/clean
#znap prompt agnoster/agnoster-zsh-theme


##
# Cache the output of slow commands with `znap eval`.
#

# `znap source` starts plugins.
znap source marlonrichert/zsh-autocomplete

# `znap eval` makes evaluating generated command output up to 10 times faster.
znap eval iterm2 'curl -fsSL https://iterm2.com/shell_integration/zsh'

# `znap function` lets you lazy-load features you don't always need.
znap function _pyenv pyenv "znap eval pyenv 'pyenv init - --no-rehash'"
compctl -K    _pyenv pyenv

# `znap install` adds new commands and completions.
znap install aureliojargas/clitest zsh-users/zsh-completions

fortune | cowsay | lolcat
```

### Setting up zerotier
```
curl -s https://install.zerotier.com | sudo bash
sudo zerotier-cli join <accountid>
```

---
#### references


```cardlink
url: https://cloudzy.com/blog/test-disk-speed-in-linux/
title: "How to Test Disk Speed Using the Linux Command Line?|(Measure Disk Performance with fio,dd and Graphical Method)🏎️"
description: "💡 Note: Are slow disk speeds and subpar server performance hindering your Linux operations? It's a common bottleneck many face, but there's a straightforwa"
host: cloudzy.com
favicon: https://cloudzy.com/wp-content/uploads/favicon.png
image: https://cloudzy.com/wp-content/uploads/test-disk-speed-in-linux-using-commands-min.png
```


```cardlink
url: https://www.kevsrobots.com/blog/raspberrypi5-nvme-nas.html
title: "How to install an NVMe drive on a Raspberry Pi 5"
description: "Learn how to install an NVMe drive on a Raspberry Pi 5 and setup a NAS server."
host: www.kevsrobots.com
image: https://www.kevsrobots.com//assets/img/blog/nvme/nvme.jpg
```



```cardlink
url: https://starship.rs/guide/#🚀-installation
title: "Starship: Cross-Shell Prompt"
description: "Starship is the minimal, blazing fast, and extremely customizable prompt for any shell! Shows the information you need, while staying sleek and minimal. Quick installation available for Bash, Fish, ZSH, Ion, Tcsh, Elvish, Nu, Xonsh, Cmd, and Powershell."
host: starship.rs
favicon: https://starship.rs/icon.png
image: https://starship.rs/icon.png
```



```cardlink
url: https://www.jeffgeerling.com/blog/2023/testing-pcie-on-raspberry-pi-5
title: "Testing PCIe on the Raspberry Pi 5 | Jeff Geerling"
host: www.jeffgeerling.com
favicon: https://www.jeffgeerling.com/favicon-32x32.png
```




```cardlink
url: https://www.youtube.com/watch?v=w4X55XuxvTE
title: "Adding NVMe Storage to your Raspberry Pi 5 - No more SD cards!!!"
description: "One of the great benefits of the Raspberry Pi5 is access to PCIe. This means that the Pi 5 can use (and boot from) NVMe storage. In this video I show you how..."
host: www.youtube.com
favicon: https://www.youtube.com/s/desktop/1c21ae68/img/favicon_32x32.png
image: https://i.ytimg.com/vi/w4X55XuxvTE/maxresdefault.jpg
```


```cardlink
url: https://www.youtube.com/watch?v=odG7FbptgWQ&t=306
title: "Installing the Pimoroni NVMe Base on Raspberry Pi 5"
description: "A very basic intro to installing the NVMe Base under a Raspberry Pi 5.https://shop.pimoroni.com/products/nvme-baseMake sure your eeprom firmware is up to dat..."
host: www.youtube.com
favicon: https://www.youtube.com/s/desktop/1c21ae68/img/favicon_32x32.png
image: https://i.ytimg.com/vi/odG7FbptgWQ/maxresdefault.jpg?sqp=-oaymwEmCIAKENAF8quKqQMa8AEB-AH-CYAC0AWKAgwIABABGGUgUihMMA8=&rs=AOn4CLCCme7g48ZaVEs1oa6eHfpa1Axy0g
```
