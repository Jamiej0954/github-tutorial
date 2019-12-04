## GitHub Tutorial

_By Jamie Jiang_

---
#### Git vs GitHub

Git is a **version control** that allow you to keep track of your source code history.
> Version control is the management of changes to documents, computer programs, web sites, etc.

GitHub is the service of project that uses Git to function. It's cloud-based hosting service that lets you manage Git **repositories**. In other words, it's a good platform to do collaboration projects.
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
2. Type `mkdir "The name of the directory"` to create a empty directory (You don't need the quote around the filename)
3. Type `touch README.md` to create a file within the empty directory
> Make sure that when you name your file there's no space between. Instead of a space, use dash.
4. Type `git init` to initialize git, so that the git command can run in the local repo (You have initialize the git when you see `(master)` next to the directory that you are working on)
5. Next you want to go into the README.md file. Here you can type anything into the file (Type `c9 README.md` to open file)
6. Once you have type texts into the file, you need a way to save the change you made to the file. To do this, you use `git add .` to select **everything** you change and wanted to save.
> `git add .` add everything you change to the stage. Once something is stage, it's ready to be save. It's sort of selecting what you wanted to save before doing so. If you do not want to save all the change you made and want to select file manually, you can type `git add "filename"` and this will select individual item to be put on stage.
7. Once you stage a file you would want to save the change for future use and to do this, you use `git commit -m "Enter message here`
> `git commit -m "message"` is the save as saving a snapshot of the change and the message following the commit state what is change. The message needs to be in present tense and be detailed. A bad example of commit message will be "Create stuff". A good example would be "Create a empty repo".
8. Next you would want to go to your Github account to create a repo that's remote.
> A **Remote repo** is versions of your project that are hosted on the Internet or network somewhere.
   * Once your in your GitHub account, in the top right corner, there's a plus sign. Click on that and you will have the drop down option. Select **New Respository**
   * Next you need to name the respository in the remote exactly the same name as the repo in your local. Then you will need to click create repository.
   * Then at the top of your screen, there will be a option between HTML and SSH. Make sure to select the SSH.
9. Finally, you would want to create a bridge between your local and remote repo. To do so, type the following into the command line:
```
git remote add origin git@github.com:Jamiej0954/example.git
git push -u origin master
```
> It should inculde your GitHub user name and the name of the repo.

The git remote command is essentially an interface for managing a list of remote entries that are stored in the repository.

---
#### Workflow & Commands
- When constantly updating your file within the repo, it should always be a habit to check the status to see any untrack changes that has been made to the file. To do this you type `git status` to see the status of the directory and repo that you're in. If the status contain any red text, it means that it has identify a file that have untrack and have change.
- When this occur you need to add it to the stage by typing `git add .` to stage all changes that you have made.
- After the staging, you would commit the change (`git commit -m "Message`)
- Finally, you need to push the change to your remote repo by typing `git push`
> You have already made the bridge between the local and remote repo, so when you push the change, it will show up in your remote repo.
   * Use `git remote -v` to see where the changes of your file is push to.

_Look at the Initial setup section to read the explaination of each type of command_

---
#### Rolling Back Changes
Let say you accidently made a mistake when you:
1. Edit the wrong file
> Solution: Type `git checkout filename`. (Replace the filename with the actual name of the file). This help to undo the change you made to the file.
2. Adding something unwanted onto the stage
> Solution: Type `git reset HEAD`. This remove the item off the stage.
3. Made a wrong commit
> Solution: Type `git log` to see the history of the changes you made. Find the commit that you wanted to undo. It will be follow by a long string of letter and number (the serial number). You'll need that serial number to revert the commit that you made. Type `git revert serial#` and this will undo the commit.
   * To leave the `git log` screen, press "q" on the keyboard.

---
#### Error handling
Let say you accidently made a mistake when you:
1. Initialize git in the wrong directory
> Solution: Type `rm -rf .git`. This will delete the git init within the directory.
2. Create a uneccessary repo in local and remote
> Solution: To remove repo from local you can use `rm -rf repo-name` to delete the repo. Or you can choose to delete the entire directory. To delete the entire directory, you go to a level above the dircetory that you want to remove and use `rm -rf directory name`. To remove repo from remote, there's a trash-bin icon and you click into the file to delete the file. If you want to delete the entire repo, you can go to setting within your repo and scroll all the way down until you see `Delete this Repo` (For the first time it will ask for your GitHub password, but later on it will delete with asking the user for password. It will also require you to enter the name of the repo that you want to delete.)

---
#### Collaboration
`git clone`- It copy a repository from the remote onto the local using the SSH key.
If the user wanted to clone someone else repo, it will look like:
`git clone SSH url of the other user` in their command line

Forking - It copy a repository and branches it off of the original allowing you to clone then make changes that can be saved, which you can push and request a pull request.
   * The save changes will then be transfer to the original user and the user can sumbit a pull request to the original user to pull in the changes that they made.

> The option between clone and forking is within the repo of the other user. Either option will require you to choose between SSH and HTML.

**Cloning a repository that isn't yours won't allow you to push any changes you made to the remote repo.**

`git pull`- Takes all the changes that are made from the remote repository onto the local repository and this usually happen when two or more people are working on the same file. Each person will contribute and the others will need to pull in the changes into their local repo.

When collaborating with other people on the same project, at the same time, there will be a **merge conflict**.
> The conflict arises when two separate branches have made edits to the same line in a file, or when a file has been deleted in one branch but edited in the other.

A possible solution to this will be that one user will have the repo open while the others have it closed, meaning that you're only allowing one person to work on the repo one at a time.