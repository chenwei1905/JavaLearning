# [stream](https://github.com/chenwei1905/JavaLearning)
## Stream简介
在程序编写过程中,集合的处理应该是很普遍的;Java8对collection处理花了很大的功夫，如果从JDK7过度到JDK8,这一块也可能是我们感受最为明显的;
Java8中引入了流的概念,这个流和我们使用的IO中的流并不太相同;
所有继承自Collection的接口都可以转换为Stream;

## Stream常用操作
Stream的方法分为两类，
1. 一类叫惰性求值，
2. 一类叫及早求值;

判断一个操作是惰性求值还是及早求值很简单：只需看它的返回值。如果返回值是 Stream，那么是惰性求值。其实可以这么理解，如果调用惰性求值方法，Stream 只是记录下了这个惰性求值方法的过程，并没有去计算，等到调用及早求值方法后，就连同前面的一系列惰性求值方法顺序进行计算，返回结果。
Stream.惰性求值.惰性求值. ... .惰性求值.及早求值
整个过程和建造者模式有共通之处。建造者模式使用一系列操作设置属性和配置，最后调 用一个 build 方法，这时，对象才被真正创建。

### Collect(toList()) 
`Collect(toList())`方法由Stream里的值生成的一个列表，是一个及早求值操作，可以理解为Stream向Collection的转换;
注意这边的toList()其实是Collectors.toList()因为采用了静态倒入，所以看起来显得简洁;
```java
@Test
public void test() {
    List<String> collected = Stream.of("a", "b", "c").collect(Collectors.toList());
}

```

### map
如果由一个函数可以将一种类型的值转换成另一种类型，Map操作就可以使用该函数，将一个流中的值转换成一个新的流; 
map方法就是接受的一个Function的匿名函数类，进行的转换;
```java
   @Test
   public void Test() {
        List<String> collected = Stream.of("a", "b", "hello").map(string -> string.toUpperCase()).Collect(toList());

   }
```
### filter
遍历数据并检查其中的元素时，可尝试Stream中提供的新方法filter;
filter方法就是接受的一个Predicate的匿名函数类，判断对象是否符合条件，符合条件的才保留下来；
```java
    @Test
    public void Test() {
        List<String> numbers = Stream.of("a", "1labe", "abc1")
            .filter(value -> isDigit(value.charAt(0)))
            .collect(toList());
    }

```
### flatMap
flatMap方法可用Stream替换值，然后将多个Stream连接成一个Stream,flatMap最常用的操作就是合并多个Collection
```java
@Test
public void test() {
    List<Integer> together = Stream.of(asList(1,2), asList(3,4))
        .flatMap(numbers -> numbers.stream())
        .collect(toList());
}

```
### reduce(max, average, min, count)
reduce操作可以实现从一组值中生成一个值;在上述例子中用到的Count，min和max方法，因为常用而被纳入到标准库中;事实上，这些方法都是reduce操作;
```java
 @Test
 public void test() {
     List<Integer> list = Lists.newArrayList(3, 5, 2, 9, 1);
int maxInt = list.stream()
				 .max(Integer::compareTo)
				 .get();
int minInt = list.stream()
				 .min(Integer::compareTo)
				 .get();
 }
```
`注意点`  
1. max 和 min 方法返回的是一个 Optional 对象（对了，和 Google Guava 里的 Optional 对象是一样的）。Optional 对象封装的就是实际的值，可能为空，所以保险起见，可以先用 isPresent() 方法判断一下。Optional 的引入就是为了解决方法返回 null 的问题。
2. Integer::compareTo 也是属于 Java 8 引入的新特性，叫做 方法引用（Method References）。在这边，其实就是 (int1, int2) -> int1.compareTo(int2) 的简写，可以自己查阅了解，这里不再多做赘述。
```java
    @Test
    public void test() {
        int result = Stream.of(1, 2, 3, 4)
				   .reduce(0, (acc, element) -> acc + element);
                
    }
    //10
```

## 数据的并行化操作
Stream 的并行化也是 Java 8 的一大亮点。数据并行化是指将数据分成块，为每块数据分配单独的处理单元。这样可以充分利用多核 CPU 的优势。

并行化操作流只需改变一个方法调用。如果已经有一个 Stream 对象，调用它的 parallel() 方法就能让其拥有并行操作的能力。如果想从一个集合类创建一个流，调用 parallelStream() 就能立即获得一个拥有并行能力的流。

```java
    @Test
    public void test() {
        int sumSize = Stream.of("Apple", "Banana", "Orange", "Pear")
					.parallel()
					.map(s -> s.length())
					.reduce(Integer::sum)
					.get();
    }

```
如果你去计算这段代码所花的时间，很可能比不加上 parallel() 方法花的时间更长。这是因为数据并行化会先对数据进行分块，然后对每块数据开辟线程进行运算，这些地方会花费额外的时间。并行化操作只有在 数据规模比较大 或者 数据的处理时间比较长 的时候才能体现出有事，所以并不是每个地方都需要让数据并行化，应该具体问题具体分析。

## 收集器
Stream 转换为 List 是很常用的操作，其他 Collectors 还有很多方法，可以将 Stream 转换为 Set, 或者将数据分组并转换为 Map，并对数据进行处理。也可以指定转换为具体类型，如 ArrayList, LinkedList 或者 HashMap。甚至可以自定义 Collectors，编写自己的收集器
## 元素顺序

另外一个尚未提及的关于集合类的内容是流中的元素以何种顺序排列。一些集合类型中的元素是按顺序排列的，比如 List；而另一些则是无序的，比如 HashSet。增加了流操作后，顺序问题变得更加复杂。

总之记住。如果集合本身就是无序的，由此生成的流也是无序的。一些中间操作会产生顺序，比如对值做映射时，映射后的值是有序的，这种顺序就会保留 下来。如果进来的流是无序的，出去的流也是无序的。

如果我们需要对流中的数据进行排序，可以调用 sorted 方法

```java 
    @Test
    public void test() {
        List<Integer> list = Lists.newArrayList(3, 5, 1, 10, 8);
List<Integer> sortedList = list.stream()
							   .sorted(Integer::compareTo)
							   .collect(Collectors.toList());
    }

```
## Stream操作collection集合
```java
public class CollectionStream {
    public static void main(String[] args) {
        // 创建一个集合
        Collection objs = new HashSet();
        objs.add(new String("C语言中文网Java教程"));
        objs.add(new String("C语言中文网C++教程"));
        objs.add(new String("C语言中文网C语言教程"));
        objs.add(new String("C语言中文网Python教程"));
        objs.add(new String("C语言中文网Go教程"));
        // 统计集合中出现“C语言中文网”字符串的数量
        System.out.println(objs.stream().filter(ele -> ((String) ele).contains("C语言中文网")).count()); // 输出 5
        // 统计集合中出现“Java”字符串的数量
        System.out.println(objs.stream().filter(ele -> ((String) ele).contains("Java")).count()); // 输出 1
        // 统计集合中出现字符串长度大于 12 的数量
        System.out.println(objs.stream().filter(ele -> ((String) ele).length() > 12).count()); // 输出 1
        // 先调用Collection对象的stream ()方法将集合转换为Stream
        // 再调用Stream的mapToInt()方法获取原有的Stream对应的IntStream
        objs.stream().mapToInt(ele -> ((String) ele).length())
                // 调用forEach()方法遍历IntStream中每个元素
                .forEach(System.out::println);// 输出 11 11 12 10 14
    }
}

```

## 理解Stream流水线
[理解Stream流水限](https://www.cnblogs.com/CarpenterLee/p/6637118.html)  
思考下面的代码是为了求出以字母A开头的字符串的最大长度，内部是如何实现的？
```java
    int longestStringLengthStartingWithA
        = strings.stream()
              .filter(s -> s.startsWith("A"))
              .mapToInt(String::length)
              .max();
```
一种直接的方式是，为每一个函数调用执行一次迭代，并将处理的结果放入某种数据结构中这样做是可以的，但是会带来两个问题：
1. 迭代次数多。迭代次数跟函数调用的次数相等。
2. 频繁产生中间结果。每次函数调用都产生一次中间结果，存储开销效率无法接受。
如果不用Stream API我们希望的是在一次迭代中完成所有操作，如下：
```java
    int longest = 0;
for(String str : strings){
    if(str.startsWith("A")){// 1. filter(), 保留以A开头的字符串
        int len = str.length();// 2. mapToInt(), 转换成长度
        longest = Math.max(len, longest);// 3. max(), 保留最长的长度
    }
}
```
所以在Stream流水线中我们需要解决下面的4个问题
1. 用户的操作如何记录
2. 操作如何叠加
3. 叠加之后的操作如何执行
4. 执行之后的结果保存在哪里


### 操作如何记录


注意这里使用的是“操作(operation)”一词，指的是“Stream中间操作”的操作，很多Stream操作会需要一个回调函数（Lambda表达式），因此一个完整的操作是<数据来源，操作，回调函数>构成的三元组。Stream中使用Stage的概念来描述一个完整的操作，并用某种实例化后的PipelineHelper来代表Stage，将具有先后顺序的各个Stage连到一起，就构成了整个流水线。




### 操作是如何叠加
以上只是解决了操作记录的问题，要想让流水线起到应有的作用我们需要一种将所有操作叠加到一起的方案。你可能会觉得这很简单，只需要从流水线的head开始依次执行每一步的操作（包括回调函数）就行了。这听起来似乎是可行的，但是你忽略了前面的Stage并不知道后面Stage到底执行了哪种操作，以及回调函数是哪种形式。换句话说，只有当前Stage本身才知道该如何执行自己包含的动作。这就需要有某种协议来协调相邻Stage之间的调用关系。

这种协议由Sink接口完成，Sink接口包含的方法如下表所示

方法名|作用 
----|----
void begin(long size) | 开始遍历元素之前调用该方法，通知Sink做好准备。
void end() | 所有元素遍历完成之后调用，通知Sink没有更多的元素了。
boolean cancellationRequested() | 是否可以结束操作，可以让短路操作尽早结束。
void accept(T t) | 遍历元素时调用，接受一个待处理元素，并对元素进行处理。Stage把自己包含的操作和回调方法封装到该方法里，前一个Stage只需要调用当前Stage.accept(T t)方法就行了。


### 叠加之后的操作如何执行
ink完美封装了Stream每一步操作，并给出了[处理->转发]的模式来叠加操作。这一连串的齿轮已经咬合，就差最后一步拨动齿轮启动执行。是什么启动这一连串的操作呢？也许你已经想到了启动的原始动力就是结束操作(Terminal Operation)，一旦调用某个结束操作，就会触发整个流水线的执行。

结束操作之后不能再有别的操作，所以结束操作不会创建新的流水线阶段(Stage)，直观的说就是流水线的链表不会在往后延伸了。结束操作会创建一个包装了自己操作的Sink，这也是流水线中最后一个Sink，这个Sink只需要处理数据而不需要将结果传递给下游的Sink（因为没有下游）。对于Sink的[处理->转发]模型，结束操作的Sink就是调用链的出口。


### 执行后的结果放置
最后一个问题是流水线上所有操作都执行后，用户所需要的结果（如果有）在哪里？首先要说明的是不是所有的Stream结束操作都需要返回结果，有些操作只是为了使用其副作用(Side-effects)，比如使用Stream.forEach()方法将结果打印出来就是常见的使用副作用的场景（事实上，除了打印之外其他场景都应避免使用副作用），对于真正需要返回结果的结束操作结果存在哪里呢？

**特别说明：副作用不应该被滥用，也许你会觉得在Stream.forEach()里进行元素收集是个不错的选择，就像下面代码中那样，但遗憾的是这样使用的正确性和效率都无法保证，因为Stream可能会并行执行。大多数使用副作用的地方都可以使用归约操作更安全和有效的完成。**


返回类型 |对应结束操作
----|----
boolean | anyMatch() allMatch() noneMatch()
Optional | findFirst() findAny()
归约结果 | reduce() collect()
数组 | toArray()










