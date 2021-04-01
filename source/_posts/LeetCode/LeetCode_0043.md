---
title: LeetCode_43.字符串相乘
categories: LeetCode
date: 2021-04-01
tags: Java
---

> https://leetcode-cn.com/problems/multiply-strings/

## 描述

给定两个以字符串形式表示的非负整数 num1 和 num2，返回 num1 和 num2 的乘积，它们的乘积也表示为字符串形式。

`示例 1:`
```
输入: num1 = "2", num2 = "3"
输出: "6"
```
`示例 2:`
```
输入: num1 = "123", num2 = "456"
输出: "56088"
```
`提示：`
```
num1 和 num2 的长度小于110。
num1 和 num2 只包含数字 0-9。
num1 和 num2 均不以零开头，除非是数字 0 本身。
不能使用任何标准库的大数类型（比如 BigInteger）或直接将输入转换为整数来处理。
```

## 关键点
字符串相乘，需要按照两个字符串相加的思路来拆分问题；
![alt 字符串相乘](/images/LeetCode/multipy.png)


## 源码
``` java
public class Multiply {

    public static void main(String[] args) {
        System.out.println(multiply("2", "3"));
        System.out.println(multiply("123", "456"));
    }

    public static String multiply(String num1, String num2) {
        if (num1 == null || num2 == null || num1.equals("0") || num2.equals("0")) {
            return "0";
        }
        String maxStr = num1.length() >= num2.length() ? num1 : num2;
        String minStr = num1.length() < num2.length() ? num1 : num2;

        char[] chars = minStr.toCharArray();
        String answer = "0";
        for (int i = chars.length - 1; i >= 0; i--) {
            char alpha = chars[i];
            int value = strToInt(alpha);
            if (value == 0) {
                continue;
            }
            int loc = chars.length - i;
            StringBuilder tempMaxStr = new StringBuilder(multiplyWithInt(maxStr, value));
            while (loc-- > 1) {
                tempMaxStr.append("0");
            }
            answer = add(answer, tempMaxStr.toString());
        }
        return answer;
    }

    public static String multiplyWithInt(String str, int num) {
        StringBuilder answer = new StringBuilder();
        int add = 0;
        int index = str.length() - 1;
        while (index >= 0 || add != 0) {
            int strNum = index >= 0 ? strToInt(str.charAt(index)) : 0;
            int result = strNum * num + add;
            answer.append(result % 10);
            add = result / 10;
            index--;
        }
        return answer.reverse().toString();
    }

    public static String add(String num1, String num2) {
        StringBuilder ans = new StringBuilder();
        int add = 0;
        int index1 = num1.length() - 1;
        int index2 = num2.length() - 1;
        while (index1 >= 0 || index2 >= 0 || add != 0) {
            int a = index1 >= 0 ? strToInt(num1.charAt(index1)) : 0;
            int b = index2 >= 0 ? strToInt(num2.charAt(index2)) : 0;
            int result = a + b + add;
            ans.append(result % 10);
            add = result / 10;
            index1--;
            index2--;
        }
        return ans.reverse().toString();
    }

    public static int strToInt(Character alpha) {
        return alpha - '0';
    }
}
```