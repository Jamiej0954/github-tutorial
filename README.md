## GitHub Tutorial

_By Jamie Jiang_

--- 
#### Git vs GitHub

Git is a **version control** that allow you to keep track of your source code history.
> Version control is the management of changes to documents, computer programs, web sites, etc.

GitHub is the service of project that uses Git to function. It's cloud-based hosting service that lets you manage Git **repositories** . In other words, it's a good platform to do collaboration projects. 
> Repositories or “repo” for short, is a storage location.

---
#### Initial Setup
This setup is **only** done once in the beginning when the user log into their [Github IDE.](ide.cs50.io)

Follow the following direction to setup your IDE:

1. Configuring your user info
   * In your command line, type the following: `git config --global user.email "you@example.com"`
   * Remember to use **YOUR** email address, and you need the quote around your email.
   * Then type `git config --global user.name "Your Name"`
2. Generating and connecting an SSH key
   * Make sure you are in the root directory by doing `cd ~`
   * `ssh-keygen -t rsa -b 4096 -C "you@example.com"` then slowly press `ENTER`repeatedly until you see something like:
```
The key's randomart image is:
+--[ RSA 4096]----+
|       .o o..    |
|       o +Eo     |
|        + .      |
|         . + o   |
|        S o = * o|
|           . o @.|
|            . = o|
|           . o   |
|            o.   |
+-----------------+
``` 
   * `eval "$(ssh-agent -s)"` starts the agent in the background
   * `ls -al ~/.ssh` you should now see a file named `id_rsa.pub`
   * `cat ~/.ssh/id_rsa.pub` then copy all of the result to your clipboard (it should start with ssh-rsa and end with your email address)
   * Go to [https://github.com/settings/keys](https://github.com/settings/keys) > New SSH Key
     * Title: ide50
     * Key: paste your ssh key
     * Press the green **Add SSH key**  button
   * Back in your cs50 IDE, do `sudo nano ~/.ssh/config`
   * Paste the following:
```
 Host github.com
 Hostname ssh.github.com
 Port 443
```
   * `control`+`X` to exit, then press `Y` then `ENTER`
   * `ssh -T git@github.com`
   * Type `yes`, press `ENTER`, and you should see:
> Hi "username"! You've successfully authenticated, but GitHub does not provide shell access.

> SSH key is a better option than HTML because it doesn't need the user to enter their password of their GitHub account everytime the user made a change and wanted to push the change to the remote repo. Whereas the HTML requires the user to enter their password everytime the user push their change for security purposes.

---
#### Repository Setup

--- 
#### Workflow & Commands

---
#### Rolling Back Changes