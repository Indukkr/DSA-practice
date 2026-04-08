# Minimum Window Substring

## 🧠 Brute Force Approach

### Idea
- Generate all substrings of `s`
- For each substring:
  - Check if it contains all characters of `t` with correct frequency

### Steps
1. Fix start index `i`
2. Expand `j = i → n-1`
3. For each substring:
   - Build frequency map
   - Compare with `t` map

### Complexity
- Time: O(n^3)
- Space: O(n)

### Drawback
- Recomputes frequency for every substring
- Very inefficient

---

## 🧠 Optimal Approach (Sliding Window + HashMap)

### Idea
- Use sliding window to maintain valid substring
- Expand window to satisfy condition
- Shrink window to minimize length

---

## 🔑 Key Variables

- `need` → frequency map of `t`
- `window` → current window frequency
- `required` → number of unique characters in `t`
- `formed` → number of characters currently satisfied

---

## 🧠 Steps

1. Build `need` map from `t`
2. Initialize:
   - `l = 0`, `r = 0`
   - `formed = 0`
   - `required = need.size()`

3. Expand window (`r++`):
   - Add character to `window`
   - If frequency matches `need` → `formed++`

4. When `formed == required`:
   - Update minimum window
   - Try shrinking from left:
     - Remove `s[l]`
     - If frequency becomes less than needed → `formed--`
     - Move `l++`

5. Continue until end

---

## 🎯 Key Insight

- Expand → to satisfy condition  
- Shrink → to optimize window size  

---

## ⏱ Complexity

- Time: O(n)
- Space: O(n)

---

## 🔥 Pattern

- Sliding Window (Variable Size)
- HashMap + Two Pointers

---

## 🎯 Interview Flow

1. Brute force → generate all substrings
2. Identify repeated work
3. Use sliding window to optimize
4. Track validity using `formed == required`
