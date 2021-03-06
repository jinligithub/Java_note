1，我们先来写个代码吧，让我手撕了一个生产者消费者问题，刚写完一个生产者，面试官就等不及了，看了我代码，让我口述给他剩下的。 

2，Java实现多线程有哪些方式？问我刚才的生产者消费者还可以用什么java并发包里的那些结构写出来？ 

3，Java中线程的状态有哪些？ 

4，Java中wait 和sleep的区别，wait和notify的区别 

5，项目相关 

6，redis中list的底层数据结构是什么样的 

7，redis中事务是怎么实现的 

8，redis中server和client通信方式什么(这个真的没注意到) 

9，项目中除了redis你还知道还有其他哪些工具可以实现功能？ 

10，redis和memcached的区别，各自优势 

11，把innodb的索引结构划给我看看 

12，innodb和myisam的区别





1、对测试开发的理解，对这一块需要哪方面的一些技能

2、所用的编程语言，对那个比较熟悉

3、所用到的测试框架，介绍

4、是否接触到一些客户端的主件

5、Java是否会有内存溢出

6、java实现多台机器master主从结构

7、印象比较深的Bug以及定位方法

8、有没有什么问题要问面试官的？



<https://blog.csdn.net/CCUTwangning/article/details/53666659>



## J2SE基础

### 1.九种基本数据类型的大小，以及他们的封装类。

* Java提供了一组基本数据类型，包括  boolean, byte, char, short,  int, long, float, double, void. 
* java也提供了这些类型的封装类，分别为 Boolean, Byte, Character, Short, Integer, Long, Float, Double, Void

**分类**

* 对象型(Object的直接子类):Boolean、Character(char)；
* 数值型(Number的直接子类):Byte、Double、Short、Long、Integer(int)、Float



**原因**：

1. java中使用基本类型来存储语言支持的基本数据类型，这里没有采用对象，而是使用了传统的面向过程语言所采用的基本类在型，主要是从性能方面来考虑的：因为即使最简单的数学计算，使用对象来处理也会引起一些开销，而这些开销对于数学计算本来是毫无必要的。
2. 但是在java中，泛型类包括预定义的集合，使用的参数都是对象类型，无法直接使用这些基本数据类型，所以java又提供了这些基本类型的包装器。

**区别：**

1. 基本数据类型只能按值传递，而封装类按引用传递

2. 基本类型在堆栈中创建；而对于对象类型，对象在堆中创建，对象的引用在堆栈中创建。基本类型由于在堆栈中，效率会比较高，但是可能会存在内存泄漏的问题

### 2.Switch能否用string做参数？

* 在 [Java](https://www.baidu.com/s?wd=Java&tn=44039180_cpr&fenlei=mv6quAkxTZn0IZRqIHckPjm4nH00T1Yvn163mvfdPjRzPjmvm1bd0ZwV5Hcvrjm3rH6sPfKWUMw85HfYnjn4nH6sgvPsT6KdThsqpZwYTjCEQLGCpyw9Uz4Bmy-bIi4WUvYETgN-TLwGUv3EnW0dPjD3rjbLrjT3n1TkPjb3Ps) 7之前，switch 只能支持 byte、short、char、int或者其对应的封装类以及 Enum 类型。在 [Java](https://www.baidu.com/s?wd=Java&tn=44039180_cpr&fenlei=mv6quAkxTZn0IZRqIHckPjm4nH00T1Yvn163mvfdPjRzPjmvm1bd0ZwV5Hcvrjm3rH6sPfKWUMw85HfYnjn4nH6sgvPsT6KdThsqpZwYTjCEQLGCpyw9Uz4Bmy-bIi4WUvYETgN-TLwGUv3EnW0dPjD3rjbLrjT3n1TkPjb3Ps) 7中，String支持被加上了

### 3. equals与==的区别。

* “==”比较的是值【变量(栈)内存中存放的对象的(堆)内存地址】

*  equal用于比较两个对象的值是否相同【不是比地址】

**【特别注意】**

* Object类中的equals方法和“==”是一样的，没有区别，
* 而String类，Integer类等等一些类，是重写了equals方法，才使得equals和“==不同”，所以，当自己创建类时，自动继承了Object的equals方法，要想实现不同的等于比较，必须重写equals方法。
* "=="比"equal"运行速度快,因为"=="只是比较引用.

### 4.请解释String类中两种对象实例化的区别

1. **直接赋值**：只会开辟一块堆内存空间，并且该字符串对象可以自动保存在对象池中以供下次使用。
2. **构造方法**：会开辟两块堆内存空间，其中一块成为垃圾空间，不会自动保存在对象池中，可以使用intern()
    方法手工入池

**注意：**

* 在String类中提供有方法入池操作public String intern()
* 在JVM底层实际上会自动维护一个对象池**（字符串对象池）**，如果现在采用了直接赋值的模式进行String类的对象实例化操作，那么该实例化对象（字符串内容）将自动保存到这个对象池之中。如果下次继续使用直接赋值的模式声明String类对象，此时对象池之中如若有指定内容，将直接进行引用；如若没有，则开辟新的字符串对象而后将其保存在对象池之中以供下次使用



### 5.Object有哪些公用方法？

* **public String toString()   取得对象信息**：默认Object类提供的toString()方法只能够得到一个对象的地址

* **public Boolean equals(Onject obj)    判断对象是否相等**：实际上String类的equals()方法就是覆写的Object类中的equals()方法。

* **hashCode()**：返回其所在对象的物理地址（哈希码值），常会和equals方法同时重写，确保相等的两个对象拥有相等的.hashCode。先HashCode，在比较equals

* **getClass()方法**：返回一个Class对象，反射里面用到

* **finalize()方法**：垃圾回收的时候会用到，匿名对象回收之前会调用到

* **wait()方法**：使线程停止运行，会释放对象锁。只能在同步方法或同步代码块中调用

* **notifyAll()：**唤醒所有在该对象上等待的线程。一旦该对象被解锁，他们就会去竞争。 

* **notify()**：必须在同步方法或同步代码块中调用，用来唤醒等待在该对象上的线程。如果有多个线程等待，则任意挑选一个线程唤醒。notify()方法执行后，唤醒线程不会立刻释放对象锁，要等待唤醒线程全部执行完毕后才释放对象锁。

  



### 6. 装箱与拆箱

* **装箱**：将基本数据类型变为包装类对象，利用每个包装类提供的构造方法实现
* **拆箱**：将包装类中的包装的基本数据类型取出，利用XXValue()      intValue()

![1565335335252](C:\Users\Z\AppData\Roaming\Typora\typora-user-images\1565335335252.png)



**注意**

* 对于Ingetre var =?  在[-128.127]的赋值，Ingeter对象在常量池产生（这个区间内的 Integer 值可以直接使用==进行判断）会复用已有对象。这个区间外的所有数据，都在堆上产生，不会复用已有对象。推荐使用 equals 方法进行判断

### 7.字符串与基本数据类型的转换

1. **String变为int 类型（Integer类）**：public static int parseInt(String s) throws NumberFormatExceptio
2. **String变为double类型（Double类）**：public static double parseDouble(String s) throws NumberFormatException
3. **String变为Boolean类型（Boolean类）****：public static boolean parseBoolean(String 

### 8.要将基本数据类型变为字符串：

1. 任何数据类型使用了"+"连接空白字符串就变为了字符串类型。
2. 使用String类中提供的valueOf()方法，此方法不产生垃圾

**注意**

* 需要注意的是,将字符串转为数字的时候,字符串的组成有非数字,那么转换就会出现错误 (NumberFormatException）

### 9.Java的四种引用，强弱软虚，用到的场景。

1. **强引用**：强引用值得是代码中普遍存在的，类似于Object obj= new Object（）。在JVM中只要强引用还在，垃圾回收永远不会回收此对象实例。

2. **软引用**：软引用用来描述一些有用但不必须对象，对于被软引用指向的对象，在系统中将要发生内存溢出之前，会将所有软引用对象进行垃圾回收。若内存够用，这些对象依然保留。在JDK1.2之后提供SoftReference来实现软引用。

3. **弱引用**：弱引用强度比软引用更差一点。仅被弱引用关联的对象最多只能生存到下一次GC开始之前。当垃圾回收开始工作时，无论当前内存是否够用，都会回收掉仅被弱引用关联的对象。JDK1.2之后使用WeakReference来实现 弱引用。

4. **虚引用** : 虚引用也被称为幽灵引用或者幻影引用，它是最弱的一种引用关系。一个对象是否有虚引用的存在，完全不会对其生存时间构成影响，也无法通过虚引用来取得一个对象实例。为一个对象设置虚引用的唯一目的就是能在这个对象被收集器回收时收到一个系统通知。在JDK1.2之后，提供了PhantomReference类来实现虚引用

### 10. Hashcode的作用。

* 先调用HashCode计算出哈希码，计算出对象存放的数据桶，然后调用equals比较桶里元素是否相等，若相等，则不在存放元素。如果equals返回false，则在相同的桶之后使用链表将元素连接起来。

* **如何证明两个对象真正的相等**

  若两个对象equals方法返回true，他们的hashCode必然要保持相等。但是两个对象的hashCode相等，equals不一定相等。当且仅当equals与hashCode方法均返回true，才默认两个对象真正的相等。

### 11. ArrayList、LinkedList、Vector的区别。

##### 1.ArrayList，Vector的区别：

1. **出现版本：** 
   * ArrayList  JDK1.2
   * Vector  JDK1.0 （出现在List，Collection接口之前）

2. **初始化策略区别**
   * Vector在无参构造执行后将对象数组大小初始化为10.
   * ArrayList采用懒加载策略，在构造方法阶段并不初始化对象数组，在第一次添加元素时才初始化对象数组大小为10

3. **扩容策略**
   * ArrayList扩容时，新数组大小变为原数组的1.5倍。
   * Vector扩容时，新数组大小变为原数组的2倍。

4. **线程安全性**
   * ArrayList采用异步处理，线程不安全，效率较高
   * Vector采用在方法上加锁，线程安全，效率较低。（即使要使用线程安全的List，也不用Vector）

5. **遍历**
   * Vector支持较老的迭代器Enumeration，Iterrator,LikedItwerator，Foreach
   * ArrayList支持。Iterrator,LikedItwerator，Foreach

##### **2.ArrayList，Vector的共同点：**

* 底层均使用数组实现

##### **3.ArrayList和LinkedList**

* LinkedList底层使用双向链表实现

* ArrayList底层使用数组实现

### 12.String、StringBuffer与StringBuilder的区别。

1. **可变与不可变**
   *  String类中使用字符数组保存字符串，因为有“final”修饰符，所以可以知道string对象是不可变的。
   * StringBuilder与StringBuffer都继承自AbstractStringBuilder类，在AbstractStringBuilder中也是使用字符数组保存字符串
   * 在String中使用"+"来进行字符串连接，但是这个操作在StringBuffer类中需要更改为append()方法：
2. **是否多线程安全**
   * String中的对象是不可变的，也就可以理解为常量，**显然线程安全**
   * StringBuffer对方法加了同步锁或者对调用的方法加了同步锁，所以是**线程安全的**
   * StringBuilder并没有对方法进行加同步锁，所以是**线程不安全的**

### 13.HashSet和TreeSet的区别：

**HashSet（无序存储）- HashMap**

1. 底层使用哈希表+红黑树

2. 允许存放null，无序存放

**TreeSet（有序存储）-TreeMap**

1. 底层使用红黑树

2. 不允许空值出现
3. 自定义类想要保存到TreeSet中，要么实现**Comparable**接口，要么向TreeSet传入比较器（**Comparator**接口）



### 14.Compartor接口与Compartor接口

**1. Comparable接口（内部比较器）**

若一个类实现了Comparable接口，就意味着该类支持排序。存放该类的Conllection或数组，可以直接通过Collections.sort()  或Arrays.sort()进行排序。

​       **public int  compareTo （T  o  ）：返回值的三种情况：**

* 返回正数：表示当前对象大于目标对象

* 返回0：表示当前对象等于目标对象

* 返回负数：表示当前对象小于目标对象



##### **2. Compartor（外部排序结构）**

* 若要控制某个自定义类的顺序，而该类本身不支持排序（类本身没有实现Compartor接口）。我们可以建立一个该类的“比较器”来进行排序。比较器实现Compartor接口即可。

  

  **“比较器”**：实现了Compartor接口的类作为比较器，通过比较器来进行类的排序。

   **int compare（T  o1,  T    o2）：返回值与compare返回值一样。**

  * 返回正数表示：o1>o2

  * 返回0表示：o1=o2

  * 返回小数表示：o1<o2

##### Compartor接口与Compartor接口的关系

* Comparable是排序接口，若一个 类实现了Comparable接口，意味着该类支持排序，是一个内部就比较器（自己和别人比）
* Compartor接口是比较器接口，本身不支持排序，专门有若干个第三方的比较器（实现了Compartor接口的类）来进行类的排序，是一个外部比较器（策略模式）

### 15.HashTable和HashMap/HashSet的区别

1. **版本**

   * HashTable是JDK1.0产生  
   * HashMap是JDK1.2产生

   **2.key和 value是否能为空值**

   * HashTable的key和value均不能为空
   * HashMap的key和value都可以为空，但是只有一个可以可以为空，value可以有多个为空

   **3.安全性**

   * Hashtable 在方法上加锁，线程安全，效率低
   * HashMap采用异步处理，线程不安全，效率高

   **4.底层实现**

   * HashTable底层是哈希表
   * HashMap底层是哈希表+红黑树

   **5.初始化大小：**

   * HashTable：初始大小为**11**，扩容：为原来的二倍+1  ，newSize=oldSize*2+1

   * HashMap：初始size为**16**，扩容：为原来的二倍。newsize = oldsize*2，size一定为2的n次幂

   **注意**、

   * HashMap的迭代器(Iterator)是fail-fast迭代器，而Hashtable的enumerator迭代器不是fail-fast的。所以当有其它线程改变了HashMap的结构（增加或者移除元素），将会抛出ConcurrentModificationException，但迭代器本身的remove()方法移除元素则不会抛出ConcurrentModificationException异常。

     

### 16.Map、Set、List、Queue、Stack的特点与用法。

##### Map

* Map是键值对，键Key是唯一不能重复的，一个键对应一个值，值可以重复。
* TreeMap可以保证顺序，HashMap不保证顺序，即为无序的。 
* Map中可以将Key和Value单独抽取出来，其中KeySet()方法可以将所有的keys抽取成一个Set。而Values()方法可以将map中所有的values抽取成一个集合。

##### Set

* 不包含重复元素的集合，set中最多包含一个null元素
* 只能用Iterator实现单项遍历，Set中没有同步方法

##### List

* 有序的可重复集合。
* 可以在任意位置增加删除元素。 
* 用Iterator实现单向遍历，也可用ListIterator实现双向遍历

##### Queue

* Queue遵从先进先出原则。
* 使用时尽量避免add()和remove()方法,而是使用offer()来添加元素，使用poll()来移除元素，它的优点是可以通过返回值来判断是否成功。 
* LinkedList实现了Queue接口。 
* Queue通常不允许插入null元素

##### Stack

* Stack遵从后进先出原则。
* Stack继承自Vector。 
* 它通过五个操作对类Vector进行扩展，允许将向量视为堆栈，它提供了通常的push和pop操作，以及取堆栈顶点的peek()方法、测试堆栈是否为空的empty方法等

**注意**

* 如果涉及堆栈，队列等操作，建议使用List
* 对于快速插入和删除元素的，建议使用LinkedList 
* 如果需要快速随机访问元素的，建议使用ArrayList
* HashMap和Hashtable都实现了Map接口，但决定用哪一个之前先要弄清楚它们之间的分别。主要的区别有：线程安全性，同步(synchronization)，以及速度。



### 17. HashMap 和 ConcurrentHashMap的区别，

**参考链接：**<https://www.cnblogs.com/heyonggang/p/9112731.html>

##### HashMap

- **底层实现**：底层数组+链表实现，可**以存储null键和null值**，线程**不安全**
- **初始size**为**16**，**扩容**：newsize = oldsize*2，size一定为2的n次幂
- 扩容针对整个Map，每次扩容时，原来数组中的元素依次重新计算存放位置，并重新插入
- 插入元素后才判断该不该扩容，有可能无效扩容（插入后如果扩容，如果没有再次插入，就会产生无效扩容）
- 当Map中元素总数超过Entry数组的75%，触发扩容操作，为了减少链表长度，元素分配更均匀
- 计算index方法：index = hash & (tab.length – 1)

 

##### **ConcurrentHashMap：**

* **底层实现**底层采用分段的数组+链表实现，线程**安全**
* 通过把整个Map分为N个Segment，可以提供相同的线程安全，但是效率提升N倍，默认提升16倍。(读操作不加锁，由于HashEntry的value变量是 volatile的，也能保证读取到最新的值。)
* Hashtable的synchronized是针对整张Hash表的，即每次锁住整张表让线程独占，ConcurrentHashMap允许多个修改操作并发进行，其关键在于使用了锁分离技术
* 有些方法需要跨段，比如size()和containsValue()，它们可能需要锁定整个表而而不仅仅是某个段，这需要按顺序锁定所有段，操作完毕后，又按顺序释放所有段的锁
* **扩容**：段内扩容（段内元素超过该段对应Entry数组长度的75%触发扩容，不会对整个Map进行扩容），插入前检测需不需要扩容，有效避免无效扩容
* ConcurrentHashMap是使用了锁分段技术来保证**线程安全**的，一次锁住一个桶。

- 在hashMap的基础上，ConcurrentHashMap将数据分为多个segment(类似hashtable)，默认16个（concurrency level），然后在每一个分段上都用锁进行保护，从而让锁的粒度更精细一些，并发性能更好



### 18.ConcurrentHashMap为何高效实现线程安全

<https://www.jianshu.com/p/afced7423ce6>

##### **JDK1.7之前的ConcurrentHashMap**

* 将原先的16个桶设计改为16个Segment,每个Segment都有独立的一把锁。拆分后的每个Segment都相当于原先的一个HashMap(double-hash设计).并且Segment在初始化后无法扩容，每个Segment对应的哈希表可以扩容,扩容只扩容相应Segment下面的哈希表。Segment之间相互不影响
* 先判断我在哪个segment下面，然后再hash一次判断我在哪个segment的哪个具体的桶里面，然后进行链表存储。JDK1.7concurrentHashMap底层是两个哈希表的嵌套
* **线程安全**:使用ReentrantLock保证相应Segment下的线程安全
  * 哈希表(Segment)+小哈希，一张表16把锁,支持的并发线程数为16，使用Lock体系保证线程安全

![1565339930252](C:\Users\Z\AppData\Roaming\Typora\typora-user-images\1565339930252.png)

##### **JDK1.8的ConcurrentHashMap**

* **整体结构**与HashMap别无二致，都是使用哈希表+红黑树结构
* **线程安全**:
  * 使用内建锁Sychronized+CAS锁每个桶的头结点,使得锁进一步细粒度化。
  * 一张表有多个锁(初始化为16，随着哈希表的扩容而不断增加，支持的并发线程数也不断增加)
    使用CAS+synchronized同步块保证线程安全

![1565339736502](C:\Users\Z\AppData\Roaming\Typora\typora-user-images\1565339736502.png)

##### JDK7与JDK8 ConcurrentHashMap的变化:

1. ###### 结构上的变化:

   * 取消原先的Segment设计，取而代之的是使用与HashMap同样的数据结构，
   * 即哈希表+红黑树,并且引入了懒加载机制。（JDK1.7一上来就初始化，JDK1.8 在第一次put时才初始化）

2. ###### 线程安全:

   * **锁粒度更细**:由原来的锁Segment一片区域到锁桶的头结点
   * 由原先的ReentrantLock替换为Sychronized+CAS:现版本的sychronized已经经过不断优化，性能上与ReentrantLock基本没有差异，

并且相对于ReentrantLock，使用Sychronized可以节省大量内存空间（原来ReentrantLock下的segment都得加入同步队列，都得继承AQS下的Node，而synchronized只是锁住头结点，头结点下边的节点都不会加入同步队列里，所以 节省了空间），这是非常大的优势所在。



### 19.HashMap的底层源码。

**1. 成员变量:树化、数据结构**

* DEFAULT_INITIAL_CAPACITY(初始化容量-桶数量) : 16

* DEFAULT_LOAD_FACTOR(负载因子): 0.75

* TREEIFY_THRESHOLD(树化阈值) : 8（默认是8，可以改）

* MIN_TREEIFY_CAPACITY(树化最少元素个数) : 64

* UNTREEIFY_THRESHOLD(解树化，返回链表的阈值) : 6

* Node<K,V>[] table : 真正存储元素的哈希表

**2. 为什么要树化**

* 因为之前链表如果太长查找速度很慢，变成红黑树速度快很多（log（n））。

**3. 树化的逻辑**

* 当一个桶中链表元素个数>=8,并且哈希表中所有元素个数加起来超过64，此时会将此桶中链表结构转为红黑树结构(提高链表过长导致的查找太慢问题，从原来的O(n)优化为O(logn),减少哈希碰撞（目的是解决安全问题）)
* 若只是链表个数大于8而哈希表元素不超过64，此时只是简单的resize而已，并不会树化。

**4. 构造函数**

* HashMap同样采用**懒加载策略(**不会在对象产生时初始化哈希表)

* // 初始化负载因子,默认桶数目16，负载因子0.75

* this.loadFactor = DEFAULT_LOAD_FACTOR;

**5. put与get流程**

* **put方法:**

  1. 若HashMap还未初始化，先进行哈希表的初始化操作(默认初始化为16个桶)

  2. 对传入的key值做hash，得出要存放该元素的桶编号
     1. 若没有发生碰撞,即头结点为空,将该节点直接存放到桶中作为头结点
     2. 若发生碰撞
        * 此桶中的链表已经树化，将节点构造为树节点后加入红黑树
        * 链表还未树化，将节点作为链表的最后一个节点入链表

  3. 若哈希表中存在key值相同的元素，替换最新的value值

  4. 若桶满了(rize++ 是否大于threshold)，调用resize()扩容哈希表。

  thresholed = 容量(默认16) * 负载因子 (默认0.75)

  

  **get方法:**

  1. .当表还未初始化或者key值为null,return null

  2. 表已经初始化并且key不为null
     1. key值刚好是桶的头结点，直接返回
     2. 遍历桶的其他节点
        * 若已经树化，调用树的遍历方式找到指定key对应的Node返回
        * 调用链表的遍历方式找到指定key对应的Node返回



**6. 哈希算法，扩容，性能**

**HashMap中的hash方法:**

​	static final int hash(Object key) {

   	     int h;

​	        return (key == null) ? 0 : (h = key.hashCode()) ^ (h >>> 16);

​	}

1. **为何不采用Object类提供的hashCode方法计算出来的key值作为桶下标:**

   * 基本不会发生碰撞，哈希表就和普通数组基本没有区别

2. **为何h >>> 16?为何取出key值得高16位右移参与hash运算?**

   * 因为hash基本上是在高16位进行hash运算
   * 直接使用Object的哈希算法求出来的哈希码太大了

3. **为何HashMap中容量均为2^n ?**

   * (n - 1) & hash : 当n为2^n，此时的位运算就相当于 hash % (n-1)

   * 为何n必须2^n?------>保证所有数组下标都有可能被访问到

   * **(n - 1) & hash :**

     * 保证得到的数组下标一定在哈希表长度范围内

     

4. **扩容resize()**
   1. 负责哈希表的初始化操作
   2. 当表中元素个数达到阈值: 容量 * 负载因子后进行**扩容为原哈希表的二倍**(扩容的是桶的个数)
   3. 扩容后，原来元素进行rehash:(HashMap最大的开销)。要么元素还待在原桶中，要么待在double 桶中



**5.性能问题**

1. **多线程下:在竞争激烈的场景下使用HashMap会造成CPU飙到100%，**
   * 解决:使用ConcurrentHashMap来代替HashMap

2. **性能主要开销 : resize()后的rehash过程**
   * 解决:在能预估存放元素个数的前提下传入适当的初始化参数来尽量避免resize()
3. **JDK1.8引入红黑树大程度优化了HashMap的性能**，这主要体现在hash算法不均匀时，即产生的链表非常长，这时把链表转为红黑树可以将复杂度从O(n)降到O(logn)。

**6.HashMap是如何工作的？ **

* HashMap在Map.Entry静态内部类实现中存储key-value对。HashMap使用哈希算法，在put和get方法中，它使用hashCode()和equals()方法。当我们通过传递key-value对调用put方法的时候，HashMap使用Key hashCode()和哈希算法来找出存储key-value对的索引。Entry存储在LinkedList中，所以如果存在entry，它使用equals()方法来检查传递的key是否已经存在，如果存在，它会覆盖value，如果不存在，它会创建一个新的entry然后保存。当我们通过传递key调用get方法时，它再次使用hashCode()来找到数组中的索引，然后使用equals()方法找出正确的Entry，然后返回它的值。



**小tips:**

在resize过程中若发现桶下的红黑树节点<=UNTREEIFY_THRESHOLD,会将红黑树解除树化还原为链表结构。

### 20. TreeMap、HashMap、LindedHashMap的区别。

**1、实现**

* TreeMap：SortMap接口，基于红黑树

* HashMap：基于数组+链表实现）实现

* LinkedHashMap：就是数组+链表实现，其底层采用了Linked双向链表来保存节点的访问顺序，所以保证了有序性。



**2、存储**

* TreeMap：默认按键的升序排序

* HashMap：随机存储

* LinkedhashMap ：默认是按插入顺序排序

  

**3、遍历**

TreeMap：Iterator遍历是排序的

HashMap：Iterator遍历是随机的

LindedHashMap：terator遍历，维护一条双向链表，实现了散列数据结构的有序遍历



**4、键值对**

TreeMap：键、值都不能为null

HashMap：只允许键、值均为null

LinkedHashMap：允许使用 null 值和 null 键

**5、安全**

TreeMap：非并发安全Map

HashMap：非并发安全Map

LinkedhashMap :线程不安全

**6、效率**

* TreeMap：有序的，效率比HashMap低

* HashMap：无序的，效率高

- LinkedHashMap：结合HashMap和TreeMap的优点，有序的同时效率也不错仅比HashMap慢一点

**7.版本：**

HashMap 是JDK1.2产生的

TreeMap是JDK1.2

 LinkedHashMap是 JDK1.4 以后产生的

##### LindedHashMap

* LinkedHashMap 是HashMap的一个子类，如果需要输出的顺序和输入的顺序相同，那么用LinkedHashMap可以实现。

* LinkedHashMap 维护着一个运行于所有条目的双重链接列表。此链接列表定义了迭代顺序，该迭代顺序可以是插入顺序或者是访问顺序。

* 链表中元素的顺序可以分为：**按插入顺序的链表**，和**按访问顺序(调用 get 方法)的链表**。**默认是按插入顺序排序**，**如果指定按访问顺序排序，那么调用get方法后，会将这次访问的元素移至链表尾部**，不断访问可以形成按访问顺序排序的链表。

* 插入有序: 即遍插入时后插入的排在后面，迭代访问时是按照插入的顺序进行迭代的

* 访问有序: 访问有序指的是每次访问元素时，先将元素从链表中删除，接着再将此元素放到链表末尾，这样确保访问的有序性

  

### 21.Collection包结构，与Collections的区别。

* collection是集合类的上级接口，子接口主要有Set 和List、Map。 
* Collections是针对集合类的一个帮助类，提供了操作集合的工具方法：一系列静态方法实现对各种集合的搜索、排序、线程安全化等操作。

### 22. try catch finally，try里有return，finally还执行么？

1. 不管有木有出现异常，finally块中代码都会执行；

2. 当try和catch中有return时，finally仍然会执行；

3. finally是在return后面的表达式运算后执行的（此时并没有返回运算后的值，而是先把要返回的值保存起来，管finally中的代码怎么样，返回的值都不会改变，任然是之前保存的值），所以函数返回值是在finally执行前确定的；

4. finally中最好不要包含return，否则程序会提前退出，返回值不是try或catch中保存的返回值。

5. **注意**

   * 任何执行try 或者catch中的return语句之前，都会先执行finally语句，如果finally存在的话。
   * 如果finally中有return语句，那么程序就return了，所以finally中的return是一定会被return的，

   * 编译器把finally中的return实现为一个warnin

### 23.Excption与Error包结构。OOM你遇到过哪些情况，SOF你遇到过哪些情况。

1. Error就是Java运行时内部错误与资源耗尽错误（死循环和内存泄漏），这种内部错误一旦出现，除了告知用户并使程序安全终止之外，在无能为。断电。

2. Exception是程序正常运行过程中，可以预料的异常情况，可以对他们进行捕捉，并进行相应的处理
3. 异常能被程序本身可以处理，错误是无法处理（断电）。

**OOM（内训泄漏OutOFMemorError）**:无用对象无法被GC，即无法被垃圾回收

**SOF （堆栈溢出 StackOverflow）**：当应用程序递归太深而发生堆栈溢出时，抛出该错误。

* 因为栈一般默认为1-2m，一旦出现死循环或者是大量的递归调用，在不断的压栈过程中，造成栈容量超过1m而导致溢出。

### 24. Java面向对象的三个特征与含义。

**封装**：

* 也就是把客观事物封装成抽象的类，并且类可以把自己的数据和方法只让可信的类或者对象操作，对不可信的进行信息隐藏。简而言之就是，内部操作对外部而言不可见(保护性)。发动机和汽车的关系，
* **实现方式**：private实现类封装处理，内部类，final

**继承**

* 它可以使用现有类的所有功能,并在无需重新编写原来的类的情况下就有 和父类一样的属性和方法，并且可以对 这些功能进行扩展。
* **实现方式**：extends

**多态**：

* 多态就是指一个类实例的相同方法，在不同情形有不同表现形式。多态机制使具有不同内部结构的对象可以共享相同的外部接口。，对象的向上向下转型
* **实现方式**：接口，抽象类，覆写，重载

### 25.Override（覆写）和Overload（重载）的含义去区别。

**重写（覆写）**：

* **发生在父类与子类中**，在子类中定义了与父类方法名称，返回值类型、参数类型及个数完全相同的方法。
* 但是被覆写的方法**不能够拥有比父类更为严格的访问控制权限**：private<default <public

**重载**：

*   **同一个类中进行方法重载** ，方法的声明部分，包括名字，完全相同，**只有参数不同**（参数个数，类型，顺序）。
  * 1.如果参数个数不同，就不管它的参数类型了！
  * 2.如果参数个数相同，那么参数的类型必须不同。

### 26.Interface与abstract类的区别。

**1.结构组成：**

1. 抽象类：普通类+抽象方法
2. 接口：抽象方法+全局常量

**权限：**

1. 抽象类：有各种权限
2. 接口：只有public

**子类使用：**

1. 抽象类：使用extends关键字继承抽象类
2. 结果使用implements实现接口

**关系：**

1. 抽象类：一个抽象类可以实现多个接口

2. 接口：接口不能继承抽象类，但是接口可以使用extends实现多个父接口

**子类的限制**

1. 抽象类：一个子类只能继承一个父接口

2. 接口：一个类可以实现多个接口

![1565352063065](C:\Users\Z\AppData\Roaming\Typora\typora-user-images\1565352063065.png)

### 27.静态类与非静态类的区别。

1. 内部静态类不需要有指向外部类的引用。但非静态内部类需要持有对外部类的引用。
2. 非静态内部类能够访问外部类的静态和非静态成员。静态类不能访问外部类的非静态成员。他只能访问外部类的静态成员。
3. 一个非静态内部类不能脱离外部类实体被创建，一个非静态内部类可以访问外部类的数据和方法，因为他就在外部类里面。

* 静态对象是类共同拥有的，非静态对是类独立拥有的, 
* 静态对象内存空间上是固定的 ，非静态对空间在各个附属类里面分配 
* 先分配静态对象的空间 ，继而再对非静态对象分配空间。也就是初始化顺序是先静态再非静态. 



**静态**：指以static关键字修饰的，包括类，方法，块，字段。

**非静态**，指没有用static 修饰的。

##### 静态有一些特点：

1. 全局唯一，任何一次的修改都是全局性的影响

2. 只加载一次，优先于非静态。**在类加载时JVM会把它放到方法区**，被本类以及本类中所有实例所公用。

3. 使用方式上不依赖于实例对象。**访问方法**：1）类名.静态方法名    2）类名.静态变量名）

4. 生命周期属于类级别，从JVM 加载开始到JVM卸载结束

##### 只有内部类才能被声明为静态类，即静态内部类

* a.静态内部类的创建不需要外部类，可以直接创建
* b.静态内部类不可以访问外部类的任何非static成员变量和方法
  * 静态内部类不能访问外部类成员变量，但可以存在成员变量
  * 成员内部类不能存在静态变量，但可以访问外部类的静态变量





### 28.java多态的实现原理。

* **a. 抽象的来讲**，多态的意思就是同一消息可以根据发送对象的不同而采用多种不同的行为方式。（发送消息就是函数调用）
* **b. 实现的原理是动态绑定**，程序调用的方法在运行期才动态绑定，追溯源码可以发现，JVM 通过参数的自动转型来找到合适的办法。

### 29.实现多线程的方式

1. **继承hread类**：

   * （假设实现类为MyRunnable）并重写run()方法，然后new一个MyThread对象并对其调用start()即可启动新线程。

   * 有单继承局限

2. **实现Runnable接口**

   * （假设实现类为MyRunnable），而后将MyRunnable对象作为参数传入Thread构造器，在得到的Thread对象上调用start()方法即可。

   * 避免点继承的局限，一个类可以继承多个接口

3. **实现Callable接口**：有返回值

   *   Callable 使用 call（） 方法运行任务， Runnable 使用 run() 方法运行任务 

4. **线程池** （推荐创建线程的方式）

### 30.JAVA 中堆和栈的区别，说下java 的内存机制

* **a. 栈内存**：基本数据类型比变量和对象的引用都是在栈分配的
* **b. 堆内存**：用来存放由new创建的对象和数组
* **c. 类变量（static修饰的变量**）：程序在一加载的时候就在堆中为类变量分配内存，堆中的内存地址存放在栈中
* **d. 实例变量**：当你使用java关键字new的时候，系统在堆中开辟并不一定是连续的空间分配给变量，是根据零散的堆内存地址，通过哈希算法换算为一长串数字以表征这个变量在堆中的”物理位置”,实例变量的生命周期–当实例变量的引用丢失后，将被GC（垃圾回收器）列入可回收“名单”中，但并不是马上就释放堆中内存
* **e. 局部变量:** 由声明在某方法，或某代码段里（比如for循环），执行到它的时候在栈中开辟内存，当局部变量一但脱离作用域，内存立即释放





### 31.线程同步的方法：sychronized、lock、reentrantLock等。

* synchronized: 可以来对一个代码块或是对一个方法上锁，被“锁住”的地方称为临界区，进入临界区的线程会获取对象的monitor，这样其他尝试进入临界区的线程会因无法获取monitor而被阻塞。由于等待另一个线程释放monitor而被阻塞的线程无法被中断。
* ReentrantLock: 尝试获取锁的线程可以被中断并可以设置超时参数。



### foreach与正常for循环效率对比。

链接：https://www.jianshu.com/p/ba821be173ae

* 循环ArrayList时，普通for循环比foreach循环花费的时间要少一点；循环LinkList时，普通for循环比foreach循环花费的时间要多很多。
   当我将循环次数提升到一百万次的时候，循环ArrayList，普通for循环还是比foreach要快一点；但是普通for循环在循环LinkList时，程序直接卡死。

* **结论**：
  * **需要循环数组结构的数据时**，建议使用普通for循环，因为for循环采用下标访问，对于数组结构的数据来说，采用下标访问比较好。
  * **需要循环链表结构的数据时**，一定不要使用普通for循环，这种做法很糟糕，数据量大的时候有可能会导致系统崩溃。

* **原因**：foreach使用的是迭代器







### 锁的等级：方法锁、对象锁、类锁。

**1.基础**
 Java中的每一个对象都可以作为锁。

* 对于同步方法，锁是当前实例对象。 

* 对于静态同步方法，锁是当前对象的Class对象。

* 对于同步方法块，锁是Synchonized括号里配置的对象。

  当一个线程试图访问同步代码块时，它首先必须得到锁，退出或抛出异常时必须释放锁。

**方法锁**

* 通过在方法声明中加入 sync hronized关键字来声明 synchronized 方法。
* synchronized 方法控制对类成员变量的访问：
  * 每个类实例对应一把锁，每个 synchronized 方法都必须获得调用该方法的类实例的锁方能执行，否则所属线程阻塞，方法一旦执行，就独占该锁，直到从该方法返回时才将锁释放，此后被阻塞的线程方能获得该锁，重新进入可执行状态。这种机制确保了同一时刻对于每一个类实例，其所有声明为 synchronized 的成员函数中至多只有一个处于可执行状态，从而有效避免了类成员变量的访问冲突。

**对象锁**

* 当一个对象中有同步方法或者同步 块，线程调用此对象进入该同步区域时，必须获得对象锁。如果此对象的对象锁被其他调用者占用，则进入阻塞队列，等待此锁被释放（同步块正常返回或者抛异常终止，由JVM自动释放对象锁）。
* 注意，方法锁也是一种对象锁。当一个线程访问一个带synchronized方法时，由于对象锁的存在，所有加synchronized的方法都不能被访问（前提是在多个线程调用的是同一个对象实例中的方法）。

链接：https://www.jianshu.com/p/92b75042c059

**类锁**

* 一个class其中的静态方法和静态变量在内存中只会加载和初始化一份，所以，一旦一个静态的方法被申明为synchronized，此类的所有的实例化对象在调用该方法时，共用同一把锁，称之为类锁



**同步的原理**

* JVM规范规定JVM基于进入和退出 Monitor 对象来实现方法同步和代码块同步，但两者的实现细节不一样。
* 代码块同步是使用monitorenter和monitorexit指令实现，而方法同步是使用另外一种方式实现的，细节在JVM规范里并没有详细说明，但是方法的同步同样可以使用这两个指令来实现。
   monitorenter指令是在编译后插入到同步代码块的开始位置，而monitorexit是插入到方法结束处和异常处，JVM要保证每个monitorenter必须有对应的monitorexit与之配对。任何对象都有一个monitor与之关联，当且一个monitor被持有后，它将处于锁定状态。线程执行到 monitorenter 指令时，将会尝试获取对象所对应的 monitor 的所有权，即尝试获得对象的锁。
* 有一个monitorEnter，有多个MonitorExit，因为要保障证异常情况下线程也能做出的退出
* 获取一次Monitor，计数器加一，当Monitor的计数器时，线程退出

链接：https://www.jianshu.com/p/ba821be173ae



### 写出生产者消费者模式。



### ThreadLocal的设计理念与作用。

链接：https://www.jianshu.com/p/4765eef0c979

* ThreadLocal的作用是提供线程内的局部变量，在多线程环境下访问时能保证各个线程内的ThreadLocal变量各自独立。也就是说，每个线程的ThreadLocal变量是自己专用的，其他线程是访问不到的。ThreadLocal最常用于以下这个场景：多线程环境下存在对非线程安全对象的并发访问，而且该对象不需要在线程间共享，但是我们不想加锁，这时候可以使用ThreadLocal来使得每个线程都持有一个该对象的副本。

* **实现原理**

  * 1.每个Thread对象内部都维护了一个ThreadLocalMap这样一个ThreadLocal的Map，可以存放若干个ThreadLocal。

  * 当我们在调用get()方法的时候，先获取当前线程，然后获取到当前线程的ThreadLocalMap对象，如果非空，那么取出ThreadLocal的value，否则进行初始化，初始化就是将initialValue的值set到ThreadLocal中。

  * 当我们调用set()方法的时候，很常规，就是将值设置进ThreadLocal中。

  * ThreadLocalMap里面存储的Entry对象本质上是一个WeakReference<ThreadLocal>。也就是说，ThreadLocalMap里面存储的对象本质是一个对ThreadLocal对象的弱引用，该ThreadLocal随时可能会被回收！即导致ThreadLocalMap里面对应的Value的Key是null。我们需要把这样的Entry给清除掉，不要让它们占坑，避免内存泄漏。
     那为什么需要弱引用呢？因为线程的声明周期是长于ThreadLocal对象的，当此对象不再需要的时候如果线程中还持有它的引用势必也会产生内存泄漏的问题，所以自然应该是用弱引用来进行key的保存。

    


### ThreadPool用法与优势。

* **参数**
  * **coolPoolSize（核心线程池的大小）：**
    * 当提交一个任务到线程池时，只要核心线程池未达到corePoolSize。创建新线程来执行任务，调用ppreStartAllCoreThreads（），线程池会提前创建并启动所有核心线程
  * **BlockingQueue<Runnable>workQueue(任务队列)：保存等待执行任务的队列**
    * -ArrayBlockingQueue：基于数组有界阻塞队列，按照FIFO原则对元素进行排列。
    * -LinkedBlockingQueue：基于链表的无界阻塞队列，按照FIFO排列元素，吞吐量要高于ArrayBlockingQueue。内置线程池newFixedThreadPool -固定大小线程池就采用此队列。
    * -SynchronousQueue：一个不存储元素的阻塞队列（无界队列）。每个插入操作需要等待另一个线程的移除操作，否则插入操作一直处于阻塞状态，吞吐量通常高于LinkedBlockingQueue。内置线程池newCachedThreadPool - 缓存线程池就采用此队列。
    * -priorityBlockingQueue ：具有优先级的证书队列
  * **maximumPoolSize：线程池的最大数量**
  * **RejectedExecutionHandler（饱和策略）**
    * -AbortPolicy：无法处理新任务抛出异常（JDK默认采用此策略）
    * -CallerRunsPolicy：使用调用者艘在的线程来处理任务。
    * DiscardOldestPolicy：丢弃队列里最近的一个任务，并执行当前任务。
    * DiscardPolicy：不处理，丢弃任务，也不报异常。

* **.线程池的执行流程**
  * **第一步**：判断 核心线程池是否已满，如果未满，创建一个新的线程来执行未执行的任务。如果已满，判断是否有空闲线程，有的话将任务分给空闲线程，否则执行步骤2.（创建线程需要获得全局锁）
  * **第二步**：判断工作队列（阻塞队列BlockingQueue）是否已满，如果未满，将任务存储在工作队列中等待空闲队列调度，如果工作队列已满，执行步骤三。
  * **第三步**：判断当前线程池是否已达到最大值，如果没有达到最大值，则创建新的线程来执行任务（创建线程需要获得全局锁），否则，执行4
  * **第四步**：调用饱和策略来处理此任务。

* **使用线程池的优势：**
  - 降低资源消耗：重复利用已创建的线程，降低创建和销毁造成的消耗。
  - 提高响应速度：任务可以不需要等到线程创建就能立即执行(参考上条)。
  - 提高管理性：可以进行统一的分配、调优和监控。

### Concurrent包里的其他东西：ArrayBlockingQueue、CountDownLatch等等。

链接：https://www.jianshu.com/p/4765eef0c979

* **CountDownLatch**: 允许线程集等待直到计数器为0。

  * 适用场景: 当一个或多个线程需要等待指定数目的事件发生后再继续执行。

* **ArrayBlockingQueue**:  一个基于数组实现的阻塞队列，它在构造时需要指定容量。

  * 当试图向满队列中添加元素或者从空队列中移除元素时，当前线程会被阻塞。通过阻塞队列，我们可以按以下模式来工作：工作者线程可以周期性的将中间结果放入阻塞队列中，其它线程可以取出中间结果并进行进一步操作。
  * 若工作者线程的执行比较慢（还没来得及向队列中插入元素），其他从队列中取元素的线程会等待它（试图从空队列中取元素从而阻塞）；
  * 若工作者线程执行较快（试图向满队列中插入元素），则它会等待其它线程取出元素再继续执行。

  

  

  

  

### wait()和sleep()的区别。

* **来自不同的类**：sleep来自Thread类，和wait来自Object类
* **锁：**调用sleep()方法的过程中，线程不会释放对象锁。而 调用 wait 方法线程会释放对象锁。sleep睡眠后不出让系统资源，wait让出系统资源其他线程可以占用CPU
* sleep(milliseconds)需要指定一个睡眠时间，时间一到会自动唤醒
* **使用范围**：wait，notify和notifyAll只能在同步控制方法或者同步控制块里面使用，而sleep可以在任何地方使用

### Set、List、Map之间的区别是什么?

Collection是最基本的集合接口,Set 和List 都继承了Conllection,Map没有。

- Set是最简单的一种集合。集合中的对象不按特定的方式排序，并且没有重复对象。
- List的特征是其元素以线性方式存储，集合中可以存放重复对象。
- Map 是一种把键对象和值对象映射的集合，它的每一个元素都包含一对键对象和值对象。





### Java IO与NIO。

链接：https://www.jianshu.com/p/4765eef0c979

* **Java IO是面向流的**，这意味着我们需要每次从流中读取一个或多个字节，直到读取完所有字节；**NIO是面向缓冲的**，也就是说会把数据读取到一个缓冲区中，然后对缓冲区中的数据进行相应处理。

* Java IO是阻塞IO，而NIO是非阻塞IO。

* Java NIO中存在一个称为选择器（selector）的东西，它允许你把多个通道（channel）注册到一个选择器上，然后使用一个线程来监视这些通道：若这些通道里有某个准备好可以开始进行读或写操作了，则开始对相应的通道进行读写。而在等待某通道变为可读/写期间，请求对通道进行读写操作的线程可以去干别的事情。





### 反射的作用于原理。

* **思想**：JAVA反射机制是在运行状态中, 对于任意一个类, 都能够知道这个类的所有属性和方法; 对于任意一个对象, 都能够调用它的任意一个方法和属性; 这种动态获取的信息以及动态调用对象的方法的功能称为java语言的反射机制.
* **主要作用**
  * 运行时取得类的方法和字段的相关信息。
  * 创建某个类的新实例(.newInstance())
  * 取得字段引用直接获取和设置对象字段，无论访问修饰符是什么。
* **用处如下：**
  * 观察或操作应用程序的运行时行为。
  * 调试或测试程序，因为可以直接访问方法、构造函数和成员字段。
  * 通过名字调用不知道的方法并使用该信息来创建对象和调用方法。

### 泛型常用特点，List能否转为List。

链接：https://www.jianshu.com/p/4765eef0c979

**泛型：**JDK1.5版本以后出现的新特性，用于解决安全问题，是一个类型安全机制。
**优点**：

- 将运行时期出现的问题CLassCastException（类型匹配异常）,转移到了编译时期，方便与程序员解决问题，让运行时期问题减少，安全了。
- 避免了强制类型转换，且运行时不会提示程序类型没检查的不安全提示。

**泛型的使用时间：**泛型技术是给编译器使用的技术,用于编译时期。确保了类型的安全。 运行时，会将泛型去掉，生成的class文件中是不带泛型的,这个称为泛型的擦除。 为什么擦除呢？因为为了兼容运行的类加载器。 泛型的补偿：在类加载器原有基础上，编写一个补偿程序。在运行时，通过反射， 获取元素的类型进行转换动作。不用使用者在强制转换了。

**通配符**---解决泛型参数统一化问题

**泛型察除**

* 泛型信息仅存在于代码阶段，进入JVM之前，与泛型相关信息会被察除掉，专业术语就叫类型察除。换句话，泛型类与普通类在JVM中没有任何区别。

* 泛型类进入JVM之前会进行类型察除，泛型类的类型参数如果没有指定类型上限，则察除成为Object类。如果类型参数指定类型上限，则察除为相应类型上限。
* **设置泛型的上限**---用于泛型类的声明，也可用于方法参数，
  * 泛型类声明：T  extends   类：表示方法入参只能接受（父类）以及其子类对象
* **设置泛型下限**--只能用于方法参数
  * ？ super 类（>=类）：表示方法入参只能接收类以及其父类对象



### 父类的静态方法能否被子类重写，为什么？

父类的静态方法可以被子类继承，也就是说子类可以调用父类的静态方法,但是不能重写。

### 解析XML的几种方式的原理与特点：DOM、SAX、PULL。

链接：https://www.jianshu.com/p/6067beaab41c

* **DOM：消耗内存：**先把xml文档都读到内存中，然后再用DOM API来访问树形结构，并获取数据。这个写起来很简单，但是很消耗内存。要是数据过大，手机不够牛逼，可能手机直接死机

* **b. SAX**：解析效率高，占用内存少，基于事件驱动的：更加简单地说就是对文档进行顺序扫描，当扫描到文档(document)开始与结束、元素(element)开始与结束、文档(document)结束等地方时通知事件处理函数，由事件处理函数做相应动作，然后继续同样的扫描，直至文档结束。

* **c. PULL**：与 SAX 类似，也是基于事件驱动，我们可以调用它的next（）方法，来获取下一个解析事件（就是开始文档，结束文档，开始标签，结束标签），当处于某个元素时可以调用XmlPullParser的getAttributte()方法来获取属性的值，也可调用它的nextText()获取本节点的值。

  

  

  

### Java1.7与1.8新特性。

链接：https://www.jianshu.com/p/4765eef0c979

**Java 7:**

-  **对集合的支持**： 创建List / Set / Map 时写法更简单了。
- **对资源的自动回收管理**
- **泛型实例创建过程中类型引用的简化**
- **在数字中使用下划线**
- **对字符串进行switch case**
- **二进制符号**
- **一个catch里捕捉多个异常类型**

**Java 8:**

- **Lambdas表达式与Functional接口**
- **接口的默认与静态方法**
- **方法引用**
- **重复注解**
- **更好的类型推测机制**
- **扩展注解的支持**

JDK7：<https://www.csdn.net/article/2011-07-22/302072>

JDK8:<https://www.open-open.com/lib/view/open1403232177575.html>

### if和switch的区别：

- if ：
  1. 对具体的值进行判断
  2. 对区间判断
  3. 对运算结果是boolean类型的表达式进行判断
- switch :
  1. 对具体的值进行判断；
  2. 值的个数通常是固定的。



1. ### 设计模式：单例、工厂、适配器、责任链、观察者等等。

2. ### JNI的使用。



# JVM

### 1.内存模型以及分区，需要详细到每个区放什么。

**1.线程私有内存：每个线程都有，彼此之间完全隔离。**

1. **程序计数器**：是比较小的内存空间，当前线程所执行的字节码的行号指示器。
   * 若当前线程执行的是Java方法，计数器记录的是正在执行的JVM字节码指令地址。
   * 若当前线程执行的是native方法，计数器值为空。
   * **异常：**程序计数器是唯一一块不会产生OOM异常（内存溢出）的区域
2. **虚拟机栈**：Java方法执行的内存模型
   * 个方法的执行同时都会创建一个栈帧来存储局部变量表，操作数栈，方法出口等信息，每个方法从调用直到执行完毕的过程，对应一个栈帧在虚拟机的入栈和出栈过程。
   * **生命周期与线程相同：**在创建线程的同时创建线程的虚拟机栈，线程执行结束，虚拟机栈与线程一同被收回。
   * **异常**：
     * .若线程请求的栈的深度大于JVM允许的深度（-Xss设置栈容量），抛出StackOverflowError异常。（递归，如果递归层数很深，会栈溢出）（常见于单线程）
     * .虚拟机在进行栈的动态扩展时，若无法申请到足够内存，抛出OOM （OutOfMemoryError）异常　（常见于多线程 ）
3. **本地方法栈**：本地方法（native方法）执行的内存模型。
   * HotSpot虚拟机中，本地方法栈与虚拟机栈是同一块内存区域。

**2.线程共享内存：所有线程共享此内存空间，对空间所有的线程可见**

1. **堆（GC堆）**

   * java堆（Java　Heap）是JVM管理的最大内存区域。在JVM启动时创建。所有线程共享此内存，此内存中存放的是对象实例以及数组。

   * Java堆是垃圾回收器管理的最主要的内存区域。Java堆可以处于物理上不连续的内存空间。

     - －Ｘｍｘ设置堆最大值
     - －Xms设置堆最小值

   * **异常：**

     - 若在堆中没有足够的内存完成对象实例分配且堆无法再次扩展时。抛出OOM异常

     

     **注意：**

     - 内存溢出：内存中的对象确实还应该存活，但是由于堆内存不够产生的异常。困
     - 内存泄漏：无用对象无法被GC

2. **方法区**

   * 用于存储JVM加载的类信息，常量，静态变量等数据。JDK１.８之前，方法区也叫永久代，JDK１.８之后称为元空间（Meta　Space）
   * **异常：**方法区无法满足内存分配需求时，抛出OOM异常

3. **运行时常量池**

   * 运行时常量池方法区的一部分，存放字面量与符号引用。
     * 字面量：字符串常量（JDK１.７移到堆中），final常量，基本数据类型的值。
     * 符号引用：字段，类，方法的完全限定名（包名＋类名），名称，描述。
     * 对象产生：符号引用－＞类－＞具体引用



<https://blog.csdn.net/weixin_34257076/article/details/89549745>

### 2.GC的两种判定方法（判断对象是否存活）：引用计数与引用链(可达性分析算法)

**1.引用计数法**

* **算法思想**：
  * 给每一个对象附加一个引用计数器，每当有一个地方引用此对象，计数器加一，当有一个引用失效时，计数器减一。在任意时刻，只要计数器值为0,的对象就是不能再使用的，即对象已死。

* **特点：**
  * 引用计数法实现简单，效率也较高。Python使用引用计数法来管理内存。
  * 但是无法解决循环引用问题（我中有你，你中有我）。
  * JVM并没有采用此算法。
  * -XX：printGC：打印具体的垃圾回收日志

**2.可达性分析算法**：Java采用可达性分析算法来判断对象是否存活

* **核心思想：**
  * 通过一系列“GC Roots”的对象作为起点，从这些起点开始向下搜索对象，搜索走过的路径，称为“**引用链“**，当一个对象到任意一个GC  Roots 对象没有任何引用链想链接时，（从GC Roots到对象不可达时），证明对象已死。

* Java中能作为**GC Roots 的对象**包含以下四种：
  * 虚拟机栈(栈帧中的本地变量表)中引用的对象
  * 方法区中类静态属性引用的对象
  * 方法区中常量引用的对象
  * 本地方法栈中JNI(Native方法)引用的

* **JDK1.2之后对于引用的概念做了扩充**

  1. **强引用**：强引用值得是代码中普遍存在的，类似于Object obj= new Object（）；在 JVM 只要强引用还在，垃圾回收永远不会回收此对象实例。

  2. **软引用**：软引用用来描述一些有用但不必须对象，对于被软引用指向的对象，在系统中将要发生内存溢出之前，会将所有软引用对象进行垃圾回收。若内存够用，这些对象依然保留。在JDK1.2之后提供SoftReference来实现软引用。

  3. **弱引用**：弱引用强度比软引用更差一点。仅被弱引用关联的对象最多只能生存到下一次GC开始之前。当垃圾回收开始工作时，无论当前内存是否够用，都会回收掉仅被弱引用关联的对象。JDK1.2之后使用WeakReference来实现 弱引用。

  4. **虚引用** : 虚引用也被称为幽灵引用或者幻影引用，它是最弱的一种引用关系。一个对象是否有虚引用的存在，完全不会对其生存时间构成影响，也无法通过虚引用来取得一个对象实例。为一个对象设置虚引用的唯一目的就是能在这个对象被收集器回收时收到一个系统通知。在JDK1.2之后，提供了PhantomReference类来实现虚引用

* **3对象的自我拯救--finalize**
  * 在可达性分析算法中不可达的 对象，也并非房“非死不可“，所有不可达的对象处于”缓刑“阶段要宣告一个对象的彻底死亡，需要经历两次标记过程：
    * 如果对象不可达，那么它将会被第一次标记并且进行一次筛选。**筛选的条件**是此对象是否有必要执行finalize()方法。当对象没有覆盖finalize方法，或者finzlize方法已经被虚拟机调用过，虚拟机将这两种情况都视为“没有必要执行”，对象被回收。
    * 筛选成功（对象覆写了finalize()方法并且未被执行），会将此对象放入F-Queue，如果对象在finalize()成功自救（此对象与GC Roots建立联系），则对象会在**第二次被标记**时被移除回收集合，成功存活，若对象在fianlize()中仍与GC Roots不可达，宣告死亡。

### 3.回收方法区：方法区(永久代)

* 垃圾回收主要收集两部分内容 : **废弃常量**和**无用的类**。

* **思想**

  * 回收废弃常量和回收Java堆中的对象十分类似。以常量池中字面量(直接量)的回收为例，假如一个字符串"abc"已经进入了常量池中，但是当前系统没有任何一个String对象引用常量池的"abc"常量，也没有在其他地方引用这个字面量，如果此时发生GC并且有必要的话，这个"abc"常量会被系统清理出常量池。常量池中的其他类(接口)、方法、字段的符号引用也与此类似。

* **判定一个类是否是"无用类"需要同时满足下面三个条件：**

  *  该类所有实例都已经被回收(即在Java堆中不存在任何该类的实例)

  * 加载该类的ClassLoader（加载器）已经被回收

  *  该类对应的Class对象没有在任何其他地方被引用，无法在任何地方通过反射访问该类的方法

### 4.垃圾回收算法

**1.标记清除算法**

* **思想：**
  * 分为标记和清除两个阶段，标记阶段标记出此次垃圾回收需要回收的对象，清除阶段一次性清除所有带标记的对象。

* **问题**
  * 效率：标记与清除的效率都不高
  * 空间问题：标记清除算法会产生大量不连续的空间，若程序中需要分配大量连续对象时，由于空间碎片较多无法找到连续内存而不得不再次触发GC

**2.复制算法（新生代垃圾回收算法 ）**

* **思想：**
  * 将内存分为大小相等的两块，每次只使用其中一块内存，当使用的内存需要进行垃圾回收时会将此区域里的所有存活对象一次性复制到保留区域，然后将此内存一次性清理掉。

* **问题**
  * 内存利用率太低。商用JVM都对复制算法做了改进。

* **JVM改进后的复制算法**
  * 新生代中98%的对象都是“朝生夕死”（存活时间非常短），所以并不需要一比一划分内存空间。
  * **将内存（新生代内存）分为一块较大的Eden（伊甸园）和两块较小的Survivor（幸存者，大学一样，一块称为From区，一块为To区）空间。每次只使用Eden和其中的一块Survivor区域。（默认为：8:1:1）**
  * **HotSpot复制算法流程**
    * 当Eden区满的时候，会触发第一次Minor GC，将所有存活对象拷贝到Survivor的From区域，然后一次性清除Eden区。当Eden区再次触发MinorGC，会扫描Eden区和From区域，将两块空间中的存活对象拷贝到To区，而后一次性清除Eden区和Survivor区。
    * 当后续Eden区再次发生Minor GC会对Eden区和To区进行回收，存活对象移动到From区，后续流程类似。只是将From区域和To区来回作为保留区域。
    * 部分对象会在From和To区域来回复制。如此交换15（MaxTenuringThreshold，默认为15次），最终会存入老年代。
    * **注意**：Survivor区域无法存放所有存活对象，需要依赖其他内存（如老年代）进行分配担保（父债子偿的例子）。



**3. 标记整理算法（老年代的垃圾回收（GC）算法**

老年代中的对象存活率较高，因此不适用复制算法（需要大量进行对象的复制过程，效率较低）

* **思想**：：算法分为标记与整理两个阶段。标记过程与标记清除过程一致，**整理过程**需要让所有存活对象向一端移动，而后直接清除掉存活对象边界以外的内存。





**4.  分代回收算法（Java）**

* **思想**：根据对象的存活周期将内存划分为以下两块。
  * 新生代：每次GC都有大部分对象死去，只有少量存活，因此采用复制算法。座椅Minor GC(采用复制算法)非常频繁，一般回收速度也比较快
  * 老年代：因为的存活率较高，没有额外空间对其分配担保，采用标记-整理算法。



**注意**

* **MInorGC（称为新生代GC）**：指的是发生在新生代的垃圾回收，由于新生代对象大多数存活周期较短，因此  MinorGC发生频率非常频繁，一把回收速度也较高。
* **FullGC（称为老年代GC或者MajorGC）**：指的是发生在老年代的垃圾回收，出现MajorGC通常至少会伴随一次MinorGC（并非绝对），一般FullGC比MinorGC慢10倍以上，发生频率较低。：



### 6.垃圾收集器（垃圾回收算法的具体体现）--JDK8

**新生代垃圾回收器**：Serial（串行），ParNew（并行），Parallel    Scavenge（并行）

**老年代垃圾回收器：**CMS（并发 ，第一款并发的垃圾回收器），Serial  Old（串行），Parallel  Old（并行）

**全区域垃圾回收器：**G1（并发）垃圾回收器是用在heap memory很大的情况下，把heap划分为很多很多的region块，然后并行的对其进行垃圾回收。G1垃圾回收器在清除实例所占用的内存空间后，还会做内存压缩。

**注意：**

* 串行：垃圾回收线程与用户线程在JVM 中顺序执行
* 并行：多个垃圾回收线程一起执行，用户线程仍处于等待状态
* 并发：垃圾回收线程和用户线程一起执行(不一定并行，可能会交替执行)，用户程序继续运行，而垃圾收集程序在另外一个CPU上
* STW：当垃圾回收线程工作时，用户线程处于等待状态

### 7.对象分配策略

1. **对象优先在Eden分配**
   * 大多数情况下，对象在新生代Eden区中分配。当Eden区没有足够的空间进行分配时，虚拟机将发生一次Minor GC

2.  **大对象直接进入老年代**
   * 大对象是指，需要大量连续空间的Java对象，最典型的大对象就是那种很长的字符串以及数
   * 大对象对虚拟机的内存分配是一个坏消息，经常出现大对象容易导致内存还有不少空间时就提前触发GC以获取足够的连续空间来放置大对象
   * 虚拟机提供了一个**-XX:PretenureSizeThreshold**参数，令大于这个设置值的对象直接在老年代分配
     * 这样做的目的在于避免Eden区以及两个Survivor区之间发生大量的内存复制(新生代采用复制算法收集内存)

3. **长期存活的对象将进入老年代**
   * 虚拟机给每个对象定义了一个**对象年龄(Age)计数器**。如果对象在Eden出生并经
     过一次Minor GC后仍然存活，并且能被Survivor容纳的话，将被移动到Survivor空间中，并且把对象年龄设为1.对象在Survivor空间中每经历一次Minor GC，年龄就增加1岁。当它的年龄增加到一定程度(默认为**15岁**)，就将晋升到老年代中。
   * 对象晋升到老年代的年龄阈值，可以通过参数-XX:MaxTenuringThreshold设置。

4. **动态对象年龄**
   * JVM并不是永远要求对象的年龄必须到达MaxTenuringThreshold才能晋升老年代，若Survivor空间中相同年龄的所有对象大小 总和大于Survivor空间的一半，此时年龄大于等于该年龄的对象就可以进入老年代，无需等到MaxTenuringThreshold要求的年龄









### 8.对象创建方法，对象的内存分配，对象的访问定位。

<https://blog.csdn.net/qq_41907991/article/details/84310145>

<https://www.jianshu.com/p/73bc18bab332>

##### 1.对象的创建

1. **对象的创建方法**：new的过程

   - **第一：进行类加载检查**：当遇到一个new指令，首先检查能否在方法区的常量池中能否定位到这个类的符号引用，并且检查类有没有进行加载、解析和初始化；

   - **第二：分配空间**：有两种常见的分配方式，一是指针碰撞，二是空闲列表，分别针对连续分配内存和不连续的。

     - **"指针碰撞"（Bump the Pointer）**：Java堆是绝对规整的：一边是用过的内存，一边是空闲的内存，中间一个指针作为边界指示器，分配内存的方式就是将指针向空闲空间。那边挪动与对象相等大小的距离,这种分配方式称为指针碰撞

     - **空闲列表**：java堆中的内存不是规整的，已使用的内存和空闲的内存相互交错，这样就无法进行简单地指针碰撞了，这时候虚拟机会维护一张列表，列表中记录哪些内存块是可用的，在分配内存的时候就从列表中找到一块足够大的空间划分给对象实例，同时更新列表上的记录，这种内存分配的方式叫做“空闲列表”

     - **线程安全问题**：对象的创建是在堆上的，而堆是线程共享的，上面两种方式分配内存的操作都不是线程安全的；内存分配的大小是在类加载完成之后就已经确定的，

       - **同步处理**： JVM采用CAS（Compare and Swap）机制加上失败重试的方式，保证更新操作的原子性；（v,o,n）
       - **本地线程分配缓冲区**：把分配内存的动作按照线程划分在不同的空间中进行。在每个线程在Java堆预先分配一小块内存，称为本地线程分配缓冲区（Thread Local Allocation Buffer,TLAB）；哪个线程需要分配内存就从哪个线程的TLAB上分配；只有TLAB用完需要分配新的TLAB时，才需要同步处理；

       

   - **第三：初始化**。将分配的内存初始化为0值。

   - **第四：基本设置**。进行基本的设置，确定这个对象是哪个类的实例，对象的Hash码，对象的年龄等等。

##### 2.对象的内存布局

* **第一：对象头（Header）**
  * 第一部分是**“Mark Word**”，用于存储对象自身的运行时数据，如哈希码、GC分代年龄、持有的锁等等；
  * 第二部分是类型指针，指向它的类元数据的指针，通过这个虚拟机来确定这个对象是哪个类的实例。
* **第二：实例数据（Instance Data）**
  * 对象真正存储的数据，就是程序代码中定义的字段内容。
* **第三：对齐填充（Padding）**
  * 用于使对象的开头必须是8字节的整数倍，无特殊意义。

![1565363594168](C:\Users\Z\AppData\Roaming\Typora\typora-user-images\1565363594168.png)

3. ##### 对象的访问定位

   Object objectRef = new Object();  

   Object objectRef  这部分将会反映到Java栈的本地变量中，作为一个reference类型数据出现。而“new Object()”这部分将会反映到Java堆中，形成一块存储Object类型所有实例数据值的结构化内存，根据具体类型以及虚拟机实现的对象内存布局的不同，这块内存的长度是不固定。另外，在java堆中还必须包括能查找到此对象类型数据（如对象类型、父类、实现的接口、方法等）的地址信息，这些数据类型存储在方法区中。

   * **第一：句柄访问（间接)**：在Java堆中划分一块内存作为句柄池（即一个句柄列表），reference中存储的就是对象在句柄池中的地址，得到了句柄池的地址就可以知道对象的实例数据和类型数据的位置。
   * **第二：直接指针访问（直接）**：reference中存储的直接就是对象的实例数据的地址，而实例数据中自己有一个指针存储对象类型数据的地址（方法区中），不需要reference来存储。





1. GC的三种收集方法：标记清除、标记整理、复制算法的原理与特点，分别用在什么地方，如果让你优化收集方法，有什么思路？



1. GC收集器有哪些？CMS收集器与G1收集器的特点。



### 9.Minor GC与Full GC分别在什么时候发生？

1. **Minor GC**

   * 当Eden区满时，触发Minor GC。即申请一个对象时，发现eden区不够用，则触发一次MinorGC。

2. **Full GC**

   * 当老年代无法分配新的内存的时候，会导致MinorGC

   * 调用System.gc时，系统建议执行Full GC，但是不必然执行

   * 方法去空间不足

   * 通过Minor GC后进入老年代的平均大小大于老年代的可用内存

   * 由Eden区、From Space区向To Space区复制时，对象大小大于To Space可用内存，则把该对象转存到老年代，且老年代的可用内存小于该对象大小。

     

###  10.几种常用的内存调试工具：jmap、jstack、jconsole。

* **jps：进程状态工具**：列出正在运行的JVM 进程，并返回进程ID

  * jps -l ：输出主类 全名，返回进程ID

* **jmap ：内存印象工具（查看Java堆具体信息）**

  * jamp 用于生成堆转储快照（堆得快照）

  * jmap  -heap  PID:显示JVM堆得具体信息

* **jstack     Java栈跟踪工具**

  * jstack  生成当前JVM线程的快照
  * 可用于定位线程出现长时间停顿的原因，如线程间死锁，死循环问题。

* **jstat：JVM统计信息监视工具**：显示本地或远程JVM中类装载，内存，垃圾回收等数据

  * jstat  -gcutil  PID：显示垃圾回收信息

* **jinfo：JVM配置信息查看工具**

* **jhat：heap文件的分析工具**





### 11.加载的五个过程：加载、验证、准备、解析、初始化。

链接：https://www.jianshu.com/p/3556a6cca7e5

##### 1.加载

* 通过类的全限定名来获取定义此类的二进制字节流
* 将这个类字节流代表的静态存储结构转为方法区的运行时数据结构
* 在堆中生成一个代表此类的java.lang.Class对象，作为访问方法区这些数据结构的入口。

##### 2.验证

主要确保Class文件的字节流中包含的信息符合当前虚拟机的要求，并且不会危害虚拟机的自身安全。

* 文件格式验证：基于字节流验证。
* 元数据验证：基于**方法区**的存储结构验证。
* 字节码验证：基于方法区的存储结构验证。
* 符号引用验证：基于方法区的存储结构验证。

##### 3.准备

* 为类变量分配内存，并将其初始化为默认值。（此时为默认值，在初始化的时候才会给变量赋值）即在方法区中分配这些变量所使用的内存空间

##### 4.解析：把类型中的符号引用转换为直接引用。

* **符号引用**与虚拟机实现的布局无关，引用的目标并不一定要已经加载到内存中。各种虚拟机实现的内存布局可以各不相同，但是它们能接受的符号引用必须是一致的，因为符号引用的字面量形式明确定义在Java虚拟机规范的Class文件格式中。
* **直接引用**可以是指向目标的指针，相对偏移量或是一个能间接定位到目标的句柄。如果有了直接引用，那引用的目标必定已经在内存中存在
* **分类**：
  * 类或接口的解析
  * 字段解析
  * 类方法解析
  * 接口方法解析

##### 5.初始化

java中，对于初始化阶段，有且只有以下五种情况才会对要求类立刻“初始化”（加载，验证，准备，自然需要在此之前开始）：

* 使用new关键字实例化对象、访问或者设置一个类的静态字段（被final修饰、编译器优化时已经放入常量池的例外）、调用类方法，都会初始化该静态字段或者静态方法所在的类。

* 初始化类的时候，如果其父类没有被初始化过，则要先触发其父类初始化。

* 使用java.lang.reflect包的方法进行反射调用的时候，如果类没有被初始化，则要先初始化。

* 虚拟机启动时，用户会先初始化要执行的主类（含有main）

* jdk 1.7后，如果java.lang.invoke.MethodHandle的实例最后对应的解析结果是 REF_getStatic、REF_putStatic、REF_invokeStatic方法句柄，并且这个方法所在类没有初始化，则先初始化。

  



### 12.双亲委派模型：Bootstrap ClassLoader、Extension ClassLoader、ApplicationClassLoader。

##### 1.BootStrap(启动类加载器)

* a.使用C++语言实现，是JVM的自身的一部分，独立于JVM外部，并且无法实现java程序的直接引用

* b.负责将存放于JAVA_HOME\bin目录下的，能被JVM识别的所有类库（例如：jar-java基础类库）加载到JVM中
* jar文件->压缩文件:  存放若干个编译好的class文件

##### 2.ExtClassLoader（扩展类加载器）

* a.使用java语言实现，可以被java程序直接引用
* b.负责将存放于 JAVA_HOME\bib\ext（xml文件解析类，界面框架类）目录下的所有能被JVM识别的类库

##### 3. **APPClassLoader（应用程序类加载器）**

* a.使用java程序实现，如果用户没有自定义类加载器，则APPClassLoader就是程序中默认的类加载器。
* b.负责加载用户ClassPath指定的类库



##### 双亲委派模型

* **工作流程**

  * 如果一个类加载器收到了类加载器的请求.它首先不会自己去尝试加载这个类.而是把这个请求委派给父加载器去完成.每个层次的类加载器都是如此.因此所有的加载请求最终都会传送到Bootstrap类加载器(启动类加载器)中.只有父类加载反馈自己无法加载这个请求(它的搜索范围中没有找到所需的类)时.子加载器才会尝试自己去加载。

* **双亲委派模型的意义 **

  * 双亲委派模型对于保证java程序的稳定运行十分重要

    * 例如类java.lang.Object,它存放在rt.jart之中.无论哪一个类加载器都要加载这个类.最终都是双亲委派模型最顶端的Bootstrap类加载器去加载.因此Object类在程序的各种类加载器环境中都是同一个类.

    * 相反.如果没有使用双亲委派模型.由各个类加载器自行去加载的话.如果用户编写了一个称为“java.lang.Object”的类.并存放在程序的ClassPath中.那系统中将会出现多个不同的Object类.java类型体系中最基础的行为也就无法保证.应用程序也将会一片混乱.

      

    * 

  

![1565364586313](C:\Users\Z\AppData\Roaming\Typora\typora-user-images\1565364586313.png)



JVM过去过来就问了这么些问题，没怎么变，内存模型和GC算法这块问得比较多，可以在网上多找几篇博客来看看。

# 类集

### 1.Fail-Safe和Fail-Fast机制

##### fail-fast策略(java.util 除了TreeSet外的所有集合), 不能在多线程下发生并发修改（迭代过程中被修改）

* **发生时间**：
  * ConCurrentModificationException发生在Collection集合使用迭代器遍历时，是因为在集合遍历时修改集合内容报错
  * 当多个线程对同一个集合进行操作的时候，某线程访问集合的过程中，该集合的内容被其他线程所改变(即其它线程通过add、remove、clear等方法，改变了modCount的值)；这时，就会抛出ConcurrentModificationException异常。
* **产生原因**：
  * 在执行checkForComodification()方法的 modCount 不等于expectedModCount时产生的
  * 常的抛出条件是检测到 modCount！=expectedmodCount 这个条件。如果集合发生变化时修改modCount值刚好又设置为了expectedmodCount值，则异常不会抛出。因此，不能依赖于这个异常是否抛出而进行并发操作的编程，这个异常只建议用于检测并发修改的bug。
  * **modCount**：
    * 表示当前集合修改的次数，如果在一个并发的情况下，如果集合已经添加完元素，用户一应正在遍历了，如果这个时候修改内容，就要有一个东西告诉用户这个值已经修改了，
    * 它保证了用户不会脏读数据（下载看到的数据不是最新的），modCount保证了用户看到的值一定是最新的值)
  * **expectedModCount**
    * 是迭代器中记录当前集合的修改次数
    * 取得当前集合迭代器时（及调用list.Iterator（）方法时），expectedModCount=modCount，换言之，迭代器就是当前集合的一个副本
* **作用：**
  * 快速失败策略保证了所有用户在进行迭代遍历集合时，拿到的数据一定是最新的数据（避免“脏读”产生）
* **解决方法**：使用Iterator迭代器的remove（）不会出现此错误。

##### fail-safe？juc包下所有线程安全的集合

* **场景**：
  *  java.util.concurrent包下的容器都是安全失败，可以在多线程下并发使用，并发修改copyOnWriteArrayList、copyOnWriteArraySet、coucurrentHashMap
* **出现原因**
  * 不产生ConcurrentModificationException异常
* **原理**
  *  由于**迭代时是对原集合的拷贝进行遍历**，所以在遍历过程中对原集合所作的修改并不能被迭代器检测到，所以不会触发ConcurrentModificationException。CopyOnWriteArrayList类中实现的
* **缺点**
  *  基于拷贝内容的优点是避免了Concurrent Modification Exception，但同样地，迭代器并不能访问到修改后的内容，即：**迭代器遍历的是开始遍历那一刻拿到的集合拷贝，在遍历期间原集合发生的修改迭代器是不知道的**。
* **ArrayList和CopyOnWriteArrayList的区别**
  * 和ArrayList继承于AbstractList不同，CopyOnWriteArrayList没有继承于AbstractList，它仅仅只是实现了List接口
  *  ArrayList的iterator()函数返回的Iterator是在AbstractList中实现的；而CopyOnWriteArrayList是自己实现Iterator。
  *  ArrayList的Iterator实现类中调用next()时，会“调用checkForComodification()比较‘expectedModCount’和‘modCount’的大小”；但是，CopyOnWriteArrayList的Iterator实现类中，没有所谓的checkForComodification()，更不会抛出ConcurrentModificationException异常。

## 操作系统

\1. 进程和线程的区别。

\2. 死锁的必要条件，怎么处理死锁。

\3. Window内存管理方式：段存储，页存储，段页存储。



\4. 进程的几种状态。

\5. IPC几种通信方式。

\6. 什么是虚拟内存。

\7. 虚拟地址、逻辑地址、线性地址、物理地址的区别。





## 三、 项目

关于项目，这部分每个人的所做的项目不同，所以不能具体的讲。项目不再与好与不好，在于你会不会包装，有时候一个很low的项目也能包装成比较高大上的项目，多用一些专业名词，突出关键字，能使面试官能比较容易抓住重点。在聊项目的过程中，其实你的整个介绍应该是有一个大体的逻辑，这个时候是在考验你的表达与叙述能力，所以好好准备很重要。

面试官喜欢问的问题无非就几个点：

1. XXX（某个比较重要的点）是怎么实现的？

2. 你在项目中遇到的最大的困难是什么，怎么解决的？

3. 项目某个部分考虑的不够全面，如果XXXX，你怎么优化？

4. XXX（一个新功能）需要实现，你有什么思路？

## 四.问面试官的问题

以下是我常问的几个问题，如果需要可以参考：

1. 贵公司一向以XXX著称，能不能说明一下公司这方面的特点？

2. 贵公司XXX业务发展很好，这是公司发展的重点么？

3. 对技术和业务怎么看？

4. 贵公司一般的团队是多大，几个人负责一个产品或者业务？

5. 贵公司的开发中是否会使用到一些最新技术？

6. 对新人有没有什么培训，会不会安排导师？

7. 对Full Stack怎么看？

8. 你觉得我有哪些需要提高的地方？