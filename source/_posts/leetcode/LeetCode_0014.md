---
title: LeetCode_14.最长公共前缀
categories: LeetCode
tags: Java
---

> https://leetcode-cn.com/problems/longest-common-prefix/

## 描述
编写一个函数来查找字符串数组中的最长公共前缀。
如果不存在公共前缀，返回空字符串 ""。

`示例 1:`
```
输入：strs = ["flower","flow","flight"]
输出："fl"
```
`示例 2:`
```
输入：strs = ["dog","racecar","car"]
输出：""
解释：输入不存在公共前缀。
```
`提示：`
```
0 <= strs.length <= 200
0 <= strs[i].length <= 200
strs[i] 仅由小写英文字母组成
```

## 关键点
1、在于对比两个字符串的最大前缀，是最后结果的子集；
2、根据当前的前缀，依次遍历全部字符串，去做对比；


## 源码
``` java
public class LongestCommonPrefix {

    public static void main(String[] args) {
        System.out.println(longestCommonPrefix(new String[]{"flower", "flower", "flower", "flower"}));
        System.out.println(longestCommonPrefix(new String[]{"flower", "flow", "flight"}));
        System.out.println(longestCommonPrefix(new String[]{"dog", "racecar", "car"}));
        System.out.println(longestCommonPrefix(new String[]{"a"}));
        System.out.println(longestCommonPrefix(new String[]{"ab", "a"}));
    }

    public static String longestCommonPrefix(String[] strs) {
        if (strs == null || strs.length == 0) {
            return "";
        }
        int length = strs.length;
        String prefix = strs[0];
        for (int i = 1; i < length; i++) {
            prefix = longestCommonPrefix(prefix, strs[i]);
            if (prefix.length() == 0) {
                break;
            }
        }
        return prefix;
    }

    public static String longestCommonPrefix(String str1, String str2) {
        int length = Math.min(str1.length(), str2.length());
        int index = 0;
        while (index < length && str1.charAt(index) == str2.charAt(index)) {
            index++;
        }
        return str1.substring(0, index);
    }
}
```