# 💰 Coin Change (LeetCode) — Unbounded Knapsack

## 📌 Problem
Given an array `coins[]` and an integer `amount`:

- Each coin can be used **infinite times**
- Return **minimum number of coins** needed to make the amount
- If not possible → return `-1`

---

## 🧠 Pattern Recognition

- Infinite supply → **Unbounded Knapsack**
- Minimize number of coins → **Min DP**
- Choice: pick / not pick

---

## 💡 DP Definition

dp[i][j] = minimum coins needed to form amount `j` using first `i` coins

---

## 🧱 Base Cases

- dp[i][0] = 0  
  → 0 coins needed to make amount 0

- dp[0][j] = INF  
  → impossible to make amount with 0 coins

```java
INF = Integer.MAX_VALUE - 1  // to avoid overflow
```

---

## 🔁 Transition

For each coin:

### ❌ If coin > amount:
```
dp[i][j] = dp[i-1][j]
```

### ✅ Else:

```
pick     = 1 + dp[i][j - coins[i-1]]   // same row → reuse coin
notPick  = dp[i-1][j]

dp[i][j] = min(pick, notPick)
```

---

## 🔥 Key Insight (IMPORTANT)

👉 We use `dp[i][...]` in pick (not `i-1`)

Reason:
- We can reuse same coin multiple times
- This makes it **unbounded knapsack**

---

## ✅ Code

```java
class Solution {
    public int coinChange(int[] coins, int amount) {

        int n = coins.length;
        int[][] dp = new int[n + 1][amount + 1];

        for (int i = 0; i <= n; i++) {
            dp[i][0] = 0;
        }

        for (int j = 0; j <= amount; j++) {
            dp[0][j] = Integer.MAX_VALUE - 1;
        }

        dp[0][0] = 0;

        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= amount; j++) {

                if (coins[i - 1] > j) {
                    dp[i][j] = dp[i - 1][j];
                } else {
                    int pick = dp[i][j - coins[i - 1]] + 1;
                    int notPick = dp[i - 1][j];
                    dp[i][j] = Math.min(pick, notPick);
                }
            }
        }

        return dp[n][amount] == Integer.MAX_VALUE - 1 ? -1 : dp[n][amount];
    }
}
```

---

## 🔍 Dry Run (coins = [1,2,5], amount = 5)

Possible ways:
- 5 → 1 coin ✅
- 2+2+1 → 3 coins
- 1+1+1+1+1 → 5 coins

👉 Answer = 1

---

## ⏱️ Complexity

- Time: O(n × amount)
- Space: O(n × amount)

---

## ⚠️ Common Mistakes

- ❌ Using `coins[i]` instead of `coins[i-1]`
- ❌ Using `Integer.MAX_VALUE` → overflow
- ❌ Using `dp[i-1]` in pick (wrong for unbounded)

---

## 🎯 Interview Explanation (One-liner)

> “This is an unbounded knapsack problem where we minimize the number of coins.  
We use DP where for each coin we either pick it (stay on same row) or skip it.”

---

## 🚀 Optimization (Follow-up)

Can be optimized to:
- 1D DP → O(amount) space

---

## 🔥 Final Takeaway

If:
- infinite supply + minimize/maximize  
👉 Think **Unbounded Knapsack**

---
