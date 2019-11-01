----
![image](https://github.com/Tuple-list/JavaScript-Study/blob/master/pic/mountains-1412683.svg)
![pic](https://img.shields.io/badge/lable-study-brightgreen)

## 声明
+ const命令：  声明常量  
+ let命令：  声明变量  
> 作用  
 + 作用域
   - 全局作用域 
   - 函数作用域 **function(){}**  
   - 块级作用域 {}  
 + 作用范围 
   - **var** 命令 在全局代码中执行 
   - **const命令** 和 let命令只能在代码中执行 
 + 赋值使用 
   - const命令声明常量后必须立马赋值 
   - let命令声明变量后可立马赋值或使用时在赋值 
 + 声明方法 
   var, const, let, function,  class, import  
 > 重点难点 
 
 + 不允许重复声明  
 + 未定义就使用会报错：const命令和let命令不存在变量提升 
 + 暂时性死区： 在代码内使用let命令声明变量之前，该变量都不可用 
 ----
 
 ## 解构赋值  
 
   + 字符串解构：const[a, b, c, d, e] = "hello" 
   + 数值解构： const{toString: s} = 123 
   + 布尔值解构： const{toString: b} = true 
   + 对象解构 
     - 形式：  const {x, y} = {x: 1, y: 2}  
     - 默认：  const{x, y = 2} = {x:1} 
     - 改名：  const {x, y: z} = {x: 1, y: 2}
   + 数组解构 
     - 规则： 数据机构具有Interator接口 可采用数组形式的解构赋值 
     - 形式： const[x, y] = [1, 2] 
     - 默认： const[x, y = 2] = [1] 
   + 函数参结构 
     - 数组结构
     
     
