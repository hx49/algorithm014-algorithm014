## 字符串基础知识

**定义**

- Python：

  x = 'abbc'

  x = "abbc"

- Java：

  String x = "abbc";

- C++：

  string x("abbc");

> Python 和 Java 的 String 是 immutable 的，即不可变的，**线程安全**。当改变 String 中的内容时，其实是创建了一个新的 String。
>
> C++ 的 String 是可变的。



**遍历字符串**

```java
String x = "abbc";
for (int i = 0 ; i < x.size() ; ++ i) {
    char ch = x.charAt(i);
}
for ch in x.toCharArray() {
    System.out.println(ch);
}
```



**字符串比较**

String x = new String("abb");

String y = new String("abb");

 x == y ---> false （比较指针/地址）

x.equals(y) ---> true（比较内容）

x.equalsIgnoreCase(y) ---> true（比较内容，可忽略大小写）



