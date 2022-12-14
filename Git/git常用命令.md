### 1、查看特定 commit 的修改

```bash
# 查看特定 commit 的修改
git show [commit]

# 查看特定 commit 特定文件 的修改
git show [commit]:[filename]
```

### 2、查看一个文件的历史提交

```bash
git log -p [filename]
```

### 3、查看远程仓库地址

```bash
git remote -v
```

### 4、git reset --hard  | --soft | --mixed 的区别

- --hard 退回到某一个版本，这个版本之后的提交都不见了
- --soft  退回到某一个版本，这个版本之后的提交都等待commit
- --mixed (默认)退回到某一个版本，这个版本之后的提交都等待add

### 5、如何覆盖上一次的提交记录？

```bash
# 使用一次新的commit,替代上一次提交 (important)
# 如果代码没有变化，则用来改写上一次commit的提交信息
git commit --amend -m [message]
```

### 6、如何合并某一次 commit 的修改？
`git cherry-pick`：能够把另一个分支的一个或多个提交复制到当前分支。

```bash
git cherry-pick [commit]
```
具体使用如下：  

1. 首先git checkout 到另一个分支，然后使用git log找到想要复制的commit 的id,记录下来。
2. 切换到自己分支，使用git cherry-pick  [上面记录的commit id]  回车即可!

如果想要复制多个, 使用`git cherry-pick commitid1 commitid2 ... commitid100`。它们必须按照时间顺序放置，否则命令将失败，但不会报错，commitid1为最早提交(不包括)，commitid100为最新提交(包括)。  
如果想要包括commitid1,那么在commitid1后加^即可，即 git cherry-pick commitid1^ commitid2 ... commitid100

> git cherry-pick 参考： http://www.ruanyifeng.com/blog/2020/04/git-cherry-pick.html

### 7、如何清除未跟踪的文件？

```bash
git clean -f
```

### 8、查看两次 commit 的差异

```bash
# 比较两个 commit 之间的差异
git diff [commit1] [commit2]

# 显示暂存区与工作区的差异
git diff
```

### 9、如何合并多个 commit?

1、使用 git reset（推荐）

先 reset 到先前的某一个 ID ，保留修改记录。再集中进行一次 commit:

```bash
git reset —soft [commitID]
```

2、使用 git rebase（操作相对复杂）

```bash
git rebase -i [commitID]
```

3、如果是合并其他分支，但是不需要知道这个分支里的 commit 记录，可以：

```bash
git merge —squash [branch-name]
```

### 10、git submodule 用过吗？它的常见用法用法有哪些？

1、添加一个子模块

```bash
git submodule add [git repo]
```

2、查看子模块

```bash
git submodule
```

3、初始化子模块

当前 repo 刚从仓库里拉下来，这时候子模块还没有初始化，需要初始化子模块：

```bash
git submodule init
```

4、更新子模块

初始化后，需要需要从远端更新子模块的代码：

```bash
git submodule update
```

5、初始化并更新子模块

将上面两个操作结合：

```bash
git submodule update --init
```

6、初始化递归更新子模块

有时候子模块里会嵌套子模块，这时候需要递归初始化子模块：

```bash
git submodule update —init --recursive
```
