---
title: "Hashmapimplements"
date: 2020-09-30T19:32:13+08:00
draft: false
---
# jdk11的HashMap源码分析

## 文档注释部分：

* HashMap是无序的，特别是不保证顺序随时间不变
* get 和 put 操作是常量时间复杂度的---O(1)
* 装载因子设置为0.75，平衡了空间和时间消耗。更高的装载因子降低了空间成本却增大了查找的花费，导致put、get操作时间变慢。
* 如果初始容量（initial capacity）比最大元素数（maximum number of entries）除以装载因子的值还大，那么不会再进行rehash操作。
* **一般采用桶（binned、bucketed）哈希表，但是如果桶元素太多，会变成树（TreeNodes），树的结构就像TreeMap**
* 由于 resize 和 removal 操作导致树的结点太少的时候，会将红黑树变为哈希桶（untreeified）

## 继承关系

```java
public class HashMap<K,V> extends AbstractMap<K,V>    
implements Map<K,V>, Cloneable, Serializable
```
* HashMap可被序列化，可被克隆

## 参数
```java
static final int DEFAULT_INITIAL_CAPACITY = 1 << 4; // aka 16
// 必须是2的幂
static final int MAXIMUM_CAPACITY = 1 << 30;
// 必须是2的幂
static final float DEFAULT_LOAD_FACTOR = 0.75f;

static final int TREEIFY_THRESHOLD = 8;
// 当一个hash桶的元素数大于8，那么就变成红黑树实现

static final int UNTREEIFY_THRESHOLD = 6;
// 当resize让一个树的元素小于6时，就把它变为桶

static final int MIN_TREEIFY_CAPACITY = 64;
// 整个hash表执行树化操作的最小容量，表里的元素数大于64才会树化桶
```

## put()

>[代码注解来源](https://blog.csdn.net/lxyer4u/article/details/86233382)

* 找一个元素的所在位置 `p = tab[i=(n-1) & hash]`，其中n表示哈希表的长度，是 2 的幂减 1，`n-1`是每位都是1的二进制数，借助`与`运算即可快速完成取模操作
* HashMap的 bucket 容量必须为2的幂的另一个重要原因是一旦满足此条件，那么length即为偶数，length - 1便为奇数，所以length - 1的最后一位必为1。因此，h & (length - 1)得到的值既可能是奇数，也可能是偶数，这确保了散列的均匀性。如果length - 1是偶数，那么h & (length - 1)得到的值必为偶数，那么HashMap的空间便浪费了一半。

* **尾插法**插入新元素

![put函数注释1](/put-01.png)
![put函数注释2](/put-02.png)

## get()
>[代码注解来源](https://blog.csdn.net/lxyer4u/article/details/86233382)

* 如果key值存在，检查hash值相等的第一个元素是不是，不是的话分红黑树和链表两种情况检查。

![get函数注释1](/get-01.png)
![get函数注释2](/get-02.png)

## 参考文献
1. [https://www.cnblogs.com/helloworldcode/p/13057434.html](https://www.cnblogs.com/helloworldcode/p/13057434.html)

2. [https://segmentfault.com/a/1190000007699188](https://segmentfault.com/a/1190000007699188)

3. [https://blog.csdn.net/lxyer4u/article/details/86233382](https://blog.csdn.net/lxyer4u/article/details/86233382)
