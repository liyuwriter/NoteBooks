GIT笔记

一、GIT是什么？

​	GIT是一个分布式版本控制软件。

二、GIT的安装：

​	Linux安装：

1. yum源安装：

   ```shell
   yum info git # 查看git版本
   yum install git # 安装git
   ```

2. 源码安装：

   > 本环境发行版为：CentOS 8.2.2004   
   >
   > 内核：Kernel4.18
   >
   > GIT版本: 2.27

   ```shell
   yum install dh-autoreconf curl-devel expat-devel gettext-devel openssl-devel perl-devel zlib-devel getopt #安装依赖库
   ln -s /usr/bin/db2x_docbook2texi /usr/bin/docbook2x-texi # 创建软连接
   tar -zxf git-2.2.7.tar.gz  # 解压下载的git软件包
   cd git-2.2.7 # 进入解压文件路径
   make configure # 开始检查编译环境
   ./configure --prefix=/usr  # 配置编译环境
   make all doc info  # 开始编译安装
   sudo make install install-doc install-html install-info
   ```

三、GIT的初始化：

 在使用GIT前，请了解GIT的配置文件，GIT有三个配置文件：

- /etc/gitconfig  (全局用户和仓库通用配置)
- ~/.gitconfig  or  ~/.config/git/config  (当前用户配置,你可以传递 `--global` 选项让 Git 读写此文件，这会对你系统上 **所有** 的仓库生效。)
- 当前使用仓库目录下的.git/config  (当前仓库配置)

  每个配置文件级别会覆盖上一个配置文件：当前仓库目录配置文件 > ~/.gitconfig > /etc/gitconfig

  在安装完成GIT后，首要的任务是配置用户名和Email，这是因为每一次使用`git commit`命令时都会使用到这些信息，它们会写入到你的每一次提交中，且不能更改:

  ```shell
  git config --global  user.name "Rick"
  git config --global  user.email Rick@city.com
  # 使用global则会将所有仓库默认使用此用户名和email，如果想在不同的仓库间使用不同的用户和email，请在具体仓库目录中使用git config 命令设置（不加--global）。
  ```

  可以使用`git config --list`命令查看所有配置，还可以使用`git config <key>`来获取指定的配置信息，如下：

  ```shell
  [root@test git]# git config --list
  user.name=Rick
  user.email=Rick@city.com
  color.ui=auto
  core.repositoryformatversion=0
  core.filemode=true
  core.bare=false
  core.logallrefupdates=true
  remote.origin.url=https://github.com/git/git.git
  
  # git config <key>
  [root@test git]# git config user.name
  Rick
  ```

四、GIT基础操作：

  **获取GIT仓库**

  获取GIT仓库有两种方式：

- 初始化本地仓库

- 从其他服务器克隆一个已经存在的仓库

  初始化本地仓库：

  如果你有一个尚未在GIT版本控制的目录，并且想要使用GIT来控制它，那么首先进入该目录，然后对此目录进行GIT初始化：

  ```shell
  cd /root/git-test  # 进入要初始化的目录
  git init  # 初始化此目录，此命令会创建一个.git目录，这个目录中的文件包含此仓库所有必须文件。
  ```

  从其他服务器克隆一个已经存在的仓库，`git clone`命令会把对端服务器上所有的数据都复制出来：

  ```shell
  git clone https://github.com/git/git.git # 克隆git软件仓库，此命令会在当前目录下生成克隆软件的同名目录，并且在此目录中，生成.git文件夹。
  ```

 

 **GIT的三个区**

  ![img](C:\Users\User\Desktop\work_word\word\GIT\git-threedir)

  GIT工具有三个区：

1. working directory
2. stage/index area
3. commit history

  这三个区的有各自的作用与状态：

1. work directory：工作区，是当前git仓库目录所在的路径。
2. stage/index area：缓存区，当使用`git add`命令将文件纳入git跟踪后，便会保存在这里。
3. commit history：提交，当使用`git commit`命令将文件提交后，文件便从缓存区提交到commit history中，此时HEAD指针指向的位置；

  假如在git初始化仓库中新建a.txt和b.txt文件，我们如何将他们纳入到git管理呢？如下：

  ```shell
  cd /home/test  # 进入git仓库目录
  touch a.txt b.txt
  git status # 查看此时文件状态，打印如下：
  On branch master
  No commits yet
  Untracked files:  # 提示我们有两个文件处于untracked状态，可以使用git add 命令将文件纳入到git管理并跟踪
    (use "git add <file>..." to include in what will be committed)
          a.txt
          b.txt
  nothing added to commit but untracked files present (use "git add" to track)
  
  # 使用git add a.txt b.txt 将此工作目录中的文件纳入到git管理，并且提交到缓存区
  git add a.txt b.txt
  git status # 此时再查看文件状态，打印如下：
  On branch master
  No commits yet
  Changes to be committed:  # 提示我们有两个新文件纳入了git管理，且可以使用commit提交
    (use "git rm --cached <file>..." to unstage)
          new file:   a.txt
          new file:   b.txt
  ```

  此时a.txt和b.txt文件均处于git管理状态，且放入了缓存区（在Changes to be committed下面的文件都处于缓存区）。

  如果此时修改处于缓存区的文件会发生什么呢？我们将a.txt文件加入一行：

  ```shell
  echo "Hello,World" > a.txt
  git status # 查看现在文件状态，打印如下：
  On branch master
  No commits yet
  Changes to be committed:
    (use "git rm --cached <file>..." to unstage)
          new file:   a.txt
          new file:   b.txt
          
  Changes not staged for commit: 
    (use "git add <file>..." to update what will be committed)
    (use "git restore <file>..." to discard changes in working directory)
          modified:   a.txt
  ```

  此时，a.txt文件处于`Changes not staged for commit:`标签下。这说明此文件已经被修改，但是还没有放入缓存区，如果要放入缓存区，可以使用`git add`命令。从这点我们就能发现，`git add`是多功能命令，它既可以用来添加新的纳管追踪文件，又可以将已经追踪的文件放入缓存区。现在我们可以将a.txt文件放入缓存区，再查看文件状态：

  ```shell
  git add a.txt
  git status # 查看文件状态打印如下：
  On branch master
  No commits yet
  
  Changes to be committed:
    (use "git rm --cached <file>..." to unstage)
          new file:   a.txt
          new file:   b.txt
  ```

  细心的同学可能已经发现了上面a.txt文件同时出现在**缓存区和非缓存区**，假设我们在修改a.txt文件后，没有使用`git add`命令将文件纳入到缓存区，而是直接使用`git commit`命令提交，此时你会发现增加的"Hello,World"并没有出现，这是因为`git add`命令只是暂存了当前的版本，如果修改后不执行`git add`命令直接`git commit`，则GIT将你最后一次运行`git add`命令时的版本提交上去，也就是后面增加的内容是无效的。所以更改已经在缓存区的文件后，要使用`git add`命令重新把最新的版本缓存起来后在提交。

  例子如下：

  ```shell
  git status # 现在有两个文件在缓存区，我们将b.txt文件加入一行“I'm B”
  On branch master
  No commits yet
  
  Changes to be committed:
    (use "git rm --cached <file>..." to unstage)
          new file:   a.txt
          new file:   b.txt
  
  echo "I'm B" > b.txt
  git status # 查看目前文件状态，打印如下：
  On branch master
  No commits yet
  
  Changes to be committed:
    (use "git rm --cached <file>..." to unstage)
          new file:   a.txt
          new file:   b.txt
  
  Changes not staged for commit:
    (use "git add <file>..." to update what will be committed)
    (use "git restore <file>..." to discard changes in working directory)
          modified:   b.txt
  
  git commit -m "Add I'm B" b.txt # 直接使用commit提交b.txt
  ```

  这时候有些同学可能疑惑，现在b.txt文件已经有我们新增的"I'm B"，为什么会说并没有保存呢？这是因为当前文件是本地的文件，`git commit`提交后，git并不知道b.txt文件里面有内容，我们可以使用`git log`命令查看commit的版本，并使用`git reset --hard` 切换到之前的提交版本中，对命令不熟悉的同学不要惊慌，后面都会有介绍。下面开始这个版本回退吧~

  ```shell
  git log # 查看上次commit提交的hash值，打印如下：
  commit aedf6bffc8ae24441922cf852c9f96d8d6d3009e (HEAD -> master) # 版本号
  Author: yu.li <liyuwriter@163.com>
  Date:   Thu Dec 15 15:46:02 2022 +0800
  
      Add I'm B  # 提交时-m增加的内容也在这里
  
  git reset --hard aedf6
  cat b.txt # 此时并没有增加的内容
  ```



**GIT忽略文件**

  有些在工作区的文件我们可能不想让它被GIT纳管，例如一些编译产生的临时文件等，这时就可以使用`.gitignore`配置文件来控制。

  在目录下创建`.gitignore`文件，如下：

  ```shell
  cat .gitignore
  .gitignore # 屏蔽本身.gitignore文件
  *.[ca] # 屏蔽所有以.c或.a结尾的文件
  ```

  创建两个测试文件x.c和y.a文件，使用`git status`命令查看GIT是否会检查这两个文件：

  ```shell
  touch x.c y.a
  git status  # 此时git并不会检查x.c和y.a文件
  On branch master
  nothing to commit, working tree clean
  ```



**查看已经缓存和未缓存的修改**

  通常使用`git status`命令可以查看文件更改后是否缓存，例如更改b.txt文件。

  ```shell
  echo "add test" >> b.txt
  git status  # 查看状态，此时提示我们b.txt文件被修改，但是没有缓存。 
  On branch master
  Changes not staged for commit:
    (use "git add <file>..." to update what will be committed)
    (use "git restore <file>..." to discard changes in working directory)
          modified:   b.txt
  
  no changes added to commit (use "git add" and/or "git commit -a")
  ```

  假如我们想更详细查看未缓存的文件更新了哪些内容时，可以使用`git diff`命令：

  ```shell
  git diff  # 打印如下：
  diff --git a/b.txt b/b.txt
  index b982ed7..18751db 100644
  --- a/b.txt
  +++ b/b.txt
  @@ -1,2 +1,3 @@
   I'm B
   test
  +add test  # 新增加一行
  ```



**提交更新**

  前面我已经简单的使用过`git commit`命令来提交版本，但是没有具体介绍此命令，下面我们开始介绍GIT中的提交版本。我们先更新b.txt文件，写入“add commit test"，然后使用`git add`命令缓存，最后使用`git commit`命令提交此次更新。

  ```shell
  echo "add commit test" >> b.txt
  git add b.txt
  git commit b.txt
  ```

  此时会弹出如下界面：

![image-20221215170547256](C:\Users\User\Desktop\work_word\word\GIT\image-20221215170547256.png)

  默认注释的内容是最后一次运行`git status`命令时的输出，你可以选择删除这些注释，或保留。

  剩下的事情GIT是让你输入这次更新的内容详情，以便后面版本回退时好让我们知道这次commit更新了哪些东西。输入完成后保存退出即可；

  如果你嫌弃这样每次commit后都要输入提交内容很麻烦，则可以使用`git commit -m "此次更新说明"`命令来简化，如下：

  ```shell
  echo "test 2 commit" >> b.txt
  git add b.txt
  git commit -m "add test 2 commit" b.txt
  git log # 查看所有commit，打印如下：
  
  commit e3a22f650d632934e13e4c9a5d0cad40944a62f3 (HEAD -> master)
  Author: Rick <Rick@city.com>
  Date:   Thu Dec 15 17:16:00 2022 +0800
  
      add test 2 commit
  
  commit f2d289611e1d812a482bad1435fd761c67eca515
  Author: Rick <Rick@city.com>
  Date:   Thu Dec 15 17:05:19 2022 +0800
  
      add test commit
  
  commit a3deb1399d76992442fbfc3def9d5a25e66ec651
  Author: Rick <Rick@city.com>
  Date:   Thu Dec 15 16:08:28 2022 +0800
  
      test
  
  commit aedf6bffc8ae24441922cf852c9f96d8d6d3009e
  Author: Rick <Rick@city.com>
  Date:   Thu Dec 15 15:46:02 2022 +0800
  
      Add I'm B
  ```



**跳过缓存区**

  前面介绍中，我们说如果一个已经被跟踪的文件，修改后没有使用`git add`命令添加到缓存区，直接使用`git commit`命令提交后，则修改的内容不会被记录到git中。缓存区虽然能让我们很详细知道此次提交的细节，但是这样也会显得很繁琐。如果不想将文件添加到缓存区而直接commit提交，则可以使用`git commit -a -m "add new txt"`命令跳过缓存区，直接提交。



**移除文件**

  如果有些文件在工作目中已经`commit`到GIT版本管理中后，不想再使用GIT进行管理的时候，可以使用`rm`命令将其删除后，再使用`git rm`命令删除。

  ```shell
  touch r.txt 
  git add r.txt
  git commit -m "add r.txt" 
  rm -rf r.txt
  git status # 打印如下
  On branch master
  Changes not staged for commit: # 显示有文件未在缓存区，可以使用git add/rm更新commit，或使用git restore恢复文件
    (use "git add/rm <file>..." to update what will be committed)
    (use "git restore <file>..." to discard changes in working directory)
          deleted:    r.txt
  
  git rm r.txt # 删除r.txt文件
  git status # 打印如下：
  On branch master
  Changes to be committed:
    (use "git restore --staged <file>..." to unstage)
          deleted:    r.txt
  
  git commit -m "delete r.txt" # 重新提交
  git status # 打印如下：
  On branch master
  nothing to commit, working tree clean
  ```

  如果有些文件我们已经将它提交到缓存区时，则可以使用`git rm -f`命令将文件进行移除，参数`-f`是强制移除。例如，我们创建一个c.txt文件，把它纳管到git中，然后删除。下一次commit提交时，该文件就不再纳入版本管理了。

  ```shell
  touch c.txt
  git status  # 打印如下：
  On branch master
  Untracked files:
    (use "git add <file>..." to include in what will be committed)
          c.txt
  nothing added to commit but untracked files present (use "git add" to track)
  
  git add c.txt
  git status # 打印如下：
  On branch master
  Changes to be committed:
    (use "git restore --staged <file>..." to unstage)
          new file:   c.txt
  
  git rm -f c.txt
  git status # 打印如下：
  On branch master
  nothing to commit, working tree clean
  ```

  

**移动文件**

  GIT中可以使用`git mv`命令来移动文件，例如我们将b.txt文件重命名为e.txt文件。

  ```shell
  git mv b.txt e.txt
  git status # 打印如下：
  On branch master
  Changes to be committed:
    (use "git restore --staged <file>..." to unstage)
          renamed:    b.txt -> e.txt
  ```

  其实底层GIT的操作是这样的，如果你这样做，GIT也会认为这是一次重命名操作：

  ```shell
  mv b.txt e.txt
  git rm b.txt
  git add e.txt
  ```



**查看提交历史**

  前面我们已经介绍了使用`git log`命令来查看提交的历史，下面我们来仔细的了解这个命令是如何工作的。在不加入任何参数的情况下，这个命令会列出每个提交的SHA-1校验和、作者的名字和Email地址、提交的时间和提交说明。

  ```shell
  git log # 打印历史commit
  commit e2af180575ff8683c2183f88c18d605ac68b66ee (HEAD -> master)
  Author: Rick <Rick@city.com>
  Date:   Thu Dec 15 17:52:56 2022 +0800
  
      delete r.txt
  
  commit 13ddf40f9bfc2da51505b495489f8df8e2e98d7c
  Author: Rick <Rick@city.com>
  Date:   Thu Dec 15 17:51:33 2022 +0800
  
      add r.txt
  
  commit e3a22f650d632934e13e4c9a5d0cad40944a62f3
  Author: Rick <Rick@city.com>
  Date:   Thu Dec 15 17:16:00 2022 +0800
  
      test
  
  commit aedf6bffc8ae24441922cf852c9f96d8d6d3009e
  Author: Rick <Rick@city.com>
  Date:   Thu Dec 15 15:46:02 2022 +0800
  
      Add I'm B
  ```

  如果使用`-p或--patch`，它会显示每次提交的差异。

  ```shell
  git log -p # 查看每次commit的差异
  ...#省略#...
  diff --git a/b.txt b/b.txt
  index 91f8088..b982ed7 100644
  --- a/b.txt
  +++ b/b.txt
  @@ -1 +1,2 @@
   I'm B
  +test
  
  commit aedf6bffc8ae24441922cf852c9f96d8d6d3009e
  Author: Rick <Rick@city.com>
  Date:   Thu Dec 15 15:46:02 2022 +0800
  
      Add I'm B
  
  diff --git a/b.txt b/b.txt
  new file mode 100644
  index 0000000..91f8088
  --- /dev/null
  +++ b/b.txt
  @@ -0,0 +1 @@
  +I'm B
  ```

  或者使用`--stat`参数，来看出每次提交的简略统计信息。

  ```shell
  git log --stat # 打印如下：
  ...#省略#...
   b.txt | 2 ++
   1 file changed, 2 insertions(+)
  
  commit a3deb1399d76992442fbfc3def9d5a25e66ec651
  Author: Rick <Rick@city.com>
  Date:   Thu Dec 15 16:08:28 2022 +0800
  
      test
  
   b.txt | 1 +
   1 file changed, 1 insertion(+)
  
  commit aedf6bffc8ae24441922cf852c9f96d8d6d3009e
  Author: Rick <Rick@city.com>
  Date:   Thu Dec 15 15:46:02 2022 +0800
  
      Add I'm B
  
   b.txt | 1 +
   1 file changed, 1 insertion(+)
  ```



**撤销操作**

  在任何时候，你都可以进行撤销的动作。假如在我们提交完成后发现有几个文件没有添加，或提交信息写错了，此时就可以使用`git commit --amend`命令来进行重新提交。

  `git commit --amend`命令会将暂存区中的文件提交，如果自从上次提交以来你还未更改任何文件，那么你所修改提交的只是提交信息，如果提交后发现忘记暂存某些需要的修改，则可以像下面这样操作：

  ```shell
  git commit -m "test"
  git add fiel.txt
  git commit --amend
  ```



**远程仓库**

  远程仓库是为了能和更多的同学协同工作，使用`git remote`命令查看已经配置的远程仓库。

  ```shell
  # 首先clone远端仓库
  git clone git@github.com:Rick/git.git
  git remote # 查看远端仓库，默认克隆名称为origin
  git remote -v # 显示详细信息，回显如下：
  origin  git@github.com:Rick/git.git (fetch)
  origin  git@github.com:Rick/git.git (push)
  ```

  添加远程仓库，使用`git remote add <shortname> <url>`命令，不指定`<shortname>`时默认为origin。

  ```shell
  git remote add  git@github.com:Rick/git.git 
  git remote add Name_a git@github.com:Rick/git.git 
  ```

  从远程仓库中抓取与拉取文件，使用`git fetch`命令。这个命令会访问远程仓库，从中拉取当前你还没有的数据，执行完成后，你将拥有远程仓库的所有分支。如果你使用了`git clone`命令，则会自动添加远程仓库，并名称默认为`origin`。

  推送到远程仓库，可以使用`git push <remote> <branch>`命令。

  ```shell
  git push origin master # 将本地仓库推送到远端仓库master分支中
  # 这条命令生效的前提是你具有远程仓库的写入权限，且之前没有人推送过master分支，如果有人在你推送之前更新了master分支，则你需要先抓取他的更新后，合并到你的分支后再更新远端master分支
  ```

  查看远端仓库信息可以使用`git remote show <remote>`命令，如下：

  ```shell
  git remote show origin # 打印如下：
  * remote origin
    Fetch URL: https://github.com/git/git.git
    Push  URL: https://github.com/git/git.git
    HEAD branch: master
    Remote branches:
      jch    tracked
      main   tracked
      maint  tracked
      master tracked
      next   tracked
      seen   tracked
      todo   tracked
    Local branch configured for 'git pull':
      master merges with remote master
    Local ref configured for 'git push':
      master pushes to master (up to date)
  ```

  远程仓库的重命名与移除，如果想要修改远程仓库的名称，可以使用`git remote rename <old_name> <new_name>`。

  ```shell
  git remote rename origin test_git
  git remote # 打印如下
  test_git
  ```

  移除远程仓库使用`git remote remove <name>`命令。

  ```shell
  git remote remove test_git
  git remote #无打印
  ```





  

  

























