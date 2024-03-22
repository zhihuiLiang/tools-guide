# 博客搭建教程
+ *ref*: https://www.bilibili.com/video/BV1ts4y1f7Gu/?spm_id_from=333.337.search-card.all.click&vd_source=4c36fed0ac4fc28cd70d870cf1efa09b
## 安装必备软件
+ git
+ Node.js（长期维护版本）
+ Hexo(博客框架)
### Hexo安装步骤
+ 新建一个文件夹
+ 打开`gitbash`，运行以下命令
```
npm install hexo-cli -g
hexo init blog
cd blog
npm install
hexo server
```
 ## 编写个人博客
 + 打开`gitbash`, 运行`hexo new "文章标题"
 + 编辑生成的md文件
 + 运行'hexo g'生成网页
 + 运行'hexo server' 生成博客
 ## 更改博客样式
 + 在hexo官网底部进去探索主题，选中主题到github主题，里面有博客配置指南
 + 在本地文件`blog`目录下克隆主题
 + 在`_config`更换博客主题
 ## 修改主题配置
 可修改`themes/主题名`文件夹的`_config`文件修改主题样式
 ## 注册`gitee`账号
 + 实名`gitee`账号
 + 新建仓库，路径需要输入个人空间地址
 + 配置ssh密钥
 + 在博客根目录`_config`中的`deploy`字段下添加
 ```
  type: 'git'
  repository: <git地址>
 ```
+ 在博客根目录打开一个`gitbash`窗口，运行
`npm install hexo-deployer-git --save`
将博客部署到`gitee`中
+ 运行`hexo g`生成博客
+ 运行`hexo d`部署博客
+ 打开gitee的仓库，点击`管理`仓库开源，点击`服务`打开`gitee pages`
## 修改博客
+ 可以运行`hexo clean`清理缓存