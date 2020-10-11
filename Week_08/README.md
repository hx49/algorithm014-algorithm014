## 位运算

**位运算符**

|              含义              | 运算符 |         实例         |
| :----------------------------: | :----: | :------------------: |
|              左移              |   <<   |     0011 => 0110     |
|              右移              |   >>   |     0110 => 0011     |
|             按位或             |   \|   | 0011 \| 1011 => 1011 |
|             按位与             |   &    | 0011 & 1011 => 0011  |
|            按位取反            |   ~    |     0011 => 1100     |
| 按位异或（相同为零、不同为一） |   ^    | 0011 ^ 1011 => 1000  |

**XOR - 异或**

异或：相同为0，不同为1。也可用“不进位加法”来理解。

异或操作的一些特点：

> x ^ 0 = x
>
> x ^ 1s = ~x // 注意1s = ~0;
>
> x ^ (~x) = 1s
>
> x ^ x = 0
>
> c = a ^ b => a ^ b = c, b ^ c = a // 交换两个数
>
> a ^ b ^ c = a ^ (b ^ c) = (a ^ b) ^ c //  associative 组合

**指定位置的位运算**

> 1、将x最右边的n位清零：x & (~ 0 << n)
>
> 2、获取x的第n位值(0或者1)：(x >> n) & 1
>
> 3、获取x的第n位的幂值：x & (1 << n)
>
> 4、仅将第n位置为1：x | (1 << n)
>
> 5、仅将第n位置为0：x & ( ~(1 << n))
>
> 6、将x最高位至第n位(含)清零：x & ((1 << n) - 1)

**位运算的应用**

- 判断奇偶：

x % 2 == 1 —> (x & 1) == 1

x % 2 == 0 —> (x & 1) == 0

- x >> 1 —> x / 2

即：x = x / 2； —> x = x >> 1；

​		mid = (left + right) / 2； —> mid = (left + right) >> 1；

- x = x & (x - 1) 清零最低位的1
- x & -x => 得到最低位的1
- x & ~x = 0



## 布隆过滤器

布隆过滤器 Bloom Filter

一个很长的二进制向量和一系列随机映射函数。布隆过滤器可以用于检索一个元素是否在一个集合中。

优点：空间效率和查询时间都远远超过一般的算法。

缺点：有一定的误识别率和删除困难。

**布隆过滤器 vs 哈希表**

哈希表不仅可以判断是否元素在集合中，还可以存元素本身和元素的各种额外信息。（HashTable + 拉链存储重复元素）

![image-20200930092917559](C:\Users\huang\Desktop\algorithm014\algorithm014-algorithm014-1\Week_08\README.assets\image-20200930092917559.png)

使用布隆过滤器查数据时，若查到不在，那么肯定不在；若查到存在，只能说是可能存在，需要继续在数据库中查询。

布隆过滤器只是挡在一台机器前面的快速查询的缓存，真正要确定元素一定存在，必须要再访问这个机器里面的一个完整的存储数据结构（一般为数据库）

**案例**

1、比特币网络

2、分布式系统（Map-Reduce) —— Hadoop、search engine

3、Redis 缓存

4、垃圾邮件、评论等的过滤

**Java 实现**

- [布隆过滤器 Java 实现示例 1](https://github.com/lovasoa/bloomfilter/blob/master/src/main/java/BloomFilter.java)
- [布隆过滤器 Java 实现示例 2](https://github.com/Baqend/Orestes-Bloomfilter)



## LRU Cache

**Cache 缓存**

1、记忆

2、钱包 - 储物柜

3、代码模块

**LRU Cache**

- 两个要素：大小、替换策略

  替换策略：

  - LFU - least frequently used
  - LRU - least recently used
  - [替换算法总揽](https://en.wikipedia.org/wiki/Cache_replacement_policies)

- Hash Table + Double LinkedList

- O(1) 查询、修改、更新

![image-20200930231024422](C:\Users\huang\Desktop\algorithm014\algorithm014-algorithm014-1\Week_08\README.assets\image-20200930231024422.png)

**实现**

[LRU 缓存机制](https://leetcode-cn.com/problems/lru-cache/#/)



## 排序算法

**算法分类**

1、比较类排序：

​	通过比较来决定元素间的相对次序，由于其时间复杂度不能突破 O(nlogn)，因此也称为非线性时间比较类排序。

2、非比较类排序：

​	不通过比较来决定元素间的相对次序，它可以突破基于比较排序的时间下届，以线型时间运行，因此也称为线性时间非比较类排序。

![img](C:\Users\huang\Desktop\algorithm014\algorithm014-algorithm014-1\Week_08\README.assets\849589-20190306165258970-1789860540.png)

**算法复杂度**

![img](C:\Users\huang\Desktop\algorithm014\algorithm014-algorithm014-1\Week_08\README.assets\849589-20180402133438219-1946132192.png)

- 重点考察时间复杂度为 O(nlogn) 的排序算法：堆排序、快速排序、归并排序。

------

### 初级排序 - O(n^2)

1、选择排序(Selection Sort)

​	每次找最小值，然后放到待排序数组的起始位置。

2、插入排序(Insertion Sort)

​	从前到后逐步构建有序序列；对于未排序数据，在已排序序列中从后向前扫描，找到相应位置并插入。

3、冒泡排序(Bubble Sort)

​	两层嵌套循环，每次查看相邻的元素，如果逆序，则交换。

------

### 高级排序 - O(N*LogN)

**1、快速排序(Quick Sort)**

​	数组取标杆 pivot，将小元素放 pivot 左边，大元素放 pivot 右边，然后依次对左边和右边的子数组继续快排，以达到整个序列有序。

> note：正常情况下数组的 prepend 操作的时间复杂度是 O(n)，但是可以进行特殊优化到 O(1)。采用的方式是申请稍大一些的内存空间，在数组最开始预留一部分空间，然后 prepend 的操作则是把头下标前移一个位置即可。

```java
public static void quickSort (int[] array, int begin, int end) {
    if (end <= begin) return;
    int pivot = partition(array, begin, end);
    quickSort(array, begin, pivot - 1);
    quickSort(array, pivot + 1, end);
}

static int partition (int[] a, int begin, int end) {
    // pivot:标杆位置,counter:小于 pivot 的元素的个数
    int pivot = end, counter = begin;
    for (int i = begin; i < end ; i ++) {
        if (a[i] < a[pivot]) {
            int temp = a[counter]; a[counter] = a[i]; a[i] = temp;
            counter ++;
        }
    }
    int temp = a[pivot]; a[pivot] = a[counter]; a[counter] = temp;
    return counter;
}
调用方式：quickSort(a, 0, a.length - 1)
```

**2、归并排序(Merge Sort) - 分治**

1. 把长度为 n 的输入序列分为两个长度为 n/2 的子序列；
2. 对这两个子序列分别采用归并排序；
3. 将两个排序好的子序列合并成一个最终的排序序列。

```java
public static void mergeSort (int[] array, int left, int right) {
    if (right <= left) return;
    int mid = (left + right) >> 1; // (left + right) / 2
    
    mergeSort(array, left, mid);
    mergeSort(array, mid + 1, right);
    merge(array, left, mid, right);
}

public static void merge (int[] arr. int left, int mid, int right) {
    int[] temp = new int[right - left + 1]; // 中间数组
    int i = left, j = mid + 1, k = 0; // k:temp中已填入的元素的个数
    
    while (i <= mid && j <= right) {
        temp[k ++] = arr[i] <= arr[j] ? arr[i ++] : arr[j ++];
    }
    
    while (i <= mid) temp[k ++] = arr[i ++];
    while (j <= right) temp[k ++] = arr[j ++];
    
    for (int p = 0 ; p < temp.length ; p ++) {
        arr[left + p] = temp[p];
    }
    // 也可以用 System.arraycopy(a, start1, b, start2, length)
}
```

> 归并和快排具有相似性，但步骤顺序相反
>
> 快排：先调配出左右子数组，然后对于左右子数组进行排序
>
> 归并：先排序左右子数组，然后合并两个有序子数组

**3、堆排序(Heap Sort)** - 堆插入 O(logN)，取最大/小值 O(1)

1. 数组元素依次建立小顶堆；
2. 依次取堆顶元素，并删除。

```java
static void heapify(int[] array, int length, int i) {
    int left = 2 * i + 1, right = 2 * i + 2；
    int largest = i;
    if (left < length && array[left] > array[largest]) {
        largest = left;
    }
    if (right < length && array[right] > array[largest]) {
        largest = right;
    }
    if (largest != i) {
        int temp = array[i]; array[i] = array[largest]; array[largest] = temp;
        heapify(array, length, largest);
    }
}
public static void heapSort(int[] array) {
    if (array.length == 0) return;
    int length = array.length;
    for (int i = length / 2-1; i >= 0; i-) 
        heapify(array, length, i);
    for (int i = length - 1; i >= 0; i--) {
        int temp = array[0]; array[0] = array[i]; array[i] = temp;
        heapify(array, i, 0);
    }
}
```

------

### 特殊排序 - O(n)

1、计数排序(Counting Sort)

​	计数排序要求输入的数据必须是有确定范围的整数。将输入的数据值转化为键存储在额外开辟的数据空间中；然后依次把计数大于1的填充回原数组。

2、桶排序(Bucket Sort)

​	桶排序(Bucket Sort)的工作原理：假设输入数据服从均匀分布，将数据分到有限数量的桶里，每个桶再分别排序（有可能再使用别的排序算法或是以递归方式继续使用桶排序进行排）。

3、基数排序(Radix Sort)

​	基数排序是按照低位先排序，然后收集；再按照高位排序，然后再收集；以此类推，直到最高位。有时候有些属性是有优先级顺序的，先按低优先级排序，再按高优先级排序。