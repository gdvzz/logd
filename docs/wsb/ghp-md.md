---
layout: default
---

# Github建站
`更新-260722` \| `发布-260719`

<!--  -->
<br>

## e1-安装相关软件

主要有：

- git
- VSCode

<!--  -->
<br>

## e2-建网站

参考资料：[用 Github + Markdown 创建个人网站↗](https://wssh.gdvzz.com/)

> 虽然没有明确申明，应该也是使用了 `jekyll-theme-primer` theme。

<!--  -->
<br>

## e3-建网站jtd

使用 `just-the-docs` theme 建网站。主要有 2 个参考资料：

- 参考资料：[新建网站_jtd](https://logd.gdvzz.com/blog/newsjtd)

    主要分享用 `just-the-docs` theme，如何快速建个网站，并能访问。

- 参考资料：[关于本站↗](https://tnt.gdvzz.com/about.html)

    怎么搭网站的部分，可以忽略。建议参考上面那个资料。

    主要可以看看 **定制配置网站** 那个章节。

<!--  -->
<br>

## e4-建网站mm

使用 `minimal-mistake` theme 建网站。

可以参考 [Minimal Mistakes remote theme starter↗](https://github.com/mmistakes/mm-github-pages-starter) 快速建站：

- 点击 [Use this template↗](https://github.com/mmistakes/mm-github-pages-starter/generate) 快速建站。

    先复制（新建）一个仓库，到自己的账号下。

    然后操作 GitHub Pages，发布网站即可。尚未定制的样例网站可参考：[mm↗](https://aics27.gdvzz.com/)

- 点击 [configure as necessary↗](https://mmistakes.github.io/minimal-mistakes/docs/configuration/) 做相关配置。

<!--  -->
<br>

## e5-前端三件套

[前端三件套简介↗](./ghp-md.assets/index.html)


<!--  -->
<br>

## e6-git

[B站-停止死记硬背Git命令，学习数据模型 - PawelCodeStuff - 中配↗](https://www.bilibili.com/video/BV1kdKa62ENf)

### 不同版本切换
<br>
做个网页，然后修改，然后切换到修改前的网页。

0. **启动一个终端（PowerShell）**

1. **在 PC（个人电脑）新建目录，用于实验**

    ```bash
 mkdir ~/tmp260722
    ```

2. **切换目录**

    ```bash
cd ~/tmp260722
    ```

3. **初始化git仓库**

    ```bash
git init
    ```

4. **写一个 html**

    在实验目录中，写一个 html。并浏览器查看
    
    或下载样例：[a.html](./ghp-md.assets/a.html)

5. **提交本地仓库**

    ```bash
git status
    ```

    ```bash
git add .
    ```

    ```bash
git commit -m "v1.0"
    ```

6. **修改这个html 文件**

7. **修改后的文件提交本地仓库**

    ```bash
git status
    ```

    ```bash
git add .
    ```

    ```bash
git commit -m "v2.0"
    ```

8. **查看提交记录**

    ```bash
git log
    ```

    得到以下类似信息：

    ```text
    commit bf930ffe1ed11811e7b6ab620d704ffb2db34e28 (HEAD -> master)
    Author: gdv2 <gdv2@examle.com>
    Date:   Wed Jul 22 18:31:17 2026 +0800

        v2.0

    commit 3d51415ca315a2f4bc7255c5e85894fa1dd77423
    Author: gdv2 <gdv2@examle.com>
    Date:   Wed Jul 22 18:29:06 2026 +0800

        v1.0
    ```

    得到 v1.0 对应的 commit id 是 3d51415...

9. **“恢复”v1.0**

    ```bash
git checkout -b show-v1 3d51415
    ```

    浏览器查看 html，的确回到 v1.0 的网页

10. **回到v2.0**

    先查看分支信息：

    ```bash
    git branch -v
    ```

    得到如下类似信息：

    ```text
  master  bf930ff v2.0
* show-v1 3d51415 v1.0
    ```

    回到 v2.0：

    ```bash
git checkout master
    ```

    浏览器查看 html，回到 v2.0 的网页 


<!--  -->
<span style="font-size:12px; color:#999">THE END</span>