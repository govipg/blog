# HashMap在1.7和1.8的变化

HashMap在1.7的时候，底层是**数组+链表**

<img src="images/hashmap总体结构.png" alt="hashmap总体结构" style="zoom:67%;" />

数组是HashMap的主体，链表则是主要为了解决哈希冲突而存在的 

**其中：链表的节点存储的是一个 Entry 对象，每个Entry 对象存储四个属性（hash，key，value，next）** 



JDK1.7的时候使用的是数组+ 单链表的数据结构。

但是在JDK1.8及之后时，使用的是数组+链表+红黑树的数据结构

（当链表的深度达到8的时候，也就是默认阈值，就会自动扩容把链表转成红黑树的数据结构来把时间复杂度从O（n）变成O（logN）提高了效率）。 



## JDK 8.0与JDK 7.0中HashMap底层的变化：

1. `new HashMap()`:底层没有创建一个长度为16的数组
2. JDK 8.0底层的数组是：`Node[]`,而非 `Entry[]`
3. 首次调用put()方法时，底层创建长度为16的数组
4. JDK 7.0底层结构只有：数组+链表。JDK 8.0中底层结构：数组+链表+红黑树。
   - 形成链表时，七上八下（jdk7:新的元素指向旧的元素。jdk8：旧的元素指向新的元素）
   - 当数组的某一个索引位置上的元素以链表形式存在的数据个数 > 8 且当前数组的长度 > 64时，此时此索引位置上的所数据改为使用红黑树存储。

## 扩容

当HashMap**中的元素个数超过数组大小\*loadFactor时，就会进行数组扩容。**

loadFactor的默认值为0.75，数组大小为16。也就是说，默认情况下，那么当HashMap中元素个数超过16`*`0.75=12的时候，就把数组的大小扩展为2`*`16=32，即扩大一倍，然后重新计算每个元素在数组中的位置。

## JDK1.8中的put方法

put存值的方法，过程如下：

1. 首先根据`key`的值计算`hash`值，找到该元素在数组中存储的下标
2. 如果数组是空的，则调用`resize`进行初始化；
3. 如果没有哈希冲突直接放在对应的数组下标里
4. 如果冲突了，且`key`已经存在，就覆盖掉`value`
5. 如果冲突后是链表结构，就判断该链表是否大于`8`，如果大于`8`并且数组容量小于`64`，就进行扩容；如果链表节点数量大于`8`并且数组的容量大于`64`，则将这个结构转换成红黑树；否则，链表插入键值对，若key存在，就覆盖掉`value`
6. 如果冲突后，发现该节点是红黑树，就将这个节点挂在树上