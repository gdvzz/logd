---
title: 新建网站_jtd
slug: lg-new-website-with-jtd
excerpt: 使用 just-the-docs theme 在 github 新建网站
categories:
  - 笔记
tags: []
halo:
  site: https://ai2.gdvzz.com
  name: 6de53d3d-2373-41b9-b4b3-3ad511ef4f6a
  publish: true
---

<!-- # 新建网站_jtd -->
`更新-260421` \| `发布-260420`

本文描述使用 GitHUb Pages 建站（使用 just-the-docs theme）的操作步骤，供感兴趣人员参考。

---

## 基本步骤

只要操作以下几个步骤，就可以得到一个网站。

**1、登录 github**

如何创建 github 账号并登录 github，请参考相关指导。此处从略。

**2、访问 [https://just-the-docs.com/ ↗](https://just-the-docs.com/)**

**3、使用 just-the-docs 模板**

在 [https://just-the-docs.com/#getting-started↗](#https://just-the-docs.com/#getting-started)下面，找到 [use the template](https://github.com/just-the-docs/just-the-docs-template/generate)，并点击

**4、创建用于网站的新仓库**

上一步点击 use the template 链接后，会跳转到您的 github 创建新仓库界面。输入以下信息，就可以创建用于网站的新仓库： 

- **Include all branches**： `Off`（默认值，先不改）
- **Repository name**: `xxx`（输入您期望的仓库名字，比如 jtdsh）
- **Choose visibility**: `Public`（默认值，不改。如改成 Private，则无法免费创建网站）

然后点击 **Create repository** 绿色按钮。

**5、网站构建和部署选择 GitHub Actions**

- 点击新建仓库顶部的 **Settings**，在 Settings 界面的左侧导航栏找到并点击 **Pages**
- 在出现的 Pages 界面中，设置 **Build and deployment** → **Source** : `GitHub Actions`

**6、重新运行工作流**

- 点击新建仓库顶部的 **Actions**
- 在左侧导航栏找到并点击 **Deploy Jekyll site to Pages**
- 在右侧界面中点击 **Run workflow**

**7、访问网站**

- 点击新建仓库顶部的 **Settings**，在 Settings 界面的左侧导航栏找到并点击 **Pages**
- 在出现的 Pages 界面中，点击右上按钮 **Visit site**，就可以访问网站了。
    
✅ 完成！
 

<!-- https://gdvzz.github.io/tai_test/ -->

---

## 修改分支（可选）

不喜欢分支是main，可以修改为其他分支名字，比如 master。本章节操作是可选的。之所以想修改分支，主要是为了熟悉 Github Action。

**1、在 github 修改分支**

- 点击新建仓库顶部的 **Settings**，在 Settings 界面的左侧导航栏找到并点击 **General**
- 在出现的 General 界面中，设置 **Default branch** : `master`

修改后，在仓库的 Code 界面有如下提示信息：

```bash
The default branch has been renamed!

main is now named master

If you have a local clone, you can update it by running the following commands.

git branch -m main master
git fetch origin
git branch -u origin/master master
git remote set-head origin -a
```

**2、git clone 到本地电脑**

将仓库 clone 到本地电脑 ~/gdvzz 目录下：

```bash
~/gdvzz % git clone git@github.com:gdvzz/jtdsh.git
```

✳️ git clone 完成后，在 gdvzz 会创建 jtdsh 子目录。

**3、更改 git remote（可选）**

不喜欢远程的名字是默认的 origin，可以执行以下命令，改成其他名字比如 jtdsh。

先进入本地仓库的目录：

```bash
cd ~/gdvzz/jtdsh
```

查看当前远程的名字（默认是 origin）：

```bash
git remote -v
```

删除当前远程 origin：

```bash
git remote rm origin
```

增加新的远程比如 jtdsh：

```bash
git remote add jtdsh git@githubvzz.com:gdvzz/jtdsh.git
```

git  remote add 命令中的 `githubvzz.com`，对应于本地电脑 `~/.ssh/config` 文件中的如下片段。如果 `Host githubvzz.com` 改成 `Host abc.com`，则上述命令要相应改为 `git remote add jtdsh git@abc.com:gdvzz/jtdsh.git`。

```bash
# github - gdvzz@outlook.com
Host githubvzz.com
HostName github.com
User git
IdentityFile ~/.ssh/id_ed25519_gdvzz_olk
```

**4、更新网站-推送内容** 

先更改 markdown 文件内容，比如更改 `index.md`。

然后在本地电脑依次执行：

```bash
cd ~/gdvzz/jtdsh
git status
git add .
git commit -m "update index.md"
git push jtdsh
```

✳️ 执行 git push jtdsh 如提示 `git push --set-upstream jtds master`，就按提示重新执行。一般第一次 push 到 github 需要这样，后续就执行 git push jtdsh 即可。

✅ push 成功了。
❌ 但没有重新刷新网页。查看 github 上该仓库的 Action，发现没有执行部署的工作流。

### 修改配置文件

和 AI 交流后得到修改相关 yaml 文件的建议。

**1、修改 ci.yml 和 pages.yml**

```yml
name: CI

on:
  push:
    branches: ["master"]   # 原为 "main"
  pull_request:

# ... 其余内容不变
```

```yml
name: Deploy Jekyll site to Pages

on:
  push:
    branches: ["master"]   # 原为 "main"
  workflow_dispatch:

# ... 其余内容不变
```

**2、测试**

更改文件比如 `index.md`，然后 git push jtdsh。 发现网页内容还未更新。查看 github Action，看到 build 通过了，但 deploy 报错如下：

```markdown
Annotations
2 errors and 1 warning
deploy
Branch "master" is not allowed to deploy to github-pages due to environment protection rules.
deploy
The deployment was rejected or didn't satisfy other protection rules.
```

**3、修改 github 相关设置**

以下是从 AI 交流获得的：

这个错误不是你的配置写错了，而是 GitHub 在为你新创建的 github-pages 环境设置了一个“安全锁”，这个锁默认只允许仓库的默认分支进行部署。

在你将仓库的默认分支从 main 改为 master 之后，github-pages 环境的规则并没有自动更新，所以系统拒绝了来自 master 分支的部署请求。

进入环境设置页面：在 GitHub 上打开你的仓库，点击 Settings 标签，然后在左侧菜单栏中找到 Environments 并点击。

选择 github-pages 环境：在环境列表中找到 github-pages 并点击。

修改部署分支规则：

找到 Deployment branches 部分，将下拉选项从默认的 Only branches that match the default branch（通常为 main）改为 Selected branches。

点击 Add deployment branch rule 按钮，在弹出的输入框中输入 master，然后点击 Add rule 保存。

完成以上设置后，重新运行失败的 GitHub Actions 工作流，部署应该就能成功了。

**4、再测试**

完成上述设置后，重新运行 Action 里面失败的job，网页刷新了。

✅ 至此，分支修改为 master，并且也能重新部署网页了。

---

## 网站内容放到 /docs 目录（可选）

可以考虑将网站内容放到 /docs 目录中，这样可以创建 /code 目录放代码。本章节操作是可选的。之所以想修改存放目录，主要也是为了熟悉 Github Action。和 AI 交流后得到如下修改建议。

**1、修改 bundler 的扫描目录**

dependabot.yml 原配置中 bundler 的 directory: / 表示在仓库根目录查找 Gemfile。文件移动后，Gemfile 位于 docs/ 下，因此需要将目录改为 /docs。

```yml
version: 2
updates:
  - package-ecosystem: bundler
    # directory: /
    directory: "/docs"  # by George 260421
```    

**2、ci.yml 设置工作目录为 docs**

需要在 build job 中添加 defaults.run.working-directory: docs，使所有 run 命令在 docs/ 目录下执行（包括 bundle exec jekyll build）。

```yml
jobs:
  # Build job
  build:
    runs-on: ubuntu-latest
    defaults:
      run:
        working-directory: docs   # by George 260421
```

**3、pages.yml 设置工作目录为 docs**

设置工作目录为 docs，并保持其他配置与 ci.yml 类似，在 build job 中添加 defaults.run.working-directory: docs。注意 upload-pages-artifact 默认上传 ./_site，由于工作目录已改为 docs，它会自动上传 docs/_site，无需额外修改。

```yml
jobs:
  # Build job
  build:
    runs-on: ubuntu-latest
    defaults:
      run:
        working-directory: docs   # by George 260421
```

**4、修改后的目录结构**

```bash
jtdsh/
├── .github/
│   ├── dependabot.yml
│   └── workflows/
│       ├── ci.yml
│       └── pages.yml
├── docs/                     # 新目录，所有网站源文件移入
│   ├── Gemfile
│   ├── Gemfile.lock
│   ├── _config.yml
│   ├── index.md
│   └── ...（其他文件）
├── .gitignore
├── LICENSE
├── README.md
└── index.md.bak              # 备份文件可保留在根目录或移走
```

**5、测试**

更改文件比如 `index.md`，然后 git push jtdsh，网页内容没有更新。检查 github Actions，发现在 build 时报错 `bundler: command not found: jekyll`。

**6、为 ruby/setup-ruby 显式指定 working-directory**

和 AI 交流后得到，为解决报错 `bundler: command not found: jekyll`，需要在 ci.yml + pages.yml，为 ruby/setup-ruby 显式指定 working-directory。

pages.yml 片段如下：

```yml
      - name: Setup Ruby
        uses: ruby/setup-ruby@v1
        with:
          ruby-version: '3.3' # Not needed with a .ruby-version file
          bundler-cache: true # runs 'bundle install' and caches installed gems automatically
          cache-version: 0 # Increment this number if you need to re-download cached gems
          working-directory: docs   # by George 260421
```

ci.yml 片段如下：

```yml
      - name: Setup Ruby
        uses: ruby/setup-ruby@v1
        with:
          ruby-version: '3.3' # Not needed with a .ruby-version file
          bundler-cache: true # runs 'bundle install' and caches installed gems automatically
          cache-version: 0 # Increment this number if you need to re-download cached gems
          working-directory: docs   # by George 260421
```

**7、再测试**

更改文件比如 `index.md`，然后 git push jtdsh，网页内容没有更新。检查 github Actions，发现 ci.yml 通过了，pages.yml 的 Upload artifact 报错`tar: _site/: Cannot open: No such file or directory`。

**8、修改 Upload artifact**

和 AI 交流后得到：修改 pages.yml 中的 Upload artifact 步骤,显式告诉 upload 步骤去 docs/_site 找构建产物。

pages.yml 片段如下：

```yml
      - name: Upload artifact
        # Automatically uploads an artifact from the './_site' directory by default
        uses: actions/upload-pages-artifact@v5
        with:
          path: docs/_site # by George 260421
```

**9、再再测试**

更改文件比如 `index.md`，然后 git push jtdsh，网页内容更新了。

✅ 至此，网站文件都移到 /docs 目录中。

<!--  -->
<span style="font-size:12px; color:#999">THE END</span>
