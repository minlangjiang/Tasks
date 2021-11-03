# Git Bash的简单使用教程

[![HUST潘潘](https://pic3.zhimg.com/v2-fd97daa2f44e7be898e791c8619c6bae_xs.jpg)](https://www.zhihu.com/people/panda-9-6)

[HUST潘潘](https://www.zhihu.com/people/panda-9-6)

码农

57 人赞同了该文章

Git的下载安装及配置详见这篇笔记：

[HUST小菜鸡：Git的下载安装及配置39 赞同 · 12 评论文章![img](https://pic2.zhimg.com/v2-364b3b84c530fa02ee988088b3c0e0b5_180x120.jpg)](https://zhuanlan.zhihu.com/p/123195804)

## 一、本地文件的基本操作

进入某一个文件夹，和Linux系统一样有两种方式：

1. 直接进入该文件夹位置，然后右键Git Bash Here，在当前文件夹打开Git Bash，类似于打开Terminal，此时的终端的路径就是在当前文件夹，然后对文件进行相关操作
2. 在桌面右键Git Bash Here，通过dir查看当前目录文件，通过cd命令进入文件夹，通过cd ..命令返回上一级，也可以使用cd xxx/xxx/xxx一次性直接到达指定位置，通过rm指令删除指定文件（**注意在Git Bash中，使用cd命令是‘/’而不是Windows系统中的‘\’**）
3. 可以通过pwd命令来查看当前是在哪个文件夹进行的操作

```pytb
15890@LAPTOP-PanXF MINGW64 /d/Git (master)
$ pwd
/d/Git
```

## 二、将文件夹变成本地仓库

进入到指定的文件夹之后，使用git init指令将本地文件夹变成本地仓库

```text
git init
```

你会发现原来的文件路径后面多出一个（master）

本地文件夹中也会出现.git隐藏文件夹（是git的控制文件），千万不可以删除

![img](https://pic1.zhimg.com/80/v2-ab6b3664031ff05368e129581f897f2c_720w.jpg)

## 三、添加文件

我在文件夹中复制进去了自己的一个测试代码的文件，然后使用如下指令

```text
git add 文件名.文件类型
```

**敲黑板！！！**肯定有好奇宝宝和我一样，文件既然已经放进了仓库的问价中，为什么还要用git add指令去添加呢。可以理解为将此文件交给git去管理。

git文件有四种状态，1. untracked files、2. change to be commited、3. nothing to commit, working directory clean、4. changes not staged for commit。

对于同一个文件既有change to be committed 又有 change not staged for commit，说明文件在add后进行了修改，如果这时候直接执行commit, add过后进行的修改不会修改到仓库，文件的状态会变为第四个4. changes not staged for commit，如果这时候执行add，然后在commit,这样add后的修改也会一起提交到仓库。我们平时使用git的时候一般都是2，3，4不断的循环，现在假设Git中没有add命令会怎么样呢？我们会发现只会有三个状态1，3，4，少了状态2,4，我们只需要在3,4两个状态间循环就可以。也许你会说这不是很好嘛，简单了很多，但是往往复杂的设计是为了带来更多的功能。

有了git add 命令，你可以在随时add，如果代码出现了问题，可以随时倒回到git add 时候的状态。你还可以随时比较当前代码和git add 时代码的差别，git add 时和仓库代码的差别，当前代码和仓库代码的差别。



![img](https://pic1.zhimg.com/80/v2-915fd9f6a4cfcb5a9d72ab87275d6094_720w.jpg)

[为什么要有Git add 命令 - 我是偶哦的个人页面 - OSCHINAmy.oschina.net/abely/blog/678310![img](https://pic1.zhimg.com/v2-b7cb87ac2e44f3f70c2e1cf87f1beaa0_180x120.jpg)](https://link.zhihu.com/?target=https%3A//my.oschina.net/abely/blog/678310)

也可以用以下指令进行批量操作

```text
git add -A     提交所有变化
git add -u     提交被修改的文件和被删除的文件，不包括新文件
git add .      提交新文件和被修改的文件，不包括被删除的文件
```

## 四、提交文件

```text
git commit -m  "修改注释"
```

一定要commit，否则无法同步到云端

```text
15890@LAPTOP-PanXF MINGW64 /d/Git (master)
$ git commit -m "第二次修改"
[master 5b477e8] 第二次修改
 1 file changed, 7 insertions(+), 1 deletion(-)
```

查看修改内容

```text
git diff 文件名.文件类型
```

查看所有文件内容

```text
cat 文件名.文件类型
```

![img](https://pic1.zhimg.com/80/v2-1be0e3bc5fe4790b26b3fad39ad8b0c4_720w.jpg)

## 五、同步远程仓库

### 1、新建仓库

首先在GitHub新建一个仓库，GitHub的配置和链接参照：[HUST小菜鸡：Git的下载安装及配置](https://zhuanlan.zhihu.com/p/123195804)，新建仓库的流程如图所示

![img](https://pic4.zhimg.com/80/v2-8719f48615f142b950b5f73a0a85f40b_720w.jpg)

![img](https://pic4.zhimg.com/80/v2-eda2245aa13905620f4e82ee51721833_720w.jpg)以上两步就完成了新仓库的创建

然后会弹出一个界面，里面有不同的连接方式，选择ssh方式进行连接

![img](https://pic4.zhimg.com/80/v2-de015a30bb9aea93b16be837abf08d67_720w.jpg)

也可以选择用HTTPS进行传输，不过速度会很慢

其中**origin**是仓库的代名词，也可以换成其他的，但是自己要记住

> 要关联一个远程库，使用命令`git remote add origin git@server-name:path/repo-name.git`；
> 关联后，使用命令`git push -u origin master`第一次推送master分支的所有内容；
> 此后，每次本地提交后，只要有必要，就可以使用命令`git push origin master`推送最新修改；
> 要克隆一个仓库，首先必须知道仓库的地址，然后使用`git clone`命令克隆。
> Git支持多种协议，包括`https`，但通过`ssh`支持的原生`git`协议速度最快。

### 2、将新仓库和本地git相关联

```text
git remote add origin git@github.com:PanXF-HUST/test.git
```

复制代码到Git Bash，即可实现新仓库和这个的相关联

使用 git remote -v 命令查看关联状况

```text
git remote -v
```

![img](https://pic4.zhimg.com/80/v2-e0f5e65367606ce5c930b8cc0bede7cf_720w.jpg)

我为了测试把仓库代称改成别的名字在这里换成了test

如果不想与这个远程仓库连接了，只需要用git remote remove test即可删除连接，重新连接就可以恢复

![img](https://pic4.zhimg.com/80/v2-b853b49d556621f0d5ec756ab995884f_720w.jpg)

![img](https://pic2.zhimg.com/80/v2-67ecd27f3797a492cfd9971181d7f90d_720w.jpg)

**敲黑板！！！**肯定有小伙伴和我一样有困惑，我删除了之后我从哪里去找我的SSH呢，大家仔细对比一下刚刚的命令

git remote add origin git@github.com:PanXF-HUST/test.git

origin表示远程仓库的代名称

git@github.com:PanXF-HUST/test.git表示SSH key

![img](https://pic4.zhimg.com/80/v2-41c96a7237c6d0f970f79227ddd2f463_720w.jpg)

### 4、内容同步

在第一次同步的时候，必须使用如下指令

```text
git push -u 仓库代称 master
```

第一次推送master分支时，必须加上-u参数，git不但会推送分支，还会把本地master分支与远程master分支相关联，以后的推送直接使用git push 仓库代称 master即可

![img](https://pic3.zhimg.com/80/v2-f613d6cc072e3cb0b1ceabf99db8b896_720w.jpg)

```text
git push 仓库代称 master
```

![img](https://pic4.zhimg.com/80/v2-ea6f88a490d6560d7794c64db2d781d3_720w.jpg)

同步后可以进GitHub的web端看已经被修改

![img](https://pic1.zhimg.com/80/v2-31f108e63fc830e8453bbed3731d5dc0_720w.jpg)

### 5、查看版本信息

查看当前版本信息

```text
git log
```

![img](https://pic2.zhimg.com/80/v2-4407fadecd624ba07e64d61e171a7ea1_720w.jpg)

查看某个文件版本信息

```text
git log --follow 文件名.文件类型
```

![img](https://pic2.zhimg.com/80/v2-ab3248f4b25cfd6efd6f36de0eeac509_720w.jpg)

```text
git whatchanged 文件名.文件类型
```

![img](https://pic1.zhimg.com/80/v2-ff98ca196971e8adf9427b3807d70974_720w.jpg)

显示所有提交过的用户，按提交次数排序

```text
git shortlog -sn
```

![img](https://pic4.zhimg.com/80/v2-3e88b6752d819619c4070982c288bddf_720w.jpg)

显示指定文件是什么人在什么时间修改过

```text
git blame 文件名.文件类型

15890@LAPTOP-PanXF MINGW64 /d/Git (master)
$ git blame datatest.py
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800   1) import torch
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800   2) import torchvision
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800   3) import numpy as np
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800   4)
5b477e82 (PanXF-HUST 2020-04-04 12:26:46 +0800   5) '''edit on 2020/04/04 for first test'''
5b477e82 (PanXF-HUST 2020-04-04 12:26:46 +0800   6)
5b477e82 (PanXF-HUST 2020-04-04 12:26:46 +0800   7) '''edit on 2020/04/04 for the second test'''
5b477e82 (PanXF-HUST 2020-04-04 12:26:46 +0800   8)
5b477e82 (PanXF-HUST 2020-04-04 12:26:46 +0800   9) '''edit on 2020/04/04 for the third test'''
5b477e82 (PanXF-HUST 2020-04-04 12:26:46 +0800  10)
c31a95ae (PanXF-HUST 2020-04-04 12:57:30 +0800  11) '''edit on 2020/04/04 for the fourth test'''
c31a95ae (PanXF-HUST 2020-04-04 12:57:30 +0800  12)
5b477e82 (PanXF-HUST 2020-04-04 12:26:46 +0800  13)
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  14)
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  15) '''
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  16)     bboxes:         bbox locations list (n, 4)
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  17)     bbox_scores:    bbox scores list (n,)
:...skipping...
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800   1) import torch
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800   2) import torchvision
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800   3) import numpy as np
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800   4)
5b477e82 (PanXF-HUST 2020-04-04 12:26:46 +0800   5) '''edit on 2020/04/04 for first test'''
5b477e82 (PanXF-HUST 2020-04-04 12:26:46 +0800   6)
5b477e82 (PanXF-HUST 2020-04-04 12:26:46 +0800   7) '''edit on 2020/04/04 for the second test'''
5b477e82 (PanXF-HUST 2020-04-04 12:26:46 +0800   8)
5b477e82 (PanXF-HUST 2020-04-04 12:26:46 +0800   9) '''edit on 2020/04/04 for the third test'''
5b477e82 (PanXF-HUST 2020-04-04 12:26:46 +0800  10)
c31a95ae (PanXF-HUST 2020-04-04 12:57:30 +0800  11) '''edit on 2020/04/04 for the fourth test'''
c31a95ae (PanXF-HUST 2020-04-04 12:57:30 +0800  12)
5b477e82 (PanXF-HUST 2020-04-04 12:26:46 +0800  13)
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  14)
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  15) '''
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  16)     bboxes:         bbox locations list (n, 4)
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  17)     bbox_scores:    bbox scores list (n,)
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  18)     pose_preds:     pose locations list (n, 17, 2)
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  19)     pose_scores:    pose scores list    (n, 17, 1)
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  20)
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  21)     0       nose
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  22)     1       left_eye
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  23)     2       right_eye
:...skipping...
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800   1) import torch
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800   2) import torchvision
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800   3) import numpy as np
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800   4)
5b477e82 (PanXF-HUST 2020-04-04 12:26:46 +0800   5) '''edit on 2020/04/04 for first test'''
5b477e82 (PanXF-HUST 2020-04-04 12:26:46 +0800   6)
5b477e82 (PanXF-HUST 2020-04-04 12:26:46 +0800   7) '''edit on 2020/04/04 for the second test'''
5b477e82 (PanXF-HUST 2020-04-04 12:26:46 +0800   8)
5b477e82 (PanXF-HUST 2020-04-04 12:26:46 +0800   9) '''edit on 2020/04/04 for the third test'''
5b477e82 (PanXF-HUST 2020-04-04 12:26:46 +0800  10)
c31a95ae (PanXF-HUST 2020-04-04 12:57:30 +0800  11) '''edit on 2020/04/04 for the fourth test'''
c31a95ae (PanXF-HUST 2020-04-04 12:57:30 +0800  12)
5b477e82 (PanXF-HUST 2020-04-04 12:26:46 +0800  13)
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  14)
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  15) '''
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  16)     bboxes:         bbox locations list (n, 4)
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  17)     bbox_scores:    bbox scores list (n,)
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  18)     pose_preds:     pose locations list (n, 17, 2)
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  19)     pose_scores:    pose scores list    (n, 17, 1)
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  20)
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  21)     0       nose
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  22)     1       left_eye
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  23)     2       right_eye
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  24)     3       left_ear
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  25)     4       right_ear
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  26)     5       left_shoulder
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  27)     6       right_shoulder
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  28)     7       left_elbow
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  29)     8       right_elbow
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  30)     9       left_wrist
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  31)     10      right_wrist
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  32)     11      left_hip
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  33)     12      right_hip
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  34)     13      left_knee
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  35)     14      right_knee
:...skipping...
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800   1) import torch
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800   2) import torchvision
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800   3) import numpy as np
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800   4)
5b477e82 (PanXF-HUST 2020-04-04 12:26:46 +0800   5) '''edit on 2020/04/04 for first test'''
5b477e82 (PanXF-HUST 2020-04-04 12:26:46 +0800   6)
5b477e82 (PanXF-HUST 2020-04-04 12:26:46 +0800   7) '''edit on 2020/04/04 for the second test'''
5b477e82 (PanXF-HUST 2020-04-04 12:26:46 +0800   8)
5b477e82 (PanXF-HUST 2020-04-04 12:26:46 +0800   9) '''edit on 2020/04/04 for the third test'''
5b477e82 (PanXF-HUST 2020-04-04 12:26:46 +0800  10)
c31a95ae (PanXF-HUST 2020-04-04 12:57:30 +0800  11) '''edit on 2020/04/04 for the fourth test'''
c31a95ae (PanXF-HUST 2020-04-04 12:57:30 +0800  12)
5b477e82 (PanXF-HUST 2020-04-04 12:26:46 +0800  13)
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  14)
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  15) '''
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  16)     bboxes:         bbox locations list (n, 4)
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  17)     bbox_scores:    bbox scores list (n,)
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  18)     pose_preds:     pose locations list (n, 17, 2)
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  19)     pose_scores:    pose scores list    (n, 17, 1)
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  20)
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  21)     0       nose
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  22)     1       left_eye
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  23)     2       right_eye
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  24)     3       left_ear
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  25)     4       right_ear
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  26)     5       left_shoulder
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  27)     6       right_shoulder
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  28)     7       left_elbow
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  29)     8       right_elbow
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  30)     9       left_wrist
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  31)     10      right_wrist
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  32)     11      left_hip
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  33)     12      right_hip
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  34)     13      left_knee
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  35)     14      right_knee
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  36)     15      left_ankle
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  37)     16      right_ankle
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  38)
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  39)     part_mask
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  40)     0       head
^f01195e (PanXF-HUST 2020-04-02 23:13:47 +0800  41)     1       shoulder
:
```

## 六、远程仓库修改后更新本地仓库

### 1、克隆仓库

```text
git clone 复制的SSH或者HTTPS key
```

在团队合作中，你的队友修改了远程仓库之后，你如何确保自己的文件跟远程仓库一致呢，这就需要以下步骤了。在你init或者Clone的过程中，Git会自动在本地分支与远程分支之间，建立一种追踪关系(tracking)。比如，在git clone的时候，所有本地分支默认与远程主机的同名分支，建立追踪关系，也就是说，本地的master分支自动连接到远程的origin/master分支。

### 2、取回远程文件

```text
git pull 仓库代名称
```

我在GitHub的web端修改了文件及修改了文件名，取回远程文件



![img](https://pic3.zhimg.com/80/v2-31224eedbfee79978a3f2f73f528f41e_720w.jpg)

![img](https://pic1.zhimg.com/80/v2-bf06dba32432ebbf6bf06b329111d024_720w.jpg)

可以看到本地仓库也被修改

```text
git fetch
```

拉回远程的commit数据，将commit id更新为最新的，但是不会修改本地仓库

![img](https://pic1.zhimg.com/80/v2-82be0b3e88f406895944d9f740e5bb2c_720w.jpg)

![img](https://pic2.zhimg.com/80/v2-66f1c49b158991adf1acd1ee9897ace5_720w.png)拉回commit信息，但是本地仓库没有被修改

```text
git merge
```

合并本地仓库

![img](https://pic4.zhimg.com/80/v2-2a41caaec89fcb7b3968d2d6be90ce5f_720w.jpg)

![img](https://pic3.zhimg.com/80/v2-2c3441671efb1af4eee81090e83c35a2_720w.png)本地仓库被修改

通过以上可以对pull和push操作重新理解

**push：add——commit——push**

**pull = fetch + merge**

![img](https://pic1.zhimg.com/80/v2-3010981efd1adc73b1125583f42c3fd4_720w.jpg)