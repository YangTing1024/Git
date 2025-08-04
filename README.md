# 命令

## 基础配置

- **git config --global user.name "Ting Yang"（中间有空格需要使用双引号）**
- **git config --global user.email 123@qq.com**
- **git config --global credential.help store（保存用户名和密码）**
- **git config --global --list（查看配置信息）**

## 初始化

- **git init（初始化）**
- **git remote add origin <url>（绑定远程）**
- **git pull origin master（拉取代码）**
- **git branch dev（建分支）**
- **git checkout dev（切分支）**
- **git branch（查看本地分支）**

- - **git branch -r（查看远程分支）**
  - **git branch -a（查看所有分支）**

- **git add .（加入暂存区）**
- **git commit -m 'commit message'（提交）**
- **git checkout master（切分支）**
- **git merge dev（合并分支）**
- **git push origin master（推送）**

## 分析命令

- **git status（查看文件状态）**

- - **git status -s（简洁查看 ）**

- **git log（查看提交日志）**

- - **git log --oneline（简洁日志）**

- **git reflog（操作日志）**
- **git ls-files（所有被版本控制的文件）**
- **git remote -v（查看远程仓库网址）**

## 回滚

- **git reset --soft（工作区保留，暂存区保留）**
- **git reset --hard（工作区不保留，暂存区不保留）**
- **git reset --mixed（工作区保留，暂存区不保留）**

## 比较差异

- **git diff（比较工作区和暂存区）（未add）**
- **git diff --cached（比较暂存区和本地仓库）（未commit）**
- **git diff HEAD（所有差异）**
- **git diff 【提交ID1】 【提交ID2】**

- - **git log --oneline（查看最近的提交ID）**

- **git diff 【提交ID1】 HEAD（查看提交ID1与最新提交的差异）**

- - **HEAD表示最新的版本**

- **git diff HEAD~ HEAD（比较当前的和上一个版本的差异）**

- - **HEAD~表示上一个版本（HEAD^同理）**

- - - **HEAD~2 （表示前两个版本（可以是N））**

- - **（HEAD表示最新的版本）**

- **git diff HEAD~ HEAD 【filename】（比较具体的文件差异）**

## 删除

- **rm 【filename】（Linux移除，暂存区中还有）**
- **git rm 【filename】（从工作区及暂存区移除）**
- **git rm --cached 【filename】（从暂存区删除，工作区保留）**
- **git rm -r \*（递归删除目录下所有的子目录和文件）**

## 回退

- **撤销工作区修改：**

- - git checkout -- <文件名>（撤销单个文件修改）
  - git checkout -- .（撤销所有文件修改）
  - git restore <文件名>（更新单个文件）
  - git restore .（更新所有文件）

- **撤销暂存区修改：**

- - git reset HEAD <文件名>
  - git restore --staged <文件名>

- **回退提交记录：**

- - **软回退：**

- - - 回退到上一个提交，保留工作区和暂存区的修改
    - git reset --soft HEAD~1
    - git reset --soft <commit-hash>

- - **硬回退：**

- - - 完全回退到上一个提交，删除所有修改
    - git reset --hard HEAD~1
    - git reset --hard <commit-hash>

- - **混合回退（默认）：**

- - - git reset HEAD~1
    - git reset --mixed HEAD~1

- **创建反向提交：**

- - 创建一个新的提交来撤销指定提交的修改
  - git revert <commit-hash>
  - git revert <commit-hash1> <commit-hash2>

- **查看提交历史：**

- - git log --oneline（查看提交历史）
  - git reflog（查看操作历史）

## 忽略

- **添加 .gitignore 文件**
- **只忽略未被版本管理的东西**
- **如需忽略已被版本管理的，需先删除文件**

- - **git rm --cached 【filename】（并不会删除工作区文件）**

- **空文件夹不会被版本控制，除非里面有文件**
- **忽略文件格式**

- - **access.log（具体文件）**
  - ***.log（结尾）**
  - **temp/（文件夹）**

## 分支

### 查看命令

- **git branch（查看分支）**
- **git log --graph --oneline --decorate --all（查看分支合并情况）**

### 常见命令

- **git branch 【分支名】（创建分支）**
- **git switch 【分支名】（切换分支（推荐））**
- **git checkout 【分支名】（切换分支）**
- **git merge 【分支名】（合并分支）**
- **git branch -d 【分支名】（删除分支（未合并的修改过的分支无法删除））**

- - **git branch -D 【分支名】（未合并也可以删除）**

- **git merge --abort（终止合并操作）**

## 丢弃

- **丢弃工作区（未add）：**

- - **git restore <file>（**丢弃指定文件**）**
  - **git restore .（**丢弃所有文件**）**

- **丢弃暂存区（已add未commit）：**

- - **git restore --staged <file>（**取消文件的暂存状态，但保留工作区的修改，即从暂存区撤出**）**
  - **git reset --hard HEAD（**完全丢弃暂存区和工作区的修改**）**

- **丢弃最近一次提交（已commit）：**

- - **git reset --hard HEAD^（**HEAD^表示上一个提交，--hard 会丢弃工作区和暂存区的所有修改**）**
  - **git reset --soft HEAD^（**保留修改**）**

- **丢弃本地所有未提交的修改：**

- - **git reset --hard HEAD（**将工作区和暂存区恢复到最近一次提交的状态，所有未提交的修改都会丢失**）**

- **丢弃远程提交（已push）：**

- - **git push origin <branch> --force（**强制推送**）**
  - **git push origin <branch> --force-with-lease（**更安全**）**

- **注意事项：**

- - --hard的操作是永久丢弃修改，无法恢复，建议先备份。
  - 如果文件是新增的（未跟踪），可以直接删除文件：

- - - **rm <file>**（删除未跟踪的文件）
    - **git clean -df（**清理未跟踪文件**）**

- - - - -d：包括目录
      - -f：强制删除

## Github拉取代码

### ssh方式生成密钥

- **查看本地密钥文件：ls -al ~/.ssh**
- **生成密钥文件：ssh-keygen -t ed25519 -C "18259295592@163.com"**
- **选择保存密钥的文件位置**
- **输入密码（不输入则为空）**
-  **eval "$(ssh-agent -s)"**
- **ssh-add ~/.ssh/github_ssh**

## 标签

- **创建标签：**

- - **轻量标签：**git tag v1.0.0
  - **附注标签：**git tag -a v1.0.0 -m 'Release version 1.0.0'
  - **对特定提交打标签：**git tag -a v1.0.0 <提交hash值> -m 'Release version 1.0.0'

- **查看标签：**

- - **查看所有标签：**git tag
  - **按模式查找标签：**git tag -l 'v1.*'
  - **查看标签信息：**git show v1.0.0

- **推送标签：**

- - **推送单个标签：**git push origin v1.0.0
  - **推送所有标签**：git push origin --tags

- **删除标签：**

- - **删除本地标签：**git tag -d v1.0.0
  - **删除远程标签：**git push origin -delete v1.0.0

- **检出标签：**

- - git checkout v1.0.0

## Cherry Pick

- **基本使用：**

- - git cherry-pick <commit-hash>
  - git cherry-pick commit1 commit2 commit3（多个）
  - git cherry-pick commit1^..commit3（范围）
  - git cherry-pick --no-commit <commit-hash>（只应用更改但不提交，方便修改后再提交）
  - git cherry-pick --edit <commit-hash>（编辑提交内容）

- **遇到冲突：**

- - **使用策略：**

- - - git cherry-pick -X ours <commit-hash>（遇到冲突优先使用我们的版本）
    - git cherry-pick -X theirs <commit-hash>（遇到冲突优先使用他们的版本）

- - **处理冲突：**

- - - 解决冲突后继续：

- - - - git add .
      - git cherry-pick --continue

- - - 跳过当前提交：

- - - - git cherry-pcik --skip

- - - 中止操作，恢复到原状态：

- - - - git cherry-pick --abort

- - **实际场景**

- - - **hotfix应用到多个分支：**

```git
# 在 hotfix 分支修复了一个紧急 bug
git checkout hotfix
git commit -m "Fix critical security issue"

# 将修复应用到 main 分支
git checkout main
git cherry-pick hotfix

# 也应用到 develop 分支
git checkout develop  
git cherry-pick hotfix
```

- - - **选择性合并功能：**

```git
# 从 feature 分支只选择需要的提交
git log --oneline feature
# a1b2c3d Add user authentication
# e4f5g6h Add password validation  
# i7j8k9l Add email verification

# 只要认证功能，不要邮箱验证
git checkout main
git cherry-pick a1b2c3d e4f5g6h
```

# 图解

## 工作区域

![img](https://cdn.nlark.com/yuque/0/2025/png/28835836/1753193265338-a1917215-16a9-4abf-aa7f-3b5db45242ce.png)

## 文件状态

![img](https://cdn.nlark.com/yuque/0/2025/png/28835836/1753193420634-493818c3-4b7b-4c14-af30-effc6153a6de.png) 

## git reset的三种模式

![img](https://cdn.nlark.com/yuque/0/2025/png/28835836/1753231096140-decc0fb9-3352-432e-859a-fbd5128c53a1.png)

## 比较差异

![img](https://cdn.nlark.com/yuque/0/2025/png/28835836/1753273886171-d11cb6e0-1f79-40df-88a7-774cd21a0be9.png)

## 版本号 ![img](https://cdn.nlark.com/yuque/0/2025/png/28835836/1754206243585-3a2690f1-5c99-492e-9851-259cbf2a499c.png)

## Git Flow

![img](https://cdn.nlark.com/yuque/0/2025/png/28835836/1754206606099-14dce9b5-a519-49ff-9e01-c697d64ac328.png)

## Github Flow

![img](https://cdn.nlark.com/yuque/0/2025/png/28835836/1754206473770-4d69232c-3c11-45ff-b99b-c5dc99ddb869.png)

## 分支规范

![img](https://cdn.nlark.com/yuque/0/2025/png/28835836/1754206571785-1b012c8d-6f2d-431c-b35e-f74f9bff12d0.png)