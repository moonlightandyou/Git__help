# 一、设置git用户名和邮箱（与GitHub一致）

```
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
```

# 二、创建本地仓库

## 1.仓库初始化

```
git init
```

会在项目的根目录下创建.git文件夹,该文件夹就是git本地仓库

## 2.添加文件到暂存区

暂存区是一个中间区域，位于工作目录和 Git 仓库之间。就像是一个"准备区"：

* 使用 `git add` 命令将文件添加到暂存区
* 暂存区可以让你选择性地决定哪些修改要包含在下次提交中
* 文件的状态可以是：未跟踪(untracked)、已修改(modified)、已暂存(staged)

```
git add .  # 添加所有文件
git add 文件名  # 添加特定文件
```

## 3.提交更改

提交是对暂存区文件的快照：

* 永久保存暂存区中的更改到 Git 仓库
* 每次提交都会生成一个唯一的提交ID（commit hash）
* 包含提交信息，说明这次更改的内容

```
git commit -m "提交说明"
```

提交更改：

* **不会**改变你工作目录中的实际文件内容
* 只是在 Git 仓库中创建一个新的版本记录
* 原文件保持不变，但状态会更新为"干净"（clean）
* 所有提交都保存在 `.git` 目录中，可以随时回退或查看历史版本

关于提交

```
# 创建新分支保存更改
git switch -c new-branch-name# 查看完整提交历史

# 查看完整提交历史
git log

# 或查看简化版本
git log --oneline

#切换到特定提交
#方法1：使用 checkout（临时切换）
# 使用提交的 hash 值切换(哈希值可以通过查看简化版本log)
git checkout <commit-hash>
# 例如
git checkout abc1234

#方法2：使用 reset（永久切换）
# 软重置 - 保留修改但撤销提交
git reset --soft <commit-hash>
# 硬重置 - 完全重置到该提交
git reset --hard <commit-hash>

# 如果要在此基础上进行更改,创建新分支保存更改
git switch -c new-branch-name

#返回到最新版本
# 返回到主分支
git checkout main
# 返回到之前的位置
git switch -
```

## 4.通过软重置删除历史提交

1.重置到最早提交

```
git reset --soft <commit -hash>
```

2.创建新的单一提交

```
git add .
git commit -m "合并所有更改到一个提交"
```

3.强制同步到远程

```
git push origin main --force-with-lease
```

# 三、推送到远程仓库

## 1.新建GitHub仓库

## 2.将本地仓库与远程仓库关联

```
# 添加远程仓库地址
git remote add origin https://github.com/用户名/仓库名.git

# 验证远程仓库是否添加成功
git remote -v
```

## 3.推送代码到分支

分支是 Git 中最强大的功能之一，它允许开发者在不影响主代码的情况下进行并行开发。

**分支的基本概念**

* 分支相当于代码的一条独立时间线
* 每个分支可以独立演进
* 默认分支通常是 `main` 或 `master`
* 可以在不同分支间切换和合并

**常用分支命令**

```
# 查看所有分支
git branch

# 创建新分支
git branch 分支名

# 切换到指定分支
git checkout 分支名
# 或使用新命令
git switch 分支名

# 创建并切换到新分支
git checkout -b 分支名
# 或使用新命令
git switch -c 分支名

# 删除分支
git branch -d 分支名
# 强制删除
git branch -D 分支名

# 查看分支图
git log --graph --oneline --all
```

关于分支有更复杂的运行，这里不进行过多解释

**创建分支后，即可开始推送**

```
# 推送主分支到远程仓库
git push -u origin main
```

如果需要推送其他分支，但远程仓库没有该分支，则需要创建新推送流并指定分支

```
git push --set-upstream origin <branch name>
```

# 四、从远程克隆到本地或更新本地仓库

## 1.远程克隆

```
# 基本克隆命令格式
git clone <远程仓库URL> [本地目录名]

# 示例：克隆到当前目录
git clone https://github.com/用户名/仓库名.git

# 示例：克隆到指定目录
git clone https://github.com/用户名/仓库名.git my-project
```

## 2.更新本地

```
# 获取远程仓库的更新
git fetch origin

# 拉取并合并远程更改到当前分支
git pull origin main  # 如果是 main 分支

# 重置本地分支（强制拉取到本地）
git reset --hard origin/main
```
