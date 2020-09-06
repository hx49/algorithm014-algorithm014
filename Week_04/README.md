## 遍历类型

对于节点的访问顺序不同，分为：

深度优先：depth first search

广度优先：breadth first search

其余，优先级优先（启发式搜索）

------

### 深度优先搜索

DFS代码 - 递归写法

```java
public List<List<Integer>> levelOrder(TreeNode root) {
    List<List<Integer>> allResults = new ArrayList<>();
    if (root == null) {
        return allResults;
    }
    travel(root,0,allResults);
    return allResults;
}

private void travel(TreeNode root,int level,List<List<Integer>> results) {
    if (results.size() == level) {
        results.add(new ArrayList<>());
    }
    results.get(level).add(root.val);
    if(root.left != null) {
        travel(root.left,level+1,results);
    }
    if(root.right != null) {
        travel(root.right,level+1,results);
    }
}
```

DFS代码 - 非递归写法

```java
public List<List<Integer>> levelOrder(TreeNode root) {
    List<List<Integer>> allResults = new ArrayList<>();
    if (root == null) return allResults;
    Stack<TreeNode> nodes = new Stack<>();
    nodes.push(root);
    while(!nodes.isEmpty()) {
        TreeNode node = nodes.pop();
        List<Integer> results = new ArrayList<>();
        results.add(node.val);
        for (int i = node.children.size() - 1 ; i >= 0 ; -- i) {
            nodes.push(node.children.get(i));
        }
        allResults.add(results);
    }
    return allResults;
}
```

------

### 广度优先搜索

BFS代码

```java
public class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    
    TreeNode(int x) {
        val = x;
    }
}

public List<List<Integer>> levelOrder(TreeNode root) {
    List<List<Integer>> allResults = new ArrayList<>();
    if (root == null) {
        return allResults;
    }
    Queue<TreeNode> nodes = new LinkedList<>();
    nodes.add(root);
    while(!nodes.isEmpty()) {
        int size = node.size();
        List<Integer> results = new ArrayList<>();
        for (int i = 0 ; i < size ; i++) {
            TreeNode node = nodes.poll();
            results.add(node);
            if(node.left != null) {
                nodes.add(node.left);
            }
            if(node.right != null) {
                nodes.add(node.right);
            }
        }
        allResults.add(results);
    }
    return allResults;
}
```

------

### DFS和BFS的区别

1、BFS 适合用于搜索最短径路的解（如：求最少步数的解、最少交换次数的解），因为 BFS 搜索过程中遇到的解一定是离最初位置最近的，所以遇到一个解，一定就是最优解，此时搜索算法可以终止。而 DFS 只有全局搜索完毕后才能从所有的解中找出最优解。

2、DFS 适合搜索全部的解，因为要搜索全部的解，在记录路径的时候也会简单一点，而 BFS 搜索过程中，遇到离根最近的解，并没有什么用，也必须遍历完整棵搜索树。

3、DFS 是舍弃时间换取空间，BFS 是舍去空间换取时间。因为 DFS 要走很多的路径，可能都是没用的，（做有些题目的时候要进行剪枝，就是确定不符合条件的就可以推出，以免浪费时间，否则有些题目会TLE）；而 BFS 可以走的点要存起来，需要队列，因此需要空间来储存，但是快一点。

------

## 贪心算法 Greedy

贪心算法是一种在每一步选择中都采取在当前状态下最好或最优的解（即最有利）的选择，从而希望导致结果是全局最好或最优的算法。贪心算法可以解决一些最优化问题，常作为辅助算法。

贪心算法与动态规划不同在于它对每个子问题的解决方案都做出选择，不能回退。动态规划则会保存以前的运算结果，并根据以前的结果对当前进行选择，有回退功能。

------

## 二分查找

### 二分查找的前提

1、目标函数单调性（单调递增或递减）

2、存在上下界（bounded)

3、能够通过索引访问（index accessible)

### 代码模板

```java
public int binarySearch(int [] array, int target) {
    int left = 0, right = array.length - 1, mid;
    while (left <= right) {
        mid = (right - left) / 2 + left;
    
    	if (array[mid] == target) {
        	return mid;
    	}else if (array[mid] > target) {
        	right = mid - 1;
    	}else {
        	left = mid + 1;
    	}
	}
    return -1;
}
```

------

## 牛顿迭代法

https://www.beyond3d.com/content/articles/8/