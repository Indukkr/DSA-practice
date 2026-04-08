# Longest Substring Without Repeating Characters

## 🧠 Brute Force Approach

### Idea
- Generate all substrings
- Check each substring for unique characters using a HashSet

### Steps
1. Fix starting index `i`
2. For each `i`, expand `j = i → n-1`
3. Create a `HashSet` for each `i`
4. If `s[j]` already exists in set → break
5. Else:
   - Add character to set
   - Update max length → `j - i + 1`

### Complexity
- Time: O(n^2)
- Space: O(n)

### Drawback
- Recomputes substrings again and again
- Repeated work

---

## 🧠 Optimal Approach (Sliding Window + HashSet)

### Idea
- Maintain a window with unique characters
- Expand window when valid, shrink when duplicate found

### Steps
1. Initialize:
   - `l = 0`, `r = 0`
   - `HashSet<Character> set`

2. While `r < n`:
   - If `s[r]` not in set:
     - Add to set
     - Update answer → `r - l + 1`
     - Move `r++`
   - Else:
     - Remove `s[l]` from set
     - Move `l++`

### Key Insight
- Do not restart for every substring
- Reuse previous window

### Complexity
- Time: O(n)
- Space: O(n)

---

## 🔥 Pattern
- Sliding Window (Variable Size)
- Two Pointers + HashSet

---

## 🎯 Interview Flow
1. Start with brute force (generate all substrings)
2. Identify repeated work
3. Optimize using sliding window
