# JavaScript 学习笔记  

> ## 严格模式  
  ECMAScript5引入了严格模式（strict mode）概念，严格模式为JavaScript定义了一种不同的解析与执行模型，
  在严格模式下，ECMAScript3中的一些不确定行为会得到处理，并对某些不安全操作抛出错误。  
  
  对整个脚本启动严格模式，可以在顶部添加一个编译指示（pragma）：  
```
  "use strict";
```  
  指定函数在严格模式下执行：  
```
function doSomething(){
    "use strict";
    //函数体
}
```

> ## 变量  
  ECMAScript的变量是松散类型的，即可以用来保存任意类型数据。  
  变量可以在定义时初始化，也可以不初始化，如 var message; 未初始化的变量会保存一个特殊值——undefined;  
  变量赋值时不要求与之前的值类型一致，如：  
```
var message = "Hi";
message = 100;
```

  其实未初始化的变量，在给它赋值时，变量类型就是从undefined变为了其它类型。  
  使用var定义的变量将成为定义该变量的作用域中的局部变量。  
```
function test(){
    var message = "Hi";    //局部变量
}
test();
console.log(message);    //错误！局部变量在函数退出后已被销毁  
```

  而省略var操作符可以创建全局变量：  
```
function test(){
    message = "Hi";    //全部变量
}
test();    //注意：只有函数被调用之后，函数内部定义的变量才会被创建并赋值
console.log(message);     //输出Hi  
```

> **注意：给未经声明的变量赋值，在严格模式下会导致ReferenceError错误！**   

  可以在一条语句中定义多个变量，支持使用不同类型初始化变量：  
```
var message = "Hi",
    data,
    age = 20;
```  

> ## 数据类型  
  ECMAScript有5种基本数据类型：Undefined、Null、Boolean、Number和String，还有1种复杂数据类型：Object。  
  
+ typeof操作符  
  由于ECMAScript是松散类型的，可以使用typeof检测变量类型，可能的返回值包括：  
  "undefined"——值未初始化  
  "boolean"——值是布尔类型  
  "string"——值是字符串  
  "number"——值是数值  
  "object"——值是对象或者null  
  "function"——值是函数  
```
var message = "Hi";
var msg;
console.log(typeof message);
console.log(typeof(message));
console.log(typeof 3.14);
console.log(typeof msg);    //声明之后并未初始化值，类型是undefined
console.log(typeof msg1);    //对于未声明的变量，类型依旧是undefined
console.log(typeof null);    //对象或者null，类型是object
console.log(typeof undefined);    //undefined类型是undefined
console.log(typeof /\w/)    //正则表达式类型是object
function test(){}
console.log(typeof test)    //函数类型是function，以与普通对象区分  
```  
 
```
[输出]
string
string
number
undefined
undefined
object
undefined
object
function
```  

+ Undefined类型  
  Undefined类型包含的可能值只有1个：undefined。  
+ Null类型  
  Null类型也只有1个值：null。  
  null表示一个空对象指针，所以typeof null返回的是object。  
  实际上，undefined类型是派生自null值的，所以对他们的相等性测试会返回true：  
  ```
  console.log(null == undefined);  [输出] true  
  ```  
  任何情况下，都没有必要将一个变量的值显式设定为undefined；  
  而如果一个变量是用来存储对象的，在初始化时最好明确赋给null值，以区分null和undefined。  
+ Boolean类型  
  Boolean类型包含2个值：true和false。  
  ECMAScript中的所有类型的值，都可以调用转型函数Boolean()转换为Boolean值  
  各数据类型转为Boolean值的规则:  
  
  <table>
  <thead>
    <tr>
      <th align="center" style="color: red"}>数据类型</th>
      <th align="center">返回true</th>
      <th align="center">返回false</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Boolean</td>
      <td align="center">true</td>
      <td align="center">false</td>
    </tr>
    <tr>
      <td>String</td>
      <td align="center">非空字符串</td>
      <td align="center">空字符串</td>
    </tr>  
    <tr>
      <td>String</td>
      <td align="center">Number</td>
      <td align="center">0和NaN</td>
    </tr>  
    <tr>
      <td>Object</td>
      <td align="center">任何非null对象</td>
      <td align="center">null</td>
    </tr>  
    <tr>
      <td>Undefined</td>
      <td align="center">N/A</td>
      <td align="center">undefined</td>
    </tr>  
  </tbody>
</table>
  












