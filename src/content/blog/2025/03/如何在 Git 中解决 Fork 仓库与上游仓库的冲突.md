---
title: "如何在 Git 中解决 Fork 仓库与上游仓库的冲突2"
categories: Git
tags:
  - Git
  - Code
id: "36731f744673c26f"
date: 2025-03-25 00:19:27
recommend: true
---

:::note
用于fork别人的仓库，同步上游仓库最新代码，并解决冲突的问题。
:::


# 如何在 Git 中解决 Fork 仓库与上游仓库的冲突

当你 fork 了一个 GitHub 项目，在本地进行提交和修改后，想要同步上游仓库（upstream repository）的最新代码时，可能会遇到冲突提示，例如 GitHub 显示 `This branch has conflicts that must be resolved`。以下是解决冲突的完整步骤，帮助你保留本地修改并成功同步上游代码。

## 前提条件
- 本地仓库已经 fork 自上游仓库。
- 你在本地分支（例如 `main`）上有提交。
- 上游仓库有更新，导致合并时产生冲突。

## 解决冲突的完整步骤

### 1. 在本地设置上游仓库
确保你的本地仓库已关联上游仓库。如果尚未添加上游远程仓库，请按以下步骤操作：

```bash
# 查看当前远程仓库
git remote -v

# 添加上游仓库（替换为实际上游地址，例如 https://github.com/username/repo.git）
git remote add upstream https://github.com/username/repo.git

# 确认添加成功
git remote -v
```

输出应类似：

```bash
origin    https://github.com/your-username/repo.git (fetch)
origin    https://github.com/your-username/repo.git (push)
upstream  https://github.com/username/repo.git (fetch)
upstream  https://github.com/username/repo.git (push)
```

### 2.获取上游最新代码

切换到你的工作分支（假设为 main），然后拉取上游代码：

```bash
# 切换到 main 分支
git checkout main

# 获取上游仓库的最新数据
git fetch upstream

# 尝试合并上游代码
git merge upstream/main
```

如果出现类似以下提示：

```bash
CONFLICT (content): Merge conflict in <文件名>
Automatic merge failed; fix conflicts and then commit the result.
```

说明存在冲突，需要手动解决。

### 3.解决冲突

#### 查看冲突文件

`git status`

#### 编辑冲突文件

#### 提交文件

- `git commit`
- `git push origin main`

### 如果不想保留本地修改

如果你愿意丢弃本地提交，直接与上游同步，可以执行以下命令：

```
# 重置到上游状态
git fetch upstream
git reset --hard upstream/main

# 强制推送到你的 fork
git push origin main --force
```

> 注意：`--force` 会覆盖远程分支历史，请确保不需要保留本地提交，否则先备份代码。