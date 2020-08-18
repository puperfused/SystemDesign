## Four Areas of in GIT

- Stash Area
- Working Area (Local)
- Index (Staging Area)
- Repositry (Main area, where code sits after commit)

## Repository

- .git folder is repository area
- it stores object information or history of the code or its kinda of snapshot
- Object can be contents or code stored in form of BLOBs, or tree object which reprsent folder structure, and then we have commit object which stores the commit details.
- All of objects are immutable, they can be created or deleted but cannot be modified.
- The data or commit is stored in graphical form.
- Start of the commit references represent a branch.
- There can be only one HEAD. Changing HEAD means we are switching our branches.
- git checkout does 2 things(moves head from one branch to other ) , first, in the repo it moves the header reference generally to the another branch(so it changes the current commit), second, it takes data from new current commit and copies data to the working area and index.

## Push local directory to remote

- create a repository in git
- open git bash in your local folder you want to add to git
- initialise the folder as git repo.
    ```
    c:/local> git init
    // Add the folder
            > git add .
    // commit the file in your staged area
            > git commit -m "first commit"
    // copy the url of the git repo you created in the first step
            > git remote add origin <remote repo URL without angle brackets>
            // sets the new remote
            > git remote -v
            // verifies the new remote URL
    // push the changes in your local to github
            > git push origin master
    ```
- Done!! 
   

## Stashing

``` 
    // To stash the changes
     > git stash
    
    // To show the entries in stash
     > git stash show

    // To pop the entries from stash
     > git stash pop
    
    // To clear the entries from stash
     > git stash clear
```

## Pushing with new local branch (if upstream issue comes)

```
        > git checkout -b branchName
        > git commit -m "Random Comment"
        > git push
         //error comes saying "To push the current branch and set the remote as upstream"
        > git push --set-upstream origin branchName

```

## Git Commands

- git status
- git add filename
- git add .
- git diff  ( checks for the difference between working and index area)
- git diff --cached (checks for the difference between index and repository)
- git commit -m "Comment"  (copies the modified file from index to repo, also changes the data, updates branch or commit objects etc)
- git diff branch1 branch2 (differences between two branches)
- git checkout branch2
- git tag v1
- git push --tags
- git branch -d dev
- git push --delete origin dev