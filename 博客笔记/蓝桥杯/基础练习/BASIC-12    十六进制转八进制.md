---
date: 2018-01-12 10:07
status: public
title: 'BASIC-12    十六进制转八进制'
---

题目如下：
![](http://ove4nglsb.bkt.clouddn.com/%E5%8D%81%E8%BF%9B%E5%88%B6%E8%BD%AC%E5%8C%96%E4%B8%BA%E4%BA%8C%E8%BF%9B%E5%88%B6%E6%95%B0.png)
代码如下：
```java
package cn.lqb.grounding;

import java.util.Scanner;

public class HexToOctal {

	public static void main(String[] args) {
		Scanner input = new Scanner(System.in);
		int n = input.nextInt();
		String[] str = new String[n];
		for(int i = 0;i<n;i++) {
			str[i] = input.next();
		}
		input.close();
		for(int i=0;i<n;i++) {
			String strBinary = toBinary(str[i]);
			// 不满足三的倍数补全位数
			int len_strBin = strBinary.length();
			if(len_strBin%3 ==1) {
				strBinary = "00" + strBinary;
			}else if(len_strBin%3==2) {
				strBinary = "0" + strBinary;
			}
			String strOctal = toOctal(strBinary);
			System.out.println(strOctal);
		}
		/*Scanner input = new Scanner(System.in);
		int n = input.nextInt();
		String[] str = new String[n];
		for(int i=0;i<n;i++) {
			str[i] = input.next();
		}
		String[] binaryStr = new String[n];
		// 先将16进制转化为2进制
		for(int i=0;i<n;i++) {
			char[] c = str[i].toCharArray();
			StringBuilder strBuilder = new StringBuilder("");
			for(int j=0;j<c.length;j++) {
				switch(c[j]) {
				case '0':
					strBuilder.append("0000");
					break;
				case '1':
					strBuilder.append("0001");
					break;
				case '2':
					strBuilder.append("0010");
					break;
				case '3':
					strBuilder.append("0011");
					break;
				case '4':
					strBuilder.append("0100");
					break;
				case '5':
					strBuilder.append("0101");
					break;
				case '6':
					strBuilder.append("0110");
					break;
				case '7':
					strBuilder.append("0111");
					break;
				case '8':
					strBuilder.append("1000");
					break;
				case '9':
					strBuilder.append("1001");
					break;
				case 'A':
					strBuilder.append("1010");
					break;
				case 'B':
					strBuilder.append("1011");
					break;
				case 'C':
					strBuilder.append("1100");
					break;
				case 'D':
					strBuilder.append("1101");
					break;
				case 'E':
					strBuilder.append("1110");
					break;
				case 'F':
					strBuilder.append("1111");
					break;
				default:
					break;
				}
				binaryStr[i] = strBuilder.toString();
			}
		}
		
		// 判断长度是不是3的倍数
		for(int i = 0;i<n;i++) {
			if(binaryStr[i].length()%3==1) {
				binaryStr[i]="00"+binaryStr[i];
			}else if(binaryStr[i].length()%3==2){
				binaryStr[i]="0"+binaryStr[i];
			}
		}
		// 将2进制转化为8进制
		long[] octNum = new long[n];
		for(int i=0;i<n;i++) {
			// 将二进制数分成三个数一组的字符数组
			String[] octStr = new String[binaryStr[i].length()/3];
			// 拆分二进制数填入数组
			for(int j = 1;j<=binaryStr[i].length();j++) {
				if(j%3==0) {
					octStr[j/3-1] = binaryStr[i].substring(j-3, j);
				}
			}
			StringBuilder octBuilder = new StringBuilder();
			for(int k=0;k<octStr.length;k++) {
				if("000".equals(octStr[k])) {
					octBuilder.append("0");
				}else if("001".equals(octStr[k])){
					octBuilder.append("1");
				}else if("010".equals(octStr[k])){
					octBuilder.append("2");
				}else if("011".equals(octStr[k])){
					octBuilder.append("3");
				}else if("100".equals(octStr[k])){
					octBuilder.append("4");
				}else if("101".equals(octStr[k])){
					octBuilder.append("5");
				}else if("110".equals(octStr[k])){
					octBuilder.append("6");
				}else if("111".equals(octStr[k])){
					octBuilder.append("7");
				}
			}
			octNum[i]=Integer.parseInt(octBuilder.toString());
		}
		for(int i = 0;i<n;i++) {
			System.out.println(octNum[i]);
		}*/
	}
	
	public static String toBinary(String str) {
		int len_str = str.length();
		StringBuffer stb = new StringBuffer();
		for(int i=0;i<len_str;i++) {
			switch(str.charAt(i)) {
			case '0':
				stb.append("0000");
				break;
			case '1':
				stb.append("0001");
				break;
			case '2':
				stb.append("0010");
				break;
			case '3':
				stb.append("0011");
				break;
			case '4':
				stb.append("0100");
				break;
			case '5':
				stb.append("0101");
				break;
			case '6':
				stb.append("0110");
				break;
			case '7':
				stb.append("0111");
				break;
			case '8':
				stb.append("1000");
				break;
			case '9':
				stb.append("1001");
				break;
			case 'A':
				stb.append("1010");
				break;
			case 'B':
				stb.append("1011");
				break;
			case 'C':
				stb.append("1100");
				break;
			case 'D':
				stb.append("1101");
				break;
			case 'E':
				stb.append("1110");
				break;
			case 'F':
				stb.append("1111");
				break;
			}
		}
		return stb.toString();
	}
	public static String toOctal(String strBinary) {
		int len = strBinary.length();
		int k;
		StringBuffer stb = new StringBuffer();
		if(strBinary.substring(0, 3).equals("000")) {
			k = 3;
		}else {
			k = 0;
		}
		for(int i = k;i<len - 2;i+=3) {
			switch(strBinary.substring(i,i+3)) {
			case "000":
				stb.append("0");
				break;
			case "001":
				stb.append("1");
				break;
			case "010":
				stb.append("2");
				break;
			case "011":
				stb.append("3");
				break;
			case "100":
				stb.append("4");
				break;
			case "101":
				stb.append("5");
				break;
			case "110":
				stb.append("6");
				break;
			case "111":
				stb.append("7");
				break;
			}
			
		}
		return stb.toString();
	}
}
```
先来解释一下为什么16进制的1位数字等于二进制的4位。
因为16进制数的进率是16，二进制的进率是2，16是2的4次方，所以二进制数需要连续进位4次才能等效于16进制数进位1次。
所以同样的推理可以得到8进制的1位数字等于2进制的3位。
这个题的思路如下：
1. 先用数组存储输入的16进制数。
2. 将16进制数转化为2进制数。
3. 如果2进制数不满足3的倍数，少2位就补"00",少1位就补"0".
4. 将2进制数转化为8进制数。
5. 去除前导0，输出8进制数。
经验教训：
1. 16进制转化为2进制和2进制转化为8进制都用方法表示会更好。
2. 打开了输入流记得关闭输入流，因为输入流是jvm无法通过垃圾回收机制回收的资源，只能自己显示通过close回收。
3. java1.7的版本开始支持switch匹配字符串了，上课没听，哎，估计又打酱油去了。
4. String字符串的单个字符扫描不需要将字符串转化为字符数组，只需要使用循环调用charAt(i)进行扫描即可。