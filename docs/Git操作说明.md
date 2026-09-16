# Git操作说明

## 基本规范

- 只修改本组负责的章节目录，不修改其他章节和仓库根目录。
- 不上传医学原始数据、模型文件或大型运行结果。
- 不在代码中写入 API Key、密码、Token 等敏感信息。
- 代码必须使用相对路径，不能写死个人电脑上的绝对路径。
- 提交前应在本地完整运行一次，确认代码可以正常执行。
- 不直接修改 `main`，不使用 `git push --force`，遇到冲突先停止操作并联系仓库管理员。

## 第一次使用

以下命令以第01章为例。负责其他章节时，将命令中的 `01` 替换成相应章节号。

### 1. 检查提交身份

```bash
git config --global user.name
git config --global user.email
```

如果没有输出，只需设置一次：

```bash
git config --global user.name "你的姓名"
git config --global user.email "你的GitHub邮箱"
```

### 2. 下载对应章节分支

```bash
git clone --branch chapter-01 --single-branch https://github.com/KinokoY/CNU-AI-for-DataAnalyze.git CNU-AI-chapter-01
cd CNU-AI-chapter-01
```

一个组负责两章时，建议分别克隆到两个目录，不要在同一个目录中来回切换分支。

### 3. 确认当前分支

```bash
git branch --show-current
```

第01章必须显示 `chapter-01`。如果分支不正确，请先停止修改并切换到正确分支：

```bash
git switch chapter-01
```

## 日常提交流程

每次准备修改代码前，先进入该章节的本地仓库目录，然后执行以下步骤。

### 1. 获取远程最新版本

```bash
git pull --ff-only origin chapter-01
```

### 2. 放入并检查本章文件

将代码文件整理到 `chapters/chapter-01/` 中，然后检查改动：

```bash
git status
```

### 3. 选择本章改动

```bash
git add chapters/chapter-01
git status
```

不要使用 `git add .`，以免误提交其他文件。

### 4. 创建一次提交

```bash
git commit -m "第01章：增加数据清洗代码"
```

提交信息应简短说明本次改了什么，例如：

- `第01章：增加模型训练脚本`
- `第01章：修正绘图代码`
- `第01章：整理最终运行结果`

### 5. 推送到章节分支

```bash
git push origin chapter-01
```

### 6. 确认提交结果

```bash
git status
git log -1 --oneline
```

`git status` 显示没有待提交改动，并且 GitHub 页面能看到最新提交，即表示推送成功。

## 提交章节审核

章节达到可审核状态后，在 GitHub 仓库页面创建 Pull Request：

- `base` 选择 `main`。
- `compare` 选择本章的 `chapter-01`。
- 简单填写本次提交内容和运行情况。
- 创建后通知仓库管理员审核，不要自行合并。

## 常见情况

- 出现 `nothing to commit`：当前没有新的文件改动，不需要再次提交。
- 出现 `403` 或无权推送：确认使用的是已被添加到仓库的 GitHub 账号。
- 出现 `rejected` 或 `non-fast-forward`：先执行本章的 `git pull --ff-only`；如果仍失败，停止操作并联系管理员。
- 出现 `CONFLICT`：不要强制推送，也不要随意删除文件，保存提示信息并联系管理员处理。
