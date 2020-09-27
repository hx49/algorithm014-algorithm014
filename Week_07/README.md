## 字典树和并查集

### 字典树（Trie）的基本实现和特性

字典树，即 Trie 树，又称单词查找树或键树，是一种树形结构。典型应用是用于统计和排序大量的字符串（但不仅限于字符串），所以经常被搜索引擎系统用于文本词频统计。

它的优点是：最大限度地减少无谓的字符串比较，查询效率比哈希表高。

1、字典树的基本性质

（1）结点本身不存完整单词；

（2）从根结点到某一结点，路径上经过的字符连接起来，为该结点对应的字符串；

（3）每个结点的所有子结点路径代表的字符都不相同。

tip：结点中可以存储额外信息，例如：频次等。

2、字典树的核心思想

Trie 树的核心思想是空间换时间。

利用字符串的公共前缀来降低查询时间的开销以达到提高效率的目的。

3、字典树的数据结构![1](C:\Users\huang\Desktop\algorithm014\algorithm014-algorithm014-1\Week_07\README.assets\1.png)

```java
class Trie {
    private boolean isEnd;
    private Trie[] next;
    /** Initialize your data structure here. */
    public Trie() {
        isEnd = false;
        next = new Trie[26];
    }
    
    /** Inserts a word into the trie. */
    public void insert(String word) {
        if (word == null || word.length() == 0) return;
        Trie curr = this;
        char[] words = word.toCharArray();
        for (int i = 0;i < words.length;i++) {
            int n = words[i] - 'a';
            if (curr.next[n] == null) curr.next[n] = new Trie();
            curr = curr.next[n];
        }
        curr.isEnd = true;
    }
    
    /** Returns if the word is in the trie. */
    public boolean search(String word) {
        Trie node = searchPrefix(word);
        return node != null && node.isEnd;
    }
    
    /** Returns if there is any word in the trie that starts with the given prefix. */
    public boolean startsWith(String prefix) {
        Trie node = searchPrefix(prefix);
        return node != null;
    }

    private Trie searchPrefix(String word) {
        Trie node = this;
        char[] words = word.toCharArray();
        for (int i = 0;i < words.length;i++) {
            node = node.next[words[i] - 'a'];
            if (node == null) return null;
        }
        return node;
    }
}
```

------

### 并查集（Disjoint Set）的基本实现和特性

使用场景：组团、配对问题

在现实问题中，需要快速判断两个个体是否在同一个集合当中，或判断两个群组之间是不是一个群组以及快速地合并群组，就可以用到并查集。

1、并查集的基本操作

（1）makeSet(s)：建立一个新的并查集，其中包含 s 个单元素集合。

（2）unionSet(x,y)：把元素 x 和元素 y 所在的集合合并，要求 x 和 y 所在的集合不相交，如果相交则不合并。

（3）find(x)：找到元素 x 所在的集合的代表，该操作也可以用于判断两个元素是否位于同一个集合，只要将它们各自的代表比较一下即可。

2、并查集的 Java 实现

![image-20200926232026309](C:\Users\huang\Desktop\algorithm014\algorithm014-algorithm014-1\Week_07\README.assets\image-20200926232026309.png)

![2](C:\Users\huang\Desktop\algorithm014\algorithm014-algorithm014-1\Week_07\README.assets\2.png)

![image-20200926232343819](C:\Users\huang\Desktop\algorithm014\algorithm014-algorithm014-1\Week_07\README.assets\image-20200926232343819.png)

```java
class UnionFind { 
	private int count = 0; 
	private int[] parent; 
	public UnionFind(int n) { 
		count = n; 
		parent = new int[n]; 
		for (int i = 0; i < n; i++) { 
			parent[i] = i;
		}
	} 
	public int find(int p) { 
		while (p != parent[p]) { 
            // 进行路径压缩
			parent[p] = parent[parent[p]]; 
			p = parent[p]; 
		}
		return p; 
	}
	public void union(int p, int q) { 
		int rootP = find(p); 
		int rootQ = find(q); 
		if (rootP == rootQ) return; 
		parent[rootP] = rootQ; 
		count--;
	}
}
```



## 高级搜索

### 剪枝的实现和特性

在状态树进行搜索时，可以对以下两种情况进行剪枝：

1、已经处理过的分支，将这些分支暂存在缓存中，进而将整个分支剪掉，不需要再手动地进行计算；

2、比较差的分支或次优的分支。

**复习：回溯法**

回溯法采用试错的思想，它尝试分步的去解决一个问题。在分步解决问题的过程中，当它通过尝试发现现有的分步答案不能得到有效的正确的解答时，它将取消上一步甚至是上几步的计算，再通过其它的可能的分步解答再次尝试寻找问题的答案。

回溯法通常用最简单的递归方法来实现，在反复重复上述的步骤后可能出现两种情况：

- 找到一个可能存在的正确的答案
- 在尝试了所有可能的分步方法后宣告该问题没有答案

在最坏的情况下，回溯法会导致一次复杂度为指数时间的计算。

**实战题目：数独**

------

### 双向BFS的实现和特性

代码模板

------

### 启发式搜索的实现和特性

A*算法、优先级搜索



## 红黑树和AVL树