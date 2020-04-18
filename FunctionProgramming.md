## 软件系统的整体设计说明
组织大型程序，会受到我们对于被模拟系统的认识的支配，一般有两种特点鲜明的组织策略，它们源于对系统结构的两种非常不同的世界观;
1. 第一种组织策略式将注意里集中在对象上，将一个大型系统看成一大批的对象，它们的行为可能随着时间的进展而不断变化，
2. 另一种组织策略将注意力集中在流过系统的信息流上，非常像电子工程师观察一个信号处理系统；

基于对象的途径和流的途径，都对程序设计提出了具有意义的语言要求，对于对象而言，我们必须关注计算对象可以怎样变化而又同时保持其标识，这将抛弃函数式编程的代换模型，转向更机械式的，理论上也更不容易把握的计算的环境模型；在处理对象、变化和标识时，各种困难的基本根源在于我们需要在这一计算模型中与时间搏斗；如果允许程序的并发执行的可能性，事情就会变的困难许多，流方式特别能够用于松懈在我们的模型中对时间的模拟与计算机求值过程中的各种事情发生的顺序，可以通过一种延时求值的技术做到这一点，将流编程之前，首先要介绍一下函数式编程；  
**代换模型和环境模型的区别**

## 函数式编程简介
函数式编程作为一种编程范式，在科学领域，是一种编写计算机程序数据结构和元素的方式，它把计算过程当做是数学函数的求值，而避免更改状态和可变数据;
一般来讲就是数学上怎么用,你编程就可以这么编写;因为函数式编程没有赋值的负作用;
相同的输入只能得到相同的输出;并且函数可以用作变量的命名,可以提供给过程作为参数,可以作为返回结果,可以包含在数据接口中,";  
**函数式编程语言里面没有for/next循环，因为这逻辑意味着有状态的改变相替代的是，这种循环逻辑在函数式编程语言里是通过递归、把函数当成参数传递的方式实现的;**


## Lambda表达式
Java Lambda表达式的一个重要用法是简化某些匿名内部类（Anonymous Classes）的写法。实际上Lambda表达式并不仅仅是匿名内部类的语法糖，JVM内部是通过invokedynamic指令来实现Lambda表达式的。
下面是匿名内部类和Lambda式的转化
```
```
## 函数式接口
能够使用lambda的依据是必须有相应的函数式接口(函数接口,是指内部只有一个抽象方法的接口),这一点跟java是强类型语言吻合,也就是你不能在任何地方任性的写lambda的写lambda表达式,实际上lambda的类型就是对应函数接口的类型;
**这里可以了解一下类型签名的概念**;  
为了使用的方便java8给我提供基本的函数式接口;其中有4类是最基本的;
1. Consumer<T>: 消费型接口(void accept(T t)) --参数没有返回值
``` java
/**
 * 消费型接口Consumer<T>
 */
@Test
public void Test1() {
    cosum(500, (x) -> (system.out::println)); //函数作为参数
}
//函数的声明
public void cosum(Integer money, Consumer<Integer> c)  {
    c.accept(money);
}
```

2. Supplier<T> 供给型接口（T get（））-- 没有输入，只有返回值

```java
/**
 * 供给型接口
 */
 @Test
 public void test() {
     Random ran = new Random();
     List<Integer> list = supplier(10, () -> ran.nextInt(10);

     for (Integer i : list) {
         System.out.println(i);
     }
 }
 /**
  * 随机产生sum个数量得集合
  *
  

```


## 高阶函数
## 闭包
说到闭包,需要知道约束变量和自由变量,
1. 约束变量指的是函数内部的变量和用作函数参数的变量
2. 不是约束变量都可以称作自由变量
闭包指的是一个持有自由变量的函数和该自由变量所组成的环境就是闭包;
## 函数组合
## 科里化和部分求值 