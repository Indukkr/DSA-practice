# 🔤 Longest Palindromic Substring — LeetCode #5

## 📌 Problem

Given a string `s`, return the **longest palindromic substring**.

A palindrome reads the same forward and backward.

### Example

```text
Input:  "babad"

Output: "bab"
or
        "aba"
```

Both are valid answers.

---

# 🐢 Brute Force Approach

## 💡 Brute Force Thought Process

The most straightforward thought is:

> "I need to find the longest substring which is a palindrome."

A substring can start at any index and end at any later index.

So:

### Step 1: Generate every possible substring

Use two loops:

```text
start = 0 → n-1
end   = start → n-1
```

For every `(start, end)`:

```text
s[start...end]
```

is a possible substring.

---

### Step 2: Check whether the substring is a palindrome

Use two pointers:

```text
left  = start
right = end
```

Compare:

```text
s[left] == s[right]
```

Then move:

```text
left++
right--
```

If all characters match → palindrome.

---

### Step 3: Keep the longest palindrome

Whenever we find a palindrome longer than the current answer:

```text
maxLength = currentLength
```

and store its boundaries.

---

## 🔍 Brute Force Example

```text
s = "babad"
```

Possible substrings include:

```text
"b"
"ba"
"bab"      ← palindrome
"baba"
"babad"

"a"
"ab"
"aba"      ← palindrome
"abad"

"b"
"ba"
"bad"

...
```

We check each substring and keep the longest palindrome.

---

## 🐢 Brute Force Code

```java
class Solution {
    public String longestPalindrome(String s) {

        int start = 0;
        int maxLength = 1;

        for (int i = 0; i < s.length(); i++) {

            for (int j = i; j < s.length(); j++) {

                if (isPalindrome(s, i, j)) {

                    int length = j - i + 1;

                    if (length > maxLength) {
                        maxLength = length;
                        start = i;
                    }
                }
            }
        }

        return s.substring(start, start + maxLength);
    }

    private boolean isPalindrome(String s, int start, int end) {

        while (start < end) {

            if (s.charAt(start) != s.charAt(end))
                return false;

            start++;
            end--;
        }

        return true;
    }
}
```

---

## ⏱️ Brute Force Complexity

### Number of substrings

There are:

```text
O(n²)
```

possible substrings.

### Checking each substring

Palindrome checking can take:

```text
O(n)
```

Therefore:

```text
Time = O(n³)
Space = O(1)
```

---

# 🚀 Optimization Thought Process

Now ask:

> "Am I doing some unnecessary work?"

Yes.

For every substring, we are repeatedly checking whether it is a palindrome.

For example:

```text
"babad"
```

When checking:

```text
"bab"
```

we compare:

```text
b == b
a == a
```

But instead of generating `"bab"` first and then checking it, we can directly ask:

> "What if I start from the center of the palindrome and expand outward?"

---

# 💡 Key Observation

Every palindrome has a **center**.

### Odd-length palindrome

```text
"aba"

    b
    ↑
  center
```

The center is a single character.

So:

```java
expand(i, i, s)
```

---

### Even-length palindrome

```text
"abba"

    b b
    ↑ ↑
   center
```

The center is between two characters.

So:

```java
expand(i, i + 1, s)
```

---

# 🚀 Optimized Approach — Expand Around Center

Instead of:

```text
Generate substring
       ↓
Check palindrome
```

we do:

```text
Choose center
      ↓
Expand outward
      ↓
Check characters while expanding
      ↓
Keep longest palindrome
```

For every index `i`, check:

```java
expand(i, i, s);       // odd length
expand(i, i + 1, s);   // even length
```

---

# 🔁 Expand Function

Start with:

```text
left = center
right = center
```

or:

```text
left = center
right = center + 1
```

Then expand:

```text
left--
right++
```

while:

```text
left >= 0
right < n
s[left] == s[right]
```

---

## 🔍 Example

```text
s = "babad"

        i
        ↓
b a b a d
```

For `i = 2`:

```text
left  = 2
right = 2
```

Compare:

```text
b == b   ✅
```

Expand:

```text
left = 1
right = 3
```

Compare:

```text
a == a   ✅
```

Expand:

```text
left = 0
right = 4
```

Compare:

```text
b != d   ❌
```

Stop.

Palindrome:

```text
"aba"
```

---

# 🧠 Why `end - start - 1`?

Inside `expand()`:

```java
while(start >= 0 &&
      end < s.length() &&
      s.charAt(start) == s.charAt(end))
```

we keep expanding.

When the loop stops, `start` and `end` have already moved **one position outside the palindrome**.

Example:

```text
Palindrome:

    a b a
    ↑   ↑

After expansion:

start = -1
end   = 3
```

So actual length is:

```text
end - start - 1
```

Therefore:

```java
return end - start - 1;
```

---

# 🔥 Finding Start and End of Palindrome

After finding the length:

```java
int len = Math.max(odd_length_palindrome,
                   even_length_palindrome);
```

we need to calculate its boundaries.

```java
start = i - (len - 1) / 2;
end = i + len / 2;
```

This formula works for both odd and even length palindromes.

---

## 🔍 Example — Odd Length

```text
s = "babad"

i = 2
len = 3
```

```text
start = 2 - (3 - 1) / 2
      = 2 - 1
      = 1

end = 2 + 3 / 2
    = 2 + 1
    = 3
```

So:

```text
s[1...3] = "aba"
```

---

## 🔍 Example — Even Length

```text
s = "cbbd"

i = 1
len = 2
```

```text
start = 1 - (2 - 1) / 2
      = 1

end = 1 + 2 / 2
    = 2
```

So:

```text
s[1...2] = "bb"
```

---

# 🔧 Optimized Code

```java
class Solution {
    public String longestPalindrome(String s) {

        int start = 0;
        int end = 0;

        for (int i = 0; i < s.length(); i++) {

            int odd_length_palindrome = expand(i, i, s);

            int even_length_palindrome = expand(i, i + 1, s);

            int len = Math.max(
                odd_length_palindrome,
                even_length_palindrome
            );

            if (len > end - start + 1) {

                start = i - (len - 1) / 2;
                end = i + len / 2;
            }
        }

        return s.substring(start, end + 1);
    }

    private int expand(int start, int end, String s) {

        while (
            start >= 0 &&
            end < s.length() &&
            s.charAt(start) == s.charAt(end)
        ) {
            start--;
            end++;
        }

        return end - start - 1;
    }
}
```

---

# 🔄 Brute Force → Optimized

This is the important interview thought process.

### Brute Force

```text
Generate every substring
        ↓
Check if palindrome
        ↓
Keep longest
```

Complexity:

```text
O(n³)
```

---

### Optimization

Notice:

> We don't need to generate a substring first.

Instead:

```text
Every palindrome has a center
        ↓
Try every possible center
        ↓
Expand outward
        ↓
Keep longest
```

Complexity:

```text
O(n²)
```

---

# ⏱️ Complexity Comparison

| Approach | Time | Space |
|---|---:|---:|
| Brute Force | O(n³) | O(1) |
| Expand Around Center | O(n²) | O(1) |

---

# ⚠️ Common Mistakes

### 1. Checking only odd-length palindromes

```java
expand(i, i, s);
```

❌ Misses:

```text
"bb"
"abba"
```

Always check both:

```java
expand(i, i, s);
expand(i, i + 1, s);
```

---

### 2. Using `coins[i]`-style wrong indexing

Not applicable here, but remember:

The `i` in:

```java
expand(i, i, s)
```

represents the **center index**, not the substring's starting index.

---

### 3. Wrong palindrome length

Because pointers move outside the palindrome:

```java
return end - start - 1;
```

not:

```java
return end - start;
```

---

### 4. Wrong substring end index

Java's:

```java
substring(start, end)
```

does not include `end`.

Therefore:

```java
substring(start, end + 1)
```

---

# 🎯 Interview Explanation

### If interviewer asks: "What's your brute force approach?"

> "I can generate every possible substring using two loops and check each substring using two pointers to determine whether it is a palindrome. If it is a palindrome, I keep track of the longest one. This takes O(n³) time."

### Then explain optimization:

> "I noticed that instead of generating a substring and then checking whether it is a palindrome, I can directly use the fact that every palindrome has a center. So I consider every index as a center and expand outward. I check both odd-length and even-length palindromes. This reduces the time complexity to O(n²) while keeping O(1) extra space."

---

# 🔗 Related Patterns

| Problem | Pattern |
|---|---|
| Valid Palindrome | Two pointers |
| Longest Palindromic Substring | Expand Around Center |
| Palindrome Linked List | Middle + Reverse |
| Longest Substring Without Repeating Characters | Sliding Window |

---

# 🔥 Pattern Recognition

When you see:

```text
"Longest Palindromic Substring"
```

Think:

```text
Palindrome
    ↓
Every palindrome has a center
    ↓
Odd + Even centers
    ↓
Expand outward
    ↓
Track maximum
```

### Remember these two calls:

```java
expand(i, i, s);       // Odd
expand(i, i + 1, s);   // Even
```

---

# 🔥 Final Takeaway

The important progression is:

```text
BRUTE FORCE

Every substring
     ↓
Check palindrome
     ↓
O(n³)


OPTIMIZATION

Every palindrome has a center
     ↓
Try every center
     ↓
Expand outward
     ↓
O(n²)
```

👉 Don't just remember the `expand()` function.

Remember **why we were able to optimize**:

> **Instead of checking whether every substring is a palindrome, directly build palindromes by expanding from their centers.**
