### 安装git

##### 1.安装

```
yum install -y git
```

#####2.查看版本

```
git --version
```

##### 3.安装所需软件包

```
yum install -y curl-devel expat-devel gettext-devel openssl-devel zlib-devel gcc-c++ perl-ExtUtils-MakeMaker autoconf automake libtool
```

##### 4.下载 & 安装 & 解压

```
cd /usr/src
wget https://www.kernel.org/pub/software/scm/git/git-2.7.3.tar.gz
tar -xvzf git-2.7.3.tar.gz
```

##### 5.配置编译安装

```
cd git-2.7.3
./configure --prefix=/usr/local/app/git ##配置目录
make profix=/usr/local/app/git
make install
```

##### 6.加入环境变量

```
vim /etc/profile
```

##### 7.添加如下配置

```
# Git Config
export GIT_HOME=/usr/local/app/git
export PATH=$GIT_HOME/bin:$PATH
```

##### 8.让配置生效

```
# source /etc/profile
```

##### 9.检查版本

```.
# git --version 
```



### Git 配置

Git 提供了一个叫做 git config 的工具，专门用来配置或读取相应的工作环境变量。

这些环境变量，决定了 Git 在各个环节的具体工作方式和行为。这些变量可以存放在以下三个不同的地方：

- /etc/gitconfig 文件：系统中对所有用户都普遍适用的配置。若使用 git config 时用 --system 选项，读写的就是这个文件。
- ~/.gitconfig 文件：用户目录下的配置文件只适用于该用户。若使用 git config 时用 --global 选项，读写的就是这个文件。
- 当前项目的 Git 目录中的配置文件（也就是工作目录中的 .git/config 文件）：这里的配置仅仅针对当前项目有效。每一个级别的配置都会覆盖上层的相同配置，所以 .git/config 里的配置会覆盖 /etc/gitconfig 中的同名变量。

在 Windows 系统上，Git 会找寻用户主目录下的 .gitconfig 文件。主目录即 `$HOME` 变量指定的目录，一般都是 `C:\Documents and Settings\$USER`

此外，Git 还会尝试找寻 /etc/gitconfig 文件，只不过看当初 Git 装在什么目录，就以此作为根目录来定位。



#### 1.用户信息

配置个人的用户名称和电子邮件地址：

```
git config --global user.name "sll_git"
git config --global user.email "2522908520@qq.com"
```

如果用了 --global 选项，那么更改的配置文件就是位于你用户主目录下的那个，以后你所有的项目都会默认使用这里配置的用户信息。

如果要在某个特定的项目中使用其他名字或者电邮，只要去掉 --global 选项重新配置即可，新的设定保存在当前项目的 .git/config 文件里。

#### 2.文本编辑器

设置Git默认使用的文本编辑器, 一般可能会是 Vi 或者 Vim。如果你有其他偏好，比如 Emacs 的话，可以重新设置：:

```
git config --global core.editor vim
```

#### 3.差异分析工具

还有一个比较常用的是，在解决合并冲突时使用哪种差异分析工具。比如要改用 vimdiff 的话：

```
$ git config --global merge.tool vimdiff
```

Git 可以理解 kdiff3，tkdiff，meld，xxdiff，emerge，vimdiff，gvimdiff，ecmerge，和 opendiff 等合并工具的输出信息。

当然，你也可以指定使用自己开发的工具，具体怎么做可以参阅第七章。

#### 4.查看配置信息

要检查已有的配置信息，可以使用 git config --list 命令：

```
$ git config --list
http.postbuffer=2M
user.name=runoob
user.email=test@runoob.com
```

有时候会看到重复的变量名，那就说明它们来自不同的配置文件（比如 /etc/gitconfig 和 ~/.gitconfig），不过最终 Git 实际采用的是最后一个。

这些配置我们也可以在 ~/.gitconfig 或 /etc/gitconfig 看到，如下所示：

```
vim ~/.gitconfig 
```

显示内容如下所示：

```
[http]
    postBuffer = 2M
[user]
    name = runoob
    email = test@runoob.com
```

也可以直接查阅某个环境变量的设定，只要把特定的名字跟在后面即可，像这样：

```
$ git config user.name
runoob
```

#### 5.生成公钥和私钥

```
// 没有配置用户信息，先配置用户信息
# git config --global user.name "sll_git"
# git config --global user.email "2522908520@qq.com"
# ssh-keygen -t rsa -C "2522908520@qq.com"
Generating public/private rsa key pair.
Enter file in which to save the key (/root/.ssh/id_rsa):   # 输入保存目录，默认 ~/.ssh/id_rsa
/root/.ssh/id_rsa already exists.      # 如果已经存在文件，会提示 是否覆盖
Overwrite (y/n)? y 
Enter passphrase (empty for no passphrase):  # 输入访问该公钥/私钥 的密码，可以为空 (在使用时，会提示输入改密码)
Enter same passphrase again:
Your identification has been saved in /root/.ssh/id_rsa.
Your public key has been saved in /root/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:Cc3R8+oO557jppbl67RgDhuHstaxrZdrddcktS8f5bI vwFifhserAli@qq.com
The key's randomart image is:
+---[RSA 2048]----+
|        ..       |
|       o .o     .|
|      . o  o   ..|
|       . .  . ..o|
|        S  .   =o|
|      ..  + . +.+|
|    ..++=Bo. . =.|
|    .ooBB*=o  E .|
|   .. o=+OXo     |
+----[SHA256]-----+


// 修改 私钥密码
# cd ~/.ssh/
# ssh-keygen -f id_rsa -p
Enter old passphrase:   # 输入旧密码
Enter new passphrase (empty for no passphrase):  ## 输入新密码
Enter same passphrase again:  ## 输入新密码
Your identification has been saved with the new passphrase.
```

#### 6.忽略特殊文件

在 Git 工作目录下，可以创建 .gitignore 文件，来配置不希望被提交的文件

不需要从头写.gitignore文件，GitHub已经为我们准备了各种配置文件，只需要组合一下就可以使用了。所有配置文件可以直接在线浏览：`https://github.com/github/gitignore`

忽略文件的原则是：

- 忽略操作系统自动生成的文件，比如缩略图等；
- 忽略编译生成的中间文件、可执行文件等，也就是如果一个文件是通过另一个文件自动生成的，那自动生成的文件就没必要放进版本库，比如Java编译产生的.class文件；
- 忽略你自己的带有敏感信息的配置文件，比如存放口令的配置文件。

如：

```
.DS_Store

session_data

*.iml
.idea


# Package Files #
*.jar
*.war
*.ear
*.zip
*.tar.gz
*.rar
target

# Compiled class file
*.class

node_modules
build

# Log file
*.log

# BlueJ files
*.ctxt

# Mobile Tools for Java (J2ME)
.mtj.tmp/

# virtual machine crash logs, see http://www.java.com/en/download/help/error_hotspot.xml
hs_err_pid*
```

#### 7.配置别名

配置 git status 简写为 git st

```
git config --global alias.st status
```

--global是针对当前用户起作用的，如果不加，那只针对当前的仓库起作用。

还可以通过在配置文件加入别名配置，在.git/config下

```
$ cat .git/config 
[core]
    repositoryformatversion = 0
    filemode = true
    bare = false
    logallrefupdates = true
    ignorecase = true
    precomposeunicode = true
[remote "origin"]
    url = git@github.com:michaelliao/learngit.git
    fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
    remote = origin
    merge = refs/heads/master
[alias]
    last = log -1
```

推荐别名：

```
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
```



### 搭建 Git 服务器

#### 3.1 CentOS

1. ##### 创建一个 git 用户组和用户，用来运行 git服务：

   ```
   # groupadd git
   # useradd git -g git
   ```

1. ##### 创建证书登录

   收集所有需要登录的用户的公钥，个人公钥位于 ~/.ssh/id_rsa.pub 文件中。

   把这些公钥信息放到 /home/git/.ssh/authorized_keys 文件里，一行一个

   在本机可以用命直接导入：`cat id_rsa.pub >> ～/.ssh/authorized_keys`

   如果没有该文件创建它：

   ```
   # cd /home/git/
   # mkdir .ssh
   # touch .ssh/authorized_keys
   ```

   ##### Git服务器需要RSA认证，然后就可以 根据 authorized_keys 文件里的公钥来验证个人信息了。当然需要将 RSA 认证配置打开

   ```
   vim /etc/ssh/sshd_config
   ```

   ##### 在文件中，找到 AuthorizedKeysFile 配置节点，将下面前2句配置进去 即可

   ```
   RSAAuthentication yes     
   PubkeyAuthentication yes     
   AuthorizedKeysFile  .ssh/authorized_keys
   ```

   ##### 设置 git目录下的 权限

   ```
   # chmod 755 /home
   # chmod 700 /home/git
   # chmod 700 /home/git/.ssh
   # chmod 600 /home/git/.ssh/authorized_keys
   # chown git /home/git
   # chown git /home/git/.ssh
   # chown git /home/git/.ssh/authorized_keys
   ```

1. ##### 初始化Git仓库

   我们 先选定一个目录作为 Git 仓库，并配置 权限。并创建一个 空仓库 project1.git，并且修改 project1.git 权限(注意 要用 -R)

   ```
   # mkdir git_repository
   # chown git:git git_repository
   # cd git_repository
   # git init --bare project1.git
   Initialized empty Git repository in /home/git/git_repository/project1.git/
   # chown -R git:git project1.git
   ```

2. ##### 克隆仓库

   ```
   # git clone git@120.77.47.95:/home/git/git_repository/project1.git
   Cloning into 'project1'...
   The authenticity of host '120.77.47.95 (120.77.47.95)' can't be established.
   ECDSA key fingerprint is SHA256:V/9QGB5qBjUxa2SP5Kzl7LFXbj3+m+wTmBo1IIPYQaE.
   ECDSA key fingerprint is MD5:a2:c3:ba:fb:d1:ea:60:03:5f:71:50:14:0b:26:97:d7.
   Are you sure you want to continue connecting (yes/no)? yes
   Warning: Permanently added '120.77.47.95' (ECDSA) to the list of known hosts.
   Enter passphrase for key '/root/.ssh/id_rsa':   # 输入配置的密码(如果没有密码，则没有该选项)
   ```

3. ##### 可能出现的问题

##### 一、在 git clone 时，可能出现问题：

```
fatal: protocol error: bad line length character: This
```

/etc/passwd 下有个关于 git 的信息配置，注意需要配置为 `[保持不变]::/home/git:/bin/bash`

```
git:x:1000:1000::/home/git:/sbin/nologin

修改为

git:x:1000:1000::/home/git:/bin/bash
```

##### 二、在 push origin master 代码时，出现如下问题：

```
# git push origin master
Enter passphrase for key '/root/.ssh/id_rsa':
Counting objects: 3, done.
Writing objects: 100% (3/3), 203 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
remote: error: insufficient permission for adding an object to repository database ./objects
remote: fatal: failed to write object
error: unpack failed: unpack-objects abnormal exit
To git@120.77.47.95:/home/git/git_repository/project1.git
 ! [remote rejected] master -> master (unpacker error)
error: failed to push some refs to 'git@120.77.47.95:/home/git/git_repository/project1.git'
```

这个是因为权限问题：注意，需要使用如下命令授予权限：`chown -R git:git /home/git/git_repository/project1.git`