# Best Time to Buy and Sell Stock

## Pattern
Greedy / One Pass Optimization

---

## 🔍 Approach Thinking

### 1. Brute Force
- Try all pairs (buy day i, sell day j where j > i)
- Calculate profit:
  prices[j] - prices[i]
- Track maximum profit

- Time: O(n²)
- Space: O(1)

---

### 2. Optimal Approach (Greedy)

- Maintain:
  - minPrice → minimum price seen so far
  - maxProfit → maximum profit

- Traverse array:
  - Update minPrice
  - Calculate profit for current day
  - Update maxProfit

---

## 🧠 Core Logic

For each day:
- Treat it as selling day
- Profit = current price - minimum price so far

---

## ⚡ Key Insight

- Always buy at lowest price before current day
- Always try to sell at current price

👉 Maximize:
profit = prices[i] - minPrice

---

## 🧠 Pattern Trigger

- Single transaction
- Maximize difference (future - past)

👉 Think:
Greedy + Tracking minimum

---

## ⏱ Complexity

- Time: O(n)
- Space: O(1)

---

## ⚠️ Edge Cases

- Prices always decreasing → profit = 0
- Single element → profit = 0

---

## 🎯 Decision

- Use greedy approach to reduce O(n²) → O(n)
- Track minimum price and update profit dynamically
