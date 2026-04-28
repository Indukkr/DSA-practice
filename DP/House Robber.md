# 🏠 House Robber (LeetCode)

## 📌 Problem
Given an array `nums[]` where:
- nums[i] = money in ith house

👉 Cannot rob adjacent houses  
👉 Return **maximum money** you can rob

---

## 🧠 Intuition

At each house, you have 2 choices:

- Rob current house → skip previous
- Skip current house → take previous

---

## 💡 Recurrence

```
dp[i] = max(
    dp[i-2] + nums[i],   // pick
    dp[i-1]              // not pick
)
```

---

## 🧱 Base Cases

```
dp[0] = nums[0]

dp[1] = max(nums[0], nums[1])
```

---

## 🔁 Transition

For each index:

- pick → current + dp[i-2]
- notPick → dp[i-1]

👉 take max

---

## 🔧 Code

```java
class Solution {
    public int rob(int[] nums) {
        
        if (nums.length == 1)
            return nums[0];
            
        int[] dp = new int[nums.length];

        dp[0] = nums[0];
        dp[1] = Math.max(dp[0], nums[1]);

        for (int i = 2; i < nums.length; i++) {
            dp[i] = Math.max(dp[i-2] + nums[i], dp[i-1]);
        }

        return dp[nums.length - 1];
    }
}
```

---

## 🔍 Dry Run

nums = [2, 7, 9, 3, 1]

```
dp[0] = 2
dp[1] = 7
dp[2] = max(2+9, 7) = 11
dp[3] = max(7+3, 11) = 11
dp[4] = max(11+1, 11) = 12
```

👉 Answer = 12

---

## ⏱️ Complexity

- Time: O(n)
- Space: O(n)

---

## 🚀 Optimization (Important)

Can reduce space to O(1):

- only need last 2 values

---

## ⚠️ Edge Cases

- Single house → return nums[0]
- Two houses → return max of both

---

## 🔥 Pattern Recognition

- DP with choices (take / skip)
- Similar to:
  - Climbing Stairs (but max instead of sum)
  - Fibonacci variation

---

## 🎯 Interview Explanation

> “At each house, I decide whether to rob it or skip it. If I rob it, I add its value to dp[i-2]; otherwise I take dp[i-1]. This ensures no adjacent houses are robbed.”

---

## 🔗 Pattern Mapping

| Problem | Pattern |
|--------|--------|
| Climbing Stairs | Sum of ways |
| House Robber | Max value |
| Coin Change | Min / Count |

---

## 🔥 Final Takeaway

If:
- adjacent elements restriction + maximize value  
👉 think **take / skip DP**

---
