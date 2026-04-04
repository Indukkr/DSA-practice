# Container With Most Water

## Pattern
Two Pointers (Greedy)

---

## 🔍 Approach Thinking

### 1. Brute Force
- Consider all pairs (i, j)
- Calculate area using:
  min(height[i], height[j]) * (j - i)
- Track maximum area

- Time: O(n²)
- Space: O(1)

---

### 2. Optimal Approach (Two Pointers)

- Initialize:
  i = 0 (left)
  j = n - 1 (right)

- While i < j:
  - Calculate area:
    min(height[i], height[j]) * (j - i)
  - Update maxArea
  - Move pointer with smaller height

---

## 🧠 Core Logic

At any position:
- Area is limited by the smaller height
- Width decreases as pointers move inward

👉 To maximize area:
- Try to increase the smaller height

---

## ⚡ Pointer Movement Rule

- If height[i] < height[j]
  → i++

- Else
  → j--

---

## 🔥 Key Insight

- Moving taller pointer is useless:
  - Height remains limited by smaller one
  - Width decreases → area cannot improve

- Moving smaller pointer:
  - Chance to find taller height → area may increase

---

## 🧠 Pattern Trigger

- Two indices forming a range
- Need to maximize/minimize something
- Depends on both ends

👉 Think:
Two Pointers (Greedy decision)

---

## ⏱ Complexity

- Time: O(n)
- Space: O(1)

---

## ⚠️ Edge Cases

- Array size < 2 → return 0
- All heights same
- Strictly increasing / decreasing heights

---

## 🎯 Decision

- Use Two Pointers to reduce complexity from O(n²) → O(n)
- Always move the pointer with smaller height
