---
creation date: 2023-04-29 16:29
modification date: Saturday, 29th April 2023, 16:29:15
tags: today_i_leaned, engineering/linux/dev
---

# container_of

```c
container_of(kobj, struct my_object, kobj)
              |            |          |
              |            |          |
              \------------+----------+--------------------------------\
                           |          |                                |
                           |          |                                |
         /-----------------/          |                                |
         |                            |                                |
         V              /-------------/                                |
+------------------+    |                                              |
| struct my_object | {  |                                              |
+------------------+    V                                              V
                   +------+                                         +------+
    struct kobject | kobj |; <-- You have a pointer to this, called | kobj |
                   +------+                                         +------+
    ...
};
```