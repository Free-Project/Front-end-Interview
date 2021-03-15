# git rebase用法详解

## 命令：
```
git rebase [-i | --interactive] [<options>] [--exec <cmd>] [--onto <newbase>] [<upstream> [<branch>]]

git rebase [-i | --interactive] [<options>] [--exec <cmd>] [--onto <newbase>] --root [<branch>]

git rebase --continue | --skip | --abort | --quit | --edit-todo | --show-current-patch
```


### 示例场景1：   

有一条代码线`master`分支，同时有新开发线`dev`分支从`master`的B提交点分离出来。之后，master分支也有代码提交（C,D）。如下图：

```
      E---F---G  (dev分支)
     /
A---B---C---D  (master主干)
```

此时（**当前在dev分支**），`dev`线需要合并`master`分支的代码，那我们可以用到`git rebase`命令。

执行：`git rebase master` 或 `git rebase master dev`，成功后，dev线就会合并C和D提交的记录。如下图：

```
              E---F---G  (dev分支)
             /
A---B---C---D  (master主干)
```
> **解释**  
> `git rebase branchA branchB`：首先会取出branchB，将branchB中的提交放在branchA的尾端（最新commit点的后面），一般branchB为当前分支，可以不指定。  
> 如上例中`git rebase master dev` 或 `git rebase master`


### 示例场景2：  

两条新功能开发线，一条`dev`，`dev1`是在`dev`的基础上开的新分支，可能`dev1`的代码更稳定，此时需要将`dev1`改为`master`的一条分支，同时将`master`线上修改的代码与`dev1`进行合并。
```
                H---I---J  (dev1分支)
               /
      E---F---G  (dev分支)
     /
A---B---C---D  (master主干)
```

此时，可以执行命令：`git rebase --onto master dev dev1`，操作成功后，`dev1`线将有`master`上的最新代码，同时又包含新开发的功能：
```

      E---F---G  (dev分支)
     /
A---B---C---D  (master主干)
             \
               H---I---J  (dev1分支)
```



### 示例场景3：  

假设现在有一条分支`dev1`如下：
```
A---B---C---D---E  (dev1分支)
```
发现B和C提交的代码有问题，需要把B和C提交的代码去除，那可以执行命令：`git rebase --onto dev1~4 dev1~1 dev1`，执行后，B和C将会从dev1分支的提交记录中去除。
```
A---D---E  (dev1分支)
```



## `git rebase`命令主要参数解析：
```
git rebase [-i | --interactive] [<options>] [--exec <cmd>] [--onto <newbase>] [<upstream> [<branch>]]
```

`--onto<newbase>`  
newbase指的是需要rebase代码的起点，newbase可以是分支（branch），也可以是任意的提交记录(commitId)。rebase成功后，将以newbase为代码分支起点。
  


`<upstream>`  
需要与newbase比对的分支或提交记录。



`<branch>`  
需要rebase的工作分支。默认为HEAD，例如dev1



`--continue`  
当处理完冲突后，可以使用该命令让rebase继续。


`--abort`  
终止rebase操作，将HEAD设置为rebase之前的分支。如果指定了<branch>，则HEAD将重置为<branch>。否则，HEAD将被重置为rebase之前的分支。


      
      
`--quit`  
终止rebase操作，但不会将HEAD重置为原来的分支。index和working tree将不会发生任何改变。




`--autostash`  
在rebase操作之前自动stash当前分支未提交的代码，在rebase操作结束后，自动将stash的记录进行unstash，并与rebase后的代码合并。注意，此操作有可能会导致严重的冲突（conflict），谨慎使用。


```
-m

--merge
```
进行rebase操作的时候，同时使用merge进行代码合并。需要注意的是，在进行rebase merge产生冲突的时候，ours为<upstream>指定的分支，theirs为<branch>指定的分支。原因是，rebase merge work的工作原理为，将<branch>上的所有提交记录在<upstream> 分支上进行重提交。
