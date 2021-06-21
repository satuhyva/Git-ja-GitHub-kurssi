# Git-ja-GitHub-kurssi



## 1. GIT VS GITHUB
  
  Git = distributed version control system (tracks changes in files in a repository)
  
  GitHub = repository hosting service


## BASIC SHELL COMMANDS

### ls
  show files
  
### ls -la
  show files (a = also hidden ones, l = as a list)

### mkdir
   make a directory
  
### clear
   clear terminal
  
### cd
   change directory 
  
### .
   current directory
  
### ..
   parent directory
  
### echo
   print to terminal

### touch 
   create new file
  
### rm 
   remove file
  
### \> 
   write to file
```
  echo "HUHUU" > someNewFile.txt
```   
   
### \>>
   append to file
```
  echo "JIPPII" >> someFile.txt
```
      
### cat
   list contents of file  
```
  cat someFile.txt
```

### open .
  opens folder where you are in in finder graphical view
  
  
## 2. HOW GIT WORKS UNDER THE HOOD?

## Create new Git repository
```
  git init
```

## .git FOLDER
  Git stores data as objects of four different types (in .git/objects):
  1. **Blob** (actual files with content)
  2. **Tree** (file / folder structure)
  3. **Commit** (different versions of project)
  4. **Annotated tag** (text pointer to specific commit)
  
  Git stores data based on their hashes.
  
  Files do not have names, the "names" of files are created by hashing files.
  

## Create hashed object
  Create a hashed git object from terminal input "Hello, Git" (--stdin) and write (-w) to object folder:
```
  echo "Hello, Git" | git hash-object --stdin
```
Object b7aec520dec0a7516c18eb4c68b64ae1eb9b5a5e was written to folder b7 with name aec520dec0a7516c18eb4c68b64ae1eb9b5a5e. Note: No new file was created in main folder, only in .git/objects.

Also, you can hash (and write to objects) an already existing file:
```
  git hash-object <filename> -w
```

## Hash functions
Git utilizes **SHA1 hash function** that produces a 160 bit-long representation (= **40 hexadecimal characters** that are the folder/file name, like the b7... above).

## Git cat-file commands to read information about git objects
```
  git cat-file -p <hash>  // shows CONTENTS of file
  git cat-file -t <hash>  // shows TYPE of object
  git cat-file -s <hash>  // shows SIZE of object
  
  for example:
  git cat-file -p b7aec520dec0a7516c18eb4c68b64ae1eb9b5a5e
```

## Git object
Git object consists of four parts:
  1. Object type (e.g. blob)
  2. Object length  (e.g. 11)
  3. Delimiter (e.g \0)
  4. Content (the actual file content)

We can "calculate" the hashed representation of a file (or more precisely, the type, length, delimiter and content of the file) as git does like this:
```
echo 'blob 11\0Hello, Git' | shasum
```
Earlier, the sha1 hash we got for 'Hello, Git' was b7aec520dec0a7516c18eb4c68b64ae1eb9b5a5e. The above command gives the same result. (Here we pipe (|) the 'phrase' to shasum to we get the hashed representation  b7aec520dec0a7516c18eb4c68b64ae1eb9b5a5e). The type of object is blob, length is 11, delimiter is \0 and content is Hello, git.

## Tree objects
Tree can contain blob objects or other trees.

## Main areas where files and folders can be
1. Working directory
2. Staging area (index)
3. Repository


# 3. GIT BASIC OPERATIONS

## Commit
Type of Git object. Structure:
- Object type (commit)
- Size
- Delimiter
- Content: Author name and email, Commit description, Parent (optional), and Pointer to parent tree if not root directory)
- POINTER TO THE TREE (that is the version's tree object).

Allows storage of different "versions" or "snapshots" of the project.

## Commands
Configurations for author:
```
git config --global user.name <here your name>
git config --global user.email <here your email>
git config --list
```
Commit with a message:
```
git commit -m"some message"
```
Current state of Git repository
```
git status
```
Add files to staging area (move files from untracked or modified state to staged state; either add file name or "." for all files):
```
git add
```
Remove file from staging area:
```
git rm --cached <file name here>
```
Write files to Git repository (move files from staged state to unmodified state):
```
git commit
```
History of commit changes (or commits):
```
git log
```
Checkout commit or branch:
```
git checkout
```

### File statuses
- untracked
- unmodified
- modified
- staged


## BRANCH AND HEAD

Branch is a text reference to a specific commit.
Pointer to a branch is located in .git/refs/heads.
There may be several branches.

How does Git know which branch is current?
Head is pointer to specific commit. There may be only one HEAD.
Head is pointer to currently checked out branch.
Pointer to head is in .git/HEAD
Default is ref: refs/heads/master


## Checkout a specific branch
Git checkout takes a version from repository and takes it's contents to working directory.
It just moves HEAD pointer!


## Git branch management

git branch = list local branches

git branch \<name> = create new branch (name cannot contain a space; branch will nt become checked out)

git checkout \<name> = checkout specific branch

git branch -d \<name> = delete specific branch (lowercase d: only merged branch can be deleted; uppercase D will force deletion for unmerged branch)

git branch -m <old name> \<new name> = rename specific branch
  
git checkout -b \<name> = create and checkout branch simultaneously
  

  
# MERGING BRANCHES

## FAST FORWARD MERGE

1. Create new feature branch, like BR-1, from MASTER.
2. Make changes to BR-1 and commit.
3. Checkout receiving branch, like MASTER.
4. Merge feature branch BR-1 to checked out MASTER with
  ```
  git merge <BR-1>
  ```
  
  
Receiving branch = branch that receives changes.
Fast forward merge is possible only when no further commits have been made to the receiving branch (to which we are merging, like MASTER) after we created the branch (like BR-1 that we wish to merge) from it.
 
When merging branch BR-1 to MASTER, first checkout MASTER (so that HEAD points to MASTER).
At the merge process, the HEAD pointer (of the receiving branch MASTER) is moved to last commit of BR-1.


  
## THREE-WAY MERGE

Suppose situation:
  ```
  ancestor --- commit --- commit --- MASTER
      \
       \
        commit --- commit --- BR-1
```


















  
  
