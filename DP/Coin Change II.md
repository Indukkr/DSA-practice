# 💰 Coin Change II (LeetCode) — Count Ways (Unbounded Knapsack)

## 📌 Problem
Given:
- `coins[]` (infinite supply)
- `amount`

👉 Return **number of ways** to make the amount  
👉 Order does NOT matter (combinations, not permutations)

---

## 🧠 Pattern Recognition

- Infinite supply → **Unbounded Knapsack**
- Count total ways → **Combination DP**

---

## 🔗 Relation with Coin Change I

| Problem | Goal | Operation |
|--------|------|----------|
| Coin Change I | Minimum coins | `min()` |
| Coin Change II | Count ways | `+` |

👉 **Same structure, only transition changes**

---

## 💡 DP Definition

```
dp[i][j] = number of ways to make amount j using first i coins
```

---

## 🧱 Base Cases

```
dp[i][0] = 1  
→ One way to make amount 0 (choose nothing)

dp[0][j] = 0  
→ No way to make amount with 0 coins
```

---

## 🔁 Transition

### If coin can be used:

```
pick     = dp[i][j - coins[i-1]]   // stay on same row (reuse coin)
notPick  = dp[i-1][j]

dp[i][j] = pick + notPick
```

---

### If coin cannot be used:

```
dp[i][j] = dp[i-1][j]
```

---

## 🔥 Key Insight (IMPORTANT)

👉 We use `dp[i][...]` in pick (not `i-1`)

Reason:
- Same coin can be reused
- This makes it **Unbounded Knapsack**

---

## ✅ Code

```java
class Solution {
    public int change(int amount, int[] coins) {

        int n = coins.length;
        int[][] dp = new int[n + 1][amount + 1];

        for (int j = 0; j <= amount; j++) {
            dp[0][j] = 0;
        }

        for (int i = 0; i <= n; i++) {
            dp[i][0] = 1;
        }

        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= amount; j++) {

                if (coins[i - 1] <= j) {
                    int pick = dp[i][j - coins[i - 1]];
                    int notPick = dp[i - 1][j];
                    dp[i][j] = pick + notPick;
                } else {
                    dp[i][j] = dp[i - 1][j];
                }
            }
        }

        return dp[n][amount];
    }
}
```

---

## 🔍 Dry Run

coins = [1,2,5], amount = 5

Ways:
- 5
- 2+2+1
- 1+1+1+1+1
- 2+1+1+1

👉 Total = **4 ways**

---

## ⏱️ Complexity

- Time: O(n × amount)
- Space: O(n × amount)

---

## ⚠️ Common Mistakes

- ❌ Using `dp[i-1]` in pick (breaks unbounded logic)
- ❌ Thinking order matters (this is combination problem)
- ❌ Confusing with Coin Change I

---

## 🎯 Interview Explanation (Best Answer)

> “This is an unbounded knapsack problem where instead of minimizing coins, we count total combinations.  
For each coin, we either pick it (stay on same row to reuse it) or skip it.”

---

## 🔥 Coin Change I vs II (Quick Revision)

| Feature | Coin Change I | Coin Change II |
|--------|--------------|----------------|
| Goal | Minimum coins | Count ways |
| Transition | `min(pick, notPick)` | `pick + notPick` |
| Return | min value | total count |

---

## 🚀 Optimization

Can be optimized to:
- 1D DP → O(amount) space

---

## 🔥 Final Takeaway

If:
- infinite supply + count ways  
👉 use **Unbounded Knapsack with addition**

---
