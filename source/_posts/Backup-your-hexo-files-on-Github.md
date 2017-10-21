---
title: backup your Hexo files on Github
date: 2017-10-18 17:32:18
categories: Tech
tags:
- Hexo
- github
---
Since you have create your website using github. Here is the way that you **backup** your files so that you can write your blog *anywhere*.

### Steps
1. clone your github repository  
```
git clone git@github.com:BestJuly/BestJuly.github.io.git
```
2. create a new branch named `hexo` and copy files here   
```
git branch hexo
git checkout hexo
cp [files] ./
```
3. push to Github
```
git add*
git commit -m "add branch hexo"
git push --set-upstream origin hexo
```
4. generate and deploy your website
```
hexo generate
hexo deploy
```
Hence, you have a repository. Branch `master` is used to store the website and branch `hexo` is used to store the codes that generate the website.

### update your website on a new computer
1. clone your github repository and switch to branch `hexo`
```
git clone git@github.com:BestJuly/BestJulyk.github.io.git
git checkout hexo
```

2. install necessary things
```
npm install hexo
npm install
npm install 
hexo-deployer-git
```

3. Edit your files
4. Update files on Github
```
git add *
git commit -m "*"
git push origin hexo
```
5. Deploy your website
```
hexo generate
hexo deploy
```

> reference: http://crazymilk.github.io/2015/12/28/GitHub-Pages-Hexo%E6%90%AD%E5%BB%BA%E5%8D%9A%E5%AE%A2/#more