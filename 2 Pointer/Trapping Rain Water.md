# Trapping Rain Water (LeetCode 42)

## Problem
Given an array `height` where each element represents elevation:

- Compute how much rainwater can be trapped after raining

---

# Key Formula

Water trapped at index `i`:

`water[i] = min(maxLeft, maxRight) - height[i]`

---

# Why?
Water level is limited by the shorter boundary.

---

# Approach 1: Brute Force

## Idea
For every index:

1. Find tallest bar on left
2. Find tallest bar on right
3. Compute trapped water

---

## Complexity
- Time: `O(n^2)`
- Space: `O(1)`

---

## Why Not Optimal?
Repeatedly recomputes left/right max for every index.

---

# Approach 2: Prefix/Suffix Max Arrays

## Idea

Precompute:

- `Lmax[i]` = tallest bar from `0 → i`
- `Rmax[i]` = tallest bar from `i → n-1`

Then:

`water += min(Lmax[i], Rmax[i]) - height[i]`

---

## Complexity
- Time: `O(n)`
- Space: `O(n)`

---

## Why It Works
Removes repeated left/right scans by storing max boundaries.

---

# Approach 3: Optimal — Two Pointer

## Core Idea
Instead of storing full arrays:

Maintain:

- `leftMax`
- `rightMax`

Use two pointers:

- `left`
- `right`

---

## Key Observation

If:

`leftMax < rightMax`

Then water at `left` depends only on `leftMax`

Because:

`min(leftMax, rightMax) = leftMax`

So left side can be processed safely.

---

## Logic

### If leftMax < rightMax
- Move `left`
- Update `leftMax`
- Add trapped water at left

---

### Else
- Move `right`
- Update `rightMax`
- Add trapped water at right

---

## Complexity
- Time: `O(n)`
- Space: `O(1)`

---

# Pattern / Learning

This problem teaches:

- Advanced Two Pointer
- Prefix/Suffix Optimization
- Greedy Boundary Processing

---

# Similar Problems

- Container With Most Water
- Largest Rectangle in Histogram
- Daily Temperatures
- Trapping Rain Water II

---

# Follow Up Questions

1. Why does smaller max boundary determine water?
2. Why can we process left when `leftMax < rightMax`?
3. Can stack solution be used?
4. What changes in 2D trapping rain water?

---

# Interview Tip

Derive in this order:

1. Brute Force Formula
2. Prefix/Suffix Optimization
3. Space Optimization to Two Pointer

This shows deep understanding instead of memorization.

---

# Critical Insight

"Whichever side has smaller max boundary is safe to process."

That is the heart of the optimal solution.
