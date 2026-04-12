---
title: Squid做上网代理
slug: blog-squid
excerpt: 使用Squid做上网代理
categories:
  - 笔记
tags: []
halo:
  site: https://ai2.gdvzz.com
  name: 863ec87e-d6ac-481d-b2d4-3a98d9c64025
  publish: true
---

<!-- # 使用 Squid 做上网代理 -->

`更新-260407` \| `发布-260406`

<!-- --- -->

<!-- ## introduction -->
## 简介

开发板有时需要访问外网，比如通过 apt 安装程序。通过局域网内某个可以上外网的 Linux（或 MacOS）机器，安装 squid，是选项之一。

本文简要介绍如何安装 squid，以及如何配置 squid。

✅ 选择 squid 的理由：配置简单。

<!-- --- -->

<!-- ## install -->
## 安装

在 Ubuntu 环境下，执行如下命令安装：

```bash
sudo apt install squid
```

安装完成后，squid 默认就（在后台）启动了。

macOS 可以在**终端**中，执行 `brew install squid` 安装。

<!-- --- -->

<!-- ## config -->
## 配置

主要修改 squid 的配置文件，即可。以下以 squid 6.14 为例。

✴️ 商用环境应该有更完善的配置，此处配置仅用于个人学习。

1. **打开 squid 配置文件**

    ```bash
    sudo vim /etc/squid/squid.conf
    ```

    > 可以有多种方式编辑配置文件，比如用 vscode 编辑。此处以 vim 为例。

2. **启用 `http_access allow localnet`**

    大约在 squid.conf 1620 行左右，有一行的内容是 `# http_access allow localnet`。删除行首的 `# ` 后，表示 `http_access allow localnet` 生效了。修改后的文件片段如下：

    ```shell
    http_access allow localnet # 原来是 “# http_access allow localnet”
    ```

3. **增加允许访问的 IP**

    大约在 squid.conf 1400 行左右，添加 `acl localnet src IP地址`。

    样例 acl localnet src 49.93.0.0/16 的意思是：允许 49.93.xxx.xxx 开头的 IP 访问 squid。

    > acl localnet src 49.93.111.0/24：允许 49.93.111.xxx 开头的 IP 访问 squid。

    > acl localnet src 49.0.0.0/8：允许 49.xxx.xxx.xxx 开头的 IP 访问 squid。

    修改后的文件片段如下：

    ```shell
    ...
    acl localnet src 192.168.0.0/16 
    acl localnet src fc00::/7
    acl localnet src fe80::/10
    acl localnet src 49.93.0.0/16 # 这一行是新加的
    acl SSL_ports port 443
    ...
    ```

4. **保存（或放弃）修改**

    在 vim 界面，执行以下操作：

    - 保存：先按 `esc` 键，再输入 `:wq`，然后按 `回车` 键
    - 放弃：先按 `esc` 键，再输入 `:q!`，然后按 `回车` 键

5. **重启 squid**

    执行以下命令重启 squid：

    ```bash
    sudo systemctl restart squid
    ```

<!-- --- -->

## 其他

### 如何获得允许使用的 IP？

本地笔记本连了 WiFi 上网，要使用安装在某云主机上的 squid 作为代理。可通过如下方式获得允许使用的 IP。

1. 在安装squid 的云主机上执行如下命令查看 squid 的 访问日志：

    ```bash
    sudo tail -f /var/log/squid/access.log 
    ```

2. 本地笔记本访问某个网站

    未将本地笔记本的 IP 加入 squid.conf 配置文件之前，通常会在浏览器中得到“拒绝访问”之类的错误。

3. 查看云主机 tail 命令界面的输出

    如下样例中的 `49.93.52.189` ，就是本地笔记本访问云主机 squid 代理时的 IP。

    ```shell
    ...
    1775447516.002      2 49.93.52.189 TCP_DENIED/403 3431 CONNECT www.baidu.com:443 - HIER_NONE/- text/html
    ...    
    ```

### 云主机要放通 3128 端口

如果 squid 是安装在云主机上，记得要放通 3128 端口（squid的默认端口）。即允许其他机器，可以访问该云主机的 3128 端口。如何放通，可查云主机相关文档，或者咨询AI。

如果不放通 3128 端口，则不能成功：squid.conf 按文档修改了，squid 服务也重启了，就是不生效。


<!--  -->
<span style="font-size:12px; color:#999">THE END</span>
