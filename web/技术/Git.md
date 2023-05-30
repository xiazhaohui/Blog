<!--
 * @Author: 夏朝辉 lesslessmore@163.com
 * @Date: 2023-05-30 14:25:28
 * @LastEditors: 夏朝辉 lesslessmore@163.com
 * @LastEditTime: 2023-05-30 14:44:03
-->
# Git

# 配置相关

常用命令

```bash
# 查看远程仓库地址
git remote -v

# 删除远程仓库地址
git remote rm origin

# 添加新的远程仓库地址
git remote add origin url

# 更换远程仓库地址
git remote set-url origin NEW_URL
```

# 分支相关

## Git规范

项目中一般会有三个环境分支，分别为测试环境分支（develop）、预发环境分支（prepub）和线上环境分支（master）

### 分支命名规范

#### 分支类型

- 功能分支：feature
- 测试分支：dev
- bug分支：hotfix
- 基建类分支：const

#### 分支结构

分支类型/日期/开发人员/功能描述

示例：feature/202205/xia/ma-graph-dnd

图解：

![Untitled](/assets/web/技术/git-branch-structure.png)

- 功能分支：feature/年月/开发人员/功能描述
- 测试分支：dev/年月/开发人员/功能描述
- bug分支：hotfix/年月/开发人员/bug描述
- 基建类分支：const/年月/开发人员/功能描述
- 例：feature/202205/xia/ma-graph-dnd

### commit规范

建议遵循Angular提交规范，其格式包括Header、Body和Footer三个内容，其中Header为必填项。

Header部分包括三个字段，分别是**type**、**scope**和**subject**

示例：feat(view)：新增页面触发方式

图解

![Untitled](/assets/web/技术/git-commit-standard.png)

- type用于说明commit的提交类型，包括以下表格选项
- scope用于说明commit的影响范围，如数据(**data**)、视图(**view**)、逻辑(**logic**)等
- subject用于说明commit的细节描述

| 类型 | 功能 | 描述 |
| --- | --- | --- |
| feat | 功能 | 新增功能，迭代项目需求 |
| fix | 修复 | 修复缺陷，修复上个版本存在问题 |
| docs | 文档 | 更新文档，不涉及代码 |
| style | 样式 | 更新样式，不影响代码逻辑 |
| refactor | 重构 | 重构代码，非新增功能也非修复缺陷 |
| pref | 性能 | 优化性能，提高代码执行性能 |
| test | 测试 | 更新测试，追加测试用例验证代码 |
| build | 构建 | 更新构建，改动构建工具或外部依赖 |
| ci | 脚本 | 更新脚本，改动CI或执行脚本配置 |
| chore | 事务 | 变动事务，改动其他不影响代码的事务 |
| revert | 回滚 | 回滚版本，撤销某次commit提交 |
| merge | 合并 | 合并分支，合并分支代码到其它分支 |
| sync | 同步 | 同步分支，同步分支代码到其它分支 |
| impr | 改进 | 改进性能，升级当前功能模块 |

### 关于合并

每次合并功能分支到测试、预发或线上分支前，要做几件事

1. 开发完成后，`git pull origin master`，同步线上最新代码到功能分支
2. 合并方式1:切换到测试、预发或线上分支，拉取该分支最新代码，然后merge功能分支到此分支
3. 合并方式2:在Git仓库上面提交merge request
4. 合并方式3:在SourceTree上面合并

合并分支过程中，若有冲突，则解决冲突后再提交合并。

若在Git仓库合并分支发生冲突，可以选择在Git仓库或本地解决冲突后再进行合并。

【注意】

1. 从master切新分支
2. 合并前先git pull
3. 不要合并develop分支到任何分支！

#### 开发流程

1. 从master线上分支切一个功能分支进行开发
2. 合并功能分支到develop测试分支进行测试
3. 合并功能分支到prepub预发分支进行测试
4. 合并功能分支到master线上分支发布

## Git命令

| 命令 | 描述 |
| --- | --- |
| git log | 查看commit记录 |
| git branch | 查看分支列表 |
| git branch -D [分支名] | 删除某条分支 |
| git checkout [分支名] | 切换到某个分支 |
| git checkout -b [新分支名] | 从当前分支上切出一条新的分支 |
| git merge [分支名] | 合并某分支到当前分支 |
| git pull | 从远程仓库拉取当前分支的最新代码 |
| git push | 把当前分支推送到远程仓库 |
| git stash | 暂存代码 |
| git reset | 回溯代码 |
| git cherry-pick | 复制具体的某条commit |
| git reflog | 查看commit历史 |

### merge

描述：合并分支

> 优点：不会破坏原分支的提交记录
缺点：会产生新的merge commit记录，并进行两条分支线的合并
>

```bash
# 合并feature-202210分支到当前分支
git merge feature-202210
```

### rebase

描述：合并commit记录，保持分支整洁（消除了git merge产生的merge commits）

> 优点：无需新增提交记录到目标分支，reabse后可以直接将对象分支的提交历史加到目标分支上，形成线性提交历史记录，更加直观
缺点：不能在一个共享分支上进行reabse操作，会带来分支安全问题
>

```bash
# rebase feature-202210分支到当前分支
git rebase feature-202210
```

### stash

描述：暂存更改

```bash
# 保存当前未commit的代码
git stash

# 保存当前未commit的代码并添加备注
git stash save "备注的内容"

# 列出stash的所有记录
git stash list

# 删除stash的所有记录
git stash clear

# 应用最近一次的stash
git stash apply

# 应用最近一次的stash，随后删除该记录
git stash pop

# 应用某一次的stash，首先需要git stash list列出记录，查找对应某条stash的id
git stash apply stash@{1}

# 删除最近的一次stash
git stash drop
```

### reset

描述：回溯commit

```bash
# 回退已提交的commit，强制回溯
git reset --hard

# 回退已提交的commit，并将commit的修改内容放回到暂存区
git reset --soft
```

### cherry-pick

描述：将已经提交的commit，复制出新的commit应用到分支里

```bash
# commitHash和之前的不一样，但是提交时间还是保留之前的
git cherry-pick {commitHash}

# 一次提交多个
git cherry-pick commit1 commit2

# 一次提交两个commit之间的所有commit
git cherry-pick commit1^..commit2
```

```bash
# 解决冲突后继续
git cherry-pick --continue

# 放弃cherry-pick
git cherry-pick --abort

# 退出cherry-pick
git cherry-pick --quit
```

### reflog

描述：commit历史
