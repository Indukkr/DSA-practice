# 🧗 Climbing Stairs (LeetCode)

## 📌 Problem
Given `n` stairs, you can climb:
- 1 step
- 2 steps

Return the number of distinct ways to reach the top.

---

## 💡 Intuition
To reach stair `i`, you can come from:
- `i-1` (1 step)
- `i-2` (2 steps)

So:

ways(i) = ways(i-1) + ways(i-2)

👉 This is a Fibonacci pattern.

---

## 🧠 Approach (Space Optimized DP)

Instead of using a DP array, we only keep track of:
- `prev` → ways to reach (i-1)
- `prevToPrev` → ways to reach (i-2)

---

## ✅ Code

```java
class Solution {
    public int climbStairs(int n) {

        if (n <= 1)
            return n;

        int curr = 0;
        int prev = 1;
        int prevToPrev = 1;

        for (int i = 2; i <= n; i++) {
            curr = prev + prevToPrev;
            prevToPrev = prev;
            prev = curr;
        }

        return curr;
    }
}
```

---

## 🔍 Dry Run (n = 5)

Initial:
prevToPrev = 1
prev = 1

i = 2 → curr = 2  
i = 3 → curr = 3  
i = 4 → curr = 5  
i = 5 → curr = 8  

Answer = 8

---

## ⏱️ Complexity

- Time: O(n)
- Space: O(1)

---

## 🎯 Pattern

- Fibonacci DP
- Only last 2 states required

---

## ⚠️ Edge Case

- n = 0 → 0
- n = 1 → 1

---

## 🔥 Key Takeaway

If:
- problem depends on last 2 states  
👉 use variables instead of DP array (space optimization)

---
