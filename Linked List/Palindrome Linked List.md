# 🔗 Palindrome Linked List (LeetCode)

## 📌 Problem
Given the head of a singly linked list:

👉 Return `true` if it is a palindrome  
👉 Otherwise return `false`

---

## 🧠 Intuition

A palindrome means:
- Forward == Backward

But linked list:
- ❌ No backward traversal
- ❌ No random access

👉 So we:
1. Find middle
2. Reverse second half
3. Compare both halves

---

## 🚀 Approach (Optimal)

### Step 1: Find middle of list
- Use slow & fast pointer

### Step 2: Reverse second half
- Reverse list from `mid.next`

### Step 3: Compare both halves
- Compare values node by node

---

## 🔁 Flow

```
1 → 2 → 3 → 2 → 1

Step 1: mid = 3  
Step 2: reverse second half → 1 → 2  
Step 3: compare → match ✅
```

---

## 🔧 Code

```java
class Solution {
    public boolean isPalindrome(ListNode head) {
        
        if (head == null || head.next == null) return true;

        ListNode mid = findMidNode(head);
        ListNode head1 = head;
        ListNode head2 = reverseSecondHalfOfList(mid.next);
        mid.next = null;

        while (head1 != null && head2 != null) {
            if (head1.val != head2.val)
                return false;

            head1 = head1.next;
            head2 = head2.next;
        }

        return true;
    }

    public ListNode findMidNode(ListNode head) {
        ListNode slow = head;
        ListNode fast = head;

        while (fast.next != null && fast.next.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }

        return slow;
    }

    public ListNode reverseSecondHalfOfList(ListNode head) {
        ListNode current = head;
        ListNode previous = null;

        while (current != null) {
            ListNode forward = current.next;
            current.next = previous;
            previous = current;
            current = forward;
        }

        return previous;
    }
}
```

---

## 🔍 Dry Run

List: `1 → 2 → 3 → 2 → 1`

- mid = 3  
- second half = `2 → 1`  
- reversed = `1 → 2`  
- compare:
  - 1 == 1  
  - 2 == 2  

👉 Palindrome ✅

---

## ⏱️ Complexity

- Time: O(n)
- Space: O(1) ⭐

---

## ⚠️ Edge Cases

- Empty list → true  
- Single node → true  
- Even length list → works correctly  

---

## 🔥 Key Concepts Used

- Slow & Fast Pointer (middle)
- Linked List Reversal
- Two pointer comparison

---

## 🎯 Interview Explanation (Perfect Answer)

> “I find the middle of the list using slow-fast pointers, reverse the second half, and then compare both halves node by node. This gives O(n) time and O(1) space.”

---

## 🚀 Optional Improvement

👉 Restore the list after checking (reverse again)

(Not required unless explicitly asked)

---

## 🔥 Final Takeaway

If:
- need to compare forward & backward in linked list  
👉 reverse second half + compare

---
