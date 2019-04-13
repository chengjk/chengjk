title: Hexo github pages 实践
date: 2016-11-26 12:33:41
tags: hexo
---
## Github 


**一个Github账号可不可以有多个Pages？**
可以 ,github支持一个个人主页和多个项目主页。个人主页地址是https://{usermame}.github.io; 项目主页的路径是 https://{username}.github.io/project. 个人主页和项目主页都可以自定义域名，方法一致。

**是否支持二级域名？**
支持常规二级域名，不支持通配符`*.example.com`。常用的是 `www`，顶级域名 `@`


 1. 创建 github repo。
 2. Setting > GitHub Pages>Source。选择 master branch。
 3. Setting > GitHub Pages>Theme chooser。选择一个jekyll主题,不选会使用默认空白主题。
 4. 下载空仓库到本地。 `git clone  git@github.com/chengjk/chengjk.github.com.git `


## Hexo
 1. 进入项目跟目录初始化hexo `hexo init`
 2. 添加 CNAME 文件 指向自己的域名 e.g. `blog.example.com`
 3. 创建 edit分支用于写作。hexo 默认deploy 到 master分支,master也是github的默认分支。在edit分支写作，该分支只存源码和配置。
 4. 编辑  .gitignore  排除工具和发布文件夹

	> .DS_Store
	> Thumbs.db
	> db.json
	> *.log
	> node_modules/
	> public/
	> .deploy*/
	> .git/

 5. 主题。 在themes 文件夹中 下载一款自己喜欢的主题，编辑_config.yml个人配置。 增加一个文件描述主题添加到版本管理，用于在其他环境写作。



接下来就可以在 edit分支写作，然后 hexo deploy到master分支。然后就可以在自己的域名下看到新写的文章了。

---
## 域名解析

记录类型| 主机记录|记录值
-|-|-
CNAME  | www| {username}.github.io

记录类型为A的记录值是ipv4，CNAME的记录值是域名。主机记录就是二级域名，常用默认是www，直接用顶级域名配 @，二级域名不支持通配`*`。

我们既然是Github Pages, 就选CNAME，把值设置为{username}.github.io. 当域名dns解析状态为正常时，就可以用了。
---
