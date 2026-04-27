# 🔗 Linked List Cycle Detection (LeetCode)

## 📌 Problem
Given the head of a singly linked list:

👉 Return `true` if there is a cycle  
👉 Otherwise return `false`

---

## 🧠 Intuition

If there is a cycle:
- Fast pointer will eventually **meet** slow pointer

If no cycle:
- Fast pointer reaches `null`

---

## 🚀 Approach (Floyd’s Algorithm)

Use two pointers:
- `slow` → moves 1 step
- `fast` → moves 2 steps

---

## 🔁 Logic

- Move both pointers
- If they meet → cycle exists
- If fast reaches end → no cycle

---

## 🔧 Code

```java
public class Solution {
    public boolean hasCycle(ListNode head) {

        ListNode slow = head;
        ListNode fast = head;

        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;

            if (fast == slow)
                return true;
        }

        return false;
    }
}
```

---

## 🔍 Dry Run (Cycle Case)

```
1 → 2 → 3 → 4 → 5
          ↑     ↓
          ← ← ← ←
```

- slow: 1 → 2 → 3 → 4  
- fast: 1 → 3 → 5 → 4  

👉 They meet → cycle detected ✅

---

## 🔍 Dry Run (No Cycle)

```
1 → 2 → 3 → 4 → null
```

👉 fast reaches null → no cycle ❌

---

## ⏱️ Complexity

- Time: O(n)
- Space: O(1) ⭐

---

## ⚠️ Edge Cases

- Empty list → false  
- Single node (no cycle) → false  
- Single node (self-cycle) → true  

---

## 🔥 Key Insight

👉 Fast pointer moves faster  
👉 If cycle exists → distance reduces → they meet

---

## 🎯 Interview Explanation

> “I use Floyd’s cycle detection where a slow pointer moves one step and a fast pointer moves two steps. If a cycle exists, they will eventually meet.”

---

## 🚀 Follow-ups

- Find **starting node of cycle** (very important)
- Find **length of cycle**

---

## 🔥 Final Takeaway

If:
- need to detect cycle in linked list  
👉 use slow-fast pointer (Floyd’s Algorithm)

---
