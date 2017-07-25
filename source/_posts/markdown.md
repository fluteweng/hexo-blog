title: markdown的使用
tags: []
categories: []
date: 2017-07-21 16:14:00
---

**[markdown官方文档地址](https://daringfireball.net/projects/markdown)**
### 标签列表 ###

##### 1. 标题 #####
  标题分为六级，分别对应html的h1~h6标签
  > 一级标题写法
  ```
  一级标题
  =======
  
  # 一级标题 #
  ```
  >二级标题写法
  ```
  二级标题
  ---

  ## 二级标题 ##
  ```
  >三至六级标题写法
  ```
  ### 三级标题 ###
  #### 四级标题 ####
  ##### 五级标题 #####
  ###### 六级标题 ######
  ```
##### 2. 字体 #####
  字体有两种：粗体、斜体
  修饰符有两种：“_”和"*"
  >字体写法
  ``` 
  *斜体*
  _斜体_

  **粗体**
  __粗体__

  ***粗斜体***
  ___粗斜体___
  ```
##### 3. 链接和图片 #####
  链接有两种写法
  >链接写法
  ``` 
  
    // title 单双引号均可以
    文字链接 [Some one's blog](https://fluteweng.github.io 'Some one's blog') 
    网站链接 <https://fluteweng.github.io>


    // title 只可以为双引号
    文字链接的另一种写法  [Some one's blog][1]
    [1]: https://fluteweng.github.io "Some one's blog"
  ```
  图片也有两种写法
  >图片写法
  ```
  图片链接 ![Baidu logo](http://www.baidu.com/img/baidu.svg '百度logo')

  图片链接的另一种写法 ![Baidu logo][2]
  [2]: http://www.baidu.com/img/baidu.svg "百度logo"

  // 原生html写法，可以使用html标签去控制图片属性
  <img src="http://www.baidu.com/img/baidu.svg" width="400" height="100">
  ```

##### 4. 列表 #####
  列表有两种，有序和无序，有序修饰符一种，无序列表修饰符有3种
  >有序的写法
  ``` 
    // 阿拉伯数字加英文版句号“.”加空格，阿拉伯数字不代表序号，序号由书写顺序决定
    3. 有序列表1
    2. 有序列表2
    1. 有序列表3

    // 页面将会显示为
    1. 有序列表1
    2. 有序列表2
    3. 有序列表3
  ```
  >无序的写法
  ```
    // “*” “+” 或者 “-” 加空格 表示无序列表
    * 无序列表1
    + 无序列表2
    - 无序列表3
     - 子无序列表
  ```
##### 5. 段落引用 #####
  >段落引用的写法
  ```
  >引用部分
  >>二级引用
  >>>>>>>多级引用
  ```
##### 6. 代码引用 #####
  >代码引用写法
  ```
    // "`"为键盘左上角~的按键，实际使用时 ``` 后不要加空格
    ``` 
    引用代码片段
    ``` 
    // 添加语言的语法高亮
    ```javascript 
      function(){
        console.log("I'm javascript code")
      }
    ``` 
    ```python 
    #!/bin/env python
    def main():
      print "I'm python code"
    ``` 
  ```
  
##### 7. 其他 #####
分隔符
  >分隔符写法
  ```
    // 中间空一行
    分隔符前

    ---
    分隔符后
  ```
引用段落不延续
 >不延续的写法
  ```
    // 中间空一行
    >第一行
    延续行

    不延续行

    >第一行
    延续行

    >含空行的延续行
  ```
转义字符
  ```
  \*非斜体\*
  \*\*非粗体\*\*
  ```

其他相关链接：
  <http://www.appinn.com/markdown>
  <http://www.cnblogs.com/hnrainll/p/3514637.html>
  <https://segmentfault.com/markdown#articleHeader12>