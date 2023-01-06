---
creation date: 2023-01-06 14:44
modification date: Friday, 6th January 2023, 14:44:03
tags: today_i_leaned, engineering/devops/git
---

# Untitled

1.  Delete All local tags. (Optional Recommended)
    
    ```bash
    git tag -d $(git tag -l)
    ```
    
2.  Fetch remote All tags. (Optional Recommended)
    
    ```bash
    git fetch
    ```
    
3.  Delete All remote tags.
    
    ```bash
    # Note: pushing once should be faster than multiple times
    git push origin --delete $(git tag -l) 
    ```
    
4.  Delete All local tags.
    
    ```bash
    git tag -d $(git tag -l)
    ```