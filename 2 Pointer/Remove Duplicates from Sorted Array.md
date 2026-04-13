# Remove Duplicates from Sorted Array (LeetCode 26)

## Problem
Given a sorted array:

- Remove duplicates in-place
- Each unique element should appear only once
- Return number of unique elements
- Relative order must be maintained

---

# Approach 1: Brute Force (Using Extra Array / Set)

## Idea
Store unique elements separately and copy back.

## Complexity
- Time: `O(n)`
- Space: `O(n)`

## Why Not Optimal?
Problem requires in-place modification with `O(1)` extra space.

---

# Approach 2: Optimal — Slow/Fast Pointer

## Key Observation
Array is sorted.

This means:
- Duplicate elements are adjacent
- We only need to compare current element with previous unique element

---

## Core Idea

Use two pointers:

- `slow` -> Tracks last unique element position
- `fast` -> Scans entire array

---

## Logic

### If nums[fast] == nums[slow]
Duplicate found  
→ Ignore it  
→ Move `fast`

---

### If nums[fast] != nums[slow]
New unique element found  

- Increment `slow`
- Place current unique value at `nums[slow]`

---

## Why This Works
Front portion of array always stores unique elements compactly.

At any moment:

`nums[0...slow]` contains all unique values found so far.

---

## Complexity
- Time: `O(n)`
- Space: `O(1)`

---

# Pattern / Learning

This problem teaches:

- Slow/Fast Pointer Technique
- In-place Array Compaction
- Handling Sorted Arrays Efficiently

---

# Similar Problems

- Move Zeroes
- Remove Element
- Sort Colors
- Merge Sorted Array

---

# Follow Up Questions

1. What if array is not sorted?
2. How to allow duplicates at most twice?
3. How to remove a specific value instead of duplicates?
4. Can this pattern be generalized for filtering arrays in-place?

---

# Interview Tip

Mention this key observation:

"Since array is sorted, duplicates are adjacent,  
so we can compact unique values in-place using slow/fast pointers."

That is the main insight interviewer wants.
