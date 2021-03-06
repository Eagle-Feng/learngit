

# Git学习--by[廖雪峰](https://www.liaoxuefeng.com/wiki/896043488029600)

## Tips of Git

* 官方网站[Git](https://git-scm.com/)

* 学习[网站](https://blog.csdn.net/l_215851356/article/details/79063942)

* 简易流程

  > 1. 创建本地仓库
  >
  >    ```
  >    $ mkdir learngit
  >    $ cd learngit
  >    $ pwd
  >    /Users/myname/learngit
  >    ```
  >
  >    ```
  >    $ git init
  >    Initialized empty Git repository in /Users/michael/learngit/.git/
  >    ```
  >
  > 2. 添加文件到缓存区
  >
  >    ```
  >    $ git add readme.txt
  >    $ git add file2.txt file3.txt
  >    ```
  >
  > 3. 提交到本地版本库
  >
  >    ```
  >    $ git commit -m "some comment"
  >    ```
  >
  > 4. 与远程仓库建立连接
  >
  >    创建ssh key
  >
  >    ```
  >    $ ssh-keygen -t rsa -C "youremail@example.com"
  >    ```
  >
  >     将`id_rsa.pub`内容复制远程库（github/gitee）的SSH公钥中
  >
  > 5. 本地库与远程库关联
  >
  >    在远程库中创建与本地库同名的仓库
  >
  >    使用`git remote`命令建立连接（关联GitHub：name=github，关联码云：name=gitee）
  >
  >    ```
  >    $ git remote add name git@server-name:path/repo-name.git
  >    ```
  >
  >    对于使用`git clone`命令从远程库克隆仓库到本地
  >
  >    ```
  >    $ git clone git@github.com:michaelliao/gitskills.git
  >    ```
  >
  >    此时无需使用`git remote`命令建立连接，可以使用`git remote -v`查看`name`
  >
  > 6. 推送本地库到远程库
  >
  >    第一次推送
  >
  >    ```
  >    $ git push -u name master
  >    ```
  >
  >    后续推送
  >
  >    ```
  >    $ git push name master
  >    ```
  >
  >    不同远程库，`name`也不同，可通过`git remote -v`查看
  >
  > 7. 上述流程第一次完成后，后续只需：
  >
  >    ```
  >    $ git add *
  >    $ git commit *
  >    $ git push *
  >    ```
  >
  >    
  >
  > 8. 可以通过`git status`查看仓库状态
  >
  > 9. 



## 安装Git

### 在Windows是安装Git

从Git官网下载[安装程序](https://git-scm.com/downloads)或[腾讯软件中心](https://pc.qq.com/detail/13/detail_22693.html)，然后按默认选项安装即可,安装完成后，在开始菜单里找到“Git”->“Git Bash”.

安装完成后，还需要最后一步设置，在命令行输入：

```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```

因为Git是分布式版本控制系统，所以，每个机器都必须自报家门：你的名字和Email地址。

注意`git config`命令的`--global`参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址

### 创建版本库

第一步，选择一个合适的地方，创建一个空目录：

```
$ mkdir learngit
$ cd learngit
$ pwd
/Users/michael/learngit
```

第二步，通过`git init`命令把这个目录变成Git可以管理的仓库：

```
$ git init
Initialized empty Git repository in /Users/michael/learngit/.git/
```

### 添加文件到仓库

- 文件放到`learngit`目录下（子目录也行）

第一步，用命令`git add`告诉Git，把文件添加到仓库：

```
$ git add readme.txt
$ git add file2.txt file3.txt
```

第二步，用命令`git commit`告诉Git，把文件提交到仓库：

```
$ git commit -m "wrote a readme file"
[master (root-commit) eaadf4e] wrote a readme file
 1 file changed, 2 insertions(+)
 create mode 100644 readme.txt
```

---

---

## 远程仓库

### 与GitHub建立连接

第1步：创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有`id_rsa`和`id_rsa.pub`这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：

```
$ ssh-keygen -t rsa -C "youremail@example.com"
```

如果一切顺利的话，可以在用户主目录里找到`.ssh`目录，里面有`id_rsa`和`id_rsa.pub`两个文件，这两个就是SSH Key的秘钥对，`id_rsa`是私钥，不能泄露出去，`id_rsa.pub`是公钥，可以放心地告诉任何人。

第2步：登陆GitHub，打开“Account settings”，“SSH Keys”页面：

然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴`id_rsa.pub`文件的内容：

![github-addkey-1](https://www.liaoxuefeng.com/files/attachments/919021379029408/0)

点“Add Key”，你就应该看到已经添加的Key：

![github-addkey-2](https://www.liaoxuefeng.com/files/attachments/919021395420160/0)

### 与远程仓库关联

把一个已有的本地仓库与之关联，然后，把本地仓库的内容推送到GitHub仓库

- 要关联一个远程库，使用命令`git remote add origin git@server-name:path/repo-name.git`；

- 关联后，使用命令`git push -u origin master`第一次推送master分支的所有内容；

- 此后，每次本地提交后，只要有必要，就可以使用命令`git push origin master`推送最新修改；
- *origin 自定义*

### 关联非master分支库

github上已经有master分支 和dev分支

在本地

`git checkout -b dev` 新建并切换到本地dev分支

`git pull origin dev `本地分支与远程分支相关联

在本地新建分支并推送到远程

`git checkout -b test`

`git push origin test `  这样远程仓库中也就创建了一个test分支

### 克隆远程仓库

用命令`git clone`克隆一个本地库：

```
$ git clone git@github.com:michaelliao/gitskills.git
```

克隆非master分支(在克隆主分支之后)

```
$ git checkout -b branchName origin/branchName
```

查看关联的远程库的名称

```
$ git remote -v
```



### 与码云gitee关联

- 在码云上注册账号并登录后，先上传自己的SSH公钥,把用户主目录下的`.ssh/id_rsa.pub`文件的内容粘贴进去

- 关联本地仓库

1. 首先，我们在码云上创建一个新的项目，项目名称最好与本地库保持一致：

2. 然后，我们在本地库上使用命令`git remote add`把它和码云的远程库关联：

```
   git remote add origin git@gitee.com:liaoxuefeng/learngit.git
```

3. 之后，就可以正常地用`git push`和`git pull`推送了！

如果在使用命令`git remote add`时报错：

```
git remote add origin git@gitee.com:liaoxuefeng/learngit.git
fatal: remote origin already exists.
```

这说明本地库已经关联了一个名叫`origin`的远程库，此时，可以先用`git remote -v`查看远程库信息：

```
git remote -v
origin	git@github.com:michaelliao/learngit.git (fetch)
origin	git@github.com:michaelliao/learngit.git (push)
```

可以看到，本地库已经关联了`origin`的远程库，并且，该远程库指向GitHub。

我们可以删除已有的GitHub远程库：

```
git remote rm origin
```

再关联码云的远程库（注意路径中需要填写正确的用户名）：

```
git remote add origin git@gitee.com:liaoxuefeng/learngit.git
```

此时，我们再查看远程库信息：

```
git remote -v
origin	git@gitee.com:liaoxuefeng/learngit.git (fetch)
origin	git@gitee.com:liaoxuefeng/learngit.git (push)
```

现在可以看到，origin已经被关联到码云的远程库了。通过`git push`命令就可以把本地库推送到Gitee上。

### 同时关联GitHub与gitee

git给远程库起的默认名称是`origin`，如果有多个远程库，我们需要用不同的名称来标识不同的远程库。

仍然以`learngit`本地库为例，我们先删除已关联的名为`origin`的远程库：

```
git remote rm origin
```

然后，先关联GitHub的远程库：

```
git remote add github git@github.com:michaelliao/learngit.git
```

注意，远程库的名称叫`github`，不叫`origin`了。

接着，再关联码云的远程库：

```
git remote add gitee git@gitee.com:liaoxuefeng/learngit.git
```

同样注意，远程库的名称叫`gitee`，不叫`origin`。

现在，我们用`git remote -v`查看远程库信息，可以看到两个远程库：

```
git remote -v
gitee	git@gitee.com:liaoxuefeng/learngit.git (fetch)
gitee	git@gitee.com:liaoxuefeng/learngit.git (push)
github	git@github.com:michaelliao/learngit.git (fetch)
github	git@github.com:michaelliao/learngit.git (push)
```

如果要推送到GitHub，使用命令：

```
git push github master
```

如果要推送到码云，使用命令：

```
git push gitee master
```

## 分支管理

查看分支：`git branch`

创建分支：`git branch <name>`

切换分支：`git checkout <name>`或者`git switch <name>`

创建+切换分支：`git checkout -b <name>`或者`git switch -c <name>`

合并某分支到当前分支：`git merge <name>`

```
$ $ git merge --no-ff -m "merge with no-ff" dev
```

删除分支：`git branch -d <name>`

用带参数的`git log`也可以看到分支的合并情况：

```
$ git log --graph --pretty=oneline --abbrev-commit
*   cf810e4 (HEAD -> master) conflict fixed
|\  
| * 14096d0 (feature1) AND simple
* | 5dc6824 & simple
|/  
* b17d20e branch test
* d46f35e (origin/master) remove test.txt
* b84166e add test.txt
* 519219b git tracks changes
* e43a48b understand how stage works
* 1094adb append GPL
* e475afc add distributed
* eaadf4e wrote a readme file
```