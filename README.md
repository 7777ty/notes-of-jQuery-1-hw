# jQuery是什么？
1. jQuery是一款优秀的javaScript库，从命名就可以看出jQuery的主要用途是用来做查询的。write less,do more.
2. jQuery分为（1.x、2.x、3.x），
    * 1.x：兼容ie678，但其较其他版本文件较大，功能不再新增，最终版本：1.12.4（2016年5月20日）。
    * 2.x:不兼容ie678，相对1.x文件要小，官方只作BUG维护，功能不再新增，最终版本：2.24（2016年5月20日）。
    * 3.x：不兼容ie678，只支持最新的浏览器，很多老的jQuery插件不支持这个版本，相较于1.x文件较小，提供不包含Ajax/动画API版本。

-----------------

## 如何使用jQuery
1. 下载jQuery库。
2. 引入jQuery库。
3. 编写jQuery代码。

    原生JS的固定写法：
    ```JavaScript
    window.onload=function(ev){}
    ```

    jQuery的固定写法：
    ```JavaScript
    $(document).ready(function(){

    })
    ```

## jQuery的入口函数的几个区别

1. 原生JS与jQuery入口函数的加载模式不同。
原生JS会等到DOM元素加载完毕，并且图片也加载完毕才会执行。
jQuery会等到DOM加载完毕，但不会等到图片也加载完毕就会执行。

2. 原生JS如果编写了多个入口函数，后面编写的会覆盖前面写的。
jQuery中编写了多个入口函数，后面的不会覆盖前面的。
  
### jQuery入口函数的其他写法
```JavaScript
//第一种写法
$(document).ready(function(){
    alert("hello");
});

//第二种写法
jQuery(document).ready(function(){
    alert("hello");
});

//第三种写法
$(function(){
    alert("hello");
});

//第四种写法
jQuery(function(){
    alert("hello");
});

```
-------------------

## jQuery的冲突问题

主要是$的冲突问题:
1. 释放$的使用权：释放操作必须在编写其他jQuery代码之前编写，释放之后就不能在使用$，而改为使用jQuery。
```JavaScript
jQuery.noConflict();
```

2. 自定义访问符号
```JavaScript
var ty = jQuery.noConflict();
```

------------------

上述代码即表明释放了$的使用权并把ty设为访问符号。

## jQuery的核心函数

1. $(); 就代表调用了jQuery的核心函数，其可接受的参数：
    1. 函数
    ```JavaScript
    $(function(){
        alert("hello");
    });
    ```
    2. 字符串
    2.1 字符串选择器
    ```JavaScript
    $(".box1");
    $("#box2");
    ```

    2.2 代码片段
     ```JavaScript
     var $p = $("<p>我是段落</p>")；   //会创建对应的DOM元素
     $box1.append($p);
     ```
    3. DOM元素
     如果将原生DOM元素传给jQuery核心函数，那么它会把原生DOM元素包装成一个jQuery对象返回给我们。

## jQuery对象
jQuery是一个伪数组。

---------------

## jQuery的静态方法
直接添加在类上的为静态方法，添加到原型上的是实例方法。静态方法通过类名调用，实例方法通过类的示例调用。

### each方法:

原生JS的forEach方法：

```JavaScript
var arr =[1,3,5,7,9];

arr.forEach(function(value,index){
    console.log(index,value);   
});     //参数一是遍历到的元素，二是遍历到的索引。原生JS的forEach方法只能遍历到数组，不能遍历伪数组。
```

jQuery的each方法

```JavaScript
var arr =[1,3,5,7,9];

$.each(arr,function(index,value){
    console.log(index,value);    
});      //参数一：数组；参数二：回调函数
//回调函数中的参数一：当前遍历到的索引；参数二:遍历到的元素。jQuery的each方法是可以遍历伪数组的。
```

### map方法：

原生JS的map方法：

```JavaScript
var arr =[1,3,5,7,9];

arr.map(function(value,index,array){
    console.log(index,value,array);
});     //参数一：遍历到的元素；参数二：遍历到的索引；参数三：当前遍历的数组。不能遍历伪数组。
```

jQuery的map方法

```JavaScript
$map(arr,function(value,index){
    console.log(index,value);
});     /*参数一：要遍历的数组；参数二：遍历到的索引。
*回调函数的参数：一:遍历到的元素，二：遍历到的索引。
*和jQuery中的each静态方法一样，map静态方法也可以遍历伪数组。
*/
```

jQuery中的each静态方法和map静态方法的区别：
each静态方法默认的返回值是遍历的对象；map静态方法默认的返回值是一个空数组。
each的的静态方法不支持在回调函数中对遍历的数组进行处理，而map静态方法可以在回调函数中通过return对遍历的数组进行处理，然后生成一个新的数组返回。

### jQuery中的其他静态方法

1.$.trim();  作用：去除字符串两端的空格；参数：需要去除空格的字符串；返回值：去除空格后的字符串。

2.$.isWindow();  作用：判断传入对象是否是window对象；返回值：布尔值

3.$.isArray();  作用：判断传入对象是否是真数组；  返回值：布尔值；

4.$.isFunction();  作用：判断传入对象是否是函数；  返回值：布尔值；  用这个函数判断jQuery框架本质是一个函数。

5.$.holdReady(true);  作用：暂停ready执行；

------------

## jQuery中的内容选择器

#### :empty

```JavaScript
var $div=$("div:empty");  //找到所有div中内容为空的指定元素（即既没有文本，也没有子元素）；
```

#### :parent

```JavaScript
var $div=$("div:parent");  //先找到所有div，然后从找到的div中找到有子元素或文本内容的指定元素。
```

#### :contains（text）

```JavaScript
var $div=$("div:contains('我是div')");  //先找到所有div，然后从中找到的div中找到所有包含指定文本内容的指定元素。
```

#### :has(selector)

```JavaScript
var $div=$("div:has('span')");  //先找到所有div，然后从中找到的div中找到所有包含指定子元素的指定元素。
```

-------------

## jQuery中属性和属性节点

### 什么是属性？

对象身上保存的变量就是属性。

#### 如何操作属性？

赋值：对象.属性名称=值；  对象["属性名称"]=值；
获取：对象.属性名称；    对象["属性名称"]；

#### 什么是属性节点？

在编写HTML标签中添加的属性就是属性节点

#### 如何操作属性节点？

赋值：DOM元素.setAttribute("属性名称","值")；
获取：DOM元素.getAttribute("属性名称")；

#### 属性和属性节点有什么区别？

任何对象都有属性，但只有DOM对象才有属性节点。

### jQuery中操作属性节点的方法

1. attr（name|pro|key|，val|fn）
作用：获取或者设置属性节点的值，可以传递一个参数，也可以传递两个；如果传递一个参数，代表获取属性节点的值。如果传递两个参数代表设置属性节点的值。
2. removeAttr(name)   作用：会删除所有找到元素指定的属性节点。以空格隔开就可以删除个节点：
```JavaScript
$("span").removeAttr("class id");
```

### jQuery中操作属性的方法

1. prop方法
特点与attr方法一致。
```JavaScript
$("span").eq(0).prop("demo","cty");     //为span的第一个属性设置或新增值为cty的demo属性。
```

2. removeProp方法
与removeAttr方法一致。

prop方法不仅能操作属性还能操作属性节点。官方推荐在操作属性节点时，具有true和法拉瑟两个属性的属性节点，如：checked，selected，或者disabled使用prop(),其他的使用attr()。
```JavaScript
$("span").prop("class","box");
```
### jQuery中操作类的方法

1. addClass(class|fn)

 作用：添加一个类，如果要添加多个那么用空格隔开就可以了。
 ```JavaScript
 $("div").addClass("class1 class2");
 ```

2. removeClass([class|fn])
 ```JavaScript
 $("div").removeClass("class1 class2");
 ```

3. toggleClass(class|fn[,sw])
作用：切换类
 ```JavaScript
 $("div").toggleClass("class1 class2");
 ```

### jQuery中操作文本值的方法
1. html([val|fn])  
和原生JS中的innerHTML一模一样
```JavaScript
$("div").html("<p>我是段落<span>我是span</span></p>");  //设置

$("div").html();    //获取

```

2. text([val|fn])  
和原生JS中的innerText一模一样

```JavaScript
$("div").text("我是段落我是span");  //设置

$("div").text();    //获取

```

3. val([val|fn|arr])
和value属性一样

### jQuery操作css样式的方法

1. 逐个设置

```JavaScript
$("div").css("width","100px");
$("div").css("height","100px");
$("div").css("background","red");
```

2. 链式设置

```JavaScript
$("div").css("width","100px").css("height","100px").css("background","red");     //链式操作大于三步一般建议分开
```

3. 批量设置

```JavaScript
$("div").css({
    width:100px;
    height:100px;
    background:red;
});
```

4. 获取css样式值

```JavaScript
$("div").css("width");     //获取宽度样式值
```

----------------

### jQuery位置和尺寸的操作方法

1. width([val|fn])  获取或设置一个元素的宽度。
   height([val|fn])  获取或设置一个元素的高度。
   innerWidth()  获取或设置一个元素的宽度+内边距的总和
   innerHeight()  获取或设置一个元素的高度+内边距的总和
   outerWidth([options])
   outerHeight([options])

2. offset([coordinates])
    作用：获取或设置元素距离窗口的偏移位。

3. position()
    作用：获取元素距离定位元素的偏移位。只能获取，不能设置。

4. scrollTop()
    作用：获取或设置元素或网页的滚动偏移位。在获取和设置网页滚动的偏移位时，为了保证浏览器兼容，需要按照如下的写法：

    ```JavaScript
    console.log($("body").scrollTop()+$("html").scrollTop());     //获取

    $("html,body").scrollTop(300);     //设置
    ```

---------------

## jQuery事件绑定与解绑

### 事件绑定
1. eventName(fn);
编码效率高，部分jQuery事件没有实现，不能添加。

```JavaScript
$(".son").cilck(function(){
    alert("Hi");

});
```

注意点：在jQuery中，如果通过核心函数找到的元素不止一个，那么在添加事件时，jQuery会遍历所有找到的元素，给所有找到的元素添加事件。

2. on(eventName,fn);
编码效率低，所有js事件都可以添加。

```JavaScript
$(".son").on("click",function(){
    alert("Hi");
});
```


可添加多种相同/不同类型的事件，且不会覆盖。

### 事件解绑
1. off(); 
    作用：移除事件，如果不传参，会移除所有事件。如果传一个参数，会移除所有指定类型的事件。如果传递两个参数，那么将会移除指定类型的指定参数。


## jQuery的事件冒泡与默认行为

### 什么是事件冒泡？
事件冒泡就是事件从里向外，从下至上，从下级往上级传递的过程。
### 如何阻止事件冒泡？
1. 在子事件中加入代码(return false;)。

2. 调用event的stopPropagation()方法：

```JavaScript
$(".son").click(function(event)){
    alert("son");
    event.stopPropagation();
}

```

### 什么是默认行为？
例如点击a标签时会默认跳转，这样的行为就是默认行为。

### 如何阻止默认行为？

1. 在事件中加入代码(return false;)。

2. 调用event的preventDefault()方法：

```JavaScript
$(".son").click(function(event)){
    alert("son");
    event.preventDefault();
}

```

### 事件的自动触发
1. trigger()  会触发事件冒泡和事件的默认行为。
2. triggerHandler()  不会触发冒泡事件和默认行为。

面试题：如果想用trigger()方法触发某一事件的默认行为，那么应该采取监听该事件的子事件，通过事件冒泡的手段来达到目的。

### jQuery的自定义事件
想要自定义事件，必须满足两个加条件：
1. 事件通过on绑定
2. 事件必须通过trigger()来触发

```JavaScript
$(".son").on("myClick",function(){
    alert("hi");
});

$(".son").trigger("myClick");
```

### jQuery的事件命名空间
想要添加事件命名空间，必须满足两个加条件：
1. 事件通过on绑定,通过.来添加命名空间
2. 通过trigger()或triggerHandler()或来触发

```JavaScript
$(".son").on("myClick.cty",function(){
    alert("hi");
});

$(".son").trigger("myClick");
```

面试题：
1. 利用trigger()触发子元素带命名空间的事件，那么子元素带相同命名空间的事件也会被触发，而父元素没有命名空间的事件不会被触发。
2.  利用trigger()触发子元素不带命名空间的事件，那么子元素所有相同类型的事件和父元素所有相同类型的事件都会被触发。

### jQuery事件委托

1. 什么是事件委托？
请别人帮忙做事，做完后将做完的结果反馈给我们。

```JavaScript
$("ul").delegate("li","click",function(){
    console.log($(this).html());
});
```

上述代码就是将li的点击事件委托交给ul，事件委托就是找一个在入口函数执行之前就已经有的元素，来监听动态添加的元素的某些事件
