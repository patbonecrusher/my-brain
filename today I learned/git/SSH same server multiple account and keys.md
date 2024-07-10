---
creation date: 2024-05-13 22:09
modification date: Monday, 13th May 2024, 22:09:27
tags:
  - today_i_leaned
  - engineering/scm/git
---
# Why Multiple SSH keys?

There are numerous reasons you may need to use multiple SSH keys for accessing GitHub and BitBucket

You may use the same computer for work and personal development and need to separate your work.

When acting as a consultant, it is common to have multiple GitHub and/or BitBucket accounts depending on which client you may be working for.

You may have different projects you're working on where you would like to segregate your access. 

Whatever your reason may be, handling this in a standard Mac/linux PC setup is difficult.

Use the following guide to ensure you code is easy to manage, all changes correspond to the correct identity,
 and checking out new repositories is not a hassle.

This guide will work on Mac OS, most Linux distributions and on Windows when using Cygwin, GitBash, or Windows Subsystem for Linux
with OpenSSH installed.

<b>You must have Git 2.13 or above and OpenSSH installed to use the following guide.</b>

## 1. Create keys 

You will need one key for each different account you will use on either GitHub or BitBucket.  

Whichever site you have more identities with determines how many keys you will need.

A single key can act both as a GitHub and BitBucket key but cannot be associated with more than one BitBucket or GitHub account.

If you already have created a key in ~/.ssh/id_rsa (the default location), you may use that in place of the ~/.ssh/msmith key
in my examples or you can leave that key and add additional keys for the other identities.

Create the keys and ssh-add them (make sure to enter a secure password and do not just leave it blank)
```bash
$  ssh-keygen -t rsa -b 4096 -f ~/.ssh/key1_rsa -C "msmith@example.com" 
Generating public/private rsa key pair.
Enter passphrase (empty for no passphrase): ************
Enter same passphrase again: 
Your identification has been saved in /Users/me/.ssh/key1_rsa.
Your public key has been saved in /Users/me/.ssh/key1_rsa.pub.
The key fingerprint is:
...
$  ssh-add ~/.ssh/key1_rsa


$  ssh-keygen -t rsa -b 4096 -f ~/.ssh/key2_rsa -C "jblige@example.com" 
Generating public/private rsa key pair.
Enter passphrase (empty for no passphrase): ************
Enter same passphrase again: 
Your identification has been saved in /Users/me/.ssh/key2_rsa.
Your public key has been saved in /Users/me/.ssh/key2_rsa.pub.
The key fingerprint is:
...

$ ssh-add ~/.ssh/key2_rsa
```

## 2. Setup ~/.ssh/config

Create a file in ~/.ssh/config (if it does not already exist).  You must make sure it is readable only by the owner
and the group and public bits are set off.
```bash
touch ~/.ssh/config
chmod 600 ~/.ssh/config
```

We now need to add SSH configuration that specifies the github and bitbucket hostnames but with a suffix appended to qualify
which key to use.  We set the `HostName` to the correct github.com or bitbucket.org address.

Note: Linux users should either omit `UseKeychain yes` or add `IgnoreUnknown UseKeychain` (thanks soulofmischief)
```
~/.ssh/config
...

Host github.com-msmith
HostName github.com
UseKeychain yes
AddKeysToAgent yes
User git
IdentityFile ~/.ssh/msmith_rsa
IdentitiesOnly

Host bitbucket.org-msmith
HostName bitbucket.org
UseKeychain yes
AddKeysToAgent yes
User git
IdentityFile ~/.ssh/msmith_rsa
IdentitiesOnly

Host github.com-jblige
HostName github.com
UseKeychain yes
AddKeysToAgent yes
User git
IdentityFile ~/.ssh/jblige_rsa
IdentitiesOnly

Host bitbucket.org-jblige
HostName bitbucket.org
UseKeychain yes
AddKeysToAgent yes
User git
IdentityFile ~/.ssh/jblige_rsa
IdentitiesOnly

...
```
## 3. Add public keys to GitHub and BitBucket

Log into GitHub for each user and add the keys from ~/.ssh/xxxxx.pub to the respective users authorized SSH keys.

For more information on this see:
https://confluence.atlassian.com/bitbucket/set-up-an-ssh-key-728138079.html

or


https://help.github.com/en/articles/adding-a-new-ssh-key-to-your-github-account

## 4. Create key specific .gitconfig

You will need a single directory where all code that corresponds to a given key will be checked out to.

I prefer to keep all those directories in one directory in my home `~/src` and I name them according to the account
name associated with the key

```bash
mkdir -p ~/src/msmith
mkdir -p ~/src/jblige
```

In each directory put a `.gitconfig` file.
```
~/src/msmith/.gitconfig
...
[user]
  email = msmith@example.com
    
[url "git@bitbucket.org-msmith"]
  insteadOf = git@bitbucket.org
  
[url "git@github.com-msmith"]
  insteadOf = git@github.com
```
```
~/src/jblige/.gitconfig
...
[user]
  email = jblige@example.com
  signingkey = ABCD1234
  
[url "git@bitbucket.org-jblige"]
  insteadOf = git@bitbucket.org
  
[url "git@github.com-jblige"]
  insteadOf = git@github.com
  
[commit]
  gpgsign = true
```
This way, I use the correct email address for both keys and have even set up automatic commit signing for jblige.
I also rewrite all the hostnames for the original SSH connections to the correctly suffixed hostnames I created
in the SSH config file.

For more information about GPG signing see:
https://help.github.com/en/articles/signing-commits

or

https://confluence.atlassian.com/bitbucketserver/using-gpg-keys-913477014.html

## 5. Setup Git config `includeif`

To activate the .gitconfig files in ~/src/*, edit the .gitconfig file in your home directory and add an `includeif`
statement for each of the .gitconfig files referencing the directory they are in

```
~/.gitconfig
...

[includeif "gitdir:~/src/msmith/"]
	path = ~/src/msmith/.gitconfig
	
[includeif "gitdir:~/src/jblige/"]
	path = ~/src/jblige/.gitconfig
	
```

<b>Do not forget the trailing slash in the `[includeif "gitdir:...` statement.</b> (thanks loizoskounios)

## 6. Cloning the repositories

You then clone the code using the SSH clone address (i.e. git@bitbucket.org... or git@github.com..., not https://bitbucket.org... nor https://github.com...)
into the directory that corresponds to the key you want to use for that clone.

```bash
$  cd ~/src/msmith
$  git clone git@github.com:someuser/somerepo.git
...

```

Because of the rewriting, git will actually attempt to clone using the suffixed address corresponding to the configuration in
the SSH config file but because of the SSH configuration it will use the original hostname when actually connecting to the host
ensuring you use the right key.

All commits/pulls/pushes to/from those repositories will use the corresponding config/key/account.


### Credits

This work was adapted from the following
* https://medium.com/@trionkidnapper/ssh-keys-with-multiple-github-accounts-c67db56f191e
* https://gist.github.com/jexchan/2351996
* http://blog.bennycornelissen.nl.s3-website-eu-west-1.amazonaws.com/post/juggling-multiple-git-identities/

---
#### references

```cardlink
url: https://medium.com/@trionkidnapper/ssh-keys-with-multiple-github-accounts-c67db56f191e
title: "SSH Keys with Multiple GitHub Accounts"
description: "This article explains how to manage multiple SSH keys for different GitHub.com accounts so that you can access multiple accounts and…"
host: medium.com
favicon: https://miro.medium.com/v2/1*m-R_BkNf1Qjr1YbyOIJY2w.png
image: https://miro.medium.com/v2/resize:fit:1200/1*2lI3BuvRv-YEUoTdpjxyig.jpeg
```


```cardlink
url: https://gist.github.com/jexchan/2351996
title: "Multiple SSH keys for different github accounts"
description: "Multiple SSH keys for different github accounts. GitHub Gist: instantly share code, notes, and snippets."
host: gist.github.com
favicon: https://github.githubassets.com/favicons/favicon.svg
image: https://github.githubassets.com/assets/gist-og-image-54fd7dc0713e.png
```


```cardlink
url: http://blog.bennycornelissen.nl.s3-website-eu-west-1.amazonaws.com/post/juggling-multiple-git-identities/
title: "Juggling multiple Git identities"
description: "This blog post explains how you can have multiple Git identities and make sure you automatically use the correct identity whenever you commit something."
host: blog.bennycornelissen.nl.s3-website-eu-west-1.amazonaws.com
```



```cardlink
url: https://gist.github.com/yinzara/bbedc35798df0495a4fdd27857bca2c1
title: "Managing SSH keys and repo cloning using multiple accounts on GitHub and BitBucket"
description: "Managing SSH keys and repo cloning using multiple accounts on GitHub and BitBucket - github_bitbucket_multiple_ssh_keys.md"
host: gist.github.com
favicon: https://github.githubassets.com/favicons/favicon.svg
image: https://github.githubassets.com/assets/gist-og-image-54fd7dc0713e.png
```



