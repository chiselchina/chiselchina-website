# Chisel中文社区

该站点基于 [Hexo](https://hexo.io/) 并且基于[Corporate theme](https://github.com/ptsteadman/hexo-theme-corporate)构建而成。网站内容在 `src` 文件夹内，格式为 Markdown。欢迎 issue 或 pull request。

## 开发

``` bash
$ npm install
$ npm start # 开发服务器地址为 http://localhost:4000
```
## 部署

首先在[这里](https://github.com/settings/keys)将您的SSH公钥添加到github账号里。

运行：
```
hexo clean
hexo deploy
```
会自动生成网站并check in到`publish`分支。然后publish分支会通过webhook自动部署到web服务器。
