# First Git Commands 
**[DW]** The episode before this is "Git and Github" which is about concept. Here, this episode moves to hands-on use of Git. If we provide a link to the setup instruction, it will help with the transition from concept to practical. [/DW]

You should have already completed the setup instructions for this workshop and have Git installed. Launch a command line environment (in Windows launch “Git Bash” from the Start Menu, on Linux or Mac start a new Terminal). We will use this command line interface throughout these materials, we prefer this for educational reasons because the command line is a common environment for all the operating systems.

You must provide some extra information before it is ready to interact with Git.
The information is related to the person who uses Git and it gives the identity of the user in any project which you might work on your computer. In collaborative projects this is used to distinguish who has made what changes. You only need to perform the above commands once for each new computer Git is installed on.

**[DW]** A little more hand holding might be useful, i.e. show a picture of Bash, and then explain the git config commands. [/DW]

```bash
 git config --global user.name "FIRST_NAME LAST_NAME"   # Use the name that you wish to be identified 

 git config --global user.email "email@example.com"  # Use your email that is linked with your GitHub 
 ```

 ## Creating a Repository 
Now Git is ready and we will use it in a new project.
In Git terminology a project is called a repository (frequently shortened to repo). 
Let's start a project within your directories. Let's create a directory called 'cooking' where we will store some folders and recipes. We want 'cooking' to be immediately under our home directory, e.g. \Users\mary\cooking 

Within 'cooking' we create (with `mkdir`) other directories: 'recipes', 'tools', 'videos'. We go to the directory recipes and we create files 'pizza.md' and 'cake.md' files.
```bash 
pwd 
```
Output
```bash 
 \Users\mary\
 ```
 ```bash
mkdir cooking 
cd cooking
```
```bash 
pwd 
```
Output
```bash 
 \Users\mary\cooking
 ```
 ```bash
mkdir recipes tools videos
ls
```
Output
```bash
recipes	tools		videos
```
Create pizza.md and cake.md

```bash
touch pizza.md cake.md
ls
```

**[DW]** An output needing for the 'ls' command just above here. [/DW]

## Create a Git repository  
To start using Git with our recipes we need to create a repository for it. Make sure the current working directory for your terminal is recipes and run:  **git init**

```bash
git init
```
Output

```bash
Initialized empty Git repository in /Users/mary/cooking/recipes/.git/
``` 
If I want to see  all the files is in the recipes directory run **ls -a**

```bash
ls -a
```
Output

```bash
.		..		.git		cake.md		pizza.md
``` 
We can see the hidden directory .git in the recipes directory, this signifies that it is a Git directory.
In general we can create various Git repositories within your projects. Whatever happens in those folders, whatever git commands you run, whatever history is stored, they are completely separated and not connected. 
**BEWARE** when you initialise a Git repository inside a folder all the nested folders within it are automatically in the Git repository (there is no need to initialise Git within the directory again).

It is a common mistake to create Git directories in some or all the subdirectories, this complicates the process and end in error messages.

The folder tree of this project should look like the picture. Only the directory recipes is a Git repo. (the Git sign is added for visualizing that we have initiated a Git repo, you will not see it at your computer)

**[DW]** Picture belog does not show up [/DW]

![Directories_tree](./fig/repo_directories_tree.png)

## Master and main branches (You DON'T need to TYPE the COMMANDS in this section if you've done them in the set-up)
 Traditionally, the default branch name in Git whenever you init a repository was master. However, the sensitivity of the online community has shifted lately and GitHub now use 'main' as the default name instead. 
 You can read the reason in this [link](https://www.theserverside.com/feature/).

**If you have done this step in the set up page and you don't need to repeat it here**

If you are using Git version 2.28 or higher (you can find the version you are using with git --version) you can change the default branch name to 'main' for all new repositories with:

```bash
git config --global init.defaultBranch main
```
With this command the word "master" in the Git code is replaced by the word "main" and GitHub will use it from then on. So there is an alignment for the main branch between Git and GitHub.

For existing repositories or if your Git version is lower than 2.28, you can create the master branch normally and then re-name it with:

 ```bash
git branch -m master main
```


## Always Check!  Git Status

Before we do anything else run the **git status**

```bash
git status
```
Output

```bash
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	.DS_Store
	baking/
	food/

nothing added to commit but untracked files present (use "git add" to track)

```
This is a very useful command that we will use a lot. It should be your first point of call to figure out the current state of a repository and often suggests commands that can be used for different tasks.

Don’t worry about all the output for now, the important bit is that the 2 directories and their files we already have are untracked in the repository (directory).

 We want to add the files to the list of files tracked by Git. Git does not track any files automatically and you need make a conscious decision to add a file. 
 At the next session **[DW]** check session name [/DW/] 4_Git_Commit_Commands you will be instructed how to make changes over time and save them in tracked versions indicated by messages.

## Common mistake of creating multiple Git repos

As discussed above, creating Git repositories within an existing Git repository will cause confusion!! 

![Warning](./fig/Warning_repo.png)




To solve this problem you need to **delete the .git** where you don't need it.

You need to go to the relevant directory and delete it with the command **rm -r**

Do not follow these commands unless you have made the mistake.
Lets say that the directory food inside the recipes directory was accidentally made a git repo.
```bash 
food $ git init 
```


Output

```bash 

Initialized empty Git repository in /Users/mary/cooking/recipes/food/.git/
(base) mary  food % ls -a
.		..		.git		curry.md	pizza.md
```
Always check with **ls -a** and you observe that amongst the files in the food directory there is a .git hidden directory that you don't want it to be there as it will confuse Git. 
You need to remove it using the **rm -r** command for removing directories.

Make sure you are in the food directory 
```base
food % rm -r .git
(base) mary food % ls -a 
```
Output
```base
.		..		curry.md	pizza.md
```
Now there is only the parent directory (recipes) that is a Git directory and we can use Git as main branch. 

Another way (which is recommended) is to go one directory ahead (ie recipes) and we remove the .git repository at foods. ALWAYS CHECK with **pwd**

``` bash
cd ..
pwd 
---------
Output 
-------
/Users/mary/cooking/recipes
```
``` bash 
recipes % rm -rf food/.git
cd food # go to the nested directory
food % ls -a
```
-----
Output
-----
```bash
.		..		curry.md	pizza.md
```
This is recommended when there are many nested git directories in the parent (ie recipes).
But be careful the syntax! Running this command in the wrong directory will remove the entire Git history of a project you might want to keep. Therefore, always check your current directory using the command `pwd`.

In this section we present:

- How to create a Git repo using the git init command
- How to avoid the confusion between master and main commands and  always use the main command in Git which is a common command with GitHub.
- How to always check the current state of the repository with the git status command. 
- How to correct mistakes which involved accidental multiple Git repos that confuse the Git software.

Key Points 

**[DW]** The first three are not covered in this episode[/DW]

* Use **git config -- global** to configure a user name, email address, editor, and other preferences once per machine.
* **git config -h**  Opens the use of the config, Opens the Git manual
* **git config --help**
* **git init** initializes a repository.
* Git stores all of its repository data in the **.git** directory.
* **rm -r .git** # Removes the git directory (rm -r <directory name>)
