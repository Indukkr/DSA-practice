# Longest Common Prefix

## 🧠 Problem
Given an array of strings, find the longest common prefix among them.

---

## 🧠 Brute Force Approach (Horizontal Scanning)

### Idea
- Start with first string as prefix
- Compare it with each string and shrink prefix until it matches

### Steps
1. Take `prefix = strs[0]`
2. For each string:
   - While current string does not start with `prefix`
       - remove last character from `prefix`
3. Return prefix

### Complexity
- Time: O(n * k)
- Space: O(1)

---

## 🧠 Optimal Approach (Vertical Scanning)

### Idea
- Compare characters column-wise across all strings

### Steps
1. Iterate index `i` from 0 to `strs[0].length()`
2. Take character `ch = strs[0].charAt(i)`
3. For every string:
   - If `i == strs[j].length()` OR mismatch → return prefix
4. Append `ch` to prefix

### Code Logic
- Outer loop → index
- Inner loop → strings

### Complexity
- Time: O(n * k)
- Space: O(1)

---

## 🧠 Divide and Conquer Approach

### Idea
- Split array into halves
- Find prefix for each half
- Merge results

### Complexity
- Time: O(n * k)
- Space: O(log n) (recursion stack)

---

## 🧠 Binary Search Approach

### Idea
- Binary search on prefix length

### Steps
1. Find shortest string length = `minLen`
2. Binary search from `0 → minLen`
3. Check if prefix of length `mid` is common

### Complexity
- Time: O(n * k * log k)
- Space: O(1)

---

## 🔥 Pattern
- String Traversal
- Vertical Scanning

---

## 🎯 Key Insight
- Prefix cannot exceed shortest string
- Stop early when mismatch found

---

## 🎯 Interview Flow
1. Explain brute force (horizontal scan)
2. Move to vertical scanning (clean + intuitive)
3. Mention advanced approaches (D&C / Binary Search)
