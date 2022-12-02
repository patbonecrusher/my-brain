---
creation date: 2022-11-13 22:15
modification date: Sunday 13th November 2022, 22:15:08
tags: engineering, engineering/coding, engineering/coding/webpack, today_i_leaned
---

# webpack error

When seeing this error:
```shell
Error: error:0308010C:digital envelope routines::unsupported
```

Run this before `npm run start`

```shell
export NODE_OPTIONS=--openssl-legacy-provider
```