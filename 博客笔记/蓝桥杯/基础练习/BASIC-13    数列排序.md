---
date: 2018-01-12 09:53
status: public
title: 'BASIC-13    数列排序'
---

题目如下：
![](http://ove4nglsb.bkt.clouddn.com/%E6%95%B0%E5%88%97%E6%8E%92%E5%BA%8F.png)
代码如下：
```java
import java.util.Scanner;

public class SortTheColumns {

	public static void main(String[] args) {
		Scanner input = new Scanner(System.in);
		int n = input.nextInt();
		int[] num = new int[n];
		for(int i = 0;i<n;i++) {
			num[i] = input.nextInt();
		}
		// 冒泡排序只需要循环n-1次
		for(int i = 1;i<n;i++) {
			// 外层循环每次循环完之后已经将最大的数字排到数组的后面，所以只需要循环n-i次了
			for(int j = 0;j<n-i;j++) {
				if(num[j]>num[j+1]) {
					int temp = num[j];
					num[j] = num[j+1];
					num[j+1] = temp;
				}
			}
		}
		for(int i = 0;i<n;i++) {
			System.out.print(num[i]+" ");
		}
	}
}
```
好惭愧啊，都大三了，写个冒泡排序还这个吃力，再次遇到冒泡排序，总结一下。
冒泡排序总共分成两层，外层控制的循环的次数，且每次循环完之后会将最大的或者最小的那个数放到数组的最后面，内层循环控制的是每两个数进行比较，因为外层循环完之后找到了最大的或者最小的那个数之后，内层循环就不需要再去比较了，因此只需要比较n-i次就可以了。
再错打脸。