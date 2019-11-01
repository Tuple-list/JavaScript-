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
    - getAttribute		获取元素节点中指定属性的属性值	
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
   + 匈牙利命名法： 变量名 = 类型 + 对象描述
	   - Int	
		 - Float	
		 - Boolean	
		 - String	
		 - Array	
		 - Object	
		 - Function	
		 - Regular Expression 正则	
	 + 驼峰命名法	
	   - 全部小写  单词之间用下划线分割
           - 大小写混合
	     - 大驼峰 每个单词首字母大写
	     - 小驼峰 第一个单词首字母小写，其他首字母大写	
  + 规则
  

   
     
      
    
