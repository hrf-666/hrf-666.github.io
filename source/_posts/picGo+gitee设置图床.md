---
title: picGo+gitee设置图床
date: 2023-08-24 10:58:25
categories:
  - 笔记
tags:
  - 笔记
---


@[TOC](picGo+gitee+typora设置图床)

#   picGo+gitee设置图床



> 当我了解picGo+gitee可以设置图床的时候，我决定试一试。
>
> 考虑github国外网站比较慢，我使用的是gitee进行部署。
>
> 如果是个人博客需要考虑设备外链，有可能图片显示不成功。



##  下载picGo软件

[PicGo官方网址](https://picgo.github.io/PicGo-Doc/zh/)

以上有配置说明

百度网盘链接：https://pan.baidu.com/s/1MHxXIOVRiAZqiPJv6jydxw?pwd=8888 
提取码：8888

##  安装picGo软件

> 选中自己想要安装的目录后一直点击下一步就好了

##  gitee操作

###  在gitee中创建仓库

> 直接创建就好了，这里就不截图片了。

###  在gitee中配置私人令牌

![image-20230825101809644](https://huang-ruifang.gitee.io/pic-go/public/csdn/image-20230825101809644.png)



创建一个私人令牌，全选就好了，其中token别忘记复制保存一下。

![image-20230825102021285](https://huang-ruifang.gitee.io/pic-go/public/csdn/image-20230825102021285.png)

##  配置picGo

###  在插件设置中搜索gitee插件并进行下载

我下载的是这个

![image-20230825102223142](https://huang-ruifang.gitee.io/pic-go/public/csdn/image-20230825102223142.png)

进行图床设置

![image-20230825102712490](https://huang-ruifang.gitee.io/pic-go/public/csdn/image-20230825102712490.png)

picGo设置

> 里面可以自定义设置
>
> 设置语言，
>
> 设置日志文件：可以只选择错误和提醒
>
> 设置server： 设置端口号等

picGo上传区进行上传图片

![image-20230825103231880](https://huang-ruifang.gitee.io/pic-go/public/csdn/image-20230825103231880.png)

相册能够显示图片

![image-20230825103255186](https://huang-ruifang.gitee.io/pic-go/public/csdn/image-20230825103255186.png)

以上配置完成

##  Typora+picGo设置

### Typora 下载

[Typora 官方中文站 (typoraio.cn)](https://typoraio.cn/)

百度网盘链接：https://pan.baidu.com/s/1sXFt1eSKLoCSLHmpEe80VQ?pwd=8888 
提取码：8888

###  Typora进行图像设置

![image-20230825103513332](https://huang-ruifang.gitee.io/pic-go/public/csdn/image-20230825103513332.png)

> 编写md文件时，在图片上右击直接上传到gitee仓库中

本地的图片就可以上传到gitee中了，无论你把这个md文件发给谁他就可以看见图片了，不需要再考虑路径的问题啦。
