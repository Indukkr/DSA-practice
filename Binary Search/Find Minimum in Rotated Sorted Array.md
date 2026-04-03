# Find Minimum in Rotated Sorted Array

## Pattern
Binary Search (Modified)

---

## 🔍 Approach Thinking

### 1. Brute Force
- Traverse entire array and track minimum
- Time: O(n), Space: O(1)

---

### 2. Optimal Approach (Binary Search)

- Array is sorted but rotated
- Minimum element is the pivot point

---

## 🧠 Core Logic

At each step, compare:
- nums[mid] with nums[high]

### Case 1:
- nums[mid] > nums[high]
👉 Minimum lies in right half
👉 low = mid + 1

### Case 2:
- nums[mid] <= nums[high]
👉 Right half is sorted
👉 Minimum lies in left half (including mid)
👉 high = mid

---

## ⚡ Key Insight
- One half of the array is always sorted
- The unsorted half contains the minimum

---

## 🧠 Pattern Trigger
- Rotated sorted array
- Need minimum / pivot element

👉 Think:
Binary Search

---

## ⏱ Complexity
- Time: O(log n)
- Space: O(1)

---

## ⚠️ Edge Cases
- Array not rotated (already sorted)
- Single element
- Two elements

---

## 🔁 While Loop Condition (IMPORTANT)

### Rule:
- Return inside loop → use (low <= high)
- Return after loop → use (low < high)

---

### In this problem:
- We do NOT return inside loop
- We shrink search space to one index

👉 So use:
while (low < high)

---

## 🎯 Decision
- Use Binary Search to reduce time from O(n) → O(log n)
