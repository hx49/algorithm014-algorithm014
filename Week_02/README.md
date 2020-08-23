## 哈希表

哈希表（Hash table），也叫散列表，是根据关键码值（Key value）而直接进行访问的数据结构。

它通过把关键码值映射到表中一个位置来访问记录，以加快查找的速度。

这个映射函数叫散列函数（Hash Function），存放记录的数组叫做哈希表（或散列表）。

哈希表的**查找/插入/删除**时间复杂度皆为**O(1)**

==哈希碰撞==

> 定义：当不同key得到的hash值相同时，同一个内存地址对应多个value，就产生了哈希碰撞。
>
> 解决方法：拉链式解决冲突法，将value在内存中储存的值改成一个链表，第一个值存在链表第1级，第二个碰撞的值存在链表第2级。

------

## 树、二叉树、二叉搜索树

### 树结点的定义

```java
public class TreeNode {
    public int val;
    public TreeNode left,right;
    public TreeNode(int val) {
        this.val = val;
        this.left = null;
        this.right = null;
    }
}
```

### 二叉树遍历

$\textcolor{SeaGreen}{前序遍历}$（Pre-order）：根-左-右

```java
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> list = new ArrayList<>();
        helper(root,list);
        return list;
    }
    public void helper(TreeNode root,List<Integer> list) {
        if (root != null) {
            list.add(root.val);
            if (root.left != null) {
                helper(root.left,list);
            }
            if (root.right != null) {
                helper(root.right,list);
            }
        }
    }
}
```

$\textcolor{SeaGreen}{中序遍历}$（In-order）：左-根-右

```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> list = new ArrayList<>();
        helper(root, list);
        return list;
    }
    public void helper(TreeNode root, List<Integer> list) {
        if (root != null) {
            if (root.left != null) {
                helper(root.left,list);
            }
            list.add(root.val);
            if (root.right != null) {
                helper(root.right,list);
            }
        }
    }
}
```

$\textcolor{SeaGreen}{后序遍历}$（Post-order）：左-右-根

```java
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> list = new ArrayList<>();
        helper(root, list);
        return list;
    }
    public void helper(TreeNode root,List<Integer> list) {
        if (root != null) {
            if (root.left != null) {
                helper(root.left,list);
            }
            if (root.right != null) {
                helper(root.right,list);
            }
            list.add(root.val);
        }
    }
}
```

### 二叉搜索树

又称二叉排序树、有序二叉树、排序二叉树。

==性质==：

1、左子树上的**所有结点**的值均小于它的根结点的值；

2、右子树上的**所有结点**的值均大于它的根结点的值；

3、以此类推：左、右子树也分别为二叉查找树。（重复性！！！）

$\textcolor{SeaGreen}{tips}$：二叉搜索树的中序遍历：升序排列

> 思考题：树的面试题解法一般都是递归，为什么？
>
> 树的数据结构的定义存在重复性，而递归适用于重复性的执行步骤。

------

## 堆和二叉堆、图

### 堆 Heap

Heap：可以迅速找到一堆数中的最大或最小值的数据结构。常见的堆有二叉堆(Binary)、斐波拉契堆。

大顶堆（大根堆）：根节点最大的堆。

常见操作（API）：

> find-max：       O(1)
>
> delete-max：   O(logN)
>
> insert(create)：O(logN) or O(1)

### 二叉堆

通过**完全二叉树**来实现。除了 find-max(find-min) 的时间复杂度为 O(1) ，其他操作均为 O(logN) 。

#### ==性质==（以大顶堆为例）：

1、是一颗完全二叉树；

2、树中任意节点的值总是 >= 其子节点的值。

#### 二叉堆的实现细节

1、二叉堆一般都通过“数组”实现；

2、位置关系：

> 0. 根节点（顶堆元素）是：a[0]；
> 1. 索引为 i 的左孩子的索引是 （2*i+1）；
> 2. 索引为 i 的右孩子的索引是 （2*i+2）；
> 3. 索引为 i 的父结点的索引是 floor((i-1)/2)。

3、Insert：先插入堆的尾部，再做 heapifyUp；

4、delete max：先将堆尾元素替换到顶部，再做 heapifyDown。

$\textcolor{SeaGreen}{tips}$：二叉堆是堆（优先队列 priority_queue）的一种常见且简单的实现，但并不是最优的实现。

### 图

#### 图的属性

Graph(V, E)

$\textcolor{SeaGreen}{V-vertex:点}$

> 1、度-入度和出度
>
> 2、点与点之间：连通与否

$\textcolor{SeaGreen}{E-edge:边}$

> 1、有向和无向（单行线）
>
> 2、权重（边长）

#### 图的表示和分类

表示方法：邻接矩阵、邻接表

分类：无向无权图、有向无权图、无向有权图、有向有权图

#### 常见算法

DFS - 递归写法

```java
static void dfs(Node node, HashSet<Node> set) {
        if (node == null) return;
        set.add(node);
        // process current node here
        for (Node next : node.nexts) {
            if (!set.contains(next)) dfs(next, set);
        }
    }
```

BFS

```java
static void bfs(Node node) {
        if (node == null)
            return;
        Queue<Node> que = new LinkedList<>();
        HashSet<Node> set = new HashSet<>(); //相当于记录是否访问过
        que.add(node);
        set.add(node);
        while (!que.isEmpty()) {
            Node cur = que.poll();
            //System.out.print(m.val+" ");
            //dosomething();
            for (Node next : cur.nexts) {
                if (!set.contains(next)) {
                    set.add(next);
                    que.add(next);
                }
            }
        }
    }
```



