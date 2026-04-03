# Maximum Product Subarray

## Pattern
Dynamic Programming (Kadane’s Variation)

---

## 🔍 Approach Thinking

### 1. Brute Force
- Consider all subarrays using two loops
- Compute product of each subarray and track maximum
- Time: O(n²), Space: O(1)

- Not efficient due to repeated calculations

---

### 2. Optimal Approach (DP / Kadane Variation)

- At each index, maintain:
  - max product ending here
  - min product ending here

- Why min?
  - Negative × negative → positive (can become max)

---

## 🧠 Core Logic

At index `i`, consider 3 choices:
- nums[i] (start new subarray)
- nums[i] * prevMax
- nums[i] * prevMin

👉 Then:
- currMax = max of above 3
- currMin = min of above 3

Update:
- prevMax = currMax
- prevMin = currMin
- ans = max(ans, currMax)

---

## ⚡ Key Insight
- Minimum product is important because it can turn into maximum when multiplied by a negative number

---

## 🧠 Pattern Trigger
- "Subarray"
- "Product"
- "Negative numbers involved"

👉 Think:
Track both max and min

---

## ⏱ Complexity
- Time: O(n)
- Space: O(1)

---

## ⚠️ Edge Cases
- Contains zero
- All negative numbers
- Single element

---

## 🎯 Decision
- Use DP approach to handle negative sign flips and maximize product efficiently
