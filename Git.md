# Git

[[Learn Git Branching](https://learngitbranching.js.org/?locale=zh_CN)]()

### 基础命令

#### --`Git init`

初始化本地库

```git
git init
```

#### --`Git status`

```git
git status
```

查看当前本地库状态

#### --`Git add`

从工作区提交到暂存区

```git
git add <文件名>或全部 .
```

#### --`Git commit`

提交到本地库

git commit 相当于复制一遍文件再粘贴

此外git会智能的检查当前commit与之前版本的差异

```git
git commit <-m 版本控制信息>（非必须）
```

#### 分支

在版本控制中同时推进多任务，需要使用分支进行区分 可以理解成副本 分支的底层其实也是指针的引用 可以提高开发效率

#### --`Git branch` 

```git
git branch -v 查看列出分支
```

```git
git branch <分支名>来创建分支
```

```git
git checkout <分支名>来切换分组
```

也可以使用

```git
git checkout -b <分支名>来创建并切换分支
```

```git
git branch -d <分支名> 删除分支
```

##### 分支合并

#### --`Git merge`

```git
git merge <分支名>
```

#### --`Git rebase`

```git
git rebase <分支名>
```

#### --`HEAD`

![image-20210816132156880](C:\Users\haoxi\AppData\Roaming\Typora\typora-user-images\image-20210816132156880.png)

如果想查看 HEAD 指向

可使用

```git
cat ./git/HEAD
```

如果HEAD指向的是一个引用，可使用

```git
git symbolic-ref HEAD
```

分离的HEAD就是让其指向某个具体的提交记录而不是分支名

```git
git checkout <记录名>
```

##### 提交记录

#### --`Git log`

#### --`Git reflog` 精简信息

使用

```git
git log 查看提交等操作的记录
```

##### 相对引用

切换到上一个记录

```git
git checkout <分支名> +^
```

或

```git
git checkout <分支名> +~ 可加数字 不加时跟^相同
```

强制修改分支位置

如：

```git
git branch -f main HEAD~3
```

##### 撤销变更

本地

```git
git reset <HEAD> 会导致历史记录中不存在这次删除
```

远程

```git
git revert <HEAD> 记录仍然存在 并且会存在新的提交记录 该提交记录与撤销的记录的上一个记录内容相同
```

##### 将一些提交复制到当前所在的位置

```git
git cherry-pick <提交事件>
```

#### 团队协作

#### Github 

#### --`Git push`

```git
git push <名字> <分支>
```

#### --`Git pull`

```git
git pull <名字> <分支>
```

#### --`Git clone`

```git
git clone <链接>
```

