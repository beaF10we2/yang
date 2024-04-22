java一些常用的，方便的东西

[TOC]

一些常用的转换函数



```
//String转int
Integer num = Integer.valueOf(str);
int nim=Integer.parseInt(str)

//char转String
String str = String.valueOf(c);

//int转String
java
int number = 123;  
String str = Integer.toString(number);

//降序
 Arrays.sort(array, Comparator.reverseOrder()); 
 
// 获取从索引2（包括）到索引5（不包括）的子数组  
int[] subArray = getSubArray(array, 2, 5);  

//

```

  

Array.sort(int a[]):将i个数组的所有元素按从小到大排列

### Set

![1705734445797](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\1705734445797.png)

无序的，不重复的

        // 使用 for-each 循环遍历 HashSet  
        System.out.println("使用 for-each 循环遍历 HashSet:");  
        for (String fruit : hashSet) {  
            System.out.println(fruit);  
        }  
### map

![1705738970081](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\1705738970081.png)

![1705739059546](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\1705739059546.png)

![1705741052339](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\1705741052339.png)

`map.containsKey()` 是Java中Map接口的一个方法。这个方法用于检查Map中是否包含特定的键。

具体来说，`map.containsKey(Object key)` 方法会检查Map中是否存在一个键值对，其中键是给定的`key`。如果存在这样的键值对，那么方法返回`true`，否则返回`false`。

      // 遍历键集  
            System.out.println("遍历键集:");  
            for (String key : hashMap.keySet()) {  
                System.out.println("键: " + key);  
            }  
      // 遍历值集  
        System.out.println("\n遍历值集:");  
        for (Integer value : hashMap.values()) {  
            System.out.println("值: " + value);  
        }  
### stack

![1705741215171](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\1705741215171.png)

![1705741252603](C:\Users\86176\AppData\Roaming\Typora\typora-user-images\1705741252603.png)

```
在Java中，java.util.Stack类继承自java.util.Vector类，提供了栈的功能。以下是java.util.Stack的一些常用方法：

push(E item): 将指定的元素插入此堆栈中，并覆盖堆栈顶部的元素。
pop(): 删除并返回此堆栈的顶部元素。
peek(): 返回此堆栈的顶部元素，但不删除它。
empty(): 如果此堆栈为空，则返回 true。
size(): 返回此堆栈中的元素数。
search(Object o): 返回此堆栈中指定元素的索引，以使得第一个搜索到的元素是最先插入的元素。
elementAt(int index): 获取此向量中指定索引处的元素。
indexOf(Object o): 返回此向量中首次出现的指定元素的索引，从头部开始搜索。
lastElement(): 返回并删除此向量中的最后一个元素。
removeElement(Object o): 从此向量中删除第一次出现的指定元素（如果存在）。
clear(): 移除此向量中的所有元素。
```

### List

```
在Java中，List接口是java.util包中一个非常重要的集合框架接口，它表示有序的集合（即元素按照它们被添加的顺序排列）。有许多类实现了List接口，例如ArrayList, LinkedList, Vector等。

以下是List接口的一些常用函数：

add(E e): 将指定的元素插入此列表的适当位置。
remove(Object o): 移除此列表中首次出现的指定元素（如果存在）。
contains(Object o): 返回 true 如果此列表包含指定的元素。
indexOf(Object o): 返回此列表中首次出现的指定元素的索引，从 0 开始。
lastIndexOf(Object o): 返回此列表中最后一次出现的指定元素的索引，从 0 开始。
isEmpty(): 如果此列表没有元素则返回 true。
size(): 返回此列表中的元素数。
iterator(): 返回一个迭代器，该迭代器可用于按顺序访问此列表中的元素。
toArray(): 将此列表中的所有元素收集到数组中。
subList(int fromIndex, int toIndex): 返回从 fromIndex（包括）到 toIndex（不包括）的此列表的视图。
add(int index, E element): 在指定的位置插入指定的元素。
remove(int index): 移除在指定位置的元素。
set(int index, E element): 将指定位置的元素设置为指定的值。
get(int index): 返回在指定位置的元素。
```



### 链表

```
public class ListNode {
     int val;
     ListNode next;
     ListNode() {}
     ListNode(int val) { this.val = val; }
    ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 }
```

