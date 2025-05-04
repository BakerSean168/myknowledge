# git

[Pro Git book,这是一本关于如何使用 Git 的优秀图书](https://git-scm.com/book/en/v2)

## Git 常用命令

### 配置

| 命令                                                        | 说明                  |
| ----------------------------------------------------------- | --------------------- |
| `git config --global user.name "Your Name"`                 | 设置全局 Git 用户名   |
| `git config --global user.email "youremail@yourdomain.com"` | 设置全局 Git 用户邮箱 |
| `git config --list`                                         | 列出所有 Git 配置信息 |

*这些值保存在全局配置文件 ~/.gitconfig 中*

### 基本操作

| 命令                         | 说明                           |
| ---------------------------- | ------------------------------ |
| `git init`                   | 初始化一个新的 Git 仓库        |
| `git clone [url]`            | 克隆远程仓库                   |
| `git status`                 | 查看当前仓库状态               |
| `git add [file]`             | 添加文件到暂存区               |
| `git add .`                  | 添加所有文件到暂存区           |
| `git reset [file]`           | 取消暂存                       |
| `git commit -m "message"`    | 提交暂存区的文件               |
| `git push [remote] [branch]` | 推送本地分支到远程仓库         |
| `git pull`                   | 拉取远程仓库的更新并合并到本地 |
| `git pull --rebase`          | 拉取远程仓库的更新并在本地变基 |
| `git fetch`                  | 从远程仓库获取更新但不合并     |

### 分支操作

| 命令                                     | 说明                   |
| ---------------------------------------- | ---------------------- |
| `git branch`                             | 列出所有本地分支       |
| `git branch -r`                          | 列出所有远程分支       |
| `git branch [branch-name]`               | 创建新分支             |
| `git checkout [branch-name]`             | 切换到指定分支         |
| `git checkout -b [branch-name]`          | 创建并切换到新分支     |
| `git merge [branch-name]`                | 合并指定分支到当前分支 |
| `git branch -d [branch-name]`            | 删除本地分支           |
| `git push origin --delete [branch-name]` | 删除远程分支           |

### 标签操作

| 命令                                  | 说明               |
| ------------------------------------- | ------------------ |
| `git tag`                             | 列出所有标签       |
| `git tag [tag-name]`                  | 创建新标签         |
| `git tag -d [tag-name]`               | 删除本地标签       |
| `git push origin [tag-name]`          | 推送标签到远程仓库 |
| `git push origin --delete [tag-name]` | 删除远程标签       |

### 查看历史

| 命令                     | 说明                         |
| ------------------------ | ---------------------------- |
| `git log`                | 查看提交历史                 |
| `git log --oneline`      | 查看简洁的提交历史           |
| `git log --graph`        | 查看图形化的提交历史         |
| `git diff`               | 查看工作区与暂存区的差异     |
| `git diff [branch-name]` | 查看当前分支与指定分支的差异 |

### 撤销操作

| 命令                  | 说明                             |
| --------------------- | -------------------------------- |
| `git reset [file]`    | 撤销暂存区的文件                 |
| `git reset --hard`    | 重置工作区和暂存区到最后一次提交 |
| `git revert [commit]` | 撤销指定的提交                   |
| `git rebase --abort`  | 取消变基操作                     |

### 远程仓库

| 命令                          | 说明                           |
| ----------------------------- | ------------------------------ |
| `git remote -v`               | 查看远程仓库信息               |
| `git remote add [name] [url]` | 添加远程仓库                   |
| `git remote remove [name]`    | 删除远程仓库                   |
| `git push [remote] [branch]`  | 推送本地分支到远程仓库         |
| `git pull [remote] [branch]`  | 拉取远程仓库的更新并合并到本地 |

### 技巧

`git clone --depth 1 [url]` 只克隆仓库的最新版本，而不包含完整的历史提交记录。加快大项目的克隆速度。  

## Git Tag

Git Tag 是 Git 版本控制系统中用于标记特定提交(commit)的重要功能  
它本质上是一个指向特定提交的静态指针  
与分支(branch)不同，标签(tag)不会随着新的提交而移动，它始终指向创建时指定的那个提交  

标签类型：  
1. 轻量标签  
    仅是一个指向特定提交的引用  
    `git tag v1.0.0`  
2. 附注标签  
    存储在 Git 数据库中的完整对象，包含标签名、标签信息、标签签名等元数据。  
    `git tag -a v1.0.0 -m 'Release version 1.0.0' HEAD`  

### 常用操作  

查看标签  
```bash
git tag  # 列出所有标签
git show v1.0.0  # 查看特定标签的详细信息
```

推送标签  
```bash
git push origin v1.0.0  # 推送单个标签
git push origin --tags  # 推送所有本地标签
```

删除标签  
```bash
git tag -d v1.0.0  # 删除本地标签
git push origin :refs/tags/v1.0.0  # 删除远程标签
```

检出标签  
```bash
git checkout v1.0.0  # 检出标签(进入分离头指针状态)
git checkout -b new_branch v1.0.0  # 基于标签创建新分支
```

## GitHub Flow 工作流

GitHub Flow 是一种轻量级的 Git 工作流程，特别适合持续交付和部署的场景。 
它由 GitHub 推广并广泛应用于开源项目和敏捷开发团队中。 

核心原则：  
1. 单一主分支  
2. 功能分支开发  
3. Pull Request  
4. 持续部署  
