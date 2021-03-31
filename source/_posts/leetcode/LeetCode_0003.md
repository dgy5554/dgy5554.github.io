---
title: LeetCode_03.无重复字符的最长子串
categories: LeetCode
tags: Java
---

> https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/

## 描述

给定一个字符串，请你找出其中不含有重复字符的 最长子串 的长度。

`示例 1:`
```
输入: s = "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
```
`示例 2:`
```
输入: s = "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
```
`示例 3:`
```
输入: s = "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
```
`示例 4:`
```
输入: s = ""
输出: 0
```

`提示：`
```
0 <= s.length <= 5 * 104
s 由英文字母、数字、符号和空格组成
```

## 关键点
1、重复的字符，选择最近的位置；
``` java
Math.max(charLastLocMap.get(alpha) + 1, start);
```
2、字符串长度比较，选择最大的值；
``` java
Math.max(max, end - start + 1);
```


## 源码
``` java
public class LengthOfLongestSubstring {

    public static void main(String[] args) {
        System.out.println(lengthOfLongestSubstring("abcabcbb"));
        System.out.println(lengthOfLongestSubstring("bbbbb"));
        System.out.println(lengthOfLongestSubstring("pwwkew"));
        System.out.println(lengthOfLongestSubstring(""));
    }
    
    public static int lengthOfLongestSubstring(String s) {
        if (s == null || s.length() == 0) {
            return 0;
        }
        Map<Character, Integer> charLastLocMap = new HashMap<>();
        int max = 0;
        for (int start = 0, end = 0; end < s.length(); end++) {
            char alpha = s.charAt(end);
            if (charLastLocMap.containsKey(alpha)) {
                start = Math.max(charLastLocMap.get(alpha) + 1, start);
            }
            //输出字符串
            if (end - start + 1 > 0 && end - start + 1 > max) {
                System.out.println(s.substring(start, end + 1));
            }
            max = Math.max(max, end - start + 1);
            charLastLocMap.put(alpha, end);
        }
        return max;
    }
}
```