# 🔗 Add Two Numbers — Linked List (LeetCode #2)

## 📌 Problem

Given two non-empty linked lists representing two non-negative integers:

- Digits are stored in **reverse order**
- Each node contains a single digit
- Add the two numbers
- Return the sum as a linked list

Example:

```text
l1 = 2 → 4 → 3
l2 = 5 → 6 → 4

342 + 465 = 807

Answer:
7 → 0 → 8
```

---

## 🧠 Intuition

Since digits are already stored in **reverse order**, we can add them exactly like normal addition from right to left.

At every position:

```text
sum = digit1 + digit2 + carry
```

The digit we store is:

```text
sum % 10
```

And the carry for the next position is:

```text
sum / 10
```

---

## 🚀 Approach

### Step 1: Use a Dummy Node

Create a dummy node:

```java
ListNode list = new ListNode(-1);
```

This makes it easy to build the result list without handling the first node separately.

```text
dummy → result nodes
```

At the end:

```java
return list.next;
```

---

### Step 2: Maintain Carry

Initialize:

```java
int carry = 0;
```

For every pair of digits:

```text
sum = l1.val + l2.val + carry
```

Then:

```text
digit = sum % 10
carry = sum / 10
```

---

### Step 3: Handle Different Lengths

The two linked lists may have different lengths.

Therefore, continue while:

```java
l1 != null || l2 != null || carry != 0
```

This handles:

- both lists having nodes
- only `l1` having nodes
- only `l2` having nodes
- remaining carry

---

## 🔁 Why `carry != 0` is in the while condition

Consider:

```text
l1 = 9
l2 = 1
```

Addition:

```text
9 + 1 = 10
```

We create:

```text
0
```

But `carry = 1` is still left.

So we need another node:

```text
1 → 0
```

That's why:

```java
while(l1 != null || l2 != null || carry != 0)
```

---

## 🔧 Code

```java
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {

        ListNode list = new ListNode(-1);
        ListNode temp = list;

        int carry = 0;

        while (l1 != null || l2 != null || carry != 0) {

            int sum = 0;

            if (l1 != null && l2 != null) {

                sum += l1.val;
                l1 = l1.next;

                sum += l2.val;
                l2 = l2.next;

            } else if (l2 != null) {

                sum += l2.val;
                l2 = l2.next;

            } else if (l1 != null) {

                sum += l1.val;
                l1 = l1.next;
            }

            sum += carry;

            ListNode newNode = new ListNode(sum % 10);

            temp.next = newNode;
            temp = newNode;

            carry = sum / 10;
        }

        return list.next;
    }
}
```

---

## 🔍 Dry Run

### Input

```text
l1 = 2 → 4 → 3
l2 = 5 → 6 → 4
```

### Step 1

```text
2 + 5 + 0 = 7

digit = 7 % 10 = 7
carry = 7 / 10 = 0
```

Result:

```text
7
```

---

### Step 2

```text
4 + 6 + 0 = 10

digit = 10 % 10 = 0
carry = 10 / 10 = 1
```

Result:

```text
7 → 0
```

---

### Step 3

```text
3 + 4 + 1 = 8

digit = 8 % 10 = 8
carry = 8 / 10 = 0
```

Result:

```text
7 → 0 → 8
```

Answer:

```text
7 → 0 → 8
```

---

## 🔍 Important Example — Different Lengths

```text
l1 = 9 → 9 → 9
l2 = 1
```

Addition:

```text
999 + 1 = 1000
```

Process:

```text
9 + 1 = 10 → digit 0, carry 1

9 + 0 + 1 = 10 → digit 0, carry 1

9 + 0 + 1 = 10 → digit 0, carry 1

carry = 1 → create final node
```

Result:

```text
0 → 0 → 0 → 1
```

---

## ⏱️ Complexity

Let:

```text
n = length of l1
m = length of l2
```

### Time

```text
O(max(n, m))
```

Each node is processed once.

### Space

```text
O(max(n, m))
```

For the output linked list.

👉 Extra auxiliary space is **O(1)**.

---

## ⚠️ Common Mistakes

### 1. Forgetting the carry

```java
sum = l1.val + l2.val;
```

❌ Wrong

Need:

```java
sum = l1.val + l2.val + carry;
```

---

### 2. Forgetting the final carry

Example:

```text
9 + 1 = 10
```

The final `1` must become a new node.

That's why:

```java
carry != 0
```

is part of the loop condition.

---

### 3. Advancing a null pointer

Don't do:

```java
l1 = l1.next;
```

without checking:

```java
if(l1 != null)
```

---

### 4. Returning the dummy node

```java
return list;
```

❌ Wrong

The dummy node is not part of the answer.

```java
return list.next;
```

✅ Correct

---

## 🎯 Interview Explanation

> "Since the digits are stored in reverse order, I can traverse both linked lists from their heads and perform addition digit by digit. For every position, I calculate the sum of both digits plus the carry. I store `sum % 10` in the result node and carry `sum / 10` to the next position. I use a dummy node to simplify result construction and continue until both lists are exhausted and there is no remaining carry."

---

## 🔥 Key Pattern

This problem combines:

- Linked List Traversal
- Dummy Node
- Carry Handling
- Handling Different Lengths

The core formula to remember:

```text
sum = digit1 + digit2 + carry

digit = sum % 10

carry = sum / 10
```

---

## 🔗 Related Linked List Patterns

| Problem | Main Pattern |
|---|---|
| Reverse Linked List | 3-pointer reversal |
| Middle of Linked List | Slow & Fast Pointer |
| Palindrome Linked List | Middle + Reverse |
| Linked List Cycle | Slow & Fast Pointer |
| Linked List Cycle II | Floyd's Algorithm |
| Add Two Numbers | Dummy Node + Carry |

---

## 🔥 Final Takeaway

Whenever you see:

> "Add numbers represented by linked lists"

Think:

```text
Dummy Node
     ↓
Traverse both lists
     ↓
digit1 + digit2 + carry
     ↓
sum % 10 → result
sum / 10 → carry
```

```java
while (l1 != null || l2 != null || carry != 0)
```

👉 This loop condition is the most important thing to remember.
