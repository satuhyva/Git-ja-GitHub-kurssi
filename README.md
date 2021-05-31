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
  
  
## 2. HOW GIT WORKS?

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
  

## HASHING
  
### Create hashed object
  Create a hashed git object from terminal input "Hello, Git" (--stdin) and write (-w) to object folder:
```
  echo "Hello, Git" | git hash-object --stdin
```
Object b7aec520dec0a7516c18eb4c68b64ae1eb9b5a5e was written to folder b7 with name aec520dec0a7516c18eb4c68b64ae1eb9b5a5e. Note: No new file was created in main folder, only in .git/objects.

Also, you can hash (and write to objects) an already existing file:
```
  git hash-object <filename> -w
```

### Hash functions
Git utilizes **SHA1 hash function** that produces a 160 bit-long representation (= **40 hexadecimal characters** that are the folder/file name, like the b7... above).

### Git cat-file commands to read information about git objects
```
  git cat-file -p <hash>  // shows CONTENTS of file
  git cat-file -t <hash>  // shows TYPE of object
  git cat-file -s <hash>  // shows SIZE of object
  
  for example:
  git cat-file -p b7aec520dec0a7516c18eb4c68b64ae1eb9b5a5e
```

### Git object
Git object consists of four parts:
  1. Object type (e.g. blob)
  2. Object length  (e.g. 11)
  3. Delimiter (e.g \0)
  4. Content (the actual file content)

We can "calculate" the hashed representation of contents of a file as git does like this:

Earlier, the sha1 hash we got for 'Hello, Git' was b7aec520dec0a7516c18eb4c68b64ae1eb9b5a5e. With the command:
```
echo 'blob 11\0Hello, Git' | shasum
```
We can pipe (|) the '...' to shasum and we get the same b7aec520dec0a7516c18eb4c68b64ae1eb9b5a5e.

Here type of object is blob, length is 11 and delimiter is \0 and content is Hello, git.
















  
  
