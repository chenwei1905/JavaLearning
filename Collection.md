# [集合](https://github.com/chenwei1905/JavaLearning)
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
#### Hash(哈希)
散列函数的基本特性:`根据同一散列函数计算出的散列值如果不同，那么输入值肯定也不同。但是，根据同一散列函数计算出的散列值如果相同，输入值不一定相同。
两个不同的输入值，根据同一散列函数计算出的散列值相同的现象叫做碰撞`  
常见的hash函数如下:
名称|说明
----|----
直接定址法|直接以关键字k或者k加上某个常数（k+c）作为哈希地址。
数字分析法|提取关键字中取值比较均匀的数字作为哈希地址。
除留余数法|用关键字k除以某个不大于哈希表长度m的数p，将所得余数作为哈希表地址。
分段叠加法|按照哈希表地址位数将关键字分成位数相等的几部分，其中最后一部分可以比较短。然后将这几部分相加，舍弃最高进位后的结果就是该关键字的哈希地址。
平方取中法|如果关键字各个部分分布都不均匀的话，可以先求出它的平方值，然后按照需求取中间的几位作为哈希地址。
伪随机数法|采用一个伪随机数当作哈希函数。
#### HashMap的数据结构
在Java中，保存数据有两种比较简单的数据结构：数组和链表。**数组的特点是：寻址容易，插入和删除困难；而链表的特点是：寻址困难，插入和删除容易**上面我们提到过，常用的哈希函数的冲突解决办法中有一种方法叫做链地址法，其实就是将数组和链表组合在一起，发挥了两者的优势，我们可以将其理解为链表的数组。
#### HashMap和HashTable的对比
1. HashMap默认的初始化大小为16，之后每次扩充为原来的2倍。
2. HashTable默认的初始大小为11，之后每次扩充为原来的2n+1。
3. 当哈希表的大小为素数时，简单的取模哈希的结果会更加均匀，所以单从这一点上看，HashTable的哈希表大小选择，似乎更高明些。因为hash结果越分散效果越好。
4. 在取模计算时，如果模数是2的幂，那么我们可以直接使用位运算来得到结果，效率要大大高于做除法。所以从hash计算的效率上，又是HashMap更胜一筹。
5. 但是，HashMap为了提高效率使用位运算代替哈希，这又引入了哈希分布不均匀的问题，所以HashMap为解决这问题，又对hash算法做了一些改进，进行了扰动计算。


## \* 集合接口线程的安全性
分类|实现|线程安全|排序|特点
---|----|------|----|---
List| ArrayList| 否|插入排序| 随机访问性能高
List| LinkedList| 否| 插入排序| 随机访问性能低,头尾操作性能高,不占用冗余空间
List| Vector| 是| 插入排序| 并发性能不高,线程越多性能越差
List| CopyOnWriteArrayList|是| 插入排序 |并发性能高| 占用冗余空间
Map | HashMap | 否|无序| 读写性能高| 接近于O(1)
Map | LinkedHashMap | 否 | 插入排序 |可按插入顺序遍历,性能与HashMap接近
Map | HashTable | 是 | 无序 | 并发性能不高,线程越多性能越差
Map | ConcurrentHashMap | 是 | 无序 | 并发性能比HashTable高
Map | TreeMap | 否 | key升序或降序 | 有序,读写性能O(logN)
Map | ConcurrentSkipListMap | 是 | key升序或降序 | 线程安全,性能与并发数无关,内存空间占用较大
Set | HashSet | 否 | 无序 | 同hashMap
Set | LinkedHashSet | 否 | 插入排序 | 同LinkedHashMap
Set | TreeSet | 否 | 对象升序或降序 | 同TreeMap
Set | ConcurrentSkipListSet| 否 | 无序| 同ConcurrentSkipListMap
Queue | ConcurrentLinkedQueue | 是 | 插入顺序 | 非阻塞
Queue | LinkedBlockingQueue | 是 | 插入排序 | 阻塞,无界
Queue | ArrayBlockingQueue | 是 | 插入排序 | 阻塞,有界
Queue | SynchronousQueue | 是 | | 不存储任何元素,向其中插入元素的线程会阻塞,直到有另一个线程将这个元素取走,反之亦然
Queue | PriorityQueue | 否 | 对象自然序或者自定义排序| 根据元素的优先级进行排序,保证自然序或自定义序最小的对象先出列
Deque | ConcurrentLinkedDeque | 是 | 插入排序 | 非阻塞
Deque | LinkedBlockingDeque | 是 | 插入顺序 | 阻塞,无序


## \* 集合内部实现算法的比较和场景说明
## \* 并发编程 volatile关键字和atomic包



