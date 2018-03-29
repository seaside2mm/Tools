# Git

## 0. 理论
1. 工作区 working Derectory & 版本库Repository
> git add命令实际上就是把要提交的所有修改放到暂存区（Stage），然后，执行git commit就可以一次性把暂存区的所有修改提交到分支。

1. **tracked** - a file which has been previously staged or committed;
2. **untracked** - a file which has not been staged or committed; or
3. **ignored** - a file which Git has been explicitly told to ignore.

## 1. 常用指令

+ HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令`git reset --hard commit_id`。
+ 穿梭前，用`git log`可以查看提交历史，以便确定要回退到哪个版本。或者`git log --oneline`
+ 要重返未来，用`git reflog`查看命令历史，以便确定要回到未来的哪个版本。

- `git diff HEAD -- filename`命令可以查看工作区和版本库里面最新版本的区别
- `git rm`用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失最近一次提交后你修改的内容。
- `git checkout`其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”. 
- `git checkout -- readme.txt`意思就是，把readme.txt文件在工作区的修改全部撤销，。这里有两种情况：
> - 一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
> - 一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

- `git reset HEAD file`可以把暂存区的修改撤销掉（unstage），重新放回工作区



## 2. 疑难杂症
- 删除github文件
```
git rm -r --cached some-directory
git commit -m 'Remove the now ignored directory "some-directory"'
git push origin master
```

---
> 在编译git库拉下来的代码时，往往会产生一些中间文件，这些文件我们根本不需要，尤其是在成产环节做预编译，检查代码提交是否能编译通过这种case时，我们往往需要编译完成后不管正确与否，还原现场，以方便下次sync代码时不受上一次的编译影响。

- 删除 untracked files
`git clean -f  `

 
- 连 untracked 的目录也一起删掉
`git clean -fd  `

 
- 连 gitignore 的untrack 文件/目录也一起删掉 （慎用，一般这个是用来删掉编译出来的 .o之类的文件用的）
`git clean -xfd  `

 
- 在用上述 git clean 前，强烈建议加上 -n 参数来先看看会删掉哪些文件，防止重要文件被误删
```
git clean -nxfd  
git clean -nf  
git clean -nfd  
```
