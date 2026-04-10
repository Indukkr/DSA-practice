# 4. Subarray Sum Equals K

## Pattern
Prefix Sum + HashMap (Frequency Count)

---

## 🔍 Approach Thinking

### 1. Brute Force
- Fix starting index `i`
- Extend subarray till `j`
- Keep adding elements
- If sum == k → count++

- Time: O(n²)
- Space: O(1)

---

### 2. Optimal Approach (Prefix Sum + HashMap)

- Maintain:
  - running sum (`sum`)
  - HashMap → (prefixSum → frequency)

---

### Core Logic

- At any index:
  - `sum = sum + nums[i]`

- Check:
  - If `(sum - k)` exists in map  
    → subarray found

- Add frequency:
  - `count += map.get(sum - k)`

- Store current sum:
  - `map.put(sum, map.getOrDefault(sum, 0) + 1)`

---

## 🧠 Key Insight
- Instead of checking all subarrays  
  → Check if a previous prefix sum exists

- If:
```
currentSum - previousSum = k
```
→ subarray sum = k

---

## ⚡ Important Point

- Initialize:
```
map.put(0, 1)
```
→ Handles subarrays starting from index 0

---

## 🧠 Pattern Trigger

- Count of subarrays with given sum  
- Negative numbers present (→ sliding window fails)

→ Think: Prefix Sum + HashMap

---

## ⚠️ Common Mistakes

- Using `map.get(sum)` instead of `map.get(sum - k)`
- Forgetting `map.put(0,1)`
- Not storing frequency (overwriting instead of counting)
- Trying sliding window approach
- Using wrong HashMap method (`add` instead of `put`)

---

## 🧪 Edge Cases

- k = 0  
- Negative numbers present  
- All elements = 0  
- Single element array  
- Large input  

---

## 🔁 Dry Run Hint

- nums = [1,1,1], k = 2  
- nums = [1,2,3], k = 3  
- nums = [3,4,7,2,-3,1,4,2], k = 7  

Track:
- running sum  
- map contents  
- count updates  

---

## ⏱ Complexity

- Time: O(n)  
- Space: O(n)  

---

## 🎯 Decision

- Use Prefix Sum + HashMap  
- Reduce O(n²) → O(n)

---

## 🔥 One-Line Summary

→ Count subarrays using `(sum - k)` with prefix sum + hashmap
