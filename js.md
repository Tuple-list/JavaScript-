# JavaScript 学习笔记  

![](https://img.shields.io/badge/tuple-Javascript-blue)  
<h3>原文链接</h3>  

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
  ```
  [输出]  
  true  
  true  
  false  
  false  
  false  
  false  
  ```
  
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
  ```
  [输出]  
  NaN  
  NaN  
  123  
  123  
  0  
  1  
  ```
  
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
  > **注意：在整个循环体内部定义的变量，在循环体外也依然可以获取。**  
+ for-in语句  
  for-in可以用来枚举对象的属性：  
  ```
  for(var propName in window){
  console.log(propName);
  }
  ```
  > **注意：在枚举前最好先检测对象是否为null或undefined，否则可能会报错。**  
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
  > **注意：switch语句在比较时采用的是全等（===）操作符，即类型和值都要一致。**  
  
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
  > **注意：ECMAScript中String是基本类型（5个基本类型：undefined、null、Boolean、Number、String）。**  
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
  执行环境（execution context）是JavaScript中最重要的一个概念，它定义了变量和函数有权访问的其它数据，决定了它们各自的行为。每一个执行环境当中定义的所有的变量和函数都保存在一个变量对象（variable object）中。  
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
  
---  
<h2>JavaScript学习笔记（五）引用类型</h2>   
---  

> ## Object类型    
  创建引用类型（如Object）实例的方式有2种，第一种是使用new操作符后跟Object构造函数：  
  ```
  var person = new Object();
  person.name = "Sky";
  person.age = 26;
  ```
  另一种是使用对象字面量表示法，对象字面量是对象定义的一种简写形式。  
  ```
  var person = {
      name : "Sky",
      "age" : 26    //属性名的双引号可省略
  };
  ```
  ```
  var person = {};
  //等价于：var person = new Object();
  person.name = "Sky";
  ```
  对象字面量还可以用来向函数传递大量可选参数。  
  ```
  function displayInfo(args){
    var output = "";
    if(typeof args.name == "string"){
      output += "name: " + args.name + "\n";
    }
    if(typeof args.age == "number"){
      output += "age: " + args.age + "\n";
    }
    console.log(output);
  }

  displayInfo({
    name: "Sky",
    age: 26
  });

  displayInfo({
    name: "Sky"
  });
  ```
  
  ```
  [输出]
  name: Sky
  age: 26
  name: Sky
  ```
  访问对象的属性可以使用点表示法或者方括号表示法。  
  方括号表示法的主要优点是：可以通过变量来访问属性，或者属性名可能引发语法错误时使用。  
  ```
  console.log(person.name);
  console.log(person["name"]);
  var attrName = "first name";
  console.log(person[attrName]);    //若使用person.first name显然会报错
  ```


> ## Array类型  
  + 创建数组  
  创建数组的方法：  
  ```
  var colors = new Array();
  var colors = new Array(3);    //创建一个长度为3的数组
  var colors = new Array("red", "blue", "green");    //创建数组并传递应该包含的项
  var colors = Array();    //new可以省略
  ```  
  也可以使用数组字面量表示法：  
  ```
  var colors = [];    //创建空数组
  var colors = ["red", "blue", "green"];    //创建包含3个项的数组
  ```  
  
  + 访问数组  
  使用数字索引来访问或设置数组的值。  
  ```
  var colors = ["red", "blue", "green"];
  console.log(colors[0]);
  colors[4] = "yellow";    //索引不存在则新建项
  colors[colors.length] = "brown";    //利用length属性可以方便地在数组末尾添加项
  console.log(colors);
  ```  
  
  ```
  [输出]
  red
  ["red", "blue", "green", undefined, "yellow", "brown"]
  ```  
  
  > **注意：数组的length属性不是只读的！**    
  
  ```
  var colors = ["red", "blue", "green"];
  colors.length = 2;    //最后一项被删除了
  console.log(colors);
  ```
  
  ```
  [输出]
  ["red", "blue"]
  ```
  + 检测数组  
  检测一个值是否是数组：  
  ```
  colors instanceof Array
  ```
  在IE9+浏览器上，还可以使用更准确的方法——Array.isArray()函数：  
  ```
  Array.isArray(colors)
  ```
  + 输出数组  
  使用toString()、valueOf()、join()可以将数组直接输出出来，默认以逗号分隔每项。  
  ```
  alert(colors.toString());
  alert(colors.valueOf());
  alert(colors);    
  alert(colors.join());
  alert(colors.join("|"));
  ```
  
  ```
  [输出]
  red,blue
  red,blue
  red,blue
  red,blue
  red|blue
  ```  
  + push与pop  
  栈是一种LIFO（Last-In-First-Out，后进先出）的数据结构，ECMAScript为数组提供了push()-推入和pop()-弹出的方法实现栈的行为。  
  push()接收任意数量参数，逐个添加到数组末尾，返回修改后数组长度；  
  pop()移除末尾项并返回该项。  
  ```
  var colors = new Array();
  colors.push("red", "blue");
  colors.pop();
  ```
  + shift与unshift  
  队列的访问规则是FIFO（First-In-First-Out，先进先出），在末尾添加项，在前端移除项。  
  shift()能移除数组的第一项并返回该项，unshift()能够从前端添加任意多项，并返回修改后数组长度。  
  ```
  var colors = new Array();
  colors.push("red", "blue");
  colors.shift();
  colors.unshift("green", "yellow");
  ```
  + 数组排序  
  reverse()函数可以反转数组中的项，sort会转换数组中的项为字符串后，再按升序进行排列。  
  ```
  var nums = [0,1,5,10,15];
  nums.reverse();
  console.log(nums);
  nums.sort();
  console.log(nums);
  ```
  ```
  [输出]
  [15, 10, 5, 1, 0]
  [0, 1, 10, 15, 5]
  ```
  由于sort()比较的是字符串，上例的排序并非我们想要的。但sort()支持接收一个比较函数作为参数，让我们指定比较规则。  
  ```
  var nums = [0,1,5,10,15];
  nums.sort(compare);
  console.log(nums);

  //升序比较规则函数
  function compare(value1,value2){
    return value1 - value2;
  }
  ```
  
  ```
  [输出]
  [0, 1, 5, 10, 15]
  ```  
  
  + 合并数组  
  concat()会返回当前数组的副本，如果传入参数，则会将参数添加到数组末尾后再返回新的数组。  
  ```
  var colors = ["red","blue"];
  var colors2 = colors.concat("green",["white","brown"]); 
  console.log(colors.toString());
  console.log(colors2.toString());
  ```
  ```
  [输出]
  red,blue
  red,blue,green,white,brown
  ```
  + 截取子数组  
  slice()会基于原数组返回一个子数组，原数组不会改变。第一个参数是起始位置，第二个参数（可选）是结束位置。注意：包含起始位置项但不包含结束位置项！  
  ```
  var colors = ["red","blue","green", "white"];
  var colors2 = colors.slice(1);
  var colors3 = colors.slice(1,3);    //含1但不含3
  console.log(colors.toString());
  console.log(colors2.toString());
  console.log(colors3.toString());
  ```
  
  ```
  [输出]
  red,blue,green,white
  blue,green,white
  blue,green
  ```  
  + splice方法  
  splice()算是最强大的数组方法了，主要的用法：  
  删除：splice(0,2)删除第0位置开始的2项；  
  插入：splice(1,0,"a","b")删除位置1开始的0项（即不删除项），并在位置1处插入"a","b"两项；  
  替换：splice(1,1,"a","b")删除位置1开始的1项，并在位置1处插入"a","b"两项。  
  > **注意：splice是直接修改原数组的，返回值是被删除的数组集合。**    
  ```
  var colors = ["red","blue","green", "white"];
  var removed = colors.splice(0,1);
  console.log(colors.toString());
  console.log(removed.toString());
  removed = colors.splice(1,0,"yellow");
  console.log(colors.toString());
  console.log(removed.toString());
  removed = colors.splice(1,2,"black","gray");
  console.log(colors.toString());
  console.log(removed.toString());
  ```
  
  ```
  [输出]  
  blue,green,white  
  red  
  blue,yellow,green,white  
  (空字符串)  
  blue,black,gray,white  
  yellow,green  
  ```
  + 获取位置  
  indexOf()从位置0开始查找项，lastIndexOf()从数组末尾开始查找。可选的第2个参数：开始查找的起点位置。  
  ```
  var colors = ["red","blue","green","red", "white"];
  console.log(colors.indexOf("red"));
  console.log(colors.indexOf("red",1));
  console.log(colors.lastIndexOf("red"));
  ```
  
  ```
  [输出]
  0
  3
  3
  ```  
  > **注意：比较项是否相等，采用的是全等操作符（===），类型和值都必须一致。**    
  
  + 数组迭代  
  几个常用的迭代函数：  
  every()：对数组中每一项运行指定函数，全部为true则返回true；  
  some()：只要有一项为true则返回true；  
  filter()：返回运行函数返回为true的所有项组成的数组；  
  map()：返回运行函数返回值组成的数组；  
  forEach()：对数组中每一项运行指定函数，无返回值。  
  ```
  var nums = [1,2,3,4,5];


  var everyResult = nums.every(function(item,index,array){
    if(item > 2){
      return true;
    }
  });
  console.log(everyResult.toString());

  var someResult = nums.some(function(item,index,array){
    if(item > 2){
      return true;
    }
  });
  console.log(someResult.toString());

  var filterResult = nums.filter(function(item,index,array){
    if(item > 2){
      return true;
    }
  });
  console.log(filterResult.toString());

  var mapResult = nums.map(function(item,index,array){
    return item+1;
  });
  console.log(mapResult.toString());

  var sum = 0;
  nums.forEach(function(item,index,array){
    sum += item;
  });
  console.log(sum);
  console.log(nums.toString());    //上面的操作不会修改原数组
  ```
  
  ```
  [输出]
  false
  true
  3,4,5
  2,3,4,5,6
  15
  1,2,3,4,5
  ```  
> ## Date类型  
  使用new Date()创建一个日期对象。  
  Date.parse()和Date.UTC()都返回表示日期的毫秒数，Date.parse()传递一个表示日期的字符串，而Date.UTC()传入年、月、日、时、分、秒，其中年、月必填，月是从0开始，小时是24小时制的。  
  ```
  var now = new Date();    //当前时间
  var date1 = new Date("8/19/2015");
  var date2 = new Date(Date.parse("8/19/2015"));    //与上面等价
  var date3 = new Date(2015,10,17,22,18,56);    //注意10代表11月，因为月份是从0开始的    
  var date4 = new Date(Date.UTC(2015,10,17,22,18,56));    //与上面等价
  ```  
  关于Date类型的常用方法：  
  ```
  var now = new Date();
  console.log(now.getFullYear());
  console.log(now.getMonth());    //从0开始的月份
  console.log(now.getDate());    
  console.log(now.getDay());    //星期几，0代表星期日
  console.log(now.getHours());
  console.log(now.getMinutes());
  console.log(now.getSeconds());
  console.log(now.getMilliseconds());
  console.log(now.getTimezoneOffset());    //本地时间与UTC时间相差的分钟数
  ```
  
  ```
  [输出]
  2015
  7
  19
  3
  22
  15
  22
  239
  -480
  ```

> ## RegExp类型  
  创建正则表达式：var expression = / pattern / flags ;  
  其中，模式（pattern）部分是正则表达式，flags代表1个或多个标志，可能的标志包括：  
  g：全局模式，模式被应用于所有字符串，而非发现第一个匹配后就立即停止；  
  i：忽略大小写；  
  m：多行模式。  
  模式中用到的所有元字符必须在前面加"\"转义，元字符包括：  
  ( ) [ ] { } \ ^ $ | ? * + .  
  ```
  //匹配所有的以"at"结尾的3个字符的组合，忽略大小写
  var pattern1 = /.at/gi;
  //匹配所有的".at"，忽略大小写
  var pattern2 = /\.at/gi;
  ```
  
  也可以使用RegExp构造函数创建正则表达式：  
  ```
  var pattern1 = new RegExp(".at","gi");    //注意2个参数都是字符串形式的！
  ```
  
  使用test()函数检测字符串与模式是否匹配：  
  ```
  var text="000-00-0000";
  var pattern = /\d{3}-\d{2}-\d{4}/gi;
  pattern.test(text);
  ```
  
  ```
  [输出]
  true
  ```
> ## Function类型  
  + 定义函数  
  定义函数的3种方式：  
  ```
  //方式1：函数声明定义函数
  function sum(num1, num2){
      return num1 + num2;
  }

  //方式2：函数表达式定义函数
  var sum = function(num1, num2){
      return num1 + num2;
  }

  //方式3：构造函数定义函数（不推荐）
  var sum = new Function("num1", "num2", "return num1 + num2");    //前面的参数作为函数参数，最后一个参数视作函数体
  ```
  函数其实是Function类型的实例，因此函数也是对象，函数名实际上是一个指向函数对象的指针。  
  ```
  function sum(num1, num2){
      return num1 + num2;
  }

  console.log(sum(1,2));

  var anotherSum = sum;
  console.log(anotherSum(3,4));

  sum = null;
  console.log(anotherSum(3,4));    //sum指针变为null，并不会影响anotherSum这个指针
  ```
  
  ```
  [输出]
  3
  7
  7
  ```  
  + 没有重载  
  由于没有函数签名，所以ECMAScript中没有重载的概念。同名函数后面的函数会覆盖前面的。  

  ```
  function sum(num1, num2){
      return num1 + num2;
  }

  function sum(num1, num2, num3){
    return num1 + num2 + num3;
  }

  console.log(sum(1,2,3));
  ```
  
  ```
  [输出]
  6
  ```
  其实上面的代码等价于：  
  ```
  var sum = function(num1, num2){
      return num1 + num2;
  };

  sum = function(num1, num2, num3){
    return num1 + num2 + num3;
  };

  console.log(sum(1,2,3));
  ```
  这样可以更直观的看出，后面的sum覆盖了前面的。  
  
  在代码开始执行之前，解析器会通过一个名为函数声明提升（function declaration hoisting）的过程读取全部函数声明并添加到相应的执行环境中。所以，可以先调用函数，再去用函数声明的方式定义该函数。  
  ```
  console.log(sum(1,2));
  function sum(num1, num2){
      return num1 + num2;
  }
  ```
  
  ```
  [输出]
  3
  ```
  而如果函数是利用函数表达式定义的，则必须等到解析器执行到它所在的代码行，才会被解析执行。  
  ```
  console.log(sum(1,2)); 
  var sum = function(num1, num2){
      return num1 + num2;
  };
  ```
  
  ```
  [输出]
  TypeError: sum is not a function
  ```
  + 作为值的函数  
  因为函数名本身就是变量，所以函数也可以作为值来使用。  
  现在假设有一个数组对象，需要按照对象的某个属性来进行排序，可以这样写：  
  ```
  function createComparisonFunction(propertyName){
    //该函数返回一个比较函数
    return function(obj1, obj2){
      var val1 = obj1[propertyName];    //因为这里属性值是变量，只能使用方括号表示法
      var val2 = obj2[propertyName];
      if(val1 < val2){
        return -1;
      }else if(val1 > val2){
        return 1;
      }else{
        return 0;
      }
    }
  }

  var data = [{name: "Zhang", age:20},{name: "Li", age:30}];
  //按name属性排序
  data.sort(createComparisonFunction("name"));
  console.log(data);
  //按age属性排序
  data.sort(createComparisonFunction("age"));
  console.log(data);
  ```
  
  ```
  [输出]
  [Object { name="Li", age=30}, Object { name="Zhang", age=20}]
  [Object { name="Zhang", age=20}, Object { name="Li", age=30}]
  ```  
  函数内部有2个特殊对象：arguments和this。  
  
  
  + arguments对象  
  arguments包含传入函数的参数数组，它还有1个名为callee的属性，指向函数本身。  
  ```
  //递归函数
  function factorial(num){
    if(num <= 1){
      return 1;
    }else{
      return num * arguments.callee(num - 1);    //使用arguments.callee调用函数本身，能够不依赖函数名
    }
  }

  var newFactorial = factorial;
  factorial = function(){    
    return 0;
  }

  console.log(newFactorial(5));
  console.log(factorial(5));
  ```
  
  ```
  [输出]
  120
  0
  ```
  + this对象  
  函数内部的另一个特殊对象就是this，this指向函数所在的执行环境，当在全局作用域中调用函数时，this对象引用的就是window。  
  ```
  var color = "red";

  function showColor(){
    console.log(this.color);
  }

  var obj = {
    color : "blue",
    showColor : showColor
  };

  showColor();    //获取的是window.color
  obj.showColor();    //获取的是obj.color
  ```
  
  ```
  [输出]
  red
  blue
  ```
  + 函数属性  
  ECMAScript中的函数也是对象，因此也有属性和方法。每个函数都包含2个属性：length和prototype。

  length属性表示函数的参数个数：  
  ```
  function sum(num1, num2){
    return num1 + num2;
  }
  console.log(sum.length);
  ```
  
  ```
  [输出]
  2
  ```
  + apply和call方法  
  每个函数都包含apply()和call()方法，用来在特定的作用域中调用函数。  
  apply()方法接收2个参数：一是作用域，二是传入的参数（Array实例或者arguments对象）；  
  call()方法接收1个以上不确定参数：第一个参数依旧是作用域，其余参数都直接列出传入函数。  
  ```
  function sum(num1, num2){
    return num1 + num2;
  }

  function callSum1(num1, num2){
    return sum.apply(this,[num1, num2]);
  }

  function callSum2(num1, num2){
    return sum.apply(this,arguments);
  }

  function callSum3(num1, num2){
    return sum.call(this,num1,num2);
  }

  console.log(callSum1(10,10));
  console.log(callSum2(10,10));
  console.log(callSum3(10,10));
  ```
  
  ```
  [输出]
  20
  20
  20
  ```
  apply()和call()常用来扩充函数的作用域：  
  ```
  var color = "red";

  function showColor(){
    console.log(this.color);
  }

  var obj = {
    color : "blue",
  };

  showColor.call(this);
  showColor.call(window);
  showColor.call(obj);    //showColor()中的this指向了obj
  ```
  
  ```
  [输出]
  red
  red
  blue
  ```
  上述代码的好处是：对象不需要与方法有任何耦合关系，前面的例子中obj对象需要定义一个showColor()方法，而这个例子就不需要了。  
  
  
  + bind方法  
  此外，函数还有一个方法：bind()，它会创建一个函数的实例，this值会被绑定到传给bind()的参数值。  
  ```
  var color = "red";

  function showColor(){
    console.log(this.color);
  }

  var obj = {
    color : "blue",
  };

  var showColorObj = showColor.bind(obj);
  showColorObj();
  ```
  
  ```
  [输出]
  blue
  ```
  
  
> ## 基本包装类型  
  每当读取一个基本类型值的时候，后台就会创建一个对应的基本包装类型的对象，从而让我们方便调用一些方法来操作这些数据。  
  3个基本包装类型：Boolean、Number、String。  
  因为有了基本包装类型，所以JavaScript中的基本类型可以当做对象来访问。  
  

  


  

