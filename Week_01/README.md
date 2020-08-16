# 刷题tips #

### 1、五毒神掌 ###
> 1、5-10 分钟读题和思考，如果没有思路，看题解，默写代码
> 
> 2、马上自己写，提交LeetCode，多种解法，体会优化
> 
> 3、24 小时之后，再重复做题
> 
> 4、一周后重复做题
> 
> 5、面试前一周恢复性训练


### 2、切题四件套 ###
> 1、理清题意，确定题目的要求
> 
> 2、想尽可能多的解法，对比几种写法的时空复杂度，找到比较好的解
> 
> 3、尽可能多地动手写
> 
> 4、测试用例

### 3、练习技巧 ###
> 1、切忌死磕、切忌只刷一遍
> 
> 2、多看别人的题解
> 
> 3、寻找问题的重复性，从最简单的情况开始分析
>
> 4、练习打字速度、熟练使用所用IDEA的快捷键

# 代码模板 #
### 1、遍历数组 嵌套循环 ###
    class Solution{
		public int maxArea(int[] a) {
			int max = 0;
			for(int i = 0; i <  - 1; ++i) {
         		for(int j = i + 1; j < a.length; ++j) {
             		int area = (j - i) * Math.min(a[i], a[j]);
					max = Matn.max(max, area);
         		}
     		}
			return max;
		}
	}
### 2、左右夹逼 ###
    class Solution{
		public int maxArea(int[] a) {
			int max = 0;
			for(int i = 0, j = a.length - 1; i < j; ) {
         		int minHeight = a[i] < a[j] ? a[i ++] : a[j --];
				int area = (j - i + 1) * minHeight;
				max = Math.max(max, area);
     		}
			return max;
		}
	}

