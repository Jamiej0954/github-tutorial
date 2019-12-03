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
3. Enabling Preview
  * In the top-left corner of the IDE, click **CS50 IDE** > Preferences
  * When the new window opens, on the LEFT side, click **User Settings**
  * On the **RIGHT** side, toggle **Enable Preview** to **ON**
4. Enabling Auto-Save
  * If you closed the Preferences tab, re-open it: **CS50 IDE** > Preferences
  * When the new window opens, on the **LEFT** side, scroll down and click **Experimental**
  * On the **RIGHT** side, change the **Auto-Save** dropdown to On **Focus Change**

> SSH key is a better option than HTML because it doesn't need the user to enter their password of their GitHub account everytime the user made a change and wanted to push the change to the remote repo. Whereas the HTML requires the user to enter their password everytime the user push their change for security purposes.

---
#### Repository Setup
To create a local repository, you need to do the following:
1. cd into a folder where you want your repo to live in
2. Type `mkdir "The name of the directories"` to create a empty directories (You don't need the quote around the filename)
3. Type `touch README.md` to create a file within the empty directories
> Make sure that when you name your file, there's no space between. Instead of a space, use dash.
4. Type `git init` to initialize git, so that the git command can run in the local repo (You have initialize the git when you see `(master)` next to the directories that you are working on)
5. Next you want to go into the README.md file. Here you can type anything into the file (Type `c9 README.md` to open file)
6. Once you have type in any text into the file, you need a way to save the change you made to the file. To do this, you use `git add .` to select **Everything** you change and wanted to save.
> `git add .` add everything you change to the stage. Once something is stage, it's ready to be save. It's sort of selecting what you wanted to save before doing so. If you do not want to save all the change you made and want to select file manually, you can type `git add "filename"` and this will select individual item to be put on stage.
7. Once you stage a file you would want to save the change for future use and to do this, you use `git commit -m "Enter message here`
> `git commit -m "message"` is the save as saving a snapshot of the change and the message following the commit state what is change. The message needs to be in present tense and be detailed. A bad example of commit message will be "Create stuff". A good example would be "Create a empty repo".
8. Next you would want to go to your Github account to create a repo that's remote.
> A **Remote repo** is versions of your project that are hosted on the Internet or network somewhere.
   * Once your in your GitHub account, in the top right corner, there's a plus sign. Click on that and you will have the drop down option. Select **New Respository**
   * Next you need to name the respository in the remote exactly the same name as the repo in your local. Then you will need to click create repository.
   * Then at the top of your screen there will be a option between HTML and SSH. Make sure to select the SSH.
9. Finally, you would want to create a bridge between your local and remote repo. To do so, type the following into the command line:
```
git remote add origin git@github.com:Jamiej0954/example.git
git push -u origin master
```
> It should inculde your GitHub user name and the name of the repo.

The git remote command is essentially an interface for managing a list of remote entries that are stored in the repository.

---
#### Workflow & Commands
- When constantly updating your file within the repo, it should always be a habit to check the status to see any untrack changes that has been made to the file. To do this you type `git status` to see the status of the directories and repo that you're in. If the status contain any red text, it means that it has identify a file that have untrack and have change.
- When this occur you need to add it to the stage by typing `git add .` to stage all changes that you have made.
- After the staging, you would commit the change (`git commit -m "Message`)
- Finally, you need to push the change to your remote repo by typing `git push`
> You have already made the bridge between the local and remote repo, so when you push the change, it will show up in your remote repo.
   * Use `git remote -v` to see where the changes of your file is push to.

_Look at the Initial setup section to read the explaination of each type of command_

---
#### Rolling Back Changes