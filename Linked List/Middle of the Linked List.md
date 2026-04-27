# 🔗 Middle of Linked List (LeetCode)

## 📌 Problem
Given the head of a singly linked list:

👉 Return the **middle node**

- If even length → return **second middle**

---

## 🧠 Intuition

Use two pointers:
- `slow` → moves 1 step
- `fast` → moves 2 steps

👉 When `fast` reaches end, `slow` will be at middle

---

## 🚀 Approach (Two Pointer)

- Initialize both at head
- Move:
  - slow → 1 step
  - fast → 2 steps

---

## 🔁 Loop Condition

```java
while (fast != null && fast.next != null)
```

👉 Ensures:
- No null pointer error
- Works for both odd & even length

---

## 🔧 Code

```java
class Solution {
    public ListNode middleNode(ListNode head) {

        ListNode slow = head;
        ListNode fast = head;

        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }

        return slow;
    }
}
```

---

## 🔍 Dry Run

### Odd length
```
1 → 2 → 3 → 4 → 5
            ↑
          middle = 3
```

### Even length
```
1 → 2 → 3 → 4 → 5 → 6
                ↑
           middle = 4 (second middle)
```

---

## ⏱️ Complexity

- Time: O(n)
- Space: O(1) ⭐

---

## ⚠️ Edge Cases

- Single node → return head  
- Empty list → return null  

---

## 🔥 Key Insight

👉 Fast moves twice as fast as slow  
👉 So slow covers half distance → lands at middle

---

## 🎯 Interview Explanation

> “I use slow and fast pointers. Slow moves one step, fast moves two steps. When fast reaches the end, slow will be at the middle.”

---

## 🚀 Variations

- Find **first middle** (modify loop condition)
- Used in:
  - Palindrome Linked List
  - Merge Sort on Linked List

---

## 🔥 Final Takeaway

If:
- need middle of linked list  
👉 use slow-fast pointer technique

---
