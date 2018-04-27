# chengjk.github.com

my private bolg.

edit 分支用于编辑，更新后 `hexo deploy` 发布到 master   更新页面。

更新：
1. 下载仓库 
2. 下载主题
``` sh
git co edit
cd themes
git clone $(cat remotes.txt) 

```
3. 更新主题参数。 themes 目录下的_config.yml 的参数复制到主题文件夹。
4. 编写,发布

```sh
hexo new xxx
hexo clean 
hexo g
# preview
hexo s

#deploy
hexo deploy

```

