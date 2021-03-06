*本文是[廖雪峰老师网站Git教程](https://www.liaoxuefeng.com/wiki/896043488029600)和[Git官方教程 ProGit](https://git-scm.com/book/zh/v2)的学习笔记，部分内容结合个人理解添加*  
*标题包含的链接指向我的笔记来源；正文中链接用于文内跳转*  
*本文中的代码有的用图，有的用字符，这个是看心情决定的，没有特殊含义，一般彩色的我都会截图* \_(:3 j ∠)_

---
# 目录
- [目录](#目录)
- [Git简介](#git简介)
  - [Git的诞生](#git的诞生)
  - [集中式 VS 分布式](#集中式-vs-分布式)
- [安装Git](#安装git)
- [创建版本库](#创建版本库)
  - [创建](#创建)
  - [向版本库添加文件](#向版本库添加文件)
- [时光穿梭机](#时光穿梭机)
  - [版本回退](#版本回退)
  - [工作区和暂存区](#工作区和暂存区)
  - [管理修改](#管理修改)
  - [撤销修改](#撤销修改)
  - [删除文件](#删除文件)
- [远程仓库](#远程仓库)
  - [添加远程库](#添加远程库)
  - [从远程库克隆](#从远程库克隆)
- [分支管理](#分支管理)
  - [创建与合并分支](#创建与合并分支)
  - [解决冲突](#解决冲突)
  - [分支管理策略](#分支管理策略)
  - [Bug分支](#bug分支)
  - [Feature分支（强制删除分支）](#feature分支强制删除分支)
  - [多人协作](#多人协作)
    - [推送分支](#推送分支)
    - [抓取分支](#抓取分支)
  - [Rebase](#rebase)
    - [变基的基本操作](#变基的基本操作)
- [打标签](#打标签)
  - [列出标签](#列出标签)
  - [创建标签](#创建标签)
  - [轻量标签](#轻量标签)
  - [附注标签](#附注标签)
  - [后期打标签](#后期打标签)
  - [共享标签](#共享标签)
  - [删除标签](#删除标签)
  - [检出标签](#检出标签)
- [使用GitHub](#使用github)
- [使用Gitee](#使用gitee)
- [自定义Git](#自定义git)
  - [忽略特殊文件](#忽略特殊文件)
  - [配置别名](#配置别名)
  - [搭建Git服务器](#搭建git服务器)
- [使用SourceTree](#使用sourcetree)

# [Git简介](https://www.liaoxuefeng.com/wiki/896043488029600/896067008724000)
> **世界上最先进的分布式版本控制系统**

---
## [Git的诞生](https://www.liaoxuefeng.com/wiki/896043488029600/896202815778784)
***Linus***用两个礼拜，就用 ***C*** 写出了 ***Git*** 。

---
## [集中式 VS 分布式](https://www.liaoxuefeng.com/wiki/896043488029600/896202780297248)
- 集中式
  例如 ***CVS*** 和 ***SVN*** 。集中式版本控制系统把版本库集中存放在中央服务器。很依赖网络。
- 分布式
  每个人都有自己的版本库。中央服务器只是为了方便交换而存在，没有网络并不会严重影响工作。

---
# [安装Git](https://www.liaoxuefeng.com/wiki/896043488029600/896067074338496)
**过程略略略**  
[Git官网](https://git-scm.com)  
[Git各平台版本下载](https://git-scm.com/downloads)

---
# [创建版本库](https://www.liaoxuefeng.com/wiki/896043488029600/896827951938304)
## 创建
**我**用Git Bash比较顺手，所以下面的介绍都是**Git Bash**的  
流程：
1. 首先选一个喜欢的目录，比如`C:/user/yourname/learngit`之类的。尽量不要在路径中出现中文，避免出现不必要的麻烦。  
2. 打开Git Bash，切换工作路径到选好的位置，有两种方法:  
   1. 在文件资源管理器中打开选好的文件夹，在里面点击右键，菜单里出现一个`Git Bash Here`，选他，工作路径就自动在选好的位置了。
   2. 打开`Git Bash`，使用`cd C:/user/yourname/learngit`指令即可。（如果用Git CMD的话，切换到不同盘符下的路径需要用`cd /D path`，固定搭配，具体操作可以查一下表。

    不放心的话可以用`pwd`(***<font color=red>P</font>rint <font color=red>W</font>orking <font color=red>D</font>irectory***)指令查看当前的目录。
3. 输入`git init`指令，仓库就创建好了。用`ls -ah`指令查看，可以发现目录下多出了一个`.git`文件夹，这个文件夹就是跟踪管理版本库的。不要乱动这个文件夹里的东西，否则可能会破坏版本库。  

*选定的目录不需要是空的，但是不建议初学时使用有重要文件的文件夹，否则后果自负*

## 向版本库添加文件
*版本控制系统只能跟踪文本文件的改动，比如txt文件和代码等。而对于二进制文件，如图片、视频甚至word文件等，系统只能知道有改动，不能确定改动的内容。*  
1. 在上述创建的**Git仓库所在目录**下添加文件
2. 使用指令`git add [file]`，把文件添加到<font color=pinkblue>暂存区</font>(关于暂存区的概念会在后面提到，不理解可以先向后翻看)
3. 使用指令`git commit -m ["descriptive message"]`把文件提交到仓库，此次提交的说明就是`-m`后面的字符串

有两点提示：  
1. 如果向工作区添加了新文件，则在`commit`前必须`add`，不然新文件不会被提交。  
2. 如果没有新文件，可以使用`git commit -am`指令，就相当于先`add`再`commit -m`。（`-a`即把当前所有修改了的文件添加到暂存）  
3. 一次`commit`前可以多次`add`，`add`够了再`commit`也可以。

---
---
# [时光穿梭机](https://www.liaoxuefeng.com/wiki/896043488029600/896954074659008)
接下来介绍如何在版本间进行切换。在这之前我们要了解如何查看修改：  
- 当我们修改了工作区的文件，可以使用`git status`指令查看：  
  ![git_status](images/time_travel/git_status.png)  
  图片中红字的部分就是已修改但没有`add`的文件。  
  如果想要查看修改的内容，就使用`git diff [file]`指令：  
  ![git_diff](images/time_travel/git_diff.png)  
  结果中前面有减号，红色的部分为删减部分；前面有加号，绿色的为新增的部分。  
  **如果修改过多，可能出现缩略显示的情况，即在Bash窗口最下部显示一个半角冒号`:`，这时按上下键可以翻看全部内容；不想看可以按`ｑ`结束*  
  ![git_q](images/time_travel/git_q.png)  

- 如果已经`add`过，可以使用`git diff --staged`查看`add`时与最后一次提交之间做出修改。这里不再贴图。  
  将修改`add`到暂存区后，再查看`git status`，结果如图：  
  ![status_after_adding](images/time_travel/status_after_adding.png)  

- 提交后，`git status`：  
  ![status_after_committing](images/time_travel/status_after_committing.png)  
  可以看到这时显示工作目录是干净的(working tree clean)，没有要提交的修改。

---
## [版本回退](https://www.liaoxuefeng.com/wiki/896043488029600/897013573512192)
1. 使用`git log`，查看历史提交记录。  
  例如：  
  ![git_log](images/time_travel/git_log.png)  
  其中<b><i>`478fe7...`</i></b>和<b><i>`5585b10...`</i></b>是<kbd>**`commit id`**</kbd>(版本号)  
  如果决定输出太长，不方便查看，可以使用`git log --pretty=oneline`，这样提交信息会被缩减到一行内显示。  
  ![git_log_pretty_oneline](images/time_travel/git_log_pretty_oneline.png)  
  这样，我们就得到了每次提交的版本号和相应的提示信息。  
  *提醒一下，Git的版本号不是递增的数字，而是一个SHA1计算出来的非常大的十六进制数字。这样可以更好地适应多人在同一个版本库里工作的情况。*  
2. 获得版本号后，即可用`git reset --hard HEAD^`回退到上一个提交的版本。`HEAD`表示的是当前的版本，每加一个`^`就表示向前一个版本。如果版本相差太远，比如100个版本，也可以用`HEAD~100`来表示。当然，`HEAD`也可以换成上面提到的版本号(不用全部输入，一般输入前6位就足够了)。  
*这里的`--hard`会使文件退回到选定的版本，未保存的修改将丢失*  
如果不慎选错了版本，也有办法补救。Git的版本回退仅仅是将`HEAD`指针指向这个版本，并更新工作区文件。所以再次`reset`到原来想要的版本号即可。  
![HEAD1](images/time_travel/HEAD1.png)  
![HEAD2](images/time_travel/HEAD2.png)  
如果不记得版本号，就用`git reflog`指令查看指令记录，包括`reset`和`commit`等。  
![git_reflog](images/time_travel/git_reflog.png)  
图中前面的黄字部分就是操作时版本号的一部分，用它们`reset`即可。  

这里补充一个在ProGit上学到的操作：
如果一次提交时忘记添加几个文件，或者提交信息写错了，则可以使用`git commit --amend`命令提交。例如：
```
$ git commit -am "test-amend"
[test-amend 51c6580] test-amend
 2 files changed, 27 insertions(+), 9 deletions(-)

$ git log --oneline -1
51c6580 (HEAD -> test-amend) test-amend

# 这里我添加了一个文件
$ git add .
...

$ git commit --amend -m "test amend 2"
[test-amend 5a533bc] test amend 2
 Date: Fri Feb 12 14:32:58 2021 +0800
 3 files changed, 27 insertions(+), 9 deletions(-)
 create mode 100644 images/time_travel/file_lifecycle.png

$ git log --oneline -2
5a533bc (HEAD -> test-amend) test amend 2
0e9d372 (origin/dev, dev) finish learning co-working
```
可以看到，第二次提交包括了第一次提交和后来添加的内容，并且覆盖率第一次的提交信息。最终log中只会有一个提交。

> 当你在修补最后的提交时，并不是通过用改进后的提交 **原位替换** 掉旧有提交的方式来修复的， 理解这一点非常重要。从效果上来说，就像是旧有的提交从未存在过一样，它并不会出现在仓库的历史中。  
修补提交最明显的价值是可以稍微改进你最后的提交，而不会让“啊，忘了添加一个文件”或者 “小修补，修正笔误”这种提交信息弄乱你的仓库历史。

---
## [工作区和暂存区](https://www.liaoxuefeng.com/wiki/896043488029600/897271968352576)
- **工作区**  
  在电脑中能够看到的目录，如我使用的的Git文件夹
- **版本库**  
  工作区中有一个隐藏目录<kbd>`.git`</kbd>，这个文件夹就是Git的版本库。版本库中最重要的东西就是称为 ***`stage`*** (或叫 ***`index`*** )的暂存区，还有Git自动创建的第一个分支<kbd>`master`</kbd>，以及指向<kbd>`master`</kbd>的指针<kbd>`HEAD`</kbd>  
  使用`git add`时，会将文件修改添加到<font color=red>暂存区</font>；  
  使用`git commit`时，则会把暂存区的内容提交到<font color=red>当前分支</font>。  
  ![stage](images/time_travel/stage.png)  
  下图是ProGit中的文件状态变化周期  
  ![file_lifecycle](images/time_travel/file_lifecycle.png)

---
## [管理修改](https://www.liaoxuefeng.com/wiki/896043488029600/897884457270432)
Git管理的是**修改**，而不是文件。即使增删几个字符也算修改。  
提交文件前必须先添加到暂存区，再提交到版本库。如果没有`add`或`commit -a`，则修改不会被提交。这时用`git status`查看，还会显示有改动但没提交的文件。如果不理解可以动动手，动动脑，做一做这个实验。

---
## [撤销修改](https://www.liaoxuefeng.com/wiki/896043488029600/897889638509536)
如果做出了不符合预期或错误的修改，想要撤销，需要分为以下几种情况讨论：
1. 只做出了修改，没有添加到版本库  
  <s>如果没太大改动就撤销吧，<kbd>Ctrl</kbd>+<kbd>Z</kbd>挺好使的</s>  
  如果改得稀烂，比如我侄子来敲我的键盘，或者猴子们来我的电脑上仿写莎士比亚，那就需要Git来帮忙了。  
  我向Git许愿，Git说，彳亍！然后留下了一串神秘代码:  
  ***`git checkout -- [file]`***  
  `checkout`指令会丢弃工作区的修改，把文件恢复到最后一次添加到版本库时的状态，即最后一次`add`或`commit`时的样子。  
  *<font color=red>注意</font>: 里面的<kbd>`--`</kbd>不能丢，否则会变成另一个指令*  
  不过我在尝试时发现(我使用VS Code编辑)，未保存的修改不会被清除，但是在保存时会提示我当前文件内容较新，无法保存。需要用我的版本和文件内容进行比较，或覆盖文件内容。如图：  
  ![VSCode](images/time_travel/VSCode.png)  
  因为不想找麻烦，所以我一般会保存后再恢复。  

2. 已经将修改`add`到了暂存库，但没有`commit`  
   1. 使用`git reset HEAD [file]`指令，把暂存区的修改**撤销(*unstage*)**，重新放回工作区。
   2. `git restore --staged <file>`，作用和`reset`一样，不过文件名是必要的。全部恢复时就使用`git restore --staged .` 即可，<kbd>`.`</kbd>就表示全部文件。(不过restore这个指令我不太熟悉，使用前建议查表)
3. 已经`commit`，但是没有推送到远程仓库  
  还有救，按照[版本回退](#版本回退)一节的方法可以`reset`回来。
4. 已经推送到远程仓库  
  **救不了了，等着被制裁吧**

---
## [删除文件](https://www.liaoxuefeng.com/wiki/896043488029600/900002180232448)
1. 直接在资源管理器删除  
  直接删除或使用Linux指令`rm [file]`(别问Windows指令，我也不会)。这样删除会导致版本库和工作区的不一致，这时有两个选择：  
   1. 误删  
    从版本库恢复文件(如果没提交过就拉倒了)，使用`git checkout -- [file]`即可。  
    当然，误删的文件可以恢复，但是会**丢失最近一次添加到版本库后的更改**。因此删文件要谨慎！ 
   2. 我要删我要删！  
    那就需要在版本库里也删除文件。详见下一条。
2. 在版本库中删除文件  
   <s>使用`rm -rf`指令</s> **(千万不要尝试！)**  
   使用`git rm [file]`指令，会同时删除工作区的文件和版本库的文件。  
   *使用`git rm`指令删除的文件<u>**不会进入回收站**</u>，操作前务必考虑清楚*  
   如果想只删除版本库中的文件，可以加上`--cached`选项，例如`git rm --cached test.txt`；如果要删除文件夹中的文件，就需要加上`-r`。而如果想删除远程库中的文件，则只能靠commit和push了。  
   另外补充一点，`\*~`这种格式在Git的意思是文件名以`~`为结尾的文件。

---
---
# [远程仓库](https://www.liaoxuefeng.com/wiki/896043488029600/896954117292416)
Git是分布式版本控制系统，同一个Git仓库可以分布到不同的机器上。分布的方法就是各台机器克隆原始版本库到本地。每台机器上的版本库都是一样的，没有主次之分。  
在实际操作中，通常是一台机器作为服务器，全天上班，其他人从这里<b>克隆(clone)</b>版本库、将自己的提交<b>推送(push)</b>到服务器以及从服务器仓库中<b>拉取(pull)</b>别人的提交。  
我们可以自己搭建一台服务器，但是现在我还不会XD。所以这一段将介绍利用**GitHub**创建远程仓库。  
在开始之前，需要准备以下几点：  
1. 注册GitHub账号
2. 创建SSH Key  
   在`C:/Users/yourname`文件夹下如果有`.ssh`目录，里面有`id_rsa`和`id_rsa.pub`文件的话，就不需要创建了。  
   如果没有，就在Git Bash中输入以下指令：  
   `$ ssh-keygen -t rsa -C "youremail@example.com"`  
   *参考[ssh-keygen -t rsa -C "content" 解释](https://www.cnblogs.com/xunzhiyou/p/12117261.html)*  
   > -t: The type of the key to generate  
   > -C: comment to identify the key  
   > 也就是说`-C`后面不一定要接邮箱，随便写点什么都行。  

   都是普通老百姓，也没有那么高的保密需要，所以接下来一路回车就行。不放心就查一下怎么加密码。回车到底后，SSH Key就建立完了，可以在用户主目录下的`.ssh`文件夹里找到`id_rsa`和`id_rsa.pub`两个文件。  
   需要注意的是，生成的两个文件分别名为`id_rsa`和`id_rsa.pub`。其中<font color=red>`id_rsa`为私钥，不要泄露给别人</font>；`id_rsa.pub`为公钥，就随便了。  
3. 登录GitHub，打开"Account Settings"中的"SSH Keys"界面，然后点击"Add SSH Key"，Title自拟<s>，正文不少于800字</s>，在Key栏粘贴`id_rsa.pub`文件的内容(用记事本打开即可)。  
   ![add_ssh](images/remote_repo/add_ssh.png)
   添加后即可在页面看到
   ![succeed_adding_ssh_key](images/remote_repo/succeed_adding_ssh_key.png)  
   Git支持SSH协议，所以GitHub有了公钥后，就可以确认推送人的身份，确保只有我自己可以提交。  

- **注意**：在GitHub上免费托管的仓库是公开的，但只有自己能够修改。如果想自己雪藏仓库，可以成为GitHub的付费用户，享受私人仓库；或者自己建立一个Git服务器。  

---
## [添加远程库](https://www.liaoxuefeng.com/wiki/896043488029600/898732864121440)
1. 建立远程库  
   在GitHub上创建一个新的repo(自己找吧！)，然后给仓库起个名字，比如我的是`Learning-Git`。其他保持默认，创建仓库即可。
   现在这个仓库是空的，我们可以从这个仓库克隆出新仓库，也可以把一个已有的本地仓库与之关联，然后把本地仓库的内容推送到GitHub仓库。  
2. 关联远程库  
   在Git Bash中输入指令`git remote add origin git@github.com:Lucca9102/Learning-Git`，把仓库关联到GitHub远程仓库。添加后，远程库就叫`origin`。  
3. 把本地内容推送到远程  
   使用`git push`指令，实际上就是把当前的分支`master`推送到远程。  
   第一次推送时，远程库是空的。使用使用`-u`参数，即`git push -u origin master`。这样Git不但会把本地的`master`分支内容推送到远程新的`master`分支，还会把本地的`master`分支和远程`master`分支关联起来。在以后的推送或者拉取时就可以简化指令，使用`git push origin master`即可。  
     
   第一次使用Git的`clone`或`push`指令连接GitHub时，会得到警告。警告大意就是要确认GitHub的Key的指纹信息是否真的来自GitHub的服务器。如果不放心可以和[GitHub的RSA Key的指纹信息](https://docs.github.com/en/github/authenticating-to-github/githubs-ssh-key-fingerprints)对照一下，然后输入`yes`回车即可。之后GitHub的Key就会被添加到信任列表，不会再有警告了。  
   ![warning_while_cloning](images/remote_repo/warning_while_cloning.png)  
   ![github_ssh](images/remote_repo/github_ssh.png)  

---
## [从远程库克隆](https://www.liaoxuefeng.com/wiki/896043488029600/898732792973664)
在想要克隆远程库的目录下打开Git Bash，有多种方法可以克隆仓库。下面根据其他同学(?)的笔记介绍两种方法：  
1. git(SSH协议) -> 默认，最快  
   `git clone git@github.com:lucca9102/Learning-Git.git`
2. https -> 慢，每次都要输口令；不支持https就不能用  
   `git clone https://github.com/lucca9102/Learning-Git.git`

克隆成功后效果如图：  
![clone_succeeded1](images/remote_repo/clone_succeeded1.png)  
![clone_succeeded2](images/remote_repo/clone_succeeded2.png)  

---
---
# [分支管理](https://www.liaoxuefeng.com/wiki/896043488029600/896954848507552)
以我之前小学期做的五子棋游戏为例。程序主要实现的功能有计时、游戏和聊天三项。假设这三项分别分给了两个人做，A已经做好了游戏的部分，而计时做了一半；B的聊天部分出了小bug，会影响游戏进行。这时如果一次性把功能合并在一起，程序的任一部分都没法正常运行。  
这时，为了三个功能互不影响地继续开发，B创建了一个属于自己的分支。A看不到这个分支，还在原来的分支上正常工作。B在自己的分支上工作，开发完毕后，再一次性合并到原来的分支上。这样既安全，又不影响A工作。  
在这种情形下，又体现出了Git相较SVN等的优势：创建、切换和删除分支非常快，远远超过了SVN等。  

---
## [创建与合并分支](https://www.liaoxuefeng.com/wiki/896043488029600/900003767775424)
每次我们提交，Git都会把他们串成一条时间线，这条时间线就是一个分支。按照上面的步骤操作下来，我们目前只有一条时间线，也就是我们的主分支`master`。  
开始时，`master`分支是一条线，<u>Git用`master`指向最新的提交，再用`HEAD`指向`master`</u>。每次提交，`master`分支都会向前移动一步。  
![HEAD_master](images/branch/HEAD_master.png)  
当我们创建新的分支，例如`dev`，Git就会新建一个指针`dev`，指向和`master`相同的提交，再把`HEAD`指向`dev`。这样就表示了当前分支在`dev`上。这个过程中，Git只需增加一个指针，并改变`HEAD`的指向，无需修改工作区的文件。  
![HEAD_dev](images/branch/HEAD_dev.png)  
从现在开始，每次提交后，`dev`指针会向前移动，而`master`指针不会改变。  
![dev_commit](images/branch/dev_commit.png)  
当完成了`dev`分支上的工作后，我们就可以把`dev`合并到`master`上。最简单的合并方法就是像当初创建分支时一样，直接把`master`指向`dev`的当前提交，就完成了合并。  
![merge](images/branch/merge.png)  
完成合并后，我们就可以<s>过河拆桥，卸磨杀驴，兔死狗烹，鸟尽弓藏，</s>删除掉`dev`分支，也就是删掉`dev`指针，只留下`master`一条分支。  
![del_dev](images/branch/del_dev.png)  
总结一下，大致步骤就是：
1. 创建分支
   使用`git checkout -b dev`指令，`-b`参数表示创建并切换分支。这条指令也就相当于以下两条指令：  
   ```
   $ git branch dev
   $ git checkout dev
   ```  
   创建后，可以用`git branch`查看所有分支。当前分支，也就是`dev`分支会以绿色显示，并在前面加上<kbd>`*`</kbd>。  
   ![create_dev](images/branch/create_dev.png)  
   这里的`git checkout [branch-name]`命令与前面的`git checkout -- [file]`很相近，容易混淆。所以新版本的Git提供了 ***`switch`*** 命令。使用方法如下：
   - 创建并切换到新的`dev`分支：`git switch -c dev`  
   - 切换到已有的`master`分支：`git switch master`  
   
   \* 由ProGit，`checkout`的意思是“检出”

2. 修改并提交到`dev`，方法与在`master`上提交相同。  
   ![dev_commit2](images/branch/dev_commit2.png)  

3. 合并分支  
   `dev`上的工作完成后，就可以合并分支了。  
   1. 切换到`master`分支：`git checkout master`。
   2. 把`dev`分支的工作成果合并到`master`分支：`git merge dev`。这里的`git merge`指令用于合并指定分支到当前分支。  
      合并后，Git会显示`Fast-forward`，也就是说本次合并是“快进模式”，是直接把`master`指向`dev`。不过并不是每次合并都能快进⏩，后面会学习其他合并方式。  
    
    ![Fast-forward](images/branch/Fast-forward.png)  

4. 删除分支  
   使用`git branch -d dev`删除`dev`分支，和它说再见。  
   ![del_dev2](images/branch/del_dev2.png)  

---
## [解决冲突](https://www.liaoxuefeng.com/wiki/896043488029600/900004111093344)
1. 首先准备一个新的分支`feature1`。   
   ```
   $ git switch -c feature1  
   Switched to a new branch 'feature1'
   ```
2. 在`feature1`做出修改并提交
   ```
   $ git commit -am "test commit on feature1"
   [feature1 a990895] test commit on feature1
   1 file changed, 12 insertions(+), 2 deletions(-)
   ```
3. 切换回主分支`master`  
   ```
   $ git switch master
   Switched to branch 'master'
   Your branch is up to date with 'origin/master'.
   ```  
   （如果有提交没有被推送到远程仓库，就会出现下面的提醒，不会影响实验效果）  
   ```
   $ git switch master
   Switched to branch 'master'
   Your branch is ahead of 'origin/master' by 1 commit.
     (use "git push" to publish your local commits)
   ```  
4. 在`master`做出修改并提交  
   现在分支状态如下图：
   ![drawfeature1](images/branch/drawfeature1.png)
5. 使用`git merge feature1`合并两个分支。这时可以看到：  
   ![merging](images/branch/merging.png)  
   就是说两个分支的内容有冲突，需要手动解决后才能提交。  
   此时查看`git status`：  
   ![status_while_merging](images/branch/status_while_merging.png)  
   *此时`master`处于`unmerged`状态，是无法使用`checkout`等命令的*  
  
   此时查看冲突的文件，可以发现Git用`<<<<<<< HEAD`标记了当前分支的更改；用`>>>>>>> [branch-name]`标记冲突分支的更改；用`=======`分隔冲突的内容。大致如下：  
   ```
   (不冲突的内容...)

   <<<<<<< HEAD
   (当前分支的修改...)
   =======
   (传入分支的修改...)
   >>>>>>> [branch-name]
   ```
   ![merge_when_there_are_conflicts](images/branch/merge_when_there_are_conflicts.png)  

6. 手动处理冲突，并再次提交，这样就完成了一次有冲突的合并  
   ![drawmerge](images/branch/drawmerge.png)
7. \* 删除`feature1`分支。

做完以上实验后，可以使用`git log --graph`命令查看分支的合并情况：  
![git_log_graph](images/branch/git_log_graph.png)  
*其中`--abbrev-commit`是将版本号缩写的意思。更多参数含义可以参考[git 使用详解（5）-- get log 查看提交历史](https://blog.csdn.net/wh_19910525/article/details/7468549)*  
  
在合并分支后，`master`和`feature1`的`commit`记录会按时间顺序被记录在`master`的`log`里：
![log_after_merging](images/branch/log_after_merging.png)  

---
## [分支管理策略](https://www.liaoxuefeng.com/wiki/896043488029600/900005860592480)
合并分支时，如果可能，Git会使用`Fast forward`模式。但是这种模式下，删除分支后，会丢掉分支信息。  
如果要禁用`Fast forward`模式，Git就会在合并时生成一个新的提交，这样就可以从分支历史上看出分支信息。  
下面来实验：
1. 创建分支`dev`
2. 修改并添加提交
3. **合并**  
   指令：`git merge --no-ff -m "content" [branch-name]`  
   这里的`--no-ff`就是不要`Fast-Forward`的意思。  
   因为会创建一个新的commit，所以这里还使用参数`-m`，写入commit描述。  
   ![merge_noff](images/branch/merge_noff.png)  
4. 删除`dev`分支

这时查看`git log`，发现删除分支后仍然可以看到分支的提交记录，只是分支名不再出现。  
![merge_noff_log](images/branch/merge_noff_log.png)  

**分支策略**  
在实际开发中，我们应该按照几个基本原则进行分支管理：  
1. `master`分支应该是非常稳定的，仅用来发布新版本，平时不要在上面干活；  
2. 要干活就开一个`dev`分支，`dev`分支是不稳定的。等到稳定的时候，比如到了版本1.0的时候，把`dev`分支合并到`master`分支上，在`master`分支上发布1.0版本；  
3. 每个人都整个自己的分支，时不时往`dev`上合并一部分就行。  

所以团队合作看起来就是这样：  
![branch_strategy](images/branch/branch_strategy.png)  

---
## [Bug分支](https://www.liaoxuefeng.com/wiki/896043488029600/900388704535136)
> <s>在bug开发中，软件出现就像家常便饭。</s>遇到bug时，我们可以快乐建分支，修复bug，然后再合并分支，删除临时分支。  

**但是**，天不遂人愿。当我们得到修复bug的任务时，我们在当前分支的任务很可能还没有完成，而我又不想提交。  
**幸好**，Git提供了`stash`功能，可以把当前的工作现场“储藏”起来，等以后恢复现场后继续工作。  
举个例子，现在我要完善我的命令总结文件，但是在当前`dev`分支上的笔记文件的编辑还没有完成。  
所以我：魔法カード発動！Stashしろ！　　
```
$ git stash
Saved working directory and index state WIP on dev: d03e5fa Updated instructions.md
```  
这样工作区已保存但没添加到版本库的部分就消失了。查看`git status`，可以看到`working tree clean`了。  
现在我切换到`instructions`分支完善我的命令总结。  
完成后返回`dev`分支，首先用`git stash list`看一下我们的stash列表：
```
$ git stash list
stash@{0}: WIP on dev: d03e5fa Updated instructions.md
```
列表中有一个存储内容。  
现在把这部分内容恢复到工作区，有两种方法：
1. `git stash apply`，恢复内容，但不删除stash list中的内容；如果不需要了，就使用`git stash drop`清除  
   ```
   $ git stash apply
   On branch dev
   Changes not staged for commit:
     (use "git add <file>..." to update what will be committed)
     (use "git restore <file>..." to discard changes in working directory)
           modified:   gitNote.md
           modified:   images/branch/merge_noff_log.png
   
   no changes added to commit (use "git add" and/or "git commit -a")
   
   $ git stash drop
   Dropped refs/stash@{0} (65566755d869f90f9862894ab1b44e3e3a7c49c2)
   ```
   这时再`git stash list`就看不到任何内容了

2. `git stash pop`，一步到位，直接取出内容并删除stash  
   ```
   $ git stash pop
   On branch dev
   Changes not staged for commit:
     (use "git add <file>..." to update what will be committed)
     (use "git restore <file>..." to discard changes in working directory)
           modified:   gitNote.md
           modified:   images/branch/merge_noff_log.png
   
   no changes added to commit (use "git add" and/or "git commit -a")
   Dropped refs/stash@{0} (8c5d4cd4d44cc5262ab1e5684945061dfb83f13d)
   ```

完成以上步骤后，我想把`dev`上更新的笔记同步到`instructions`上(或把`instructions`上的命令总结同步到`dev`上)。针对这种情况，Git提供了`git cherry-pick [commit]`命令，这个命令能够把*一个特定的提交*复制到当前分支。  
```
$ git cherry-pick 49e90de
[instructions 8552e23] Test cherry-pick.
 Date: Thu Feb 11 12:18:40 2021 +0800
 2 files changed, 53 insertions(+), 1 deletion(-)
 rewrite images/branch/merge_noff_log.png (99%)
```
需要注意的是，这里要复制的版本号是第一行的`49e90de...`，而复制到分支`instructions`上的则是`8552e23...`。也就是说这两个commit的改动相同，但是它们是两个不同的commit。

再举一个栗子帮助理解：  
我在命令总结里发现了错别字，想要改正它，需要以下步骤：
1. 保存当前工作区的工作  
   ```
   git stash
   Saved working directory and index state WIP on dev: 49e90de Test cherry-pick.
   ```
2. 切换分支  
   ```
   $ git switch instructions
   Switched to branch 'instructions'
   ```
3. 建立Bug分支`fix-typo`并切换  
   ```
   $ git switch -c "fix-typo"
   Switched to a new branch 'fix-typo'
   ```
4. 修改错别字，提交  
   ```
   $ git commit -am "Update instructions.md"
   [fix-typo 39a3945] Update instructions.md
    1 file changed, 16 insertions(+), 4 deletions(-)
   ```
5. 切换回`instructions`分支，合并`fix-typo`，删除`fix-typo`  
   ```
   $ git switch instructions
   Switched to branch 'instructions'

   $ git merge fix-typo
   Updating 8552e23..39a3945
   Fast-forward
    instructions.md | 20 ++++++++++++++++----
    1 file changed, 16 insertions(+), 4 deletions(-)
   
   $ git branch -d fix-typo
   Deleted branch fix-typo (was 39a3945).
   ```
6. 获得版本号，切换回`dev`，将*改正错别字的这次提交*复制到`dev`上  
   ```
   $ git log --pretty=oneline --abbrev-commit
   39a3945 (HEAD -> instructions) Update instructions.md

   $ git switch dev
   Switched to branch 'dev'

   $ git cherry-pick 39a3945
   [dev 0e01e11] Update instructions.md
    Date: Thu Feb 11 14:17:39 2021 +0800
    1 file changed, 16 insertions(+), 4 deletions(-)
   ```

7. 恢复工作区，继续工作  
   ```
   $ git stash pop
   On branch dev
   Changes not staged for commit:
     (use "git add <file>..." to update what will be committed)
     (use "git restore <file>..." to discard changes in working directory)
           modified:   gitNote.md
   ```

总结一下使用`stash`过程中的发现：  
1. stash存储的方式类似栈，每次`stash`后，最后存入的内容标号为`stash@{0}`。取出或删除时默认的stash也是`stash@{0}`  
2. stash的存取时的分支不需要一致，可以在一个分支`stash`，在好几个分支`apply`
3. 假设在分支`test`进行了`stash`操作，切换回其他分支并删除`test`后，存入的`stash`仍然存在，并且在`stash list`中查看时仍然会显示`test`的分支名

---
## [Feature分支](https://www.liaoxuefeng.com/wiki/896043488029600/900394246995648)（强制删除分支）
软件开发中，总要添加新的功能。  
但是我们不想让尚处于实验阶段的新功能代码搞乱了主分支。所以在添加新功能时，最好新建一个feature分支，在上面开发，合并，最后删除该feature分支。  
**但是**，假设这时接到指示，要取消开发并删除这些内容。如果已经提交过，使用`git branch -d [branch-name]`时会失败并报错：
```
$ git branch -d form
error: The branch 'form' is not fully merged.
If you are sure you want to delete it, run 'git branch -D form'.
```
所以要使用`git branch -D [branch-name]`强制删除：
```
$ git branch -D form
Deleted branch form (was 01e282d).
```

总结一下尝试删除分支时的发现：  
1. 如果没提交就切换分支，则修改会被保留（包括工作区和暂存区的修改），即使删除做出修改的分支后也不会消失  
2. 如果提交了修改，之后切换分支，文件会回到目标分支的状态。删除做出修改的分支后，修改会丢失  
3. 如果在新分支新建了文件，并做出了提交，则切换分支时文件会在工作区消失；删除分支时文件似乎确凿也就消失了  
4. 在`test`分支上时不能删除`test`分支，就像不能靠左脚踩右脚的方式起飞  
5. 只有分支上有提交，但没有merge，也没有推送到远程仓库的情况下需要强制删除，其他情况下`-d`就可以删除，不过可能出现警告。例如推送到远程后删除，会提示：
   ```
   $ git branch -d test-pull
   warning: deleting branch 'test-pull' that has been merged to
            'refs/remotes/origin/test-pull', but not yet merged to HEAD.
   Deleted branch test-pull (was e4b6208).
   ```

---
## [多人协作](https://www.liaoxuefeng.com/wiki/896043488029600/900375748016320)
我们从远程克隆仓库时，实际上是Git自动把本地的`master`分支和远程的`master`分支对应起来了，并且，远程库的默认名称是`origin`。  
要查看远程库的信息，用`git remote`：  
```
$ git remote
origin
```

或`git remote -v`显示更详细的信息：
```
$ git remote -v
origin  git@github.com:Lucca9102/Learning-Git.git (fetch)
origin  git@github.com:Lucca9102/Learning-Git.git (push)
```

上面显示了可以 **抓取(*fetch*)** 和 **推送(*push*)** 的`origin`地址。如果没有推送权限，就看不到push地址。

### 推送分支
推送分支就是把该分支上所有的本地提交推送到远程库。推送时要指定本地分支（如`master`）。这样Git就会把该分支推送到远程库对应的远程分支上。  
当然，并不是所有的分支都需要推送到远程库。如果需要协同工作，就需要推送上去；自己就能改的bug分支什么的，放在本地就行。 

### 抓取分支
假如我的小伙伴要和我一起工作，那他就需要先clone我的远程仓库。默认情况下，克隆下来的只有`master`分支。如果想在`dev`分支上进行工作，就需要从远程获取`dev`分支：  
1. `git switch -c dev origin/dev`
2. `git checkout -b dev origin/dev`
3. `git branch dev origin/dev`
4. (本地没有`dev`分支并且远程分支名为`dev`时)`git branch/switch/checkout dev`

*用以上方法获取的分支会自动跟踪远程分支*

现在，我的小伙伴就可以在`dev`上工作并快乐`push`了。

然而好景不长，有一天我的小伙伴向`origin/dev`推送了他的提交，而我也对同样的文件做出了修改。这时我想推送：  
![push_failed](images/branch/push_failed.png)  

这时就需要`git pull`，把最新的版本拉取到本地。这时Git会显示两个版本的冲突，和[解决冲突](#解决冲突)部分的操作完全相同。解决冲突后，再提交，最后push到远程仓库即可。成功后远程仓库也会保留两个有冲突的commit，以及最后合并成的commit。  
*个人理解就是把一个人的merge冲突变成了多个人的*

提到`pull`，假如要pull `dev`分支，当处于：
1. `dev`是在本地创建的，此前没有将其链接到远程的`dev`  
2. 本地没有`dev`分支  

两种状态时，会pull失败：
```
$ git pull
There is no tracking information for the current branch.
Please specify which branch you want to merge with.
See git-pull(1) for details.

    git pull <remote> <branch>

If you wish to set tracking information for this branch you can do so with:

    git branch --set-upstream-to=origin/<branch> dev
```
这时要建立本地`dev`分支和`origin/dev`分支的链接，按照提示操作即可：  
```
$ git branch --set-upstream-to=origin/test-pull test-pull
Branch 'test-pull' set up to track remote branch 'test-pull' from 'origin'.
```
之后再pull就可以了。  

补充：  
这里的`$ git branch --set-upstream-to`或`$ git branch -u origin/dev`命令作用就是为本地分支设置上游分支，即令本地分支跟踪选中的远程分支。  
设置好跟踪分支后，可以通过简写`@{upstream}`或`@{u}`来引用它的上游分支。比如我现在处在`dev`分支，并且它正在跟踪`origin/dev`分支，如果愿意可以使用`git merge @{u}`来代替`git merge origin/dev`。  

总结一下多人合作的过程：
1. 创建原始仓库并推送到远程仓库
2. 小伙伴们克隆仓库并开始工作  
   1. 没有冲突，各种push自己的
   2. 有冲突：  
      1. pull下来最新的commit
      2. 解决冲突
      3. commit, push

可能遇到的问题：  
1. clone下来只有主分支`master`  
   - `git (branch / switch -c / checkout -b) [branch-name] origin/[branch-name]`  
2. 不能pull  
   - `git branch --set-upstream-to=origin/[branch-name] [branch-name]`  

这里根据ProGit补充一些内容：
1. 删除远程分支：`$ git push --delete [branch-name]`  
2. 要给给定的远程仓库同步数据，可以用`git fetch <remote>`命令。这个命令查找`<remote>`(如`origin`)是哪个服务器，从中抓取本地没有的数据，并且更新本地数据库，移动`origin/master`指针到更新之后的位置。  
   `fetch`命令并不会修改工作目录中的内容，指挥获取数据然后让用户自己合并。而`pull`命令则相当于`fetch`后再`merge`。

## [Rebase](https://git-scm.com/book/zh/v2/Git-%E5%88%86%E6%94%AF-%E5%8F%98%E5%9F%BA)
*本节笔记是学习[Git官方教程 **ProGit**](https://git-scm.com/book/zh/v2)所做的*  
> 在Git 中整合来自不同分支的修改主要有两种方法：`merge`和`rebase`。

### 变基的基本操作
假如在`master`分支的某处，开发任务分叉到两个不同的分支，又各自提交了更新。  
![simple_divergent_history](images/branch/simple_divergent_history.png)  
整合分支最容易的方法是`merge`命令。它会把两个分支的最新快照（*也就是前面一直提到的**提交***，这里是`C3`和`C4`）以及二者最近的共同祖先（分支前的提交，`C2`）进行第三方合并，合并的结果是生成一个新的快照并提交。  
其实还有另一种方法：可以提取图中`C4`中引入的补丁和修改，然后再`C3`的基础上应用一次。这种操作就叫做**变基 (rebase)**。可以用`rebase`命令将提交到某一分支上的所有修改都移至另一分支上，就像“重新播放”一样。  
*我的理解是，变基的操作类似于`cherry-pick`后再整合，不记得跳到[Bug分支](#bug分支)看一下。*  
举例说明：
我创建了`test1`和`test2`两个测试分支，在两个分支下分别建立了文件test1.txt和test2.txt，之后分别以"test1"和"test2"做出提交。<font color=red><b>test2先提交，test1后提交</b></font>。  
这时我在`test2`上使用`git rebase test1`：  
```
# 把test1变基到test2上
$ git rebase test2
Successfully rebased and updated refs/heads/test1.

$ git log --oneline -2
1145418 (HEAD -> test1) test1
2ff0606 (test2) test2
```
类似地，在`test1`上使用`git rebase test2`：
```
$ git rebase test1
Successfully rebased and updated refs/heads/test2.

$ git log --oneline -2
1145418 (HEAD -> test2, test1) test1
2ff0606 test2
```
如果做出更多提交，Git也会像上面一样，按照时间顺序整理提交成一条直线。在`log --graph`中查看时也只显示一条直线。  
如果rebase时两条分支上有冲突，也会像merge有冲突时一样需要手动修改

\* 在我看来，rebase和merge两种操作只是对时间线的处理不同。ProGit中给出的原则是：  
> 总的原则是，只对尚未推送或分享给别人的本地修改执行变基操作清理历史，从不对已推送至别处的提交执行变基操作，这样，你才能享受到两种方式带来的便利。  

目前来讲，我更倾向于merge，因为我更喜欢完整的提交历史。并且我对Git的需求仅限于图一乐顺便记一下代码笔记。所以现在我打算先搁置rebase，继续学习后面的内容。等我有需求的时候会回来补笔记的\_(:3 j∠)_   
<font size="1">*也许吧*</font>

---
---
# [打标签](https://git-scm.com/book/zh/v2/Git-%E5%9F%BA%E7%A1%80-%E6%89%93%E6%A0%87%E7%AD%BE)
刻舟求剑听过没？标签就是剑🗡，commit就是舟（雾）  
说正经的，标签和commit id的关系，就像python字典中的键和值，或者域名和IP的关系。比如标签(tag)是v0.8，肯定要比版本号`1b9ed980491f1b6c5b9c9e38025ea8ff3be302ce`好记也好查得多。

---
## 列出标签
在Git中列出标签只需使用`$ git tag`即可。指令默认列出所有标签；如果要按照通配符检索，则必须使用`-l`或`--list`选项。例如`git tag -l "v1.8.5*"`，会检出所有以`"v1.8.5"`开头的标签。

---
## 创建标签
Git支持两种标签：**轻量标签(lightweight)** 和 **附注标签(annotated)**。  
> 轻量标签很像一个不会改变的分支——它只是某个特定提交的引用。  
> 而附注标签是存储在Git数据库中的一个完整的对象。它们是可以被校验的。其中包含打标签者的名字、电子邮件地址、日期时间，此外还有一个标签信息，并且可以使用GNU Privacy Guard (GPG) 签名并验证。通常会建议创建附注标签，这样你可以拥有以上所有的信息。但是如果你只是想用一个临时的标签， 或者因为某些原因不想要保存这些信息，那么也可以用轻量标签。

---
## 轻量标签
轻量标签本质上是将提交校验和存储到一个文件中——没有保存任何其他信息。  
创建轻量标签只需要提供标签名(其实也不可以使用`-a`等选项)：
```
$ git tag v0.8

$ git tag
v0.8

$ git show v0.8
commit 1b9ed980491f1b6c5b9c9e38025ea8ff3be302ce (HEAD -> dev, tag: v0.8, origin/dev)
Author: Lucca9102 <luccachina@163.com>
Date:   Fri Feb 12 20:50:29 2021 +0800

    probably finished learning rebase...

# 下面还会显示这次提交时做出的修改，不贴了
```
可以看到，使用`show`命令时，不会出现额外的标签信息，只会显示提交信息。标签默认会创建在最新的一次提交上。

---
## 附注标签
创建附注标签只需使用`git tag -a <tag> -m "<message>"`：
```
$ git tag -a v0.8 -m "finish learning chapter branch"

$ git show v0.8
tag v0.8  -> in yellow :-)
Tagger: Lucca9102 <luccachina@163.com>
Date:   Fri Feb 12 22:03:55 2021 +0800

finish learning chapter branch

commit 1b9ed980491f1b6c5b9c9e38025ea8ff3be302ce (HEAD -> dev, tag: v0.8, origin/dev)
Author: Lucca9102 <luccachina@163.com>
Date:   Fri Feb 12 20:50:29 2021 +0800

    probably finished learning rebase...

# 下面也会显示这次提交时做出的修改，不贴了
```
这时查看标签信息会出现打标签者的信息、打标签的日期、附注信息，然后显示具体的提交信息。  
如果创建时只使用`-a`，则会弹出文件提示编辑tag描述；编辑，保存并关闭文件后会生成标签（如果描述为空则会创建失败）。

---
## 后期打标签
也可以对过去的提交打标签。先在提交历史里面找一个喜欢的commit。  
这里我选的是：
```
3fba2fb Made lots of changes.
```
现在我给它打上标签`v0.5`：
```
$ git tag -a v0.5 -m "..." 3fba2fb
```
也就是在之前命令的末尾加上版本号即可。  

---
## 共享标签
默认情况下，push时不会传送标签到远程仓库服务器上。在创建完标签后，必须显式地推送标签到共享服务器上。这个过程就像共享远程分支一样——可以运行`git push origin <tagname>`；如果想要一次性推送很多标签，也可以使用`git push origin --tags`，这会把所有不再远程仓库服务器上的标签全部传送到那里。  
把标签推送到远程后，当别人从远程仓库克隆或拉取时，他们也能得到标签。  
提醒一下，`--tags`选项不会区分轻量标签或附注标签，而会把所有标签一起推送。并没有简单的选项能够只推送一种标签。

---
## 删除标签
1. 删除本地标签
   ```
   $ git tag -d v0.8
   Deleted tag 'v0.8' (was bd51835)
   ```
   上述命令并不会删除远程标签

2. 删除远程标签
   1. `git push <remote> :refs/tags/<tagname>`
      这个操作的含义是，将冒号前面的空值推送到远程签名，从而高效地删除它
      ```
      $ git push origin :refs/tags/v0.8
      To github.com:Lucca9102/Learning-Git.git
      - [deleted]         v0.8
      ```
      ! 不要手贱尝试在冒号前后加奇怪的东西。在冒号前加其他名字并不能代替远程标签名；比如`git push <remote> test:refs/tags/<tagname>`，如果本地有`test`分支的话还会在远程建立一个对应`test`的，名叫`refs/tags/<tagname>`的奇怪分支...
   2. `git push <remote> --delete <tagname>`
      字面意思，删除标签
      ```
      $ git push origin --delete v0.75
      To github.com:Lucca9102/Learning-Git.git
       - [deleted]         v0.75
      ```

---
## 检出标签
如果像要查看某个标签所指向的文本文件，可以使用`git checkout`命令。这会是仓库处于“分离指针头（detached HEAD）”状态。这个状态有些不好的副作用：  
在这种状态下，如果做了某些更改然后提交它们，标签不会发生任何变化，但这次新提交将不属于任何分支，并且将无法访问，除非通过确切的提交哈希才能访问。  
因此，如果要做出更改，比如要修复旧版本中的错误，那么通常需要创建一个新分支，并在这个分支上进行改动。(详见官方教程<u>[Git - 打标签](https://git-scm.com/book/zh/v2/Git-%E5%9F%BA%E7%A1%80-%E6%89%93%E6%A0%87%E7%AD%BE))</u>

---
---
# [使用GitHub](https://www.liaoxuefeng.com/wiki/896043488029600/900937935629664)
GitHub不仅可以托管自己的项目，也可以参与别人的项目。  
如果想参与到别人的项目中，可以在对方的主页点击Fork，把项目克隆到自己的GitHub，然后克隆到本地，就可以在上面工作了。  
如果修复了项目的bug，或新增了功能，可以给原作者提交pull request。

---
---
# [使用Gitee](https://www.liaoxuefeng.com/wiki/896043488029600/1163625339727712)
*<s>马云 </s>[码云 Gitee](https://gitee.com)*  
看来一下，和GitHub差不多。基本操作按照GitHub来就可以。  
之前我们的远程仓库一直使用`origin`的名字。其实这是个默认名字，换成别的也行，比如`git remote add github git@github.com:lucca9102/learn_git.git`也是可以的。  
想要添加多个远程库，多次`remote add`就可以了；也可以给一个远程仓库别名（比如`origin`）添加多个url，使用`git remote set-url --add origin ...`即可。  
想要重命名远程仓库的话：
1. 删除关联的远程仓库，使用`git remote rm <remote>`，之后重新添加  
2. `git remote rename oldname newname`  

---
---
# [自定义Git](https://www.liaoxuefeng.com/wiki/896043488029600/900785521032192)
Git除了用户名和邮箱后还有很多可以配置的内容。比如`git config --global color.ui true`会让Git适当地<s>给我点颜色看看，</s>在一些指令中显示不同颜色的字体。  

---
## [忽略特殊文件](https://www.liaoxuefeng.com/wiki/896043488029600/900004590234208)
创建`.gitignore`文件，在里面添加要忽略的文件或目录。比如`temp/`或`*.sh`等。在文件中，`#`开头的行会被任务是注释；`!`开头的则被认为是取反（即不忽略）。  
`.gitignore`中规定的文件不会被添加到版本库。如果一定要加，可以使用`-f`强行加入。不过更好的选择是修改`.gitignore`文件。  

补充一些规则：  
- 以斜杠 `/` 开头表示目录；  
- 以星号 `*` 通配多个字符；  
- 以问号 `?` 通配单个字符；  
- 以方括号 `[]` 包含单个字符的匹配列表（例如`*.py[cod]`）；  
- 以叹号 `!` 表示不忽略(跟踪)匹配到的文件或目录；  
- 此外，Git对于 `.gitignore` 配置文件是按行从上到下进行规则匹配的，意味着如果前面的规则匹配的范围更大，则后面的规则将不会生效

---
## [配置别名](https://www.liaoxuefeng.com/wiki/896043488029600/898732837407424)
每次输入`git branch`是一个麻烦的事情。我们可以给它起个别名，比如`git br`什么的。这时只需`git config --global alias.br branch`即可。  
`--global`是全局参数，配置后这些别名在本台机器上的所有仓库都适用。如果不加，则只对当前仓库有用。  
这种别名并不只适用于单个指令，我们甚至可以
```
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
```
这样XD  

在配置完成后，当前仓库的配置会存在`.git/config`文件中；而当前用户的配置存在用户主目录的`.gitconfig`文件中。如果想修改可以打开文件修改。

---
## [搭建Git服务器](https://www.liaoxuefeng.com/wiki/896043488029600/899998870925664)
首先需要一台运行Linux的机器，我没有，告辞  
\_(:3 j ∠)_

---
---
# [使用SourceTree](https://www.liaoxuefeng.com/wiki/896043488029600/1317161920364578)
我用着不顺手，但是界面很好看XD，有中文，而且分支很清楚  
我个人比较喜欢GitHub Desktop