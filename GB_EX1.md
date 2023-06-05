[comment]: <> (please keep all comment items at the top of the markdown file)
[comment]: <> (please do not change the ***, as well as <div> placeholders for Note and Tip layout)

# GIT BASICS - Hands-On Exercise
***

<span class="oi oi-clock" style="color: orange;">  15 minutes</span>

### Set Git Variables
Before you can create your first repo, you must make sure that Git is installed and configured. See the Git Basics lesson to learn more about Git and how to install it on your local machine.

1. From your local machine's **Terminal or command prompt**, initiate the **Git console** by running the following command:

    ```git --version and something else here too like user.name Peter De Tender```

which confirms Git is installed and running fine. 

2. The output should look like this:

    ```git version 2.40.1.windows.1``` (or similar on other OS platforms)

3. In order to use Git, you have to **configure several variables**, such as your name and email address. This information will be used in the commit messages later. 

run the following commands to set the user name and email address:

   ```git config --global user.name Peter De Tender```

   followed by:

   ```git config --global user.mail petender@microsoft.com```

4. **Validate these settings** by running the following:

    ```git config --list``` 

5. The output should look similar to below:

    PS C:\> git config --list
    diff.astextplain.textconv=astextplain
    filter.lfs.clean=git-lfs clean -- %f
    filter.lfs.smudge=git-lfs smudge -- %f
    filter.lfs.process=git-lfs filter-process
    filter.lfs.required=true
    http.sslbackend=openssl
    http.sslcainfo=C:/Program Files/Git/mingw64/etc/ssl/certs/ca-bundle.crt
    core.autocrlf=true
    core.fscache=true
    core.symlinks=false
    pull.rebase=false
    credential.helper=manager
    credential.https://dev.azure.com.usehttppath=true
    init.defaultbranch=main
    core.editor="C:\Users\petender\AppData\Local\Programs\Microsoft VS Code\bin\code" --wait
    filter.lfs.clean=git-lfs clean -- %f
    filter.lfs.smudge=git-lfs smudge -- %f
    filter.lfs.process=git-lfs filter-process
    filter.lfs.required=true
    user.name=Peter De Tender
    user.email=petender@microsoft.com
    PS C:\>

### Create your first Git Repository

Imagine you are tasked with creating a basic HTML website for a personal hobby project, related to cats. Throughout this exercise, you create the project folder, enable it as a Git repository and start creating files and subfolders. 
All changes related to the project source code will be tracked using Git.

Git works by checking for changes to files within a certain folder. We'll create a folder to serve as our *working tree* (project directory) and let Git know about it, so it can start tracking changes. We tell Git to start tracking changes by initializing a Git repository into that folder.

Start by creating an empty folder for your project, and then initialize a Git repository inside it.

1. Create a folder named **Cats**. This folder will be the project directory, also called the working tree. The project directory is where all files related to your project are stored. In this exercise, it's where your website and the files that create the website and its contents are stored.

    ```mkdir Cats```

2. **Change to the project directory** by using the ```cd``` command:

    ```cd Cats```

3. **Initialize this folder** as a Git repo, by using the following command:

    ``` git init --initial-branch=main```

4. After running this command, Git confirms the folder got initialized:

        ```
        PS C:\Cats> git init --initial-branch=main
        Initialized empty Git repository in C:/Cats/.git/
        PS C:\Cats>
        ```

[comment]: <> (this is the section for the Tip: item; consider adding a Tip, or remove the section between <div> and </div> if there is no tip)

<div style="background: lightgreen; 
            font-size: 14px; 
            color: black;
            padding: 5px; 
            border: 1px solid green; 
            margin: 5px;">
            
**Note:** Note the .git folder that got created inside the Cats folder. This is where Git stores the metadata of the Git Repository. We will share more details on this folder later. On Linux or MacOS, you should run ls -a to see this folder, since it's set up as a hidden folder.
</div>

5. Now, use a **git status command** to show the status of the working tree:

    ```git status```

6. The output from Git indicates the main branch, with nothing to commit. Makes sense so far.

        ```
        PS C:\Cats> git status
        On branch main

        No commits yet

        nothing to commit (create/copy files and use "git add" to track)
        PS C:\Cats>
        ```



### Making edits into the Git repository

1. Let's continue with **adding an index.html file into** the Cats folder, which will act as the home page of the website. **Create a new file *index.html*** inside the Cats folder.

2. **Run a git status** validation:

    ``` git status ```

Git responds by informing you that nothing has been committed, but the directory does contain a new file:

    ```
    PS C:\Cats> git status
    On branch main

    No commits yet

    Untracked files:
    (use "git add <file>..." to include in what will be committed)
            index.html

    nothing added to commit but untracked files present (use "git add" to track)
    PS C:\Cats>
    ```


3. Notice that git status gives you hints about what you can do next. Git can be configured to be less wordy, but at this stage, more is better.

Use **git add** to add the new file to Git's index, followed by **git status** to check the status. Don't forget the period at the end of the command. It tells Git to index all the files in the current directory that have been added or modified.

```git add . ```

4. A commit has now been staged. Git's index is a staging area for commits. It's a list of all the file versions that will be part of the next commit you make.

Rather than use *git add .*, you could have used *git add index.html* because index.html was the only new file in the directory. But if several files had been added, git add . would have covered them all.

Finally, use **git status** again to make sure your changes were staged properly:

``` git status```

5. You should see the following output:

    ```
    PS C:\Cats> git status
    On branch main

    No commits yet

    Changes to be committed:
      (use "git rm --cached <file>..." to unstage)
            new file:   index.html

    PS C:\Cats>
    ```

6. Now that index.html has been added to the index, the next step is to commit it.

Use the following command to **create a commit**:

```git commit index.html -m "Create index.html file"```

The -m flag in this command tells Git that you're providing a commit message.

There are many different ways to phrase commit messages, but a good guideline is to write the first line so that it says what the commit does to the tree. It's also common to capitalize the first letter, and to leave off the closing period to save space. Imagine that the first line of the message completes the sentence starting with "When pushed, this commit will..."

A commit message can have multiple lines. The first line should have no more than 50 characters and should be followed by a blank line. Subsequent lines should have no more than 72 characters. These requirements aren't firm, and they harken back to the days of punch cards and "dumb" terminals, but they do make git log output look better.

Git responds with a confirmation of what you did:

    ```
    PS C:\Cats> git commit index.html -m "Create index.html file"
    [main (root-commit) a7f28cb] Create index.html file
     1 file changed, 0 insertions(+), 0 deletions(-)
     create mode 100644 index.html
    PS C:\Cats>
    ```

7. This all worked for a newly created file. Let's continue the exercise and make changes to the existing index.html, and see how Git is interacting.

**Open index.html** in Visual Studio Code by typing code index.html at the terminal prompt:

```code index.html```

**Type or paste** the following statements in the editor:

    ```
    <h1>Our Feline Friends</h1>
    ```

8. **Save the file** and close VSCode editor. Use a **git status** command to check the status of the working tree:

```git status```

You can see that Git is aware of the changes you made:

    ```
    PS C:\Cats> git status
    On branch main
    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   index.html

    no changes added to commit (use "git add" and/or "git commit -a")
    PS C:\Cats>
    ```

9. Now, **commit the changes**:

```git commit -a -m "Add a heading to index.html"```

Note that we didn't run the git add command this time to stage our changes. Instead, we used the -a flag in the git commit command. The -a option adds all the files you modified since the last commit. It won't add new files. To add new files, you still need git add.

Check the output. It should look like this example:

    ```
    PS C:\Cats> git commit -a -m "Add a heading to index.html"
    [main 89cecb5] Add a heading to index.html
     1 file changed, 1 insertion(+)
    PS C:\Cats>
    ```

The change to index.html has been committed. There are now two versions of the file in the repo, although you see only one of them (the current one). One of the benefits of using Git is that you can roll back the changes you have made, or you can go backward in time and see previous versions. More on this important topic later.

10. The website's home page, index.html, currently contains just one line of HTML. Let's update it to do more, and then commit the change to Git.

**Reopen the index.html file** in the online editor for Cloud Shell (code index.html) and **replace the file contents** with the following HTML:

    ```HTML
    <!DOCTYPE html>
    <html>
      <head>
        <meta charset='UTF-8'>
        <title>Our Feline Friends</title>
      </head>
      <body>
        <h1>Our Feline Friends</h1>
        <p>Eventually we will put cat pictures here.</p>
        <hr>
      </body>
    </html>
    ```

11. **Save the file** and close VSCode editor.

Use a **git diff** command to see what changed:

    ```
    PS C:\Cats> git diff
    diff --git a/index.html b/index.html
    index f3b3413..48727ab 100644
    --- a/index.html
    +++ b/index.html
    @@ -1 +1,11 @@
    -<H1> Our Feline Friends</H1>
    \ No newline at end of file
    +<html>
    +  <head>
    +    <meta charset='UTF-8'>
    +    <title>Our Feline Friends</title>
    +  </head>
    +  <body>
    +    <h1>Our Feline Friends</h1>
    +    <p>Eventually we will put cat pictures here.</p>
    +    <hr>
    +  </body>
    +</html>
    \ No newline at end of file
    PS C:\Cats>
    ```

12. The output format is the same as the Unix diff command, and the Git command has many of the same options. A plus sign appears in front of lines that were added, and a minus sign indicates lines that were deleted.

The default is for git diff to compare the working tree to the index. In other words, it shows you all the changes that haven't been staged (added to Git's index) yet. To compare the working tree to the last commit, you can use git diff HEAD.

If the command doesn't return to the prompt after it executes, enter q to exit the diff view.

Next, commit the change. Instead of using the -a flag, you can explicitly name a file to be staged and committed if Git already has the file in the index (the commit command looks only for the existence of a file).

```
git commit -m "Add HTML boilerplate to index.html" index.html
```

13. Use the following command to **create and open a file** named **.gitignore** in the built-in code editor:

``` code .gitignore```

14. Add the following lines to the file:

```
*.bak
*~
```

15. This line **instructs Git to ignore files** that have file names ending in .bak or ~.

[comment]: <> (this is the section for the Tip: item; consider adding a Tip, or remove the section between <div> and </div> if there is no tip)

<div style="background: lightgreen; 
            font-size: 14px; 
            color: black;
            padding: 5px; 
            border: 1px solid green; 
            margin: 5px;">
            
**Note:** .gitignore is a very important file in the Git world because it prevents extraneous files from being submitted to version control. Boilerplate .gitignore files are available for popular programming environments and languages.
</div>


16. **Save and close** the editor, and then use these commands to commit the changes:

```
git add -A
git commit -m "Make small wording change; ignore editor backups"
```

This example uses the -A option with git add to add all untracked (and not ignored) files, and the files that have changed, to the files that are already under Git control.

If you do a git diff right now, the output will be empty because the changes have been committed. However, you can always use a git diff HEAD^ command to compare differences between the latest commit and previous commit. Try it and see. Don't forget to include the caret ^ character at the end of the command.

17. Imagine all changes have been covered for now. **Run a trace** of the different commits occured by initiating:

``` git log```

    ```
    PS C:\Cats> git log
    commit 15baa77ff0f2c0fee230f3c798e8c3ec17269d53 (HEAD -> main)
    Author: Peter De Tender <petender@microsoft.com>
    Date:   Mon May 29 20:00:13 2023 -0700

        Add HTML boilerplate to index.html

    commit 89cecb52c7c42810750c734432d67cb7284a7557
    Author: Peter De Tender <petender@microsoft.com>
    Date:   Mon May 29 19:56:22 2023 -0700

        Add a heading to index.html

    commit a7f28cbfcc6c5f890c77cdb75bb0bd69ece6ff39
    Author: Peter De Tender <petender@microsoft.com>
    Date:   Mon May 29 19:52:07 2023 -0700

        Create index.html file
    PS C:\Cats>
    ```

18. A shorter version of the commit logs is possible from:

    ```
    PS C:\Cats> git log --oneline
    15baa77 (HEAD -> main) Add HTML boilerplate to index.html
    89cecb5 Add a heading to index.html
    a7f28cb Create index.html file
    PS C:\Cats>
    ```

### Recovering files from the Git Repository

Sometimes, things go wrong. You might forget to add a new file, or maybe you add a file by mistake. Perhaps you made a spelling error in your latest commit or you committed something you didn't intend to. Perhaps you accidentally deleted a file.

Git lets you make changes fearlessly, because it always offers a way to get back to where you were. You can even change Git's commit history as long as you only change commits that haven't been shared.

Imagine that you made a change to a source code file that broke the entire project, so you want to revert to the previous version of that file. Or perhaps you accidentally deleted a file altogether. Git makes it easy to retrieve an earlier version, even if the current version no longer exists. 

1. First, **try deleting** index.html:

``` rm index.html```

2. It might seem like a bad idea, but remember: Git has your back!

Use an ```ls``` command to verify that index.html was deleted. And behold, the file is gone! PANIC!!

3. **Let's recover index.html**. Use git checkout to bring back index.html:

```git checkout -- index.html```

Use ls again to check the contents of the current directory. Has index.html been restored?

Yes! Now, the output should have an index.html file again.

4. When you want to recover deleted files, things are a little more complicated if you delete them by using **git rm** instead of by using **rm**.

To see what happens, try this command:

```git rm index.html```

5. Now, **try to recover** the file using the same command as before:

``` git checkout -- index.html```

    

6. This time, **Git complains** that it knows nothing about index.html. That's because Git not only deleted the file, it recorded the deletion in the index:

    ```
    PS C:\Cats> git checkout -- index.html
    error: pathspec 'index.html' did not match any file(s) known to git
    PS C:\Cats>
    ```

7. **Unstage the deletion** of index.html with the git reset command:

```git reset HEAD index.html```

    ```
    PS C:\Cats> git reset HEAD index.html
    Unstaged changes after reset:
    D       index.html
    PS C:\Cats>
    ```

8. Now run the **checkout command** again:

```git checkout -- index.html```

git reset unstaged the change, but the file was still deleted, so you had to use checkout to get it back.

Double-check that it worked by running ls ;).

[comment]: <> (this is the closing section of the exercise steps. Please do not change anything here to keep the layout consistant with the other markdown files.)
<br></br>
***

<div style="background: lightgray; 
            font-size: 14px; 
            color: black;
            padding: 5px; 
            border: 1px solid lightgray; 
            margin: 5px;">

**Note:** This is the end of the hands-on exercise.
</div>




