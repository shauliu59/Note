[TOC]

# 基本Linux命令

cd '文件夹名' ：进入文件夹
cd .. ：返回上一级
pwd ：显示当前所在目录路径
clear ： 清屏
ls ：列出当前目录所有文件
touch '文件名' ： 创建文件
rm '文件名' ： 删除文件
mkdir '文件夹名字' ： 新建文件夹
rm -r '文件夹名字' ： 删除文件夹
mv '文件名' '文件夹名字' ： 移动文件

# Git配置

查看Git配置 ： git config -l
查看系统config ： git config --system --list
查看当前用户配置： git config --global --list
设置用户名和邮箱
git config --global user.name "用户名"
git config --global user.email "邮箱"

# Git基本理论

本地工作区->暂存区->本地仓库->远程仓库

# Git项目搭建

## 创建本地仓库

### 创建全新的仓库

git init(在当前目录创建一个git代码库)

### 克隆远程仓库

git clone "url地址(github上的)"

## Git文件操作

### Git 文件状态

1.Untracked：未跟踪，此文件在文件夹中，但并没有加入到git库中
2.Unmodified：文件入库但未修改
3.Modified：文件已修改，并未有其他操作
4.Staged：暂存状态，执行git commit则将修改同步到库中

### 查看文件状态

git status：查看所有文件状态
git status "文件名"：查看某个特定文件状态
git status -s: 未跟踪文件前边有红色的??

### 添加文件到暂存区

git add .：添加所有文件到暂存区

### 从暂存区移除文件

git reset HEAD .

### 提交暂存区内容到本地仓库

git commit -m "注释信息"

### 忽略某些文件

*.txt：忽略所有后缀为txt的文件(!hello.txt：除了hello.txt不被忽略)
/temp：忽略temp文件夹下的所有文件，子目录不受影响
temp/：忽略子目录文件

### 查看提交历史

git log: 查看所有提交历史
git log -2: 查看最近两条提交历史

### 回退到指定版本

git reset --hard 版本Id

### 在旧版本中查看所有提交日志

git reflog

### clone别人的仓库，修改后推送到自己的远程仓库可能遇到：error: remote origin already exists. 表示远程仓库已存在。

1、先输入git remote rm origin 删除关联的origin的远程库
2、关联自己的仓库 git remote add origin 地址
3、最后git push origin master，这样就推送到自己的仓库了。

## 远程仓库

### SSH key

作用：实现本地仓库和Github之间免登录的加密数据传输
好处：免登录身份认证、数据加密传输
SSH key由两部分组成，分别是：

1. id_rsa(私钥文件，存放于客户端的电脑中即可)
2. id_rsa.pub(公钥文件，需要配置到Github中)

#### 生成SSH key

1. ssh-keygen -t rsa -b 4096 -C "github邮箱"
2. 连续三次回车，即可在C:\Users\用户文件夹\.ssh目录找到id_rsa和id_rsa.pub两个文件
3. 检测是否配置成功: ssh -T git@github.com

## 分支

初始化本地Git仓库后，默认创建一个master主分支
每个独立的功能对应一个具体分支。**分支之间互不影响**
master主分支作用: 保存和记录整个项目已完成的功能代码

### 查看所有分支

git branch(分支前有*代表当前所处分支)

### 创建新分支

git branch 分支名称
新分支代码与当前所在分支代码完全一致，用户当前所处分支还是创建分支前的分支(在master上创建还在master)

### 切换分支

git checkout 分支名

### 分支快速创建和切换分支(常用)

git checkout -b 分支名: 创建并切换到新分支

### 合并分支

功能分支的代码开发完毕后可以将分支代码合并到主分支

1. git checkout master: 切换到主分支
2. git merge 合并分支名: 将分支合并到master主分支

### 删除分支

git checkout -d 分支名
注意: 删除分支时不能处在该分支上

### 遇到冲突时的分支合并(重要)

当两个**不同的分支**对**同一文件**进行**不同修改**时，执行merge操作后会出现**冲突**,需要**手动解决冲突**

```
git checkout master
git merge A //报错，出现conflict
//需要手动解决冲突，解决冲突后重新提交
git add .
git commit -m "解决冲突"
```

### 远程分支

第一次将本地分支推送到远程仓库:

```
git push -u 远程仓库别名 本地分支名:远程分支名
git push -u origin login:log
//远程分支名与本地分支名保持一致，可简化
git push -u origin pay
```

注意：第一次推送分支需要带-U参数，此后可以直接使用git push推送代码到远程分支。

#### 查看远程仓库所有分支

git remote show 远程仓库名

### 跟踪分支

把远程仓库的远程分支下载到本地仓库

```
git checkout 远程分支名
//下载到本地仓库并对该分支重命名
git checkout -b 本地分支名 远程仓库名/远程分支名
eg. 
git checkout -b payment origin/pay
```

### 拉取远程分支(重要)

git pull

### 删除远程分支

git push 远程仓库名 --delete 远程分支名

# warning: in the working copy of 'xxx.md', LF will be replaced by CRLF the next time Git touches it

换行符CRLF会被替换成LF
false：不做任何改变。只在windows下，建议使用
`git config --global core.autocrlf false`
