title: Hexo github pages 实践
date: 2016-11-26 12:33:41
tags: hexo
---

1. 创建 github repo。
2. Setting > GitHub Pages>Source 选择 master branch
3. 下载仓库到本地。 `git clone  git@github.com/chengjk/chengjk.github.com.git `
4. 初始化。hexo
5. 添加 CNAME 文件 指向自己的域名 e.g. `chengjk.com`
6. 创建 edit分支。hexo deploy 默认deploy master分支,这也是github的默认分支，我们用了部署。写作使用edit分支，只存源码和配置。
7. 编辑  .gitignore  排除工具和发布文件夹

	> .DS_Store
	> Thumbs.db
	> db.json
	> *.log
	> node_modules/
	> public/
	> .deploy*/
	> .git/

8. 主题。 在themes 文件夹中 下载一款自己喜欢的主题，编辑_config.yml个人配置。 增加一个文件描述主题添加到版本管理，用于在其他环境写作。

揭下来就可以在 edit分支写作，然后 hexo deploy到master分支。然后就可以在自己的域名下看到新写的文章了。
