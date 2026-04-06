
## Pattern
Binary Search (Modified)

---

## 🔍 Approach Thinking

### 1. Brute Force
- Traverse array and check:
  nums[i] > nums[i-1] AND nums[i] > nums[i+1]
- Return index

- Time: O(n)
- Space: O(1)

---

### 2. Optimal Approach (Binary Search)

- Compare nums[mid] with nums[mid+1]

### Case 1:
- nums[mid] > nums[mid+1]
👉 Descending slope → peak lies on left (including mid)
👉 high = mid

### Case 2:
- nums[mid] < nums[mid+1]
👉 Ascending slope → peak lies on right
👉 low = mid + 1

---

## 🧠 Key Insight
- Always move towards the side where a peak must exist

---

## 🔁 While Loop Condition
- Return after loop → use (low < high)

---

## ⏱ Complexity
- Time: O(log n)
- Space: O(1)

---

## 🎯 Decision
- Use binary search to reduce O(n) → O(log n)

---
