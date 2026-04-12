---
title: 新增github仓库
slug: blog-newrepo
excerpt: 已有仓库的github用户下新增仓库
categories:
  - 笔记
tags: []
halo:
  site: https://ai2.gdvzz.com
  name: c52f05c9-2df7-4991-a53e-d85ec4a00c66
  publish: true
---

<!-- # 新增github仓库 -->

`更新-260407` \| `发布-260407`

<!-- --- -->

## 简介

已有仓库的 github 用户（账号），通常还需要新增仓库（repo）。本文描述相关步骤，供参考。 

如何从零创建仓库，可参考 [用 Github + Markdown 创建个人网站↗](https://wssh.gdvzz.com/)。

## 新建仓库

登录 github，在首页点击左侧右上角的绿色 **New** 按钮新建仓库，输入相关信息：

- **Repository name**：新仓库的名字。比如输入 `img` 
- **Description**：对新仓库的描述。比如，some logos of organization
- **Choose visibility**：Public 或 Private，按需选择。将用 github pages 建网站，因此要选 Public。
- **Add README**。从本地计算机推送内容到 github 的仓库，因此不加 readme，确保 github 仓库是空的。
- **Add license**。按需。此处先跳过。

然后点击屏幕右下角的 **Create repository** 按钮。

<!-- 点击后创建新仓库成功，并出现以下提示界面： -->

## 本地创建目录新增文件

✴️ 以下仅仅是样例，请修改为您的实际目录和实际文件。

1. 在 gdvzz 目录下新建子目录 img

    - gdvzz 目录对应于 github 用户（账号）gdvzz
    - img 对应于该用户下的仓库 img

2. （可选）在 img 子目录下新建子目录 docs

    本样例用于创建网站，并拟将网站的 markdown 文件放在 docs 目录中，因此要创建子目录 docs。

3. 增加文件

    新增 markdown 文件，比如 index.md。内容随便写点什么。

    只是存放代码，可复制代码文件到这里，或者新建一个输出 hello world! 的程序。

4. （可选）新建 _config.yml

    本样例用于创建网站，因此新增配置文件 `_config.yml`，内容如下：

    ```yml
    theme: jekyll-theme-primer
    title: HOME # 增加title 否则报错
    description: logos of organization # 增加 description 否则报错
    timezone: Asia/Shanghai # 设置时区
    ```

完成上述操作后，目录文件结构如下：

```bash
~/gdvzz % tree img
img
└── docs
    ├── _config.yml
    └── index.md
```

## 推送本地文件到github仓库

在本地计算机上，依次执行以下命令，将本地文件推送到 github 仓库：

```bash
cd ~/gdvzz/img
git init
git status
git add .
git commit -m "1st commit"
git remote add origin git@github.com:gdvzz/img.git
git branch -M master
git push -u origin master
```

## （可选）发布网站

1. 在 github 网站上，点击该仓库顶部右侧的 **Settings**

2. 在出现的 Settings 界面上，点击左侧的 **Pages**

3. 在 Pages 界面上，找到 **Build and deployment**

4. **Source**：选 `Deploy from a branch`

5. **Branch**：选 `master`，再选 `/docs`，然后点击 **Save** 按钮

6. 稍等片刻刷新页面，可以看到上部出现了网址：https://gdvzz.github.io.img。✅ 完成！

<!--  -->
<span style="font-size:12px; color:#999">THE END</span>
