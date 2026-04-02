# Maximum Subarray

## Pattern
Kadane’s Algorithm (Greedy / Dynamic Programming)

---

### 1. Brute Force
- Generate all possible subarrays using two loops
- Compute sum of each subarray and track maximum
- Time: O(n²), Space: O(1)

---

### 2. Better Approach (Prefix Sum Idea)
- Use prefix sum to compute subarray sum in O(1)
- Still need to check all subarrays
- Time: O(n²), Space: O(1)

---

### 3. Optimal Approach (Kadane’s Algorithm)

- Maintain a running sum
- Add current element to sum
- Update maximum sum
- If sum becomes negative → reset to 0

- Time: O(n), Space: O(1)

---

## 💻 Code (Your Approach)

```java
int maximumSum = Integer.MIN_VALUE;
int sum = 0;

for (int i = 0; i < nums.length; i++) {
    sum += nums[i];

    if (sum > maximumSum)
        maximumSum = sum;

    if (sum < 0)
        sum = 0;
}

return maximumSum;
```
## Clean Code
```java
int currentSum = nums[0];
int maxSum = nums[0];

for (int i = 1; i < nums.length; i++) {
    currentSum = Math.max(nums[i], currentSum + nums[i]);
    maxSum = Math.max(maxSum, currentSum);
}
```
## 🎯 Decision
- Brute force is inefficient for large inputs  
- Kadane’s Algorithm provides optimal linear solution  

---

## ⚡ Key Insight
- Negative running sum reduces future subarray sum  
- So discard it and start a new subarray  

---

## 🧠 Pattern Trigger
- Maximum / Minimum subarray  
- Contiguous subarray problems  
- "Best sum ending at index"  
- Running sum becomes negative → reset  

---

## ⚠️ Edge Cases
- All elements are negative  
- Single element array  

---

## 🔥 Follow-Up Questions (IMPORTANT)

### 1️⃣ Return the Subarray (Not Just Sum)

- Track indices along with sum:
  - start → beginning of subarray  
  - end → ending index  
  - tempStart → new potential start  

---

### 🧠 Idea
- When starting new subarray → update tempStart  
- When max updates → update start and end  

---

### ⚡ Key Insight
- Same Kadane logic + index tracking  

---
```java
int start = 0, end = 0, tempStart = 0;
int maxSum = nums[0];
int sum = nums[0];

for (int i = 1; i < nums.length; i++) {

    if (nums[i] > sum + nums[i]) {
        sum = nums[i];
        tempStart = i;
    } else {
        sum = sum + nums[i];
    }

    if (sum > maxSum) {
        maxSum = sum;
        start = tempStart;
        end = i;
    }
}

// Subarray = nums[start ... end]
```
