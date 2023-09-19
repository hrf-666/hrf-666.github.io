---
title: easyui tree combotree去掉默认图标或更换图标
date: 2023-09-04 10:58:25
categories:
  - 笔记
  - 前端
tags:
  - 笔记
  - 前端
---

@[TOC](easyui tree combotree 去掉默认图标)

#   easyui tree combotree去掉默认图标或更换图标


> 当我使用easyui插件编写项目的时候，我想把前面的图标去除或更改图标

<!--more-->
##  图标操作
###  1、加载Tree
```js
$("#cc").combotree({
     url: '/Pillars/GetChildAll',				//请求地址
     method: 'post',							//请求方式
     queryParams: { UnitType:'-1,3,4,5,6'},		//参数
     valueField: 'id',							//tree绑定的value值
     textField: 'text',							//tree显示的text文本
     required: true,							//是否必填(true/false)
     editable: false,							// 不能直接输入到列表框
});

```
###  2、Tree加载完成后运行
```js
onLoadSuccess: function () {
    $('#cc').combotree('tree').tree("collapseAll");	 //全部关闭
    $(".tree-icon,.tree-file").removeClass("tree-icon tree-file");//去掉最后一级图标
    $(".tree-icon,.tree-folder").removeClass("tree-icon tree-folder tree-folder-open tree-folder-closed");//去掉所有父级图标
}

```
###  3、Node展开后运行
```js
onExpand: function(node){
	$('.tree-title').prev().removeClass("tree-folder-open");
 	$('.tree-checkbox,.tree-checkbox0').prev().removeClass("tree-folder-open");
}
```

##  修改图标
###  使用css
```js
 <style>
    /*默认*/
    .tree-icon {
        background: url('../../../images/topology/端口-1.svg') no-repeat center center !important;
    }

    /*折叠时图片*/
    .tree-folder {
        background: url('../../../images/topology/物理地址.svg') no-repeat center center !important;
    }

    /*展开时图片*/
    .tree-folder-open {
        background: url('../../../images/topology/物理地址.svg') no-repeat center center !important;
    }
    </style>
```

> 当然还有很多种方法,针对特定的场景进行编码，有用到再填充这个文档



