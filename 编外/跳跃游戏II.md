# [跳跃游戏 II](https://leetcode.cn/problems/jump-game-ii/)

![image-20250417154123946](https://md-wind.oss-cn-nanjing.aliyuncs.com/md/20250417154124007.png)

## 算法原理

- **状态表示**

  定义`dp[i]`为以`i`位置为起点, 到达终点所需的最小跳跃次数

- **状态转移**

  对于`i`位置来说, 它可以依据`temp = nums[i]`, 向后最多跳`temp`个格子, 从它能向后跳到的格子中选一个最小的, 再加上从`i`位置跳到该位置的一次跳跃, 即`dp[i] = min(dp[i+j_k]) + 1`, 其中`j_k`表示可能得跳跃次数, 另外, 需要注意的是可能`nums[i]`等于0, 此时它就跳不了, 到达不了终点, 此时我们给个很大的值, 让它参与之后的比较, 但不被实际采纳

- **初始化**

  由于无论如何, 它自己都要跳一次, 所以我们把所有格初始化为一, 对于表示终点的格子来说, 再把它修改为0, 很明显, 在终点就不需要再跳了, 另外提防可能的越界情况, 为此, 可以在终点之后加一个虚拟位置, 引导其变成不可能的跳跃次数

- **填表顺序**

  从右往左

- **返回值**

  真正的起点是0下标, 直接返回`dp[0]`

## 代码编写

```cpp
class Solution {
    const int INF = 0x3f3f3f3f;
public:
    int jump(vector<int>& nums) {
        int n = nums.size();
        vector<int> dp(n+1, 1); 
        dp[n] = INF; dp[n-1] = 0;
        for(int i = n-2; i >= 0; --i)
        {
            int temp = nums[i], minjump = INF;
            for(int j = 1; j <= temp && i+j <= n; ++j) 
                minjump = min(minjump, dp[i+j]);
            dp[i] += minjump;
        }
        return dp[0];
    }
};
```

# 完