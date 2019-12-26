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
  > console.log(null == undefined);  [输出] true  

  任何情况下，都没有必要将一个变量的值显式设定为undefined；  
  而如果一个变量是用来存储对象的，在初始化时最好明确赋给null值，以区分null和undefined。  
+ Boolean类型  
  Boolean类型包含2个值：true和false。  
  ECMAScript中的所有类型的值，都可以调用转型函数Boolean()转换为Boolean值  
  各数据类型转为Boolean值的规则:  
<table>
<thead>
  <tr>
    <th align="center"}>数据类型</th>
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
     td align="center">空字符串</td>
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

  if后的条件语句会自动转换判断条件为Boolean类型  
  
+ Number类型  
  Number类型使用IEEE754格式来表示整数和浮点数值。  
  对于极大或极小的数值，可以使用科学计数法表示的浮点数值表示：  
  > var floatNum = 1.28e2;    //1.28x10^2=128  

  ECMAScript默认会将小数点后超过6位的浮点数用科学计数法表示：  
  ```
  var floatNum = 0.000000003;
  console.log(floatNum);  [输出] 3e-9  
  ```  
  
  NaN，即非数值（Not a Number），用来表示一个本来要返回数值的操作数未返回数值的情况。  
  NaN与任何值都不相等，包括NaN本身。  
  isNaN()函数可以用来确定一个传入的值经过转换后是否“不是数值”：  
  ```
  console.log(isNaN(NaN));
  console.log(isNaN("abc"));
  console.log(isNaN("123"));    //可以被转为123
  console.log(isNaN(123));
  console.log(isNaN(Infinity));    //无穷大
  console.log(isNaN(true));    //可以被转为1
  ```  
  > [输出]  
  > true  
  > true  
  > false  
  > false  
  > false  
  > false  
  
  有3个函数可以将非数值转为数值：Number()、parseInt()、parseFloat()。  
  Number()函数可以接收任何对象作为参数：  
  ```
  console.log(Number(NaN));
  console.log(Number("123abc"));
  console.log(Number("123"));
  console.log(Number(123));
  console.log(Number(null));
  console.log(Number(true));
  ```  
  > [输出]  
  > NaN  
  > NaN  
  > 123  
  > 123  
  > 0  
  > 1  
  
  parseInt()函数会尝试转换为整数值，只可以接收字符串作为参数，它会依次解析每一个字符直至遇到非数字字符：  
  ```
  console.log(parseInt(""));
  console.log(parseInt("123abc"));
  console.log(parseInt("abc123"));
  console.log(parseInt("123",10));    //还可以提供第二个参数：转换时使用的基数，即多少进制
  console.log(parseInt("3.14"));
  ```
  ```
  [输出]  
  NaN
  123
  NaN
  123
  3
  ```  
  parseFloat()函数会尝试将接收到的字符串参数转为浮点数或整数：  
  ```
  console.log(parseFloat(""));
  console.log(parseFloat("123abc"));
  console.log(parseFloat("abc123"));
  console.log(parseFloat("123.4"));
  console.log(parseFloat("123.4.5"));
  console.log(parseFloat("2.56e2"));
  ```  
  ```
  [输出]  
  NaN  
  123  
  NaN  
  123.4  
  123.4  
  256  
  ```  
+ String类型  
  String类型包含一些特殊的字符字面量，也叫转义序列，常用的如：\n换行、\r回车、\b空格、\t制表、\\斜杠、\'单引号、\"双引号、\unnnn表示一个Unicode字符。  
  转义序列会被看做一个字符：  
  > var a = "a\tb";
  > console.log(a.length);  // 3  
  
  toString()会将一个值转为字符串，但null和undefined值没有这个方法。  
  转型函数String()则支持任意类型值转为字符串：  
  ```
  console.log(String(10));
  console.log(String(true));
  console.log(String(null));
  console.log(String(undefined));
  ```  
  ```
  [输出]  
  10  
  true  
  null  
  undefined  
  ```  
  在加法运算中需要特别留意数据类型:  
  ```
  var num1 = 5;
  var num2 = 10;
  console.log("result is:" + num1 + num2);  // [输出]  result is:15  
  ```  
+ Object类型  
  Object类型是所有对象的基础。  
  > var o = new Object();  
  > var o = new Object; //无参数调用构造函数时可以省略括号  
> ## 相等操作符  
  

  
  












