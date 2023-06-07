# Git教程

[TOC]

## 新建仓库

首先，我们需要有一个github仓库来存放代码。去官网新建一个仓库：[New repository (github.com)](https://github.com/new)

<img src="./git%E6%95%99%E7%A8%8B.assets/image-20230607173140304.png" alt="image-20230607173140304" style="zoom: 43%;" />

## 配置SSH key

由于push、pull甚至有时clone都需要验证身份，我们需要在本地用ssh配置好自己的身份，即生成一个公私钥对。我们把公钥送给github：[SSH and GPG keys (github.com)](https://github.com/settings/keys)，而私钥留在本机，就可以在push的时候验证身份。

```bash
git config --global user.name "Emilytutu"
git config --global user.email "1037572899@qq.com"
ssh-keygen -t rsa -C "1037572899@qq.com"
```

![image-20230607174218971](./git%E6%95%99%E7%A8%8B.assets/image-20230607174218971.png)

可以看出我们配置了自己的用户名和邮箱，并用邮箱生成了公私钥对。我们需要把文件`id_rsa.pub`中的全部内容复制到下面，然后点击add

![image-20230607174536776](./git%E6%95%99%E7%A8%8B.assets/image-20230607174536776.png)

添加成功如下图所示：

![image-20230607174622775](./git%E6%95%99%E7%A8%8B.assets/image-20230607174622775.png)

命令`ssh -T git@github.com`可以确认SSH公私钥对是否配置正确。

![image-20230607175711704](./git%E6%95%99%E7%A8%8B.assets/image-20230607175711704.png)

## 怎样push

首先初始化git，使用SSH的方式将代码仓库克隆到本地。

![image-20230607174914687](./git%E6%95%99%E7%A8%8B.assets/image-20230607174914687.png)

```bash
git init
git clone git@github.com:Emilytutu/peerpsycoun_En.git
```

克隆到本地后，将自己的代码文件复制到该目录下。执行添加命令，配置提交记录，将代码push到自己仓库的目标分支。

```bash
git add .  // .表示添加所有，也可以制定添加一个文件。.和add之间有个空格
git commit -m “First Commit”
git push origin main
```

![image-20230607175402439](./git%E6%95%99%E7%A8%8B.assets/image-20230607175402439.png)

## 怎样比较与回退版本

下图是git的工作原理，每一步代表执行命令前后代码的状态转移。

![git工作原理](./git%E6%95%99%E7%A8%8B.assets/v2-3bc9d5f2c49a713c776e69676d7d56c5_720w.png)

```bash
git log // 查看所有提交版本
git diff xxx // 查看xxx和远程仓库的xxx有何区别。如果不加xxx则是全部比较。
```

如果需要退回版本：

```bash
git reset --hard HEAD^ // 一个^表示退回一个版本
git reset --hard HEAD~10 // 10表示退回10个版本
```

但如果又反悔了，想回到退回前的版本了呢？

```bash
git reflog
git reset --hard 36c757c // 根据前面的版本号恢复
git pull origin main // 直接从仓库获取最新版本
```

![image-20230607205603535](./git%E6%95%99%E7%A8%8B.assets/image-20230607205603535.png)

注意，由于没有push，所以这些操作都是在本地，GitHub的仓库是没有变化的。

## 怎样PR(pull request)

