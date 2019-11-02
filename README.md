## JS知识图谱
---
---


### 一. 数组

  1.创建方法
  + 空数组： var obj = new Array();		 
  + 指定长度数组  var obj = new Array(size);		
  + 指定元素数组  var obj = new Array(元素1， 元素2 ...);			
  + 单维数组  var obj =[元素1, 元素2 ...];	
  + 多维数组  var a = new Array([数组序列1], [数组序列1]...);			
  
  2.基本操作
  + 存取数据元素
    - 单维数组  数组名[下标索引];
    - 多维数组  数组名[外层数组下标][内层元素下标];
    - 特性  数组长度是弹性的，下标从0开始 数组元素可添加到对象中
  + 增加数组  使用"[]"运算符指定一个新目标
  + 删除数组  delete 数组名[下标];	
  + 遍历数组  for( var 数组元素变量 in 数组)	
  
  3.数组属性
  + constructor  引用对象的构造函数
  + length  返回数组长度
  + prototype 通过增加属性和方法扩展数组定义
  
---
### 二. JS DOM 操作
   + 1.获取节点   
   
     document	
      - getElementById 【documet.getElementById(元素ID)】  通过元素ID获取节点	
      - getElementsByName  通过元素的name属性获取节点	 
      - getElementsByTagName 通过元素标签获取节点	
      
     节点指针 
      - firstChild 【父节点.firstChild】  获取元素的首个子节点
     
      - lastChild  获取元素最后一个节点	
     
      - childNodes 获取元素子节点列表	
     
      - previousSibling  获取已知节点的前一个节点	
     
      - parentNode 获取已知节点的父节点	
	 
  + 2.节点操作  
    创建节点 
    - createElement 【document.createElement（元素标签）】  创建元素节点
    - createAttribute 创建属性节点
    - createTextNode  创建文本节点
    
    插入节点  
    - appendChild 【appendChild（所添加的新节点）】  向节点的子节点列表的末尾添加新子节点
    - insertBefore 在已知子节点前插入一个新子节点
    
    替换节点  
    - replaceChild  【replaceChild（要插入的新元素，被替换的老元素）】将某个子节点替换为另一个
    
    复制节点  
    - cloneNode 【需要被替换的节点.cloneNode(true/false)】 创建指定节点副本 true：复制所有子节点 false：仅复制当前节点  
    
    删除节点  
    - removeChild 删除指定节点
    
  + 3.属性操作
    获取属性	
    - getAttribute	获取元素节点中指定属性的属性值	
    设置属性	
    - setAttribute	创建或改变元素节点的属性	
    删除属性	
    - removeAttribute	删除元素中的指定属性		
  + 4.文本操作  
    - insetData(offset, String)	从offset指定的位置插入string	
    - appendData(string)	将string 插入到文本节点的末尾处	
    - deleteData(offset, count)	从offset起删除count个字符	
    - replaceData(off, count, string)	从offset将count个字符用string替代
    - splitData(offset)	从offset起将文本节点分成两个节点	
    - substring(offset, count)	返回由off起的count个节点
  
---
### 三.JS变量	
1.命名
   + 方法	
     + 大驼峰  每个单词首字母大写	 
     + 小驼峰  第一个单词首字母小写,其他首字母大写				 
   + 规则		
     + 首字符 字母或下划线	
     + 组成 字母，数字，下划线	
     + 禁忌 JS关键词与保留字		
     
2.声明
  + 显示声明  **var 变量名**  
  + 陋习  
    + 没有类型  
    + 重复声明  
    + 隐式声明  
    + 不声明直接赋值  
  + 正解  
    + 先声明，后读写  
    + 先赋值，后运算  
3.变量类型  
  + 值类型  
    + 占用空间固定，保存在栈中
    + 保存与复制的是**值本身**  
    + 使用typeof检测数据类型  
    + 基本类型数据是值类型  
  + 引用类型  
    + 占用空间固定，保存在栈中  
    + 保存与复制的是指向**对象的一个指针**  
    + 使用instanceof 检测数据的类型  
    + 使用new()方法构造出的对象是引用型  
    
4.作用域   
  + 全局变量    
    + 包含
      在函数体外定义的变量    
      在函数体内部定义的无var的变量  
    + 调用  
      任何位置   
  + 局部变量   
    + 包含  
      在函数内部使用var 声明的变量  
      函数的参数变量  
    + 调用  
      当前函数体内部  
  + 优先级  
    + **局部变量**高于**同名全局变量**  
    + **参数变量**高于**同名全局变量**  
    + **局部变量**高于**同名参数变量**  
  + 特性  
    生命周期  
      全局变量  &nbsp 除非被显示删除，否则一直存在  
      局部变量  &nbsp 自声明起至函数运行完毕或被显示删除  
      回收机制  &nbsp （标记清除，引用计数）  
    作用域链
      内层函数可访问外层函数局部变量  
      外层函数不能访问内层函数的局部变量  
    局部变量是调用对象的属性  
    全局变量是全局对象的属性  
    忽略块级作用域  
  
---
### 四.JS函数基础  
1.定义方法  
+ 静态方法  
```
function 函数名([虚参列表]){
    函数体;
    [return[函数返回值]]
}
```
+ 动态匿名方法  
  var 函数名 = new function(["虚参列表"], "函数体");  
+ 直接量方法  
  ```函数名 = function(["虚参列表"]{
      函数体;
  })
  ```
2.调用方法  
  + 直接调用  
    函数名(实参列表)
  + 在连接中调用  
    <a href="javascript: 函数名()">text</a>  
  + 在事件中调用  
    事件类型 = "函数名()"  
  + 递归调用  
    + 定义： 在函数体内部调用函数自身  
    + 格式
    ```
    function 函数名(){
        代码
	
	
    }
    ```
      
    
      
	
  

   
     
      
    
