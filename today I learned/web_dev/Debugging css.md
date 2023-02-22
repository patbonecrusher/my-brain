---
creation date: 2023-02-21 22:49
modification date: Tuesday, 21st February 2023, 22:49:56
tags: today_i_leaned, engineering/language/css
---

# Debugging CSS

```
* { background-color: rgba(255,0,0,.2); }
* * { background-color: rgba(0,255,0,.2); }
* * * { background-color: rgba(0,0,255,.2); }
* * * * { background-color: rgba(255,0,255,.2); }
* * * * * { background-color: rgba(0,255,255,.2); }
* * * * * * { background-color: rgba(255,255,0,.2); }
* * * * * * * { background-color: rgba(255,0,0,.2); }
* * * * * * * * { background-color: rgba(0,255,0,.2); }
* * * * * * * * * { background-color: rgba(0,0,255,.2); }
```

Different depths of nodes will use different colors allowing you to see the size of each element on the page, their margin, and their padding. Now you can quickly identify inconsistencies.