# GIT

------

[TOC]

## GIT命令大全

1. git安装后-指定名称和邮箱

   ```cpp
   $ git config --global user.name "Your Name"
   $ git config --global user.email "email@example.com"
   ```

2.  创建版本库

   ```cpp
   $ mkdir learngit	//创建
   $ cd learngit	//使用
   $ pwd	//查看当前目录
   $ git init	//初始化，生成.git文件(若该文件隐藏，则使用ls -ah)
   ```

3.  把文件添加add和提交commit到版本库

    ```cpp
    $ git add test.txt	//添加
    $ git commit -m "wrote a test file"	//提交
    $ git commit -m "add 3 files."		//一次性提交多个文件
    ```

    > [!NOTE]
    >
    > 注意：必须在当前版本库和当前目录下

4. 版本控制

   ```cpp
   $ git log	//查看提交历史记录，从最近到最远，可以看到3次
   $ git log --pretty=oneline	//加参，简洁查看
   $ git reflog	//查看每一次修改历史
   $ cat test.txt	//查看文件内容
   $ git status	//查看工作区中文件当前状态
   $ git reset --hard HEAD^（HEAD~100）（commit id）	//回退版本
   $ git checkout -- test.txt	//丢弃工作区的修改，即撤销修改
   $ git reset HEAD test.txt	//丢弃暂存区的修改（若已提交，则回退）
   ```

5.  删除文件

    ```cpp
    $ rm test.txt	//直接删除
    $ git rm test.txt
    $ git commit -m "remove test.txt"	//删错了，恢复
    $ git checkout -- test.txt
    ```

6.  远程仓库

    ```cpp
    $ ssh-keygen -t rsa -C "youremail@example.com"	//创建SSH Key
    $ git remote add origin git@github.com:Daisy/AKgit.git	//关联
    $ git push -u origin master	//将本地内容推送到远程仓库（第一次）
    $ git push origin master	//将本地内容推送到远程仓库（之后）
    $ git remote -v        //查看远程仓库信息
    $ git remote rm origin	//删除远程仓库（解绑）
    $ git clone git@github.com: Daisy/AKgit.git	//克隆远程仓库
    //克隆之后使用和查看
    $ cd gitskills
    $ ls
    $ git remote	//查看远程库的信息
    $ git remote -v	//查看远程库的详细信息
    ```

7.  多人协作

    ```cpp
    $ git checkout -b dev	//创建并切换到分支dev
    //创建并切换到分支dev，同上
    $ git branch dev	//创建
    $ git checkout dev	//切换
    //新版本
    $ git switch -c dev	//创建并切换到分支dev
    $ git switch master	//直接切换分支
    $ git branch		//查看当前分支
    $ git merge dev	（--no-ff）(-m) //合并，把dev分支的工作成果合并到master分支上
    $ git branch -d dev	//删除dev分支 
    
    $ git stash	//将现场储藏起来
    $ git stash list	//查看储存的工作现场
    //恢复和删除
    $ git stash apply
    $ git stash drop
    //恢复并删除
    $ git stash pop
    $ git cherry-pick 4c805e2	//复制修改
    
    $ git push origin master（dev）	//推送分支
    $ git checkout -b dev origin/dev	//创建远程origin的dev分支到本地
    $ git pull	//抓取分支（解决冲突）
    $ git branch --set-upstream-to=origin/dev dev//指定本地与远程dev的链接
    $ git rebase	//把本地未push的分叉提交历史整理成直线
    ```

8.  标签管理

    ```cpp
    $ git tag v1.0	//打标签
    $ git tag -a v0.1 -m "version 0.1 released" 1094adb //指定标签名和说明文字
    $ git tag	//查看所有标签
    //若是忘记打，则查找历史提交commit id ，再打上
    $ git log --pretty=oneline --abbrev-commit
    $ git tag v0.9 f52c633
    $ git show v0.9		//查看标签详细信息
    $ git tag -d v0.1	//删除标签
    $ git push origin v1.0	//推送标签到远程
    $ git push origin –tags	//一次性推送全部本地标签
    //删除标签，（若已推送到远程，先从本地删除，从远程删除）
    $ git tag -d v0.9
    $ git push origin :refs/tags/v0.9 
    ```

9.  自定义git

    ```cpp
    $ git config --global color.ui true	//让git显示颜色
    
    //忽略特殊文件
    //.gitignore文件
    # Windows:
    Thumbs.db
    ehthumbs.db
    Desktop.ini
    # Python:
    *.py[cod]
    *.so
    *.egg
    *.egg-info
    dist
    build
    # My configurations:
    db.ini
    deploy_key_rsa
    //把该文件也提交到git
    $ git add -f App.class		//强制添加被忽略的特殊文件
    $ git check-ignore -v App.class	//检查哪个规则出错
    # 排除所有.开头的隐藏文件:
    .*
    # 排除所有.class文件:
    *.class
    # 不排除.gitignore和App.class:
    !.gitignore
    !App.class
    
    $ git config --global alias.st status	//配置别名
    $ git config --global alias.unstage 'reset HEAD'  //配置操作别名
    $ git config --global alias.last 'log -1'	//显示最后一次提交信息
    $ git last	//显示最近一次的提交
    $git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"  //颜色
    $ cat .git/config //查看每个仓库的git配置文件
    $ cat .gitconfig  //查看当前用户的git配置文件
    ```


------

## GIT常用命令总结

### 常用命令

![img](./Git.assets/442d79cddf8c57572484826e340520be-1720880436068-1.png)

1. **`git init`** 

2. **`git add 文件名`**

3. **`git commit -m “备注信息”`**

   ```cpp
   git add 文件名 // 工作区提交修改到暂存区
   git checkout --文件名 // 用暂存区覆盖工作区（撤销修改）
   // 多处修改提交：多次add，最后一次commit
   ```

4. **`git status`** 与 **`git diff`** 

   ```cpp
   git status // 告诉你有文件被修改过
   git diff // 查看修改内容
   git diff common/> 1.diff // 将common目录下的改动转存为1.diff
   git diff // 工作区(work dict)和暂存区(stage)的比较
   git diff --cache // 暂存区(stage)与分支(master)的比较
   ```

5. **`git show commit_id`** // 查看某次修改

6. **`git log`** 与 **`git reflow`** 

   ```cpp
   git log // 查看提交历史，看要回退到哪个版本
   git reflow // 查看命令历史，看要回退到哪个版本    
   git log --pretty=oneline
   git log --graph --pretty=oneline --abbrev-commit // 当多人协作开发一个分支时
   // 查看历史记录通常比较凌乱，如果希望能像右图那样呈线性提交，就需要学习git rebase的用法。
   git log --graph // 可以看到分支合并图
   git --no-pager log -3 -p // 查看最近3个版本的修改情况
                            // --no-pager 不less分页显示了
                            // -3 修改3个版本
                            // -p 显示修改部分 
   ```

7. **`git pull (--rebase)`**

   ```cpp
   git pull --rebase // git pull时可以加上--rebase参数, 使之不产生Merge点, 保证了代码的整洁
   // 再次git log --graph--pretty=oneline --abbrev-commit，新的merge就会呈现线性样式
   // 但每次都加--rebase似乎有些麻烦，我们可以指定某个分支在执行git pull时默认采用rebase方式：
   git config branch.dev.rebase true  // dev为本地的分支名字
   // 如果你觉得所有的分支都应该用rebase，那就设置：
   git config --global branch.autosetuprebase always
   // 这样对于新建的分支都会设定上面的rebase = true了，已经创建好的分支还是需要手动配置的
   ```

8. **`git push (-u)`** 与 **`git branch (-u)`** 

   ```cpp
   // git push -u 与 git branch -u的区别？
   git push -u origin dev = git push origin/dev dev + git branch -u origin/dev dev 
   // git push -u origin 与 git branch -u origin的区别？
   git push origin // 不指定远程分支，则默认的远程分支与本地分支一样
   git branch origin // 不指定远程分支，则默认的远程分支为master
   ```

9. **`git reset --hard`** 与 **`git cherry-pick`** 

   ```cpp
   git reset --hard // 回退代码，回退到某个commit_id
   git cherry-pick	// 摘草莓，摘取某个commit_id到当前分支下(只要这个commit_id存在就好，不在乎它在哪个分支下的)
   git reset --hard HEAD/HEAD^/HEAD^^/HEAD~100 // 回退到上几个版本
   // HEAD是当前版本，HEAD^上个版本，HEAD^^上上个版本，HEAD~100回退100个版本
   git reset --hard 3628164 // 回退到指定版本号，版本号不用写全
   ```

10. **`git chechout`** 与 **`git branch`**

      ```cpp
      git checkout 
      git checkout -b 分支名 // 在本地当前分支的基础上，新建一个新分支
      git checkout -b 本地分支名 origin/远程分支名 // 拉取远程分支去创建本地分支
      git checkout -b 分支名 commit_id // 用某个commit新建分支
      git分支
      git branch // 查看所有本地分支
      git branch -r // 查看所有远程分支：
      git branch -a // 查看所有本地和远程分支：
      git fetch origin 远程分支名:本地分支名 // 然后
      git checkout 本地分支名 // 用远程分支新建分支
      ```

11. **`git help`** 与 **`git gui`**

     ```cpp
     // git help是个可以查看所有git命令的手册，比如要查询git branch相关参数，执行git help branch，然后OPTIONS字段就能看到所有git branch的所有参数及其解释，比如想看git branch -u的用法
     // git gui是git的图形操作界面
     ```

------

### 撤销修改

1. 撤销工作区修改(尚未add，尚未commit)

   ```cpp
   git checkout -- readme.txt
   ```

2. 撤销暂存区修改(已经add，尚未commit)

   ```cpp
   git reset HEAD readme.txt
   git checkout -- readme.txt
   // git reset命令既可以回退版本，也可以把暂存区的修改回退到工作区。当我们用HEAD时，表示最新的版本。
   ```

3. 撤销版本库修改(已经commit，尚未推送到远程)

   ```cpp 
   git reset --hard HEAD^ // 版本回退
   ```

   ```mermaid
   graph LR
   	A[工作区] -->|add| B[暂存区]
   	B[暂存区] -->|commit| C[本地版本库]
   	C[本地版本库] -->|push| D[远程版本库]
   	D[远程版本库] -->|pull/clone| C[本地版本库]
   	
   	subgraph add前退回
   		A
   		E(git checkout -- readme.txt)
   	end
   	
   	subgraph add后回退
   		B
   		F(git reset HEAD readme.txt
   			git checkout -- readme.txt)
   	end
   	
   	subgraph commit后回退
   		C
   		G(git reset --hard HEAD^)
   	end
   ```

4. 版本回退

   ```cpp
   // 删除分支
   git branch -D br // 删除本地分支
   git push origin :br  // 删除远程分支(origin 后面有空格)
   
   // 代码回滚: 指的是将代码库某分支退回到以前的某个commit_id
   // 本地代码库回滚
   git reset --hard commit_id // 回滚到commit_id，讲commit_id之后提交的commit都去除
   git reset --hard HEAD~3 // 将最近3次的提交回滚(HEAD~3可以改写成HEAD^^^)
       
   // 远程代码库回滚
   // 应用场景：自动部署系统发布后发现问题，需要回滚到某一个commit，再重新发布
   // 原理：先将本地分支退回到某个commit，删除远程分支，再重新push本地分支
   // 操作步骤：
   git checkout the_branch
   git pull
   git branch the_branch_backup // 备份一下这个分支当前的情况
   git reset --hard the_commit_id // 把the_branch本地回滚到the_commit_id
   git push origin :the_branch // 删除远程 the_branch
   git push origin the_branch // 用回滚后的本地分支重新建立远程分支
   git push origin :the_branch_backup // 如果前面都成功了，删除这个备份分支
   // 如果使用了gerrit做远程代码中心库和code review平台，需要确保操作git的用户具备分支的push权限，并且选择了Force Push选项（在push权限设置里有这个选项）
   // 另外，gerrit中心库是个bare库，将HEAD默认指向了master，因此master分支是不能进行删除操作的，最好不要选择删除master分支的策略，换用其他分支。如果一定要这样做，可以考虑到gerrit服务器上修改HEAD指针。。。不建议这样搞
   
   // 远程代码库master分支回滚
   // 在强推mster的可能会报错没有权限：You don't have permission
   // 是因为master分支一般会成为保护分支，所以我们首先要去除master为保护分支，才可以强推。
   
   
   ```

   > [!TIP]
   >
   > 标签和分支的对比
   >
   > |        |      | 标签                                           | 分支                          |
   > | ------ | ---- | ---------------------------------------------- | ----------------------------- |
   > | 新建   |      | `git tag tagname (commit_id)`                  | `git checkout -b branchname`  |
   > |        |      | `git tag -a tagname -m "标签详情" (commit_id)` |                               |
   > | 查看   | 当前 | `git show tagname`                             | 无                            |
   > |        | 全部 | ` git tag`                                     | ` git branch`                 |
   > | 推远程 |      | `git push origin tagname`                      | ` git push origin branchname` |
   > | 删除   | 本地 | ` git tag -d tagname`                          | `git branch -D branchname`    |
   > |        | 远程 | `git push origin :refs/tags/tagname`           | `git push origin :branchname` |

------



### 删除文件

```cpp
git add test.txt
git commit -m "add test.txt" 

rm test.txt  // 从工作区删除该文件

git rm test.txt
git commit -m "remove test.txt" // 从版本库中删除该文件，并提交
    
git checkout -- test.txt // 假设工作区开始就删错了，可以用版本库的覆盖工作区的
```

------

### 远程仓库

1. 连上远程库

   ```cpp
   git remote add origin git@github.com:wuhuaguo2/learngit.git  
   ```

2. 本地向远程推送内容

   ```cpp
   git push -u origin master // 第一次把本地库的master分支所有内容推送到远程库的master分支上
   git push origin master // 非第一次把本地库的master分支所有内容推送到远程库的master分支上
   git push origin dev // 非第一次把本地库的dev分支所有内容推送到远程库的master分支上
   // 远程库的名字就是origin
   ```

3. 远程库的所有内容推送到本地库上

   ```cpp
   // 第一次
   git clone git@github.com:wuhuaguo2/gitskills.git // 或
   git clone http://github.com/wuhuaguo2/gitskills // 但是接下来得输入账号密码
   
   git checkout -b dev // 如果想拉指定分支如dev，先在本地，然后
   git clone -b dev git@github.com:wuhuaguo2/gitskills.git // 或
   git clone -b dev http://github.com/wuhuaguo2/gitskills
   
   // 第二次及以上
   git pull // 命令用于从另一个存储库或本地分支获取并集成(整合)
   // git pull 命令的作用是：取回远程主机某个分支的更新，再与本地的指定分支合并。 
   // git pull = git fetch + git merge
   
   // 如果gitlab上a提交了，b又提交了，现在a在本地修改了代码，准备提交
   git add .
   git commit -m “a second tijiao” 
   git push origin master
   // 此时肯定提交不上去，需要先pull下来(pull = fetch取远程 + merge远程与本地合并)
   git pull origin master
   // 如果此时出现merge conflict，去解决冲突，然后
   git add .
   git commit -m “conflict resolved”
   git push origin master
   ```

------

### 分支管理



1. 基础命令

   ```cpp
   git branch // 查看分支
   git branch 分支名 // 创建分支
   git checkout 分支名 // 切换分支
   git checkout -b 分支名 // 创建+切换分支
   git merge 分支名 // 合并某分支到当前分支
   git branch -d 分支名 // 删除分支
   git branch -D 分支名 // 删除未被合并的分支
   
   //创建分支并上传线上
   git checkout -b xf
   git add routes/web.php
   git commit -m “test”
   git push origin xf
   
   //查看分支，并pull下来
   git fetch -all
   git pull origin xf 
   ```

2. 解决冲突

   ```cpp
   // feature分支和master分支各自修改readme.txt，在git merge feature提示冲突了
   git status // 看到2个分支对readme.txt的提交冲突了，或者
   cat readme.txt // 会看到<<<，===，>>>标记出不同分支的冲突内容 
   git add . 
   git commit . // 修改冲突
   git log --graph --pretty=oneline --abbrev-commit // 查看分支合并情况
   git branch -d feature // 删除feature分支
   ```

   > [!WARNING]
   >
   > `git checkout -b xf1 origin/dev`
   >
   > 危险操作，将本地xf1分支和线上dev分支关联起来。一般而言，本地分支和线上分支名字保持一致。

3. 分制管理策略(禁掉快进模式)

   ```cpp
   // 合并分支时，如果可能，Git会用Fast forward(快进)模式，但这种模式下，删除分支后，会丢掉分支信息。如果要用--no-ff强制禁用Fast forward模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。
   git add .
   git merge dev // 在dev分支上add, merge
   git checkout master // 切到master分支
   git merge--no-ff -m "merge with no-ff" dev // 用—no-ff来merge
   // 因为本次合并要创建一个新的commit，所以加上-m参数，把commit描述写进去
   git log --graph --pretty=oneline --abbrev-commit // 查看分支合并情况
   ```

4. BUG分支

   ```cpp
   // 在dev分支下开发，突然接到任务：去master下修复一个代号=102的bug，但此时dev上add了但未commit，咋办?
   // 用stash可以把当前工作现场“储藏”起来
   git stash 
   // 切到master分支，从master创建临时分支issue-101，修复bug
   git checkout master
   git checkout -b issue-101
   vim readme.txt
   git add readme.txt 
   git commit -m "fix bug 101" 
   // 修复完成后，切换到master分支，并完成合并，最后删除issue-101分支
   git checkout master
   git merge --no-ff -m "merged bug fix 101" issue-101
   git branch -d issue-101 
   // 回到dev分支、恢复工作区，继续开发
   git checkout dev
   git status // 显示工作区是干净的，因为存在stash里面  
   git stash list // 查看储藏列表  
   // 从储藏恢复到工作区，两种方式：
   git stash apply // 恢复工作区，再用
   git stash drop // 删除stash，或
   git stash pop // 恢复的同时把stash内容也删了
   git stash list // 再次查看，就看不到任何stash内容了
   ```

5. Feature分支

   ```cpp
   // 开发一个新的feature，最好新建一个分支。
   git branch -D 分支名 // 删除未被合并的分支
   ```

6. 多人协作

   ``` cpp
   git remote // 查看远程库的信息，默认为origin
   git remote -v // 示更详细的信息  
   git push origin branch_name // 从本地推送分支，如果推送失败，先用git pull抓取远程的新提交
   git checkout -b branch_name origin/branch_name // 在本地创建和远程分支对应的分支，本地和远程分支的名称最好一致
   git branch --set-upstream branch_name origin/branch_name // 建立本地分支和远程分支的关联
   git pull origin master // 从远程抓取分支，如果有冲突，要先处理冲突
   ```

------

### 忽略上传

> [!TIP]
>
> git忽略对已入库文件的修改

1. 忽略上传

   `.gitignore` 或者 `excludes` 只针对尚未提交到配置库的文件才起作用。而对于已经提交的文件是不起作用的。
   由此可见，这两个文件的初衷是用于排除不希望上传入库的文件。像编译产生的临时文件等。

2. 忽略更新上传

   ```cpp
   // 有个文件，我们必须入库，大家一起共享，但是每个人本地的配置又是因自己本地的环境而异。想后续不再更新给文件的修改，使用下面的命令：
   git update-index --assume-unchanged FILENAME
   // 这样，每个人，从库上取代码后，在自己本地都要执行一下上面的这个命令。这样，以后，你这个文件的修改，git 都会帮你忽略掉。
   // 当然，哪一天，你希望你的修改要提交入库，那你也必须手动修改一下 这个文件的标志位：
   git update-index --no-assume-unchanged FILENAME
   ```

------

### 文件对比

```cpp
// git对比2个版本某个文件的差异
git diff // 查看尚未暂存的某个文件更新了哪些部分
git diff filename // 查看尚未暂存的某个文件更新了哪些
git diff –cached // 查看已经暂存起来的文件和上次提交的版本之间的差异
git diff –cached filename // 查看已经暂存起来的某个文件和上次提交的版本之间的差异
git diff commit_id1 commit_id2 // 查看某两个版本之间的差异
git diff commit_id1 commit_id2 具体文件路径 //查看某两个版本的某个文件之间的差异，红色部分是commit_id1，绿色部分是commit_id2
git diff commit_id1:具体文件路径 commit_id2:具体文件路径

// git对比2个分支某个文件的差异
git diff branch1 branch2 --stat // 显示出所有有差异的文件列表
git diff branch1 branch2 // 显示出所有有差异的文件的详细差异
git diff branch1 branch2 具体文件路径 //显示指定文件的详细差异,红色部分是commit_id1,绿色部分是commit_id2
git diff branch1:具体文件路径 branch2:具体文件路径
```

------

### 高频操作

1. 分支创建

   ```cpp
   git checkout -b 分支名 commit_id // 用某个commit新建分支：
   git fetch origin 远程分支名:本地分支名 // 用远程分支新建分支，然后
   git checkout 本地分支名
   ```

2. 更改commit的备注

   ```cpp
   git commit --amend // 只想修改最后一次注释： 
   // 出现有注释的界面（你的注释应该显示在第一行），输入i进入修改模式，修改好注释后，按Esc键 退出编辑模式，输入:wq保存并退出。ok，修改完成。
   
   // 修改之前的注释
   git rebase -i HEAD~10 // 想修改的那条注释前的 pick换成edit
   git commit --amend
   git rebase --continue
   ```

3. 版本回退

   ```cpp
   // 比如commit提交最新到最旧为: D C B A 
   git reset --hard B // 回退到B，CD不要了，===>版本回退
   git revert B // 撤销B的提交，其余保留， ===>版本撤销
   git cherry-pick B // 取消对B提交的撤销，B重新回来
   ```

4. IDE上不同分支代码对比
