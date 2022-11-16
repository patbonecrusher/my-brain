---
creation date: 2022-11-13 22:15
modification date: Sunday 13th November 2022, 22:15:08
tags: engineering, engineering/scm, engineering/scm/git, engineering/devops/git, today_i_leaned
---

## Problem statement
Given the following branches in git: We wanted to revert some changes in the **f5655** commit.

![bla](./attachments/Pasted%20image%2020221107230028.png)

---
## Steps
To do so:
```bash

# First, checkout the commit to be modified
git checkout f56554181e591ac4ef6b89fa09df147d9c4fd4dd

# Reset the commit (softly, to avoid losing changes).
# This has for effect of reverting the commit, leaving all associated
# changes in staged mode.
git reset --soft HEAD@{1}

# Make any modification you want to do to that commit, and commit
# them locally.
git commit -am "updated commit"

# Finally, re-apply all other commits over the new one.
git merge 46a606ffe6fc1bc35b7c2ff618ead624ff1c28cb
git merge 5c71b467901c34fdbf9b5974b9b885fbe4efe565
git merge 8296d46ca0a222ea3428dedecb16f763ae3bcfb7
git merge 1d28384293045add4cfc8b830a910a0a868e6a34
git merge 9b74088f999df942458d80aa6c4948ab88199afb
```

---
## Results
This will result in the following branch topo

![bla](./attachments/Pasted%20image%2020221107230650.png)


---
## Notes
If the branch has previously been pushed to a remote, a force push will be necessary as the history has been rewritten.