---
date: 2018-01-12 17:36
status: public
title: 'ALGO-1	    区间k大数查询'
---

题目如下：
![](http://ove4nglsb.bkt.clouddn.com/%E5%8C%BA%E9%97%B4k%E6%95%B0.png)
代码如下：
```java
import java.util.Scanner;

public class IntervalKLargeQuery {

	public static void main(String[] args) {
		Scanner input = new Scanner(System.in);
		int n = input.nextInt();
		int[] num = new int[n];
		for(int i = 0;i<n;i++) {
			num[i] = input.nextInt();
		}
		int m = input.nextInt();
		int[] mint = new int[m];
		// 保存每行输入的三个数
		int a = 0;
		int b = 0;
		int c = 0;
		for(int i = 0;i<m;i++) {
			a = input.nextInt();
			b = input.nextInt();
			c = input.nextInt();
			mint[i] = search(a, b, c, num);
		}
		for(int i = 0;i<m;i++) {
			System.out.println(mint[i]);
		}
		input.close();
	}
	public static int search(int a,int b,int c,int[] num) {
		// 提取数组,长度正确
		int[] subNum = new int[b+1-a];
		// 赋值
		for(int i = 0;i<subNum.length;i++) {
			subNum[i] = num[a++-1];
		}
		for(int i = 1;i<subNum.length;i++) {
			for(int j = 0;j<subNum.length-i;j++) {
				if(subNum[j]<subNum[j+1]) {
					int temp = subNum[j];
					subNum[j] = subNum[j+1];
					subNum[j+1] = temp;
				}
			}
		}
		return subNum[c-1];
	}
}
```
这道题的思路就是将要求k大值的区间提取出来放到一个新的数组里面，中间赋值的时候要注意两边数组的开始下标不是一样的，另外要分清++i和i++。
经验教训：
1. 当代码量比较大的时候，最好使用方法去分步骤实现。这样比较容易找到自己的错误在哪。
2. ++i和i++要熟练分清。
3. 不要写出超过三层for循环的代码，即使能够实现功能，但是效率太慢。