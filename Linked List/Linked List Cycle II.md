# 🔗 Linked List Cycle II — Find Start of Cycle (LeetCode)

## 📌 Problem
Given the head of a linked list:

👉 Return the node where the cycle begins  
👉 If no cycle → return `null`

---

## 🧠 Intuition

Two steps:
1. Detect if cycle exists
2. Find the **starting node of cycle**

---

## 🚀 Approach (Floyd’s Algorithm)

### Step 1: Detect Cycle
- Use slow (1 step) and fast (2 steps)
- If they meet → cycle exists

---

### Step 2: Find Start Node

👉 Move one pointer to head  
👉 Keep other at meeting point  

Now move both one step at a time

👉 Where they meet again = **cycle start**

---

## 🔥 Key Insight (VERY IMPORTANT)

Let:
- Distance from head to cycle start = `L`
- Distance from cycle start to meeting point = `X`

👉 When slow & fast meet:

```
L = distance from meeting point to cycle start
```

👉 That’s why moving both pointers gives the start node

---

## 🔧 Code

```java
public class Solution {
    public ListNode detectCycle(ListNode head) {
        
        ListNode slow = head;
        ListNode fast = head;
        
        boolean cycleExist = false;

        while (fast != null && fast.next != null) {

            slow = slow.next;
            fast = fast.next.next;

            if (slow == fast) {
                cycleExist = true;
                break;
            }
        }

        if (cycleExist) {
            fast = head;

            while (slow != fast) {
                slow = slow.next;
                fast = fast.next;
            }

            return slow;
        }

        return null;
    }
}
```

---

## 🔍 Dry Run

```
1 → 2 → 3 → 4 → 5
          ↑     ↓
          ← ← ← ←
```

- Step 1: slow & fast meet inside cycle  
- Step 2:
  - fast → head
  - slow → meeting point

Move both:
👉 They meet at node `3` → cycle start

---

## ⏱️ Complexity

- Time: O(n)
- Space: O(1) ⭐

---

## ⚠️ Edge Cases

- No cycle → return null  
- Single node cycle → return that node  

---

## 🎯 Interview Explanation

> “First I detect the cycle using slow and fast pointers. Once they meet, I reset one pointer to head and move both one step at a time. The point where they meet again is the start of the cycle.”

---

## 🔗 Relation with Cycle Detection

| Problem | Goal |
|--------|------|
| Cycle Detection | Check if cycle exists |
| Cycle II | Find start of cycle |

👉 Same logic + one extra step

---

## 🔥 Final Takeaway

If:
- need cycle start  
👉 detect cycle → reset pointer → move together

---
