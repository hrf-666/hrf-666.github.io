---
title: 判断数组对象中某一属性是否包含重复的值
date: 2023-09-11 10:58:25
categories:
  - 笔记
  - 前端
tags:
  - 笔记
  - 前端
---

@[TOC](js判断数组对象中某一属性是否包含重复的值)

#  js判断数组对象中某一属性是否包含重复的值


> 当我想判断js数组对象中某一属性是否包含重复的值，有几种方法。

<!--more-->
## 1, 使用set,map实现；

```js
let arr = [{
    "name" : "张三",
    "id" : 1
    },{
    "name" : "李四",
    "id" : 3
    },{
    "name" : "张三",
    "id" : 2
}];

let names = arr.map(item => item["name"]);
let nameSet = new Set(names);

if (nameSet.size == names.length) {
    console.log("没有重复值");
} else {
    console.log("有重复值");
}
```


##  2.使用标识判断是否存在；

```js
/**
* @param arr 如：var arr = [{name: "123", age : 123}, {name:"1234432", age : 1234324}]
* @param key 如："name"
*
* @retutns boolean: true：不存在； false：存在重复
  **/
  function isRepeat(arr, key) {
      var obj = {};
      for (let i = 0; i < arr.length; i ++) {
          if (obj[arr[i][key]]) {
            return false;    // 存在
          } else {
            obj[arr[i][key]] = arr[i];
          }
      }
      return true;
  }
  ```
##  3, 双层循环

```js
/**
* @param arr 如：var arr = [{name: "123", age : 123}, {name:"1234432", age : 1234324}]
* @param key 如："name"
*
* @retutns boolean: true：不存在； false：存在重复
  **/
  function isRepeat(arr, key) {
      for (let i = 0; i < arr.length; i ++) {
          for (let j = i + 1; j < arr.length; j ++) {
              if (arr[i][key] == arr[j][key]) {
                return false;
              }
          }
      }
      return true;
  }
  var arr = [2, 3, 1, 5, 7,6, 4,9, 8];
for (let i = arr.lengtgh; i >= 0; i --) {
    for (let j = 0; j < i; j ++) {
        if (arr[j] > arr[j + 1]) {
        var temp = arr[j];
        arr[j] = arr[j + 1];
        arr[j + 1] = temp;
        }
    }
}
```



