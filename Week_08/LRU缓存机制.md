方法一：使用Java自带的数据结构 - 哈希链表LinkedHashMap

```java
class LRUCache {
    int cap;
    LinkedHashMap<Integer, Integer> cache = new LinkedHashMap<>();
    
    public LRUCache(int capacity) {
        this.cap = capacity;
    }
    
    public int get(int key) {
        if (!cache.containsKey(key)) return -1;
        makeRecently(key);
        return cache.get(key);
    }
    
    public void put(int key, int value) {
        if (cache.containsKey(key)) {
            cache.put(key, value);
            makeRecently(key);
            return;
        }
        else {
            if (cap == cache.size()) {
                int oldestKey = cache.keySet().iterator().next();
                cache.remove(oldestKey);
            }
            cache.put(key, value);
        }
    }

    private void makeRecently(int key) {
        int val = cache.get(key);
        cache.remove(key);
        cache.put(key, val);
    }
}
```



方法二：哈希表 + 双向链表

```java
class Node {
    public int key, val;
    public Node next, prev;
    public Node(int key, int val) {
        this.key = key;
        this.val = val;
    }
}

class DoubleList {
    private Node head, tail;
    private int size;
    // 初始化双向链表的数据
    public DoubleList() {
        head = new Node(0, 0);
        tail = new Node(0, 0);
        head.next = tail;
        tail.prev = head;
        size = 0;
    }
    // 在链表尾部添加节点 x
    public void addLast(Node x) {
        x.prev = tail.prev;
        x.next = tail;
        tail.prev.next = x;
        tail.prev = x;
        size ++;
    }
    // 删除链表中的 x 节点(x 一定存在)
    public void remove(Node x) {
        x.prev.next = x.next;
        x.next.prev = x.prev;
        size --;
    }
    // 删除链表中的第一个节点，并返回该节点
    public Node removeFirst() {
        if (head.next == tail) return null;
        Node first = head.next;
        remove(first);
        return first;
    }
    // 返回链表长度
    public int size() {return size;}
}

class LRUCache {
    private HashMap<Integer, Node> map;
    private DoubleList cache;
    private int cap;

    public LRUCache(int capacity) {
        map = new HashMap<>();
        cache = new DoubleList();
        this.cap = capacity;
    }
    
    public int get(int key) {
        if (!map.containsKey(key)) return -1;
        int val = map.get(key).val;
        put(key, val);
        return val;
    }
    
    public void put(int key, int value) {
        Node x = new Node(key, value);
        if (map.containsKey(key)) {
            cache.remove(map.get(key));
            cache.addLast(x);
            map.put(key, x);
        }
        else {
            if (cap == cache.size()) {
                Node first = cache.removeFirst();
                map.remove(first.key);
            }
            cache.addLast(x);
            map.put(key, x);
        }
    }
}
```

优化：增加几个函数，避免 map 和 put 直接操作 map 和 cache 的细节，以免漏掉某些操作，例如：删除时忘记维护哈希表 map 等。

```java
class Node {
    public int key, val;
    public Node next, prev;
    public Node(int key, int val) {
        this.key = key;
        this.val = val;
    }
}

class DoubleList {
    private Node head, tail;
    private int size;
    // 初始化双向链表的数据
    public DoubleList() {
        head = new Node(0, 0);
        tail = new Node(0, 0);
        head.next = tail;
        tail.prev = head;
        size = 0;
    }
    // 在链表尾部添加节点 x
    public void addLast(Node x) {
        x.prev = tail.prev;
        x.next = tail;
        tail.prev.next = x;
        tail.prev = x;
        size ++;
    }
    // 删除链表中的 x 节点(x 一定存在)
    public void remove(Node x) {
        x.prev.next = x.next;
        x.next.prev = x.prev;
        size --;
    }
    // 删除链表中的第一个节点，并返回该节点
    public Node removeFirst() {
        if (head.next == tail) return null;
        Node first = head.next;
        remove(first);
        return first;
    }
    // 返回链表长度
    public int size() {return size;}
}

class LRUCache {
    private HashMap<Integer, Node> map;
    private DoubleList cache;
    private int cap;

    public LRUCache(int capacity) {
        map = new HashMap<>();
        cache = new DoubleList();
        this.cap = capacity;
    }
    
    // 将某个 key 提升为最近使用的
    private void makeRecently(int key) {
        Node x = map.get(key);
        cache.remove(x);
        cache.addLast(x);
    }

    // 添加最近使用的元素
    private void addRecently(int key, int val) {
        Node x = new Node(key, val);
        cache.addLast(x);
        map.put(key, x);
    }

    // 删除某一个 key
    private void deleteKey(int key) {
        Node x = map.get(key);
        cache.remove(x);
        map.remove(key);
    }

    // 删除最久未使用的元素
    private void removeLeastRecently() {
        Node deleteNode = cache.removeFirst();
        int deleteKey = deleteNode.key;
        map.remove(deleteKey);
    }

    public int get(int key) {
        if (!map.containsKey(key)) return -1;
        int val = map.get(key).val;
        makeRecently(key);
        return val;
    }
    
    public void put(int key, int value) {
        if (map.containsKey(key)) {
            deleteKey(key);
            addRecently(key, value);
            // return;
        }
        else {
            if (cap == cache.size()) {
                removeLeastRecently();
            }
            addRecently(key, value);
        }
    }
}
```

