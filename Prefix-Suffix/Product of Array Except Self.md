# Product of Array Except Self

## Pattern
Prefix + Suffix (Product)

---

## 🔍 Approach Thinking

### 1. Brute Force
- Use nested loops to calculate product of all elements except self
- For each index, multiply all other elements
- Time: O(n²), Space: O(1)

---

### 2. Better Approach (Using Division)
- Compute total product of all elements
- Result[i] = totalProduct / nums[i]

### ⚠️ Handling Zero (Edge Case)

- Count number of zeros in array → count_zero

Case 1: count_zero > 1
- All elements in result will be 0

Case 2: count_zero == 1
- Only index with zero will have product of all non-zero elements
- All other positions will be 0

Case 3: count_zero == 0
- Result[i] = totalProduct / nums[i]

Note:
- Decision is based on total zero count, not individual elements

- Time: O(n), Space: O(1)

---

### 3. Prefix + Suffix Arrays
- Create two arrays:
  - left[i] → product of elements before index i
  - right[i] → product of elements after index i

- Final:
  result[i] = left[i] * right[i]

- Time: O(n), Space: O(n)

---

### 4. Optimized Approach (Single Array)
- Use result array to store left products

Step 1: Left pass
- result[i] stores product of all elements before i

Step 2: Right pass
- Maintain rightProduct = 1
- Multiply result[i] with rightProduct
- Then update rightProduct = rightProduct * nums[i]

- Time: O(n), Space: O(1) (excluding output array)

---

## 🎯 Decision
- Avoid division due to zero edge cases
- Use prefix-suffix approach for optimal and safe solution

---

## ⚡ Key Insight
- Instead of removing current element, build result using left and right contributions

---

## 🧠 Pattern Trigger
- "Can I compute result using left and right parts separately?"

---

## ⚠️ Edge Cases
- Array contains zero(s)
- Single element (edge constraint case)
