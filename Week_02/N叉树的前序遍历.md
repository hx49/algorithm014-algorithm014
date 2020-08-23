**解法一：递归**

```java
class Solution {
    List<Integer> list = new ArrayList<>();
    public List<Integer> preorder(Node root) {
        helper(root);
        return list;
    }
    public void helper(Node root) {
        if (root != null) {
            list.add(root.val);
            for (int i  = 0 ; i < root.children.size() ; i ++) {
                helper(root.children.get(i));
            }
        }
    }
}
```

**解法二：迭代**

```java
class Solution {
    public List<Integer> preorder(Node root) {
        List<Integer> list = new ArrayList<>();
        if (root == null) return list;
        Stack<Node> stack = new Stack<>();
        stack.push(root);
        while (!stack.isEmpty()) {
            root = stack.pop();
            list.add(root.val);
            for (int i  = root.children.size() - 1 ; i >= 0 ; i --) {
                stack.push(root.children.get(i));
            }
        }
        return list;
    }
}
```

