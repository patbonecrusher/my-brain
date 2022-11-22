---
creation date: 2022-11-21 23:15
modification date: Monday 21st November 2022 23:15:42
tags: engineering/devops/macOS, engineering/devops/macOS/security, today_i_leaned
---

# Disable code signature verifications altogether during regression testing

## Disabling SIP

1.  Boot into recovery mode
2.  Open Terminal
3.  csrutill disable

## No need to disable SIP

```
spctl developer-mode enable-terminal
```

  
This is in a regular Terminal window, not in recovery mode. Next, go to System Preferences -> Security & Privacy -> Privacy, and scroll down till you see an entry for "Developer Tools." Authenticate, tick the checkbox next to Terminal, and done!

![[Pasted image 20221121231814.png]]
![[Pasted image 20221121231838.png]]