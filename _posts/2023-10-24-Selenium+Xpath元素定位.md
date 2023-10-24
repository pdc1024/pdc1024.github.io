---
layout:     post
title:      Selenuim中使用xpath定位
subtitle:   Xpath特殊定位
date:       2023-10-24
author:     Pan Decai
header-img: img/post-bg-swift2.jpg
catalog: true
tags:
    - Xpath
---

# Selenium + Xpath 定位

## 文本定位text()、contains()

```html
<a class="paging">上一页</div>
<a class="paging">1</div>
<a class="paging">2</div>
<a class="paging">下一页</div>
```

> 定位方法1: text()     -- 使用文本信息定位，定位文本内容为**下一页**的a标签

```python
from selenium.webdriver.common.by import By

page_next = driver.find_element(By.XPATH, '//a[text()="下一页")]')
```

> 定位方法2：contain()   -- 使用文本信息进行模糊定位，定位文本内容包含**下一页**的a标签

```python
from selenium.webdriver.common.by import By

#1、
page_next = driver.find_element(By.XPATH, '//a[contains(text(), "下一页")]')
#2、
page_next = driver.find_element(By.XPATH, '//a[contains(string(), "下一页")]')
```

## 相邻元素定位

```python
#前一位div标签：
preceding-sibling::div[1]
#后一位p标签：
following-sibling::p[1]
#前N位span标签：
preceding-sibling::span[N]
#后N位a标签：
following-sibling::a[N]
```

## 隔壁节点或者父节点  

> 参考链接  <[(隔壁节点或者父节点  xpath ](https://blog.csdn.net/weixin_43407092/article/details/108020924?)>

### 1、parent::*    获取父节点

```html
<a>
 
    <b></b>
 
</b>
```

> 路径表达式：//b/parent::a  表示获得b节点的父节点元素a节点

### 2、ancestor::*   获取祖先节点

```html
<a>
    <b>
        <c></c>
    </b>
</a>
```

> 路径[表达式](https://so.csdn.net/so/search?q=表达式&spm=1001.2101.3001.7020)：//c/ancestor::* 表示获得c节点的祖先节点元素a节点和b节点
>
> ​          //c/ancestor::a 表示获得c节点的祖先节点元素a节点

### 3、child::*   获取子节点

```html
<a>
    <b>
        <c></c>
    </b>
        <d></d>
</a>
```

> 路径表达式：//a/child::* 表示获得a节点的子节点元素b节点和d节点
>
> ​          //b/child::c 表示获得b节点的子节点元素c节点

### 4、descendant::*   获取后代节点 （子孙节点）

```html
<a>
    <b>
        <c></c>
    </b>
        <d></d>
</a>
```

> 路径表达式：//a/descendant::* 表示获得a节点的所有后代元素，除a以外的所以节点
>
> ​          //b/descendant::c 表示获得b节点的后代元素c节点

### 5、following::* 

```html
<a>
    <c>
       <e></e>
       <f></f>
    </c>
    <d></d>
</a>
<b></b>
```

 

> 路径表达式：//a/following::* 表示获得a节点后序的所有元素，此时只获得b节点
>
> ​          //a/c/following::* 表示获得a节点下的c节点后序的所有元素，此时获得d节点和b节点
>
> ​          //a/c/e/following::* 表示获得a节点->c节点->e节点后序的所有元素，此时获得f节点、d节点和b节点

### 6、preceding::*

> 获得节点前面的节点，和5用法刚好相反

### 7、following-sibling::*

> 获得紧邻的后一兄弟节点

### 8、preceding-sibling::*

