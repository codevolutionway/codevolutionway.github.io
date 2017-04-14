# Hexo配置搭建
## Hexo安装
* git环境
```
npm install hexo-generator-index --save
npm install hexo-generator-archive --save
npm install hexo-generator-category --save
npm install hexo-generator-tag --save
npm install hexo-server --save
npm install hexo-deployer-git --save
npm install hexo-renderer-marked@0.2 --save
npm install hexo-renderer-stylus@0.2 --save
npm install hexo-generator-feed@1 --save
npm install hexo-generator-sitemap@1 --save


cnpm install hexo -server --save
```
* node.js环境

## hexo常用命令
```
//hexo版本信息
hexo -v
//初始化一个hexo
hexo init
//生成静态文件
hexo generate
hexo g
//启动本地服务，-p自定义端口(福昕PDF默认端口为4000与hexo冲突)
hexo server
hexo s -p 5000
//部署网站，使用_config.yml中的配置commit
hexo deploy
hexo d
//新建一篇文章，如果没有设置 layout 的话，
//默认使用 _config.yml 中的 default_layout 参数代替。
//如果标题包含空格的话，请使用引号括起来。
$ hexo new [layout] <title>
```

## hexo部署
首次hexo deploy部署前，需要安装插件
否则如下显示：
```
WAY@WAY-PC MINGW64 /f/Hexo (hexo)
$ hexo d
ERROR Deployer not found: git
//需要安装 hexo-deployer-git
npm install hexo-deployer-git --save
```

## Hexo版本
``` shell
Administrator@WAY-PC MINGW64 /e/hexo (hexo)
$ hexo version
hexo: 3.2.2
hexo-cli: 1.0.2
os: Windows_NT 6.1.7601 win32 x64
http_parser: 2.5.2
node: 4.4.4
v8: 4.5.103.35
uv: 1.8.0
zlib: 1.2.8
ares: 1.10.1-DEV
icu: 56.1
modules: 46
openssl: 1.0.2h
```

## 利用git解决hexo博客多PC间同步问题
新建git仓库时，创建分支hexo，将分支hexo作为默认仓库，hexo文件夹映射到该仓库
/hexo/.gitignore 配置屏蔽发布生成文件
```
.DS_Store
Thumbs.db
db.json
*.log
node_modules/
public/
.deploy*/
.deploy_git/
```

```shell
Administrator@WAY-PC MINGW64 /e/hexo (hexo)
$ git remote show hexo
* remote hexo
  Fetch URL: https://github.com/imwyw/imwyw.github.io.git
  Push  URL: https://github.com/imwyw/imwyw.github.io.git
  HEAD branch: hexo
  Remote branches:
    hexo   tracked
    master tracked
  Local branch configured for 'git pull':
    hexo merges with remote hexo
  Local ref configured for 'git push':
    hexo pushes to hexo (up to date)

```

/hexo/_config.yml 配置发布为git仓库master分支
```
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repo: https://github.com/imwyw/imwyw.github.io.git
  branch: master
```

* 综上
实现了 `hexo g` 直接发布,`git commit` 直接提交
多PC间，首次使用hexo init后git pull拉取更新，后续正常使用即可。
