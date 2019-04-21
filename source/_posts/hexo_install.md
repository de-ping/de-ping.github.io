title: 笔记：利用Hexo+github创建个人博客
tags: []
categories: []
date: 2019-04-20 18:09:00
---
### 1. 软件安装  

参考：[用Github+Hexo搭建你的个人博客：搭建篇](https://www.makcyun.top/hexo01.html)
    
    sudo apt-get install nodejs  
    sudo apt-get install npm  
    sudo apt-get install git  
    npm install -g hexo  
    npm install -g hexo-cli  
    npm install hexo-deployer-git --save 

### 2. 软件配置 
    
    hexo init blog  
    cd blog  
    npm install 
    
查看效果,首先启动hexo
     
     hexo s -g
     
然后在浏览器中查看
    
    http://localhost:4000

<!--more-->
	
### 3. Github设置  

参考：[小白独立搭建博客--Github Pages和Hexo简明教程](https://my.oschina.net/ryaneLee/blog/638440)

- 注册gibhub，创建一个名为username.github.io的repository,在setting里，选择GitHub Pages，choose a theme

- 将博客部署到Github Pages上  
      
      ssh-keygen -t rsa -C "your_email@example.com"
      copy ~/.ssh/id_rsa.pub to github
      ssh -T git@github.com
      
      git config --global user.name "username"
      git config --global user.email  "your_email@example.com"
      vi blog/_config.yml
      ...
      deploy:
        type: git
        repository: git@github.com:username/username.github.io.git
        branch: master
      ...
      
      hexo clean
      hexo d -g
      
### 4. 美化博客

参考：[用Github+Hexo搭建你的个人博客：美化篇](https://www.makcyun.top/hexo02.html)  

- 使用新主题,设置语言及网站信息
      
      cd blog/themes
      git clone https://github.com/iissnan/hexo-theme-next themes/next
      vi blog/_config.yml
      ...
      theme: hexo-theme-next
      title: Welcome
      subtitle:
      description:
      keywords:
	  author: deping
	  language: zh-CN
	  timezone:
      ...
- 选择Scheme

     修改blog/themes/hexo-theme-next/_config.yml
      scheme: Pisces

- 新建标签、分类、关于页面

      hexo new page "tags" 
	  hexo new page "categories"  
	  hexo new page "about"
      
     修改blog/themes/hexo-theme-next/_config.yml
      menu:
      home: / || home
      about: /about/ || user
      tags: /tags/ || tags
      categories: /categories/ || th
      archives: /archives/ || archive
      #schedule: /schedule/ || calendar
      #sitemap: /sitemap.xml || sitemap
      #commonweal: /404/ || heartbeat

- 页脚设置,隐藏powered By Hex,next version,显示总访客数和总浏览量  

修改blog\themes\hexo-theme-next\layout_partials\ footer.swig  

- 添加阅读全文  

在必要的地方添加<\!-- more -->即可  

### 5. 使用hexo-admin  

    npm install --save hexo-admin
    hexo s
 http://localhost:4000/admin


### 6. 备份hexo  

    npm install hexo-git-backup --save

修改blog/_config.yml  

    backup:
     type: git
     message: hexo blog source
     repository: github: git@github.com:username/username.github.io.git,source
     
     hexo b