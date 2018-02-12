---
date: 2018-01-09 20:00
status: public
title: 'BASIC-11     十六进制转十进制'
---

题目如下：
![](http://ove4nglsb.bkt.clouddn.com/%E5%8D%81%E5%85%AD%E8%BF%9B%E5%88%B6%E8%BD%AC%E5%8C%96%E4%B8%BA%E5%8D%81%E8%BF%9B%E5%88%B6.png)
代码如下：
```java
import java.util.Scanner;

public class HexadecimalToDecimal {

	public static void main(String[] args) {
		Scanner input = new Scanner(System.in);
		String str = input.next();
		char[] c = str.toCharArray();
		int n = 0;
		long num = 0;
		while (n < c.length) {
			char d = c[n];
			switch (d) {
			case 'A':
				num += 10 * Math.pow(16, c.length - 1 - n);
				break;
			case 'B':
				num += 11 * Math.pow(16, c.length - 1 - n);
				break;
			case 'C':
				num += 12 * Math.pow(16, c.length - 1 - n);
				break;
			case 'D':
				num += 13 * Math.pow(16, c.length - 1 - n);
				break;
			case 'E':
				num += 14 * Math.pow(16, c.length - 1 - n);
				break;
			case 'F':
				num += 15 * Math.pow(16, c.length - 1 - n);
				break;
			default:
				String e = String.valueOf(d);
				int f = Integer.parseInt(e);
				num += f * Math.pow(16, c.length -1- n);
				break;
			}
			n++;
		}
		System.out.println(num);
	}
}
```
1. 首先要知道16进制如何转化为10进制，16进制的范围为[0,1,2,3,4,5,6,7,8,9,A,B,C,D,E,F]，16进制数n转换为十进制数m时，先要将n拆成一个个单个字符，每一个字符代表的数乘以16的（位数-1）次方，最后在相加得到十进制数。
2. 当16进制数为FFFFFFFF时，如果使用int型去存储这个十进制数会出现精度丢失，所以需要使用长整形long去存储。注：长整形long初始化为0，后面加不加L对结果没有影响。
