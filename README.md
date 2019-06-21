# Chisel中文社区

该站点基于 [Hexo](https://hexo.io/) 并且基于[Corporate theme](https://github.com/ptsteadman/hexo-theme-corporate)构建而成。网站内容在 `src` 文件夹内，格式为 Markdown。欢迎 issue 或 pull request。

## 开发

``` bash
$ npm install
$ npm start # 开发服务器地址为 http://localhost:4000
```

本网站使用了jupyter notebook的内容，所以需要安装[hexo-jupyter-notebook插件](https://www.npmjs.com/package/hexo-jupyter-notebook)：

假设您已经安装好了python3。

第一步：

进入自己的hexo目录，安装： `npm install hexo-jupyter-notebook --save`


第二步：

安装pandoc: `sudo apt-get install pandoc`

安装nbconvert: `pip install nbconvert`

第三步：

打开hexo的配置文件 _config.yml， 把里面的`post_asset_folder: false`改为`true`

把用jupyter notebook写的内容保存为.ipynb格式的，存放到文章的asset目录中。

在需要插入的展示jupyter的地方写入：

<script src="/metronic/assets/plugins/jquery.min.js"></script>
{% asset_jupyter python3 your_jupyter_notebook.ipynb %}

然后就可以在hexo文章中显示jupyter-notebook。

## 部署

首先在[这里](https://github.com/settings/keys)将您的SSH公钥添加到github账号里。

运行：
```
hexo clean
hexo deploy
```
会自动生成网站并check in到`publish`分支。然后publish分支会通过webhook自动部署到web服务器。
