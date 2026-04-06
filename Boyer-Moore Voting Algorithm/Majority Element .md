## Pattern
Boyer-Moore Voting Algorithm

---

## 🔍 Approach Thinking

### 1. Brute Force
- Count frequency of each element
- Return element with count > n/2

- Time: O(n²)
- Space: O(1)

---

### 2. Better Approach
- Use HashMap to store frequency

- Time: O(n)
- Space: O(n)

---

### 3. Optimal Approach (Boyer-Moore)

- Maintain:
  count, candidate

- If count == 0:
  → choose new candidate

- If nums[i] == candidate:
  → count++

- Else:
  → count--

---

## 🧠 Key Insight
- Majority element cancels out all other elements

---

## ⚡ Important Point
- Initial value of candidate doesn’t matter

---

## ⏱ Complexity
- Time: O(n)
- Space: O(1)

---

## 🎯 Decision
- Use Boyer-Moore for optimal solution

---
