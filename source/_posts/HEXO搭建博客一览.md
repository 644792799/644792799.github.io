title: Hexo在Gitpage搭建博客步骤一览
tags: Hexo,Gitpage
---
# Hexo在Gitpage搭建博客步骤一览 #

> 基于SSH方式搭建

* 1：创建仓库github_username.github.io  （注意：这里需要 用户名.github.io）
* 2: 本地创建文件夹和仓库同名
      mkdir github_username.github.io
* 3：使用gitbash进入文件夹
      cd github_username.github.io
* 4：执行
      npm install hexo
      hexo init
      npm install
      npm install hexo-deployer-git --save
* 5：修改_config.yml中的deploy参数
      deploy:
        type: git
        repo: git@github.com:github_username/github_username.github.io.git #SSH地址
        branch: master #发布到master分支
* 6：启动ssh-agent
      eval $(ssh-agent -s)
* 7：添加SSH key到ssh-agent
      ssh-add ~/.ssh/id_rsa
* 8：初始化git并提交
      git init
      git checkout --orphan gh-pages #创建分支 下面所有步骤在该分支下完成
      git add .
      git commit -m "first commit"
      git remote add origin git@github.com:github_username/github_username.github.io.git
      git push -u origin ph-pages
* 9：执行
      hexo generate -d    
  生成网站并部署到GitHub上

  ---

>为什么之前很多人写了教程这里还要重新再写一次步骤

  正因为网上很多教程踩了不少的坑，最后发现还是官方文档靠谱

  __问：按照网上正确的步骤创建好了工程并发布正确了为什么gitpage访问还是404？__

  答：创建项目的名字必须是`用户名.github.io`这种结构

  __问：生成了SSH KEY Github上也配置好了，为什么PUSH的时候提示key没有授权？__

  答：步骤6、7解决了以上问题

  __问：修改了HEXO主题为什么发布后没有变化？__

  答：提交部署前先执行 `hexo clean`

  ---
