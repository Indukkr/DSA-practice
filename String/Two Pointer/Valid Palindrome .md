Problem: Valid Palindrome

Brute Force Approach:
- Create a new string
- Traverse original string:
  - Keep only alphanumeric characters
  - Convert all to lowercase
- Check if new string is palindrome:
  - Compare from start and end

Time: O(n)
Space: O(n)

---

Optimal Approach (Two Pointers):
- No extra string needed
- Use i = 0, j = n - 1

Steps:
1. While i < j:
   - Skip non-alphanumeric from left
   - Skip non-alphanumeric from right
   - Compare Character.toLowerCase(s[i]) and s[j]
   - If not equal → return false
   - Else → i++, j--

2. Return true

---

Methods:
- Character.isLetterOrDigit(ch)
- Character.toLowerCase(ch)

---

Key Insight:
- Instead of preprocessing, handle everything in one pass
- Saves space from O(n) → O(1)

---

Interview Flow:
- Start with brute force (clean + check)
- Then optimize to two-pointer (in-place)
