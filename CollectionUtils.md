# [集合工具类的使用](https://github.com/chenwei1905/JavaLearning)
## 基本工具类的介绍
目前应用的集合类在`com.dexi.utils.core.collection`中
[官方文档地址](http://docs.dxids.com/server_framework/utils/)
## 类的基本介绍

### ArrayIter

构造方法 | 说明
--------| ----------
 ArrayIter(final Object array) | 普通的基本构造
  ArrayIter(final Object array, final int startIndex) | 带有开始序列的数组
  ArrayIter(final Object array, final int startIndex, final int endIndex) | 


  接口 | 说明
----------| -----------
reset() | 重置开始序列


```java
\\测试用例


```


### BoundedPriorityQueue
构造方法 | 说明
--------| --------------
BoundedPriorityQueue(int capacity) | 
BoundedPriorityQueue(int capacity, final Comparator<? super E> comparator) | 


接口 | 说明
-----| -----------
offer(E e) | 


```java 
\\测试用例
```

### CollUtils(重点)
接口 | 说明
---------|---------


### ConcurrentHashSet


### CopiedIter


### EnumerationIter

### IteratorEnumeration

### IterUtils

### LineIter


### ComparableComparator

