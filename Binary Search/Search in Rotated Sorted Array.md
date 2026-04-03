# Search in Rotated Sorted Array

## Pattern
Binary Search (Modified)

---

## 🔍 Approach Thinking

### 1. Brute Force
- Traverse entire array and check for target
- Time: O(n), Space: O(1)

---

### 2. Optimal Approach (Binary Search)

- Array is sorted but rotated
- Cannot directly apply normal binary search
- At least one half of the array is always sorted

---

## 🧠 Core Logic

At each step:

1. Find mid
2. If nums[mid] == target → return index

---

### 🔹 Step 1: Identify sorted half

- If nums[low] <= nums[mid]
  👉 Left half is sorted

- Else
  👉 Right half is sorted

---

### 🔹 Step 2: Decide direction

#### If left half is sorted:
- Check:
  nums[low] <= target < nums[mid]

- YES → search left
- NO → search right

---

#### If right half is sorted:
- Check:
  nums[mid] < target <= nums[high]

- YES → search right
- NO → search left

---

## ⚡ Key Insight
- One half is always sorted
- Use sorted half to decide direction

---

## 🧠 Pattern Trigger
- Rotated sorted array
- Searching element

👉 Think:
Modified Binary Search

---

## ⏱ Complexity
- Time: O(log n)
- Space: O(1)

---

## ⚠️ Edge Cases
- Target not present → return -1
- Single element
- Array not rotated

---

## 🔁 While Loop Condition

- We check and return inside loop
👉 Use: while (low <= high)

---

## 🎯 Decision
- Use Binary Search to efficiently locate target in rotated array
