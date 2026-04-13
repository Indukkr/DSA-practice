# Valid Palindrome II (LeetCode 680)

## Problem
Given a string `s`:

- Return `true` if it can become a palindrome
- By deleting **at most one character**

---

# Approach 1: Brute Force

## Idea
Try deleting every character one by one:

- Remove character at each index
- Check if resulting string is palindrome

## Complexity
- Time: `O(n^2)`
- Space: `O(n)`

## Why Not Optimal?
Very inefficient for large strings.

---

# Approach 2: Optimal — Two Pointer + Greedy

## Core Idea
Use normal palindrome check with two pointers:

- `left` at start
- `right` at end

---

## Logic

### If Characters Match
Move inward normally.

---

### If Characters Mismatch
We can delete only one character.

Try both possibilities:

1. Skip left character  
2. Skip right character  

If either remaining substring is palindrome → return true

---

## Why This Works

At first mismatch:

Only one deletion allowed, so only two valid choices exist:

- Remove left mismatching char
- Remove right mismatching char

No other deletion can help.

---

## Helper Function

Use helper palindrome check for substring:

`isPalindrome(s, left, right)`

This checks whether remaining substring is strict palindrome.

---

## Complexity
- Time: `O(n)`
- Space: `O(1)`

---

# Pattern / Learning

This problem teaches:

- Two Pointer on Strings
- Greedy Decision Making
- Branching at First Constraint Violation

---

# Similar Problems

- Valid Palindrome
- Longest Palindromic Substring
- Palindrome Partitioning
- Reverse String

---

# Follow Up Questions

1. What if deletion of up to `k` characters is allowed?
2. What if insertion is allowed instead of deletion?
3. Can we return the removed character index?
4. How to solve recursively?

---

# Interview Tip

Important Insight:

"At first mismatch, only two possibilities matter:
skip left OR skip right."

That is the greedy observation interviewer expects.
