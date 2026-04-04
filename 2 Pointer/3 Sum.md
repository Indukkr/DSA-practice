# 3Sum

## Pattern
Two Pointers + Sorting + 2Sum Reduction

---

## 🔍 Approach Thinking

### 1. Brute Force
- Use 3 nested loops to check all triplets
- Time: O(n³), Space: O(1)

---

### 2. Optimal Approach
- Sort the array
- Fix one element and reduce problem to 2Sum

---

## 🧠 Core Logic

For each index `i`:
- Fix `nums[i]`
- Find two elements such that:
  nums[j] + nums[k] = -nums[i]

Use two pointers:
- j = i + 1
- k = n - 1

---

## ⚡ Key Insight
- Sorting helps:
  - Apply two-pointer technique
  - Handle duplicates efficiently

---

## 🔁 Duplicate Handling (VERY IMPORTANT)

### 1. Skip duplicate `i` (starting element)
- Avoid repeating same base element

if (i > 0 && nums[i] == nums[i-1]) continue;

---

### 2. Skip duplicate pairs (j, k)
- ONLY after finding a valid triplet

After finding triplet:
- j++
- k--

while (j < k && nums[j] == nums[j-1]) j++;
while (j < k && nums[k] == nums[k+1]) k--;

---

## ⚠️ Important Rule
- Do NOT skip duplicates for j and k before finding a valid triplet  
- Otherwise, you may skip valid combinations  

---

## 🧠 Pattern Trigger
- Triplets / pairs in sorted array  
- Need all unique combinations  

👉 Think: Two Pointers + Sorting  

---

## ⏱ Complexity
- Time: O(n²)  
- Space: O(1) (excluding output)  

---

## ⚠️ Edge Cases
- No triplet exists → return empty list  
- All elements same  
- Contains negative, positive, zero  

---

## 🎯 Decision
- Use sorting + two pointers to reduce complexity from O(n³) → O(n²)
