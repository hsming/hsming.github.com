---
layout: post
title: "CoffeeScript 学习笔记"
---


关于coffeescript的种种早有耳闻，无奈我对javascript一直很无力，所以一直没想着去认真了解一下。巧合的是某天逛图书馆的时候不小心看到了这本[深入浅出coffeescript](http://book.douban.com/subject/10599786/)，我想，这特么就是猿粪啊，都到了这个份上了再不去学习一下就太对不起这天的偶遇了，于是果断的拿了一本回来。  看着也没有觉得什么地方不懂，但也不会觉得有什么地方很懂，这感觉很难受啊，所以找来codeschool的视频再看一遍吧，随便也记些笔记强化一下。还参考了[@lilu](http://ruby-china.org/lilu)写的这篇[博客](http://lilulife.com/blog/2012/08/06/coffeescript/)，很赞！



>CoffeeScript is a little language that compiles into JavaScript. Underneath that awkward Java-esque patina, JavaScript has always had a gorgeous heart. CoffeeScript is an attempt to expose the good parts of JavaScript in a simple way.

以上摘在[官网](http://coffeescript.org/)上的第一段。分享一下codeschool列出的coffee的特点：
* Least amount of code to solve problems
* Readable and Understandable
* Easy to Maintain  

#### 一个词：`beautiful`  

-------------

相应的安装配置参考coffeescript主页上的步骤就能轻松完成了，然后如果用sublime的话，可以安装一个相应的支持coffeescrip的插件，推荐[CoffeeScript-Sublime-Plugin](https://github.com/Xavura/CoffeeScript-Sublime-Plugin)


重点是coffee，下面是跟着视频记的一些笔记：  
#### 1. 变量  
不需要像javascript那样先申明，直接`message = "It's a message. "`，而且没有`;`


#### 2. 函数  

    coffee = ->
      confirm "Ready for some Coffee?
这段coffeescript代码编译成javascript之后是：

    coffee = function() {
      return confirm("Ready for some Coffee?");
    };
对比一下可以看出来，`function(){}`写成了`->`，去掉了每行的`;`，而且没有`return`这个关键字，这和ruby一样，隐式地返回每个函数的最后一个表达式的值。
上面的这段代码只是返回一个常量，那包含参数的函数该如何呢？

    coffee = (message) ->
      answer = confirm message
      "Your answer is #{message}"
把参数列表放在`->`左边，还有就是字符串插值语法和ruby类似：`"A#{expression}Z"`。  
如果想给参数默认值的话，就可以这样`coffee = (message = 'Hello') -> `  
接下来是函数的调用，调用上面的这个函数：如果调用的是没有参数的函数的话：`coffee`，注意，不需要括号 ; 一个参数：`coffee('Yo')`，或者省略括号`coffee 'Yo'` ; 对于多个参数的函数调用也是类似的，比如`coffee('Yo', 2)`，同样也可以去掉括号`coffee 'Yo', 2`。


#### 3. 流程控制  
    if age < 18
      alert 'Under age
    else
      alert 'of age'
当然，还有更紧凑的写法直接把它们都写在一行内：`if age < 18 then alert 'Under age' else alert 'of age'`  
还有coffeescrip和javascript中操作符的差别：  
![img](http://m3.img.libdd.com/farm5/2013/0604/10/AF942A3070DE58C1EBF0032302066B4EE212E1302E9B5_500_430.jpg)  
可见coffeescript移除了js中`==`那样宽松的，强制类型转化的等于检查，改成全部用`===`进行严格比较。  
coffeescript同样支持`unless`式的判断。  
coffeescript中用`switch .. when .. then ..`代替javascript中的`switch .. case .. return ..`  
判断变量是不是`defined`或者是不是`null`可以用`？`。比如`cupsOfCoffee?`会判断它是否被定义或者是否为空。  
判断某个属性存在的时候，才会调用属性上的方法的情况，这时候也可以用`?`，比如`coffeePot?.brew()`，只有当`coffeePot`不为空的时候才会调用`brew()`方法。类似同样适用于判断函数是否存在才调用。  
判断赋值：`cupsOfCoffee ?= 0`等同于`cupsOfCoffee = 0 unlesss cupsOfCoffee?`


#### 4. 数组和循环  
coffeescript引入了ruby式的语法，用来定义连续整数数组，例如：  
`range = [1..4]` 相当于javascript的 `var range = [1, 2, 3, 4];`  
`range = [1...4]` 相当与javascript的 `var range = [1, 2, 3];`  
PS：区间也可以是倒序的如 `[5..1]`  
切分：`['a', 'b', 'c', 'd'][0...3]` 输出 `['a', 'b', 'c']`  
`['a', 'b', 'c', 'd'][0..3]` 输出 `['a', 'b', 'c', 'd']`   
非整数数组使用JSON风格的语法来定义：`locations = ['Changsha', 'Beijing']` ，或者可以把数组中的逗号换成一个回车。  
判断某个值是否在数组内可以用`in`，比如`'Changsha' in locations`会返回`true`。  
循环`for...in`，继续上面的locations数组，`alert "location: #{loc}" for loc in locations`  ；还可以用`by`设置每次循环的步长，如`alert x for x in [0..10] by 2` 会输出`[0, 2, 4, 6, 8, 10]`。  
条件迭代：`while` 和 `until` ，一直执行循环直到条件不满足 ; `loop`用于实现循环体一直执行直到被break或者return强制退出。  
对象：

    coffee =
      name: 'French'
      strength: 1
      brew: -> alert("brewing #{@name}")

调用该对象的属性或方法 `coffee.name` or `coffee.brew()`   
数组模式匹配： javascript是严格地一次赋值一个，如果想把一列值赋给一列变量，可能得写一个自定义函数了，coffeescrip则只需一行代码：`[x, y, z] = ['Joe', 'Jack', 'Jim']` ，它其实等价于把数组中的每个元素单独列出来赋值。  
吸收操作符：`a = b ? c` 表示“如果b存在则a=b，否则a=c”，同样`a = b?.property ? c` 表示”b和b.property都存在时，a=b.property，否则a=c“。

#### 5. 类和模块
原型： 原型其实就是一种对象，由原型衍生出来的所有对象都能共享原型的属性，一个对象的原型通常可以通过prototype属性来访问。一个简短的例子：  
`Boy::sing = -> console.log "It's ain't easy "`  
 这里 `Boy::sing` 是 `Boy.protootype.sing` 的简写。  
类：在背后，CoffeeScript使用JavaScript原生的原型来产生类，为静态变量继承以及上下文持久化添加了一点语法糖，而暴露给开发者的全部只有一个class关键字。看一个完整的例子：
  
    class Coffee
      constructor: (@name, @strength=1) ->

      brew: -> alert "brewing #{@name}"
      pour: (amount=1) ->
        if amount is 1
         "Poured a single cup"
        else
         "Poured #{amount} cups"
* constructor是构造函数，必须用这个名称，类似ruby中的initialize或者Python的__init__  
* `@` 相当与javascript中的 `this.`  
* `constructor: (@name, @strength=1) ->`实际是

      constructor: (name, strength=1) ->
        @name = name
        @strength = strength
继承：CoffeeScript通过extends关键字来实现继承，具体看下面这个例子：

      class MaxgoodHouse extends Coffee
        constructor: (@name, @strength=0) ->
          @brand = "Maxgood House"
        brew: -> alert "Brewing #{@brand} #{@name}"
        pour: (amount=1) ->
          "#{super(amount)}, but it sucks"
* super()的意思是“调用父类同名的方法”，在子类构造函数开始时就调用一下super()通常是明智之举。  
* 如果子类没有新定义 `constructor` ，则默认调用其父类的 `constructor`  

--------------------------
总结到越后面越有种自己什么都没懂的感觉（当然也确实是很多地方没太明白），甚至会觉得不知道该记下点什么。不得不承认，自己在javascript方面太弱了，所以面对这么优雅的coffeescript也会有不知所措 =_= ||  以后的项目里面一定要多写些javascript啊啊啊