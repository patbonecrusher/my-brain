---
creation date: 2023-04-18 22:26
modification date: Tuesday, 18th April 2023, 22:26:53
tags: today_i_leaned, engineering/devops/serial
---

# Picocom as a serial monitor replacement

### Picocom[⇠](https://www.espruino.com/Alternative+Terminal+Apps#picocom)

Picocom is installed by default in Ubuntu. Try typing `picocom` in a shell to see if it is installed in your OS. If it's not, we'd recommend using Minicom (below).

Then run picocom to connect to the device (instead of /dev/ttyACM0, use the device name you got above):

```
picocom --baud 9600 --flow n /dev/ttyACM0
```

To copy, highlight the text and press `Shift + Ctrl + C`. To paste, press `Shift + Ctrl + V`. Use `Ctrl+A`, then `Ctrl+X` to exit.