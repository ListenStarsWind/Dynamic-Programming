# [分割回文串 IV](https://leetcode.cn/problems/palindrome-partitioning-iv)

![image-20250409124345537](https://md-wind.oss-cn-nanjing.aliyuncs.com/md/20250409124345651.png)

## 题目解析

给你一个字符串 `s` ，如果可以将它分割成三个 **非空** 回文子字符串，那么返回 `true` ，否则返回 `false` 。

当一个字符串正着读和反着读是一模一样的，就称其为 **回文字符串** 。

**示例一**

>```
>输入：s = "abcbdd"
>输出：true
>解释："abcbdd" = "a" + "bcb" + "dd"，三个子字符串都是回文的。
>```

`a`没有第二个, 所以只能自成一个回文子串, 接着是`bcb`和`dd`, 

**示例二**

>```
>输入：s = "bcbddxy"
>输出：false
>解释：s 没办法被分割成 3 个回文子字符串。
>```

`x,y`没有重复的, 所以只能自成一个子串, 于是就占了两个名额, 剩下的无法构成一个回文子串.

## 算法原理

先用动态规划统计出所有子串的状态, 然后暴力枚举出所有可能得划分方式, 只要一种方式成功, 那就成功

## 代码编写

```cpp
class Solution {
public:
    bool checkPartitioning(string s) {
        int n = s.size();
        vector<vector<bool>> dp(n, vector<bool>(n));
        for(int i = n-1; i >= 0; --i)
        {
            for(int j = i; j < n; ++j)
            {
                if(s[i] == s[j])
                    dp[i][j] = i + 1 < j ? dp[i+1][j-1] : true;
            }
        }
        for(int i = 1; i < n-1; ++i)
        {
            for(int j = i; j < n-1; ++j)
            {
                if(dp[0][i-1] && dp[i][j] && dp[j+1][n-1])
                    return true;
            }
        }
        return false;
    }
};
```

# 完