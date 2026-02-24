# Claude Code


## 安装

### 方法一：通过 npm 安装 

安装过程请参考文末 [参考资料](#参考资料) 之《Claude code 保姆级入门教程，不用学命令行（2025.12 月更新）》。

在 MacOS 中，如果之前在 VSCode 安装了 Claude Code 插件，则执行 npm install 命令会报错如下：

```bash
% npm install -g @anthropic-ai/claude-code --registry=https://registry.npmmirror.com

npm error code EACCES
npm error syscall mkdir
npm error path /usr/local/lib/node_modules/@anthropic-ai
npm error errno -13
npm error Error: EACCES: permission denied, mkdir '/usr/local/lib/node_modules/@anthropic-ai'
...
```

此时在 npm install 命令前加上 sudo 即可。即执行 `sudo npm install -g @anthropic-ai/claude-code --registry=https://registry.npmmirror.com` 安装 Claude Code。

 <!-- "claudeCode.preferredLocation": "panel", -->

## 参考资料

- 15分钟Claude Code小白入门；https://b23.tv/2tMa14o
- Claude code 保姆级入门教程，不用学命令行（2025.12 月更新）；https://zhuanlan.zhihu.com/p/1985832650116715724