---
title: Create your blog on github by Hexo
date: 2017-10-08 19:24:32
categories: Tech
tags:
- Hexo
- github
---
> reference: http://wuxiaolong.me/2015/07/31/build-blog-by-hexo/

### Requirements
* Platform: Windows 10 for this doc.
* [Git](https://git-for-windows.github.io/)
* [Node.js](https://nodejs.org/en/)
* hexo: `npm install -g hexo`

### Hexo
#### Initialize
```bash
cd $YOUR_PATH
mkdir hexo
cd hexo
hexo init
npm install
```
If you want to see the website on local computer, the following code will help you.
```bash
hexo generate
hexo server
```
After that, you can review your website on `localhost:4000`

#### Github settings
1. Create a repository named yourname.github.io
2. Add deploy settings in `_config.yml`, an example is shown as follows.
```yml
deploy:
  type: git
  repo: git@github.com:BestJuly/BestJuly.github.io
  branch: master
```

#### Deploy
```bash
hexo generate
hexo deploy
```
If you have the problem: `Deployer not found: git`
```bash
npm install hexo-deployer-git --save
hexo deploy
```