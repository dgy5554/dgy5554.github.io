---
title: LeetCode_567.字符串的排列
categories: LeetCode
tags: Java
---

> https://leetcode-cn.com/problems/permutation-in-string/

## 描述
给定两个字符串 s1 和 s2，写一个函数来判断 s2 是否包含 s1 的排列。

换句话说，第一个字符串的排列之一是第二个字符串的 子串 。

`示例 1:`
```
输入: s1 = "ab" s2 = "eidbaooo"
输出: True
解释: s2 包含 s1 的排列之一 ("ba").
```
`示例 2:`
```
输入: s1= "ab" s2 = "eidboaoo"
输出: False
```
`提示：`
```
输入的字符串只包含小写字母
两个字符串的长度都在 [1, 10,000] 之间
```

## 关键点
1、子串中的字符种类和个数，对应着父串一个窗口内的子串；
``` java 
pFreq == winFreq && pCount == winCount
```
2、右指针移动后找到满足条件的右边界，左指针移动后不断缩小边界；


## 源码
``` java
public class CheckInclusion {

    public static void main(String[] args) {
        System.out.println(checkInclusion("ab", "eidbaooo"));
        System.out.println(checkInclusion("ab", "eidboaoo"));
    }
    
    public static boolean checkInclusion(String s1, String s2) {
        char[] pattern = s1.toCharArray();
        char[] text = s2.toCharArray();
        int[] pFreq = new int[26];
        int[] winFreq = new int[26];
        for (int i = 0; i < s1.length(); i++) {
            pFreq[pattern[i] - 'a']++;
        }
        int pCount = 0;
        for (int i = 0; i < pFreq.length; i++) {
            if (pFreq[i] > 0) {
                pCount++;
            }
        }
        int right = 0, left = 0;
        // 当滑动窗口中的某个字符个数与s1中对应相等的时候才计数
        int winCount = 0;
        while (right < s2.length()) {
            if (pFreq[text[right] - 'a'] > 0) {
                winFreq[text[right] - 'a']++;
                if (winFreq[text[right] - 'a'] == pFreq[text[right] - 'a']) {
                    winCount++;
                }
            }
            right++;
            while (pCount == winCount) {
                if (right - left == s1.length()) {
                    System.out.println(s2.substring(left, right));
                    return true;
                }
                if (pFreq[text[left] - 'a'] > 0) {
                    winFreq[text[left] - 'a']--;
                    if (winFreq[text[left] - 'a'] < pFreq[text[left] - 'a']) {
                        winCount--;
                    }
                }
                left++;
            }
        }
        return false;
    }
}
```