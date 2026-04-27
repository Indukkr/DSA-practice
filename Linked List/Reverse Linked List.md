# 🔗 Reverse Linked List (LeetCode)

## 📌 Problem
Given the head of a singly linked list:

👉 Reverse the list and return new head

---

## 🧠 Intuition

We need to reverse the direction of pointers:

```
1 → 2 → 3 → 4 → null
```

👉 becomes:

```
1 ← 2 ← 3 ← 4 ← null
```

---

## 🚀 Approach (Iterative)

We use 3 pointers:

- `current` → current node
- `previous` → previous node (to reverse link)
- `forward` → store next node (to not lose list)

---

## 🔁 Steps

For each node:
1. Store next node (`forward`)
2. Reverse link → `current.next = previous`
3. Move `previous` forward
4. Move `current` forward

---

## 🔧 Code

```java
class Solution {
    public ListNode reverseList(ListNode head) {

        ListNode current = head;
        ListNode previous = null;
        ListNode forward = null;

        while (current != null) {

            forward = current.next;
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

List: `1 → 2 → 3`

```
Step 1:
1 → null   2 → 3

Step 2:
2 → 1 → null   3

Step 3:
3 → 2 → 1 → null
```

👉 New head = `previous`

---

## ⏱️ Complexity

- Time: O(n)
- Space: O(1) ⭐

---

## ⚠️ Edge Cases

- Empty list → return null  
- Single node → return same node  

---

## 🔥 Key Concept

👉 Always store `next` before breaking link

```
forward = current.next
```

Otherwise list is lost ❌

---

## 🎯 Interview Explanation

> “I iterate through the list and reverse pointers one by one using three pointers: current, previous, and next. This gives O(n) time and O(1) space.”

---

## 🚀 Follow-ups

- Reverse between positions (partial reverse)
- Reverse in k-groups
- Use in palindrome linked list

---

## 🔥 Final Takeaway

If:
- need to reverse linked list  
👉 use 3-pointer technique

---
