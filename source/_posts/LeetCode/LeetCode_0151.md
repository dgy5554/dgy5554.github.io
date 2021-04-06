---
title: LeetCode_151.翻转字符串里的单词
categories: LeetCode
date: 2021-04-06
tags: Java
---

> https://leetcode-cn.com/problems/reverse-words-in-a-string/

## 描述
给定两个字符串 s1 和 s2，写一个函数来判断 s2 是否包含 s1 的排列。

换句话说，第一个字符串的排列之一是第二个字符串的 子串 。

`示例 1:`
```
输入："the sky is blue"
输出："blue is sky the"
```
`示例 2:`
```
输入："  hello world!  "
输出："world! hello"
解释：输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。
```
`示例 3:`
```
输入："a good   example"
输出："example good a"
解释：如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。
```
`示例 4:`
```
输入：s = "  Bob    Loves  Alice   "
输出："Alice Loves Bob"
```
`示例 5:`
```
输入：s = "Alice does not even like bob"
输出："bob like even not does Alice"
```
`提示：`
```
1 <= s.length <= 104
s 包含英文大小写字母、数字和空格 ' '
s 中 至少存在一个 单词
```

## 关键点

1、直接利用Java Api完成；
![alt 翻转字符串](/images/LeetCode/ReverseWhole.png)
``` java 
List<String> words = Arrays.asList(s.trim().split("\\s+"));
Collections.reverse(words);
return String.join(" ", words)
```
2、自己实现Split，Reverse和Join的过程；
``` java
// 1、去掉多余的空格
// 2、翻转整个字符串
// 3、翻转每个单词；
```

## 源码
``` java
public class ReverseWords {

    public static void main(String[] args) {
        System.out.println(reverseWords2("the sky is blue"));
        System.out.println(reverseWords2("  hello world!  "));
        System.out.println(reverseWords2("a good   example"));
        System.out.println(reverseWords2("  Bob    Loves  Alice   "));
        System.out.println(reverseWords2("Alice does not even like bob"));
    }

    // Java原生Api
    public static String reverseWords(String s) {
        List<String> words = Arrays.asList(s.trim().split("\\s+"));
        Collections.reverse(words);
        return String.join(" ", words);
    }

    // 1、去掉多余的空格
    // 2、翻转整个字符串
    // 3、翻转每个单词
    public static StringBuilder reverseWords2(String s) {
        StringBuilder sb = removeBlank(s);
        reverseEachWord(sb, 0, sb.length() - 1);
        reverseWords(sb);
        return sb;
    }

    public static StringBuilder removeBlank(String s) {
        int left = 0, right = s.length() - 1;
        // 去掉字符串开头的空白字符
        while (left <= right && s.charAt(left) == ' ') {
            left++;
        }
        // 去掉字符串末尾的空白字符
        while (left <= right && s.charAt(right) == ' ') {
            right--;
        }
        // 将字符串间多余的空白字符去除
        StringBuilder sb = new StringBuilder();
        while (left <= right) {
            char alpha = s.charAt(left);
            if (alpha != ' ') {
                sb.append(alpha);
            } else if (sb.charAt(sb.length() - 1) != ' ') {
                sb.append(alpha);
            }
            left++;
        }
        return sb;
    }

    public static void reverseWords(StringBuilder s) {
        int start = 0, end = 0, len = s.length();
        while (start < len) {
            while (end < len && s.charAt(end) != ' ') {
                end++;
            }
            reverseEachWord(s, start, end - 1);
            start = end + 1;
            end++;
        }
    }

    public static void reverseEachWord(StringBuilder word, int start, int end) {
        while (start < end) {
            char tmp = word.charAt(start);
            word.setCharAt(start++, word.charAt(end));
            word.setCharAt(end--, tmp);
        }
    }
}
```