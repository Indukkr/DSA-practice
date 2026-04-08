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
- Highly inefficient

---

## 🧠 Optimal Approach (Sliding Window + HashMap)

### Idea
- Use a single HashMap to track required characters
- Maintain a counter `requiredCount` = total characters needed
- Expand window to satisfy requirement
- Shrink window to minimize size

---

## 🔑 Key Variables

- `map` → frequency map of `t`
- `requiredCount` → total characters still needed (initial = t.length())
- `i` → left pointer
- `j` → right pointer
- `windowSize` → minimum length found
- `start_i` → starting index of answer

---

## 🧠 Steps

1. Build frequency map from `t`

2. Initialize:
   - `requiredCount = t.length()`
   - `i = 0`, `j = 0`

3. Expand window (`j++`):
   - If `map[ch] > 0` → character is needed → `requiredCount--`
   - Decrease frequency: `map[ch]--`

4. When `requiredCount == 0` (valid window):
   - Update minimum window
   - Try shrinking from left:
     - Increase frequency of `s[i]`
     - If `map[s[i]] > 0` → window becomes invalid → `requiredCount++`
     - Move `i++`

5. Continue until end

---

## 🎯 Key Insight

- Track **how many characters are still needed**
- No need for separate window map
- Negative values handle extra characters automatically

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

1. Start with brute force (all substrings)
2. Identify repeated work
3. Optimize using sliding window
4. Use `requiredCount` to track validity
