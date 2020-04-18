# 集合
## 集合的概念
Collection表示一组对象集合体,集合体是一类特殊情形的类区间,它是属于一个类的所有对象的集合体,当该类的一个对象被创建该对象可以被插入到类区间中,
并且一旦对象被删除也可以从类区间中移除,类区间允许类能像关系一样对待,从而检查类中所有的对象;  
Collection函数库是java.util包下的一些接口和类，类是用来产生对象存放数据用的，而接口是访问数据的方式;  
*Collection函数库和数组的两点不同*： 
1. 数据的容量有限制的,而Collection库没有这样的限制，它的容量可以自动调节;  
2. Collection函数库只能用来存放对象，而数组没有这样的限制;
如下是集合框架简图:  
![集合框架](https://github.com/chenwei1905/JavaLearning/blob/master/image/collection1.png)  
![集合框架](https://github.com/chenwei1905/JavaLearning/blob/master/image/collection2.png)
## 集合的类型
Collection接口：定义了存取一组对象的方法，其子接口Set和List分别定义了存储方式;  
Set中的数据对象没有顺序且不可以重复;  
List 中的数据对象有顺序且可以重复;  
Map 接口定义了存储”键(key)-值(value)映射对的方法”  
## Collection接口  
接口定义  | 说明
------------ | -------------
Boolean add(Object element) | 增加元素
Boolean remove(Object element)| 删除元素  
Boolean contains(Object element) | 包含
Boolean isEmpty()| 判空
void clear()| 集合的删除
Iterator iterator()|
Boolean containsAll(Collection c)| 
Boolean addAll(Collection c)|
Boolean removeAll(Collection c)|
Boolean retainAll(Collection c)|
Object[] toArray()|

```java
\\接口练习


```
**注意点**  
1. Collection类对象在调用remove、contains等方法时需要比较对象是否相等,这会涉及到对象类型的equals方法和hashCode方法;对于自定义的类型,需要重写equals和hashCode方法以实现自定义的对象相等规则;
2. java中规定,两个内容相同的对象应该具有相等的HashCodes



## Iterator接口
所有现实了Collection接口的容器类都有一个Iterator方法用以返回一个实现了Iterator接口的对象;  
Iterator对象称作迭代器,用以方便的实现对容器内元素的遍历操作:  

接口 | 接口说明
-----| -------
Boolean hasNext()|判断是否有元素没有返回
Object next() |返回游标当前位置的元素并将游标移动到下一个位置
Void remove() |删除游标左边的元素，在执行完next之后,操作只能执行一次 
```java
\\接口练习

```


## Set接口
Set接口是Collection接口的子接口,Set接口没有提供额外的方法,Set接口的特性是容器类中的元素是没有顺序的,而且不可以重复;
```java
\\接口练习
```

## List接口
List 容器中的元素都对应一个整数型的序记载其在容器中的位置，可以根据序号存取容器中的元素;
增加了有关序的方法
接口|说明
----|----
Void add(Object element);|
Void add(int index, Object element);|
Object get(int index);|
Object set(int index, Object element);|修改某一位置的元素
Object remove(int index);|
Int indexOf(Object o);|如果没有该数据，返回-1
```java
\\接口练习
```

### List常用算法
java.util.collections提供了一些静态方法实现了基于List容器的一些常用算法
方法|说明
-----|----
Void sort(List)| 对List容器内的元素排序，排序的规则是按照升序进行排序
Void shuffle(List) |对List容器内的元素进行随机排列
Void reverse(List) |对List容器内的元素进行逆序排列
Void fill(List, Object) |用一个特定的对象重写整个List容器
Int binarySearch(List, Object) |对于顺序的List容器，采用折半查找方法查找特定对象

## Comparable接口
根据上面的算法如何确定集合中对象“大小”顺序,就需要java.lang.Comparable接口 
接|说明
--|---
Public int compareTo(Object obj)| 返回0表示this=obj,返回正整数表示this > obj,返回负数表示 this < obj,实现了Comparable接口的类通过实现compareTo方法从而确定该类对象的排列方式

```java
 \\接口练习

```

**注意点**  
Java中的Comparable和Comparator区别比较;  
个性化比较:如果实现类没有实现Comparable接口，又想对两个类进行比较（或者实现类实现了Comparable接口，但是对compareTo方法内的比较算法不满意），那么可以实现Comparator接口，自定义一个比较器，写比较算法;
解耦:实现Comparable接口的方式比实现Comparator接口的耦合性要强一些，如果要修改比较算法，要修改Comparable接口的实现类，而实现Comparator的类是在外部进行比较的，不需要对实现类有任何修改。从这个角度说，其实有些不太好，尤其在我们将实现类的.class文件打成一个.jar文件提供给开发者使用的时候


## Map接口
实现Map接口的类用来存储(key-value)对;
Map接口的实现类有HashMap和TreeMap等;
Map中存储的键值对通过键来标识,所以键值不能重复;
接口|说明
---|---
Object put(Object key,Object value);|
Object get(Object key);|
Object remove(Object key);|
Boolean containsKey(Object key);|
Boolean containsValue(Object value);|
Int size();|
Boolean isEmpty();|
Void putAll(Map t);|
Void clear();|
### Map的Hash值说明
## \* 集合接口线程的安全性
## \* 集合内部实现算法的比较和场景说明



