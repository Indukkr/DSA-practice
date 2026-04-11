# Sort Colors (LeetCode 75)

## Problem
Given an array containing only `0`, `1`, and `2`:

- Sort the array **in-place**
- Do not use library sort
- Aim for **O(n)** time and **O(1)** space

---

# Approach 1: Brute Force (Sorting)

## Idea
Use any sorting algorithm / built-in sort.

## Complexity
- Time: `O(n log n)`
- Space: Depends on sorting algorithm

## Why Not Optimal?
- Ignores the fact that array contains only 3 distinct values
- Problem expects linear time solution

---

# Approach 2: Counting / Frequency Method

## Idea
1. Count number of `0s`, `1s`, and `2s`
2. Overwrite array:
   - Fill `0` count times
   - Then `1`
   - Then `2`

## Complexity
- Time: `O(n)`
- Space: `O(1)` (only 3 counters)

## Limitation
- Requires 2 passes through array

---

# Approach 3: Optimal — Dutch National Flag Algorithm

## Core Idea
Maintain 3 regions in array:

[0 ... low-1]     -> All 0s  
[low ... mid-1]   -> All 1s  
[mid ... high]    -> Unprocessed  
[high+1 ... n-1]  -> All 2s  

---

## Pointers Used

- `low`  -> Position where next `0` should go
- `mid`  -> Current element being processed
- `high` -> Position where next `2` should go

---

## Logic

### Case 1: nums[mid] == 0
- Swap `low` and `mid`
- Increment both `low` and `mid`

### Case 2: nums[mid] == 1
- Already in correct middle region
- Increment `mid`

### Case 3: nums[mid] == 2
- Swap `mid` and `high`
- Decrement `high`
- **Do NOT increment mid**

---

## Why Mid is NOT Incremented After Swapping with High?
Because the swapped element from `high` is unprocessed  
It can be `0`, `1`, or `2`  
So we must check it again.

---

## Complexity
- Time: `O(n)`
- Space: `O(1)`

---

# Pattern / Learning

This problem teaches:

- 3 Pointer Technique
- In-place Partitioning
- Dutch National Flag Pattern

---

# Similar Problems

- Move Zeroes
- Partition Array According to Pivot
- Segregate Even and Odd Numbers
- Quick Sort Partition Logic

---

# Follow Up Questions

1. What if array has `k` colors instead of 3?
2. Can this be solved stably?
3. What if modification of array is not allowed?
4. Why does Dutch National Flag work in one pass?

---

# Interview Tips

Always explain in this order:

1. Brute Force Sorting
2. Counting Approach
3. Dutch National Flag (Optimal)

Shows progression of thought process.
