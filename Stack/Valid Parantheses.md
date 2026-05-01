# 🔗 Valid Parentheses (LeetCode)

## 🧩 Problem
Given a string `s` containing:
```
'(', ')', '{', '}', '[' and ']'
```
Determine if the input string is **valid**.

### ✅ A string is valid if:
1. Open brackets are closed by the same type  
2. Open brackets are closed in the correct order  

---

## 💡 Intuition (My Approach)

- Use a **Stack** to track opening brackets  
- Traverse the string:
  - If opening → push  
  - If closing → check top and pop  
- If mismatch → return false immediately  
- Final check → stack should be empty  

---

## 🛠️ My Solution

```java
class Solution {
    public boolean isValid(String s) {

        Stack<Character> stack = new Stack<>();

        int n = s.length();
        
        for(int i = 0; i<n; i++){
 
            if(!stack.isEmpty() && s.charAt(i) ==')' && stack.peek() == '('){
                stack.pop();
            }
            else if(!stack.isEmpty() && s.charAt(i) =='}' && stack.peek() == '{')
                stack.pop();
            else if(!stack.isEmpty() && s.charAt(i) ==']' && stack.peek() == '[')
                stack.pop();
            else if(s.charAt(i) == '(' || s.charAt(i) =='{'|| s.charAt(i)=='[')
                stack.push(s.charAt(i));
            else
                return false;

        }

        return stack.isEmpty();
        
    }
}
```

---

## 🔍 Dry Run

### Input:
```
s = "([{}])"
```

| Char | Stack Before | Action | Stack After |
|------|------------|--------|-------------|
| (    | []         | push   | [(]         |
| [    | [(]        | push   | [(, []      |
| {    | [(, []     | push   | [(, [, {]   |
| }    | [(, [, {]  | pop    | [(, []      |
| ]    | [(, []     | pop    | [(]         |
| )    | [(]        | pop    | []          |

✅ Stack empty → Valid  

---

## ⚠️ Edge Cases (While Solving)

Think these during problem solving:

- Empty string → `""` → ✅ valid  
- Only opening brackets → `"((("` → ❌ invalid  
- Only closing brackets → `")))"` → ❌ invalid  
- Mismatch order → `"([)]"` → ❌ invalid  
- Correct nested → `"({[]})"` → ✅ valid  
- Single pair → `"()"` → ✅ valid  

---

## 🧠 Key Observations

- Always check `stack.isEmpty()` before accessing top  
- Matching must be **type + order correct**  
- Early return on mismatch saves time  
- Final stack must be empty  

---

## ⚡ Complexity

- **Time:** `O(n)`  
- **Space:** `O(n)`  

---

## 🏷️ Pattern

- Stack  
- Bracket Matching  

---

## 🚀 Notes

- This approach is **intuitive and interview-safe**
- No need to over-optimize unless asked
- Readability matters more than clever tricks

---
