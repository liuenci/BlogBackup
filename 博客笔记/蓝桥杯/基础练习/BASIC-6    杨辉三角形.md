---
date: 2018-01-08 17:26
status: public
title: 'BASIC-6    杨辉三角形'
---

题目如图：
![](http://ove4nglsb.bkt.clouddn.com/%E6%9D%A8%E8%BE%89%E4%B8%89%E8%A7%92%E5%BD%A2.png)
解题思路：
1. 找规律
   *  从输入和输出格式来看，输入数为n,则为n行n列的二维数组
   *  每一行的第一个数和最后一个数都是1.
   *  从第三行开始，除开第一个数和最后一个数，中间所有的数，假设该数的坐标为[i,j]，都等于[i-1,j-1]+[i-1,j]的和。
2. 写代码
```java
import java.util.Scanner;

public class Main {

	public static void main(String[] args) {
		Scanner input = new Scanner(System.in);
		int n = input.nextInt();
		int[][] array = new int[n][n];
		
		if(n==1) {
			System.out.println(1);
		}else if(n==2) {
			System.out.println(1);
			System.out.print(1+" "+1);
		}else {
			array[0][0] = 1;
			array[1][0] = 1;
			array[1][1] = 1;
			for(int i=2;i<n;i++) {
				for(int j=0;j<n;j++) {
					if(j==0||j==n) {
						array[i][j]=1;
					}else {
						array[i][j]=array[i-1][j-1]+array[i-1][j];
					}
				}
			}
			for(int i = 0;i<n;i++) {
				for(int j = 0;j<n;j++) {
					if(array[i][j]!=0) {
						System.out.print(array[i][j]+" ");
					}
				}
				System.out.println();
			}
		}
	}
}
```