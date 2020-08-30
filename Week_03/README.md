## 递归 Recursion

### Java 递归代码模板

```java
public void recur (int level, int param) {
    
    // terminator
    if (level > MAX_LEVEL) {
        // process result
        return;
    }
    
    // process current logic
    process(level, param);
    
    // drill down
    recur(level:level + 1, newParam);
    
    // restore current status
}
```

### 思维要点

> 1、不要人肉进行递归（最大误区）
>
> 2、找到最近最简方法，将其拆解成可重复解决的问题（重复子问题）
>
> 3、数学归纳法思维

------

## 分治、回溯

### 分治代码模板

```java
private static int divide_conquer(Problem problem, int param) {
    // recursion terminator
    if (problem == NULL) {
        int res = process_last_result();
        return res;
    }
    
    //process current problem
    subProblems = split_problem(problem);
    
    res0 = divide_conquer(subProblems[0]);
    res1 = divide_conquer(subProblems[1]);
    
    // merge
    result = process_result(res0, res1);
    
    // revert thr current level status
    return result;
}
```

