# 🔗 Swap Nodes in Pairs — Linked List (LeetCode #24)

## 📌 Problem

Given a linked list, swap every two adjacent nodes and return the modified list.

### Example

```text
Input:
1 → 2 → 3 → 4

Output:
2 → 1 → 4 → 3
```

The important point is:

👉 We need to **swap nodes**, not just swap their values.

---

# 🧠 Brute Force Thought Process

A simple approach would be:

1. Traverse the linked list
2. Swap the values of every two adjacent nodes

For example:

```text
1 → 2 → 3 → 4

swap values:

2 → 1 → 4 → 3
```

But this is not the intended approach because the problem asks us to **swap the nodes themselves**, not their values.

So we need to manipulate the `next` pointers.

---

# 🚀 Optimal Approach

We can solve this in two ways:

1. Iterative → pointer manipulation
2. Recursive → solve remaining list and connect

Both have:

```text
Time  = O(n)
Space = O(1) iterative
Space = O(n) recursive (recursion stack)
```

---

# 🔁 Approach 1 — Iterative

## 💡 Intuition

Consider:

```text
1 → 2 → 3 → 4
```

We want:

```text
2 → 1 → 4 → 3
```

For every pair, maintain:

```text
first
second
third
```

where:

```text
first  = first node of current pair
second = second node of current pair
third  = node after current pair
```

Example:

```text
first
 ↓
1 → 2 → 3 → 4
    ↑   ↑
  second third
```

---

## 🔄 Swapping the Pair

Before:

```text
1 → 2 → 3
```

We want:

```text
2 → 1 → 3
```

First save the third node:

```java
third = second.next;
```

Then reverse the two pointers:

```java
second.next = first;
first.next = third;
```

Now:

```text
2 → 1 → 3
```

---

## 🔗 Connecting Previous Pair

Consider:

```text
2 → 1     4 → 3
```

The previous pair ends at:

```text
1
```

We need:

```text
2 → 1 → 4 → 3
```

So:

```java
prev.next = second;
```

Here:

```text
prev = last node of previous swapped pair
second = first node of current swapped pair
```

---

## 🔧 Iterative Code

```java
class Solution {
    public ListNode swapPairs(ListNode head) {

        if (head == null || head.next == null)
            return head;

        ListNode first = head;
        ListNode second = head.next;
        ListNode prev = null;

        while (first != null && second != null) {

            ListNode third = second.next;

            // Swap current pair
            second.next = first;
            first.next = third;

            // Connect previous pair with current pair
            if (prev != null) {
                prev.next = second;
            } else {
                // First pair gives us the new head
                prev = second;
                head = prev;
            }

            // Move to next pair
            prev = first;
            first = third;

            if (third != null)
                second = third.next;
            else
                second = null;
        }

        return head;
    }
}
```

---

# 🔍 Iterative Dry Run

Input:

```text
1 → 2 → 3 → 4
```

### Pair 1

```text
first = 1
second = 2
third = 3
```

Swap:

```text
2 → 1 → 3 → 4
```

Now:

```text
prev = 1
first = 3
second = 4
```

---

### Pair 2

```text
first = 3
second = 4
third = null
```

Swap:

```text
4 → 3
```

Connect previous pair:

```text
2 → 1 → 4 → 3
```

Answer:

```text
2 → 1 → 4 → 3
```

---

# ⚠️ Important Iterative Insight

The first pair is special because there is no previous pair.

That's why:

```java
if (prev != null) {
    prev.next = second;
} else {
    head = second;
}
```

After the first swap, the second node becomes the **new head**.

---

# 🚀 Approach 2 — Recursive

The recursive solution is much cleaner once we understand the pattern.

Consider:

```text
1 → 2 → 3 → 4
```

Think of the list as:

```text
1 → 2 → [remaining list]
```

We can swap the first pair:

```text
2 → 1 → [remaining list]
```

But instead of manually processing the remaining list, ask recursion to solve it:

```text
swapPairs(3 → 4)
```

which returns:

```text
4 → 3
```

Then connect:

```text
2 → 1 → 4 → 3
```

---

# 🧠 Recursive Thought Process

For:

```text
1 → 2 → 3 → 4
```

We have:

```text
head = 1
head.next = 2
```

Store the second node:

```java
ListNode temp = head.next;
```

Now recursively solve:

```java
swapPairs(head.next.next);
```

This means:

```text
swapPairs(3 → 4)
```

returns:

```text
4 → 3
```

Then:

```java
head.next = swapPairs(head.next.next);
```

gives:

```text
1 → 4 → 3
```

Finally:

```java
temp.next = head;
```

gives:

```text
2 → 1 → 4 → 3
```

---

# 🧱 Base Case

We stop when:

```java
head == null
```

or:

```java
head.next == null
```

Because:

```text
null
```

or:

```text
1
```

doesn't have a pair to swap.

Therefore:

```java
if (head == null || head.next == null)
    return head;
```

---

# 🔧 Recursive Code

```java
class Solution {
    public ListNode swapPairs(ListNode head) {

        if (head == null || head.next == null)
            return head;

        ListNode temp = head.next;

        head.next = swapPairs(head.next.next);

        temp.next = head;

        return temp;
    }
}
```

---

# 🔍 Recursive Dry Run

Input:

```text
1 → 2 → 3 → 4
```

### First call

```text
swapPairs(1)
```

Save:

```text
temp = 2
```

Call:

```text
swapPairs(3)
```

---

### Second call

```text
swapPairs(3)
```

Save:

```text
temp = 4
```

Call:

```text
swapPairs(null)
```

Returns:

```text
null
```

Now:

```text
3.next = null
4.next = 3
```

Returns:

```text
4 → 3
```

---

### Back to first call

We now have:

```text
1 → 4 → 3
```

Then:

```text
2.next = 1
```

Result:

```text
2 → 1 → 4 → 3
```

---

# 🔥 Why Do We Return `temp`?

This is an important point.

Before swapping:

```text
head = 1
temp = 2
```

After swapping:

```text
2 → 1
↑
new head
```

Therefore:

```java
return temp;
```

---

# 🔄 Iterative vs Recursive

| | Iterative | Recursive |
|---|---|---|
| Time | O(n) | O(n) |
| Extra Space | O(1) | O(n) |
| Technique | Pointer manipulation | Recursion |
| Code | More complex | More concise |
| Interview | Great | Great |

---

# ⚠️ Common Mistakes

### 1. Forgetting to save `head.next`

Before changing pointers, save the second node:

```java
ListNode temp = head.next;
```

Otherwise we can lose access to the remaining list.

---

### 2. Returning `head`

After swapping:

```text
1 → 2

becomes

2 → 1
```

So `head` is no longer the first node.

Correct:

```java
return temp;
```

---

### 3. Forgetting the base case

Without:

```java
if (head == null || head.next == null)
    return head;
```

we can get a `NullPointerException`.

---

# 🎯 Interview Explanation — Iterative

> "I process the linked list in pairs. For every pair, I keep three pointers: first, second and third, where third is the node after the pair. I reverse the two nodes by changing their next pointers, then connect the previous pair to the current pair. The second node of the first pair becomes the new head."

---

# 🎯 Interview Explanation — Recursive

> "For every recursive call, I take the first two nodes as a pair. I recursively solve the remaining list starting from the third node, then connect the first two nodes in reverse order. The second node becomes the head of the current swapped pair. The recursion stops when there are fewer than two nodes."

---

# 🔗 Relation With Other Linked List Problems

| Problem | Pattern |
|---|---|
| Reverse Linked List | Reverse pointers |
| Middle of Linked List | Slow & Fast Pointer |
| Palindrome Linked List | Middle + Reverse |
| Linked List Cycle | Slow & Fast Pointer |
| Add Two Numbers | Dummy Node + Carry |
| Swap Nodes in Pairs | Pairwise Pointer Manipulation |
| Reverse Nodes in k-Group | Reversal + Grouping |

---

# 🧠 Pattern Recognition

When you see:

```text
Swap / Reverse nodes in groups
```

Think:

```text
Identify group
     ↓
Save next part
     ↓
Reverse pointers
     ↓
Reconnect with previous part
```

For pairs:

```text
1 → 2 → 3 → 4
↓   ↓
swap

2 → 1 → 4 → 3
```

---

# 🔥 Final Takeaway

The most important pointer relationship is:

```text
first → second → third
```

After swapping:

```text
second → first → third
```

So the core operations are:

```java
third = second.next;

second.next = first;
first.next = third;
```

### Recursive version — remember this pattern:

```java
ListNode temp = head.next;

head.next = swapPairs(head.next.next);

temp.next = head;

return temp;
```

👉 **Swap current pair + recursively solve the remaining list.**

---
