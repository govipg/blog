# 说一说java集合的理解

![集合结构体系图](assets/%E9%9B%86%E5%90%88%E7%BB%93%E6%9E%84%E4%BD%93%E7%B3%BB%E5%9B%BE.png)



java集合分为Collection单列集合和Map双列集合



Collection单列集合又分为List集合和Set集合，List是**有序可重复的单列集合**（可以插入多个null元素），Set是**无序不可重复的单列集合**（只允许存入一个null元素）。

List的主要实现类有：**ArrayList、LinkedList 和 Vector**

**ArrayList**：底层数据结构是数组，查询快，增删慢，线程不安全

**LinkedList**：底层数据结构是链表，查询慢，增删快，线程不安全

**Vector**：功能和ArrayList差不多，不过它是线程安全的，所以性能就差一些。

Set的主要实现类有：**HashSet、LinkedHashSet 以及TreeSet**

**HashSet**：是Set接口的主要实现类，线程不安全的

**LinkedHashSet**：是HashSet的子类，可以按照添加的顺序遍历

**TreeSet**：底层存储结构是红黑树，要求添加的元素是同一个类创建的对象，可以按照这些对象的某些属性进行排序



Map是一个键值对集合，存储键、值和之间的映射。

 **Key唯一，不可重复；value允许重复**。

主要实现类是： **HashMap、HashTable、TreeMap、ConcurrentHashMap** 

**1、HashMap**：jdk1.7的时候底层使用数组+链表；jdk1.8改用数组+链表+红黑树存储，是线程不安全的Map。（可以使用null作为key和value）

**2、HashTable**：hashTable是线程安全的，它实现线程安全的方法是在各个方法上添加了synchronize关键字。（Hashtable不允许使用null作为key和value）

**3、ConcurrentHashMap**：是线程安全的，该类在 JDK 1.7 和 JDK 1.8 的底层原理有所不同，JDK 1.7 采用数组 + 链表存储数据，使用分段锁 Segment 保证线程安全；JDK 1.8 采用数组 + 链表/红黑树存储数据，使用 CAS + synchronized 保证线程安全。

**4、TreeMap**

TreeMap也是一个很常用的map实现类，因为他具有一个很大的特点就是会对Key进行排序，使用了TreeMap存储键值对，再使用iterator进行输出时，会发现其默认采用key由小到大的顺序输出键值对，如果想要按照其他的方式来排序，需要重写也就是override 它的compartor接口。

