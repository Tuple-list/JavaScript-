# JavaScript 学习笔记  

![](https://img.shields.io/badge/tuple-Javascript-blue)  
[iBlog](https://skysun.name/blog/javascript)

<h2>JavaScript学习笔记（三）基本概念</h2>  

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
  [输出]  
  true  
  true  
  false  
  false  
  false  
  false  
  
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
  [输出]  
  NaN  
  NaN  
  123  
  123  
  0  
  1  
  
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
  ECMAScript提供了2组相等操作符：相等和不相等（==和!=）——先转换再比较，全等和不全等（===和!==）——仅比较不转换。  
  ```
  console.log(null == undefined)
  console.log(NaN == NaN)
  console.log(NaN != NaN)
  console.log(false == 0)
  console.log(5 == "5")
  ```  
  ```
  [输出]
  true
  false
  true
  true
  true
  ```  
  
  console.log(5 == "5")    //转换后的值相同，则相等  true  
  console.log(5 === "5")    //类型不同，则不全等     false  
  
> ## 语句  
+ do-while语句  
  do-while循环会先执行后判断，即循环体内的代码至少会被执行一次：  
  ```
  var i=0;
  do{
    i+=2;
  }while(i<10);
  console.log(i);
  ```
  ```
  [输出] 
  10  
  ```
+ while语句  
  while循环会先判断再执行：  
  ```
  var i=0;
  while(i<10){
    i+=2;
  }
  console.log(i);
  ```
  ```
  [输出]
  10
  ```
+ for语句  
  一个简单的for循环  
  ```
  for(var i=0;i<10;i++){
    console.log(i);
  }
  console.log(i);
  ```
  > 注意：在整个循环体内部定义的变量，在循环体外也依然可以获取。  
+ for-in语句  
  for-in可以用来枚举对象的属性：  
  ```
  for(var propName in window){
  console.log(propName);
  }
  ```
  > 注意：在枚举前最好先检测对象是否为null或undefined，否则可能会报错。  
+ lable、break与continue语句  
  使用label语句可以在代码中添加标签，以便将来使用，常用在for循环前面。  
  break会跳出整个循环，执行循环体后面的语句；continue会跳出本次循环，开始下一次循环。  
  ```
  var num = 0;
  outermost:    //定义一个标签
  for(var i = 0;i < 10;i++){
    for(var j = 0;j < 10;j++){
      if(i == 5&&j == 5){
        break outermost;    //跳出标签所在的外部循环
      }
      num++;
    }
  }
  console.log(num);
  ```
  ```
  [输出]
  55
  ```
+ switch语句  
  ```
  var i = 1;
  switch(i){
    case 0:
      console.log(0);
      break;
    case 1:    //没有break，则不会跳出，会与下面的情形合并
    case 2:
    console.log("1 or 2");
      break;
    default:
      console.log("others");
      break;
  }
  ```
  ```
  [输出]
  1 or 2
  ```
  > 注意：switch语句在比较时采用的是全等（===）操作符，即类型和值都要一致。  
  
> ## 函数  
  + arguments对象  
  ECMAScript函数的一个重要特点：命名的参数只提供便利，但不是必需的。在函数内部可以使用arguments对象来访问参数数组。  
  ```
  sayHello("Morning","Sky");

  function sayHello(){
    console.log("Good "+arguments[0]+","+arguments[1]);
  }
  ```
  + 没有重载  
  由于ECMAScript函数的参数是由包含零个或多个值的数组来表示的，没有函数签名，所以不能重载。  
  但可以根据传入参数的类型和长度（argument.length），来作出不同反应以模拟重载。  
  ```
  function doAdd(){
    if(arguments.length == 1){
      console.log(arguments[0] + 10);
    }else if(arguments.length > 1){
      var sum = 0;
      for(var i in arguments){
        sum+=Number(arguments[i]);
      }
      console.log(sum);
    }else{
      console.log(0);
    }
  }
  doAdd(10);
  doAdd(1,2,3,4,5);
  ```
  ```
  [输出]
  20
  15
  ```
---  
<h2>JavaScript学习笔记（四）基本概念</h2> 
---

[摘要] JavaScript中的变量类型、参数传递、执行环境、内存问题等。  
> ## 基本类型和引用类型的值  
  基本类型的值在内存中占据固定大小的空间，保存在栈中；引用类型的值是对象，保存在堆中。  
  + 动态属性  
  对于引用类型的值，可以动态的为其添加属性和方法。  
  ```
  var person = new Object();
  person.name = "Sky";
  console.log(person.name);
  ```
  ```
  [输出]
  Sky
  ```
  而对于基本类型的值，添加属性或方法无效。  
  ```
  var person = "person";
  person.name = "Sky";
  console.log(person.name);
  ```
  ```
  [输出]
  undefined
  ```
  > 注意：ECMAScript中String是基本类型（5个基本类型：undefined、null、Boolean、Number、String）。  
  + 复制变量值  
  基本类型的值在复制时，会在变量对象上创建一个新值，然后将该值复制到为新变量分配的位置上，即复制后两个变量是完全独立的，不会相互影响。  
  ```
  var num1 = 5;
  var num2 = num1;
  num1 = 10;
  console.log(num2);
  ```
  ```
  [输出]
  5
  ```
  当从一个变量向另一个变量复制引用类型值时，两个变量都将指向同一个对象，改变其中任何一个变量，都会影响另外一个。  
  ```
  var obj1 = new Object();
  var obj2 = obj1;
  obj1.name = "Sky";
  console.log(obj2.name);
  obj2.age = "26";
  console.log(obj1.age);
  ```
  ```
  [输出]
  Sky
  26
  ```
  + 传递参数  
  函数的参数，不论是基本类型还是引用类型，都是按值传递的。  
  下面的例子证明了引用类型的参数也是传递的值而非引用：  
  ```
  function setName(obj){
    obj.name = "Sky";
    obj = new Object();
    obj.name = "Tom";
  }
  var person = new Object();
  setName(person);
  console.log(person.name); // 如果是按引用传递，则传入的person会被重新初始化，但事实没有，这就说明了传入参数的原始的引用保持未变。  
  ```
  ```
  [输出]
  Sky
  ```
  + 检测基本类型  
  typeof操作符是确定一个变量是字符串、数值、布尔值，还是undefined的最佳工具。  
  ```
  var message = "Hi";
  var msg;
  console.log(typeof message);
  console.log(typeof(message));
  console.log(typeof 3.14);
  console.log(typeof true);
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
  boolean
  undefined
  undefined
  object
  undefined
  object
  function
  ```
  + 检测引用类型  
  检测引用类型时，还可以使用instanceof操作符，语法为：variable instanceof constructor，如果变量是给定引用类型的实例则返回true。  
  ```
  var dog = new Object();
  console.log(dog instanceof Object);
  console.log("wang" instanceof Object);
  ```
  ```
  [输出]
  true
  false
  ```
  确定一个值是哪种基本类型可以用typeof，是哪种引用类型可以用instanceof。  

> ## 执行环境  
  执行环境（execution context）是JavaScript中最重要的一个概念，它定义了变量和函数有权访问的其它数据，决定了它们各自的行为。每一个执行环境当中定义的   所有的变量和函数都保存在一个变量对象（variable object）中。  
  执行环境分为全局执行环境和局部（函数）执行环境，全局执行环境是最外围的一个执行环境，对Web浏览器来说，全局执行环境就是window对象，所有全局变量和函   数都是作为window对象的属性和方法创建的。每个函数也都有自己的执行环境，即局部执行环境。  
  
  JavaScript中没有块级作用域的概念，在if或for中定义的变量，在外部依然可以访问到，因为它们处在相同的执行环境中。  
  ```
  if(true){
    var color = "blue";
  }
  console.log(color);
  ```
  ```
  [输出]
  blue
  ```
  查询标识符时，会沿作用域链向上搜索，一直追溯到全局环境的变量对象，即越里面的标识符优先级越高。一旦找到就立即停止搜索。  
  ```
  var color = "blue";
  function getColor(){
    var color = "red";
    return color;
  }
  console.log(getColor());
  console.log(color);
  console.log(window.color);
  ```
  ```
  [输出]
  red
  blue
  blue
  ```
> ## 垃圾收集  
  “标记清除”是目前主流的垃圾收集算法，这种算法的思想是给当前不是用的值加上标记，然后再回收其内存。  
  分配给Web浏览器的可用内存通常比分配给桌面应用程序的少，这样做的目的主要是处于安全方面的考虑，防止运行JavaScript的网页耗尽全部系统内存而导致系统崩   溃。  
  
  优化内存占用的最佳方式，就是为执行中的代码只保存必要的数据。一旦数据不再有用，则将其设为null来释放引用，这种做法叫解除引用（dereferencing）。  
  
  ```
  function createPerson(name){
    var localPerson = new Object();
    localPerson.name = name;
    return localPerson;    //函数执行完退出其执行环境时，localPerson即被销毁，所以无需解除引用
  }
  var globalPerson = createPerson("Sky");

  //当不再使用该全局的变量时，则解除引用
  globalPerson = null;
  ```




  
  



  


  
  












