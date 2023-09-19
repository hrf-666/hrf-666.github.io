---
title: Hexo如何置顶文章
date: 2023-09-04 10:59:25
updated: 2023-09-05 10:59:25
categories:
  - 笔记
  - 前端
tags:
  - 笔记
  - 前端
  - Hexo
---

# Hexo如何置顶文章
<!--more-->
## 1. 需要主题支持
   3-hexo主题
## 2. 安装插件
   ``` js
   npm install hexo-generator-topindex --save
   ```
## 3. 设置置顶
   给需要置顶的文章加入top参数，如下：
```markdown 
 ---
title: Hexo如何置顶文章
date: 2023-01-23 11:41:48
top: 1
categories:
- 运维
  tags:
- linux命令
---
```

> 如果存在多个置顶文章，top后的参数越大，越靠前。



