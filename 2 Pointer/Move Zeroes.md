## Pattern
Two Pointers

---

## 🔍 Approach Thinking

### 1. Brute Force
- Create a new array
- Copy all non-zero elements
- Fill remaining with zeros

- Time: O(n)
- Space: O(n)

---

### 2. Optimal Approach (In-place Two Pointers)

- Maintain pointer `j` for position of next non-zero

- Traverse array:
  - If nums[i] != 0:
    - swap nums[i] with nums[j]
    - increment j

---

## 🧠 Core Logic
- Move all non-zero elements forward
- Push zeros to the end

---

## ⚡ Key Insight
- Maintain relative order of non-zero elements
- Perform in-place swaps

---

## 🧠 Pattern Trigger
- Rearranging elements
- Move specific values to end/start

👉 Think:
Two Pointers

---

## ⏱ Complexity
- Time: O(n)
- Space: O(1)

---

## ⚠️ Edge Cases
- All zeros
- No zeros
- Single element

---

## 🎯 Decision
- Use two pointers for optimal in-place solution
