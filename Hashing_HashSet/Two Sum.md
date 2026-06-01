# Two Sum (LeetCode 1)

## Problem
Given an integer array `nums` and an integer `target`:

- Return indices of the two numbers such that they add up to `target`
- Exactly one valid solution exists
- Cannot use the same element twice

---

# Approach 1: Brute Force

## Idea

Check every possible pair.

For each element:

- Compare with every element after it
- If sum equals target, return indices

---

## Logic

For every `i`:

Check all `j > i`

If:

`nums[i] + nums[j] == target`

Return `[i, j]`

---

## Complexity

- Time: `O(n²)`
- Space: `O(1)`

---

## Why Not Optimal?

Many unnecessary comparisons.

As input size grows, performance degrades significantly.

---

# Approach 2: Optimal — HashMap

## Core Idea

For every number:

Instead of searching for its pair,

Ask:

"What number do I need to reach target?"

---

## Observation

If current number is:

`nums[i]`

Required value is:

`target - nums[i]`

---

## Logic

For each element:

1. Compute complement

   `complement = target - nums[i]`

2. Check if complement already exists in HashMap

3. If found:
   Return stored index and current index

4. Otherwise:
   Store current number and its index

---

## Why This Works

When processing current element:

If complement has already been seen,

then the required pair has been found.

---

## Complexity

- Time: `O(n)`
- Space: `O(n)`

---

# Pattern / Learning

This problem teaches:

- HashMap Lookup
- Complement Pattern
- Trading Space for Time

---

# Similar Problems

- Two Sum II
- 3Sum
- 4Sum
- Contains Duplicate
- Subarray Sum Equals K

---

# Follow Up Questions

1. What if array is sorted?
2. What if multiple pairs exist?
3. What if we need all pairs?
4. Can it be solved without extra space?

---

# Interview Tip

Always explain in this order:

1. Brute Force
2. Why Brute Force is inefficient
3. HashMap Optimization

Key Observation:

"For every number, instead of searching for a pair,
search for the complement."

That is the core insight behind the optimal solution.
