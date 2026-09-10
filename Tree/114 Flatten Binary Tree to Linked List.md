# 🌳 Flatten Binary Tree to Linked List — LeetCode #114

## 📌 Problem

Given the root of a binary tree, flatten the tree into a linked list **in-place**.

The linked list should follow **preorder traversal**:

```text
Root → Left → Right
```

Every node should have:

```text
left = null
right = next node in preorder
```

### Example

Input:

```text
        1
       / \
      2   5
     / \   \
    3   4   6
```

Preorder:

```text
1 → 2 → 3 → 4 → 5 → 6
```

Flattened tree:

```text
1
 \
  2
   \
    3
     \
      4
       \
        5
         \
          6
```

---

# 🐢 Brute Force / Straightforward Thought Process

The first thought is:

> "The flattened tree must follow preorder traversal."

So first we can generate the preorder traversal and store all nodes in a list.

### Step 1

Perform preorder:

```text
Root → Left → Right
```

For:

```text
        1
       / \
      2   5
     / \   \
    3   4   6
```

we get:

```text
[1, 2, 3, 4, 5, 6]
```

### Step 2

Reconnect the nodes:

```text
1 → 2 → 3 → 4 → 5 → 6
```

Set:

```java
current.left = null;
current.right = next;
```

---

## 🐢 Brute Force Complexity

Traversal:

```text
O(n)
```

Extra list:

```text
O(n)
```

So:

```text
Time  = O(n)
Space = O(n)
```

The problem asks for an **in-place** transformation, so we can do better in terms of extra space.

---

# 🚀 Optimized Approach

We want to modify the tree directly without storing all nodes.

The required order is:

```text
Preorder:

Root → Left → Right
```

Instead of processing preorder from the beginning, we can process it in **reverse**:

```text
Right → Left → Root
```

This is the key idea.

---

# 🧠 Why Reverse Preorder?

Suppose preorder is:

```text
1 → 2 → 3 → 4 → 5 → 6
```

If we process it backwards:

```text
6 → 5 → 4 → 3 → 2 → 1
```

When we are processing a node, we already know the node that should come **after it** in the flattened list.

We store that node in:

```java
prev
```

---

# 🔥 Meaning of `prev`

```java
prev
```

represents:

> The node that should come immediately after the current node in the flattened preorder list.

Initially:

```java
prev = null;
```

For example, while processing:

```text
6
```

there is nothing after `6`:

```text
6 → null
```

So:

```java
6.right = prev;
```

Then:

```java
prev = 6;
```

Now when processing `5`:

```text
5 → 6
```

Then:

```java
prev = 5;
```

And so on.

---

# 🔄 Traversal Order

Instead of:

```java
flatten(root.left);
flatten(root.right);
```

we do:

```java
flatten(root.right);
flatten(root.left);
```

So traversal becomes:

```text
Right → Left → Root
```

This is **reverse preorder**.

---

# 🔍 Example

Tree:

```text
        1
       / \
      2   5
     / \   \
    3   4   6
```

Normal preorder:

```text
1 → 2 → 3 → 4 → 5 → 6
```

Reverse preorder processing:

```text
6 → 5 → 4 → 3 → 2 → 1
```

---

## Step 1 — Process 6

```text
prev = null
```

Set:

```java
6.right = null;
6.left = null;
prev = 6;
```

Result:

```text
6 → null
```

---

## Step 2 — Process 5

Currently:

```text
prev = 6
```

Set:

```java
5.right = 6;
5.left = null;
prev = 5;
```

Result:

```text
5 → 6
```

---

## Step 3 — Process 4

```text
4 → 5 → 6
```

---

## Step 4 — Process 3

```text
3 → 4 → 5 → 6
```

---

## Step 5 — Process 2

```text
2 → 3 → 4 → 5 → 6
```

---

## Step 6 — Process 1

```text
1 → 2 → 3 → 4 → 5 → 6
```

Done.

---

# 🔧 Core Logic

For every node:

```java
flatten(root.right);
flatten(root.left);
```

At this point:

```java
prev
```

already points to the next node in preorder.

So:

```java
root.right = prev;
```

Then remove the left child:

```java
root.left = null;
```

Finally:

```java
prev = root;
```

because this node will become the `prev` for the next node processed.

---

# 🔧 Code

```java
class Solution {

    TreeNode prev = null;

    public void flatten(TreeNode root) {

        if (root == null)
            return;

        // Reverse preorder: Right → Left → Root
        flatten(root.right);
        flatten(root.left);

        // Connect current node to previously processed node
        root.right = prev;

        // Flattened tree cannot have left children
        root.left = null;

        // Current node becomes previous node
        prev = root;
    }
}
```

---

# 🧠 The Most Important Part

Remember these four lines:

```java
flatten(root.right);
flatten(root.left);

root.right = prev;
root.left = null;

prev = root;
```

The order is extremely important.

---

# ⚠️ Why Right First and Left Second?

The required order is:

```text
Root → Left → Right
```

We process it backwards:

```text
Right → Left → Root
```

Therefore:

```java
flatten(root.right);
flatten(root.left);
```

If we processed:

```java
flatten(root.left);
flatten(root.right);
```

the `prev` relationship would not represent the correct next node for this technique.

---

# 🎯 Interview Thought Process

If the interviewer asks:

### "How did you come up with this?"

You can say:

> "The flattened tree has to follow preorder traversal, which is Root → Left → Right. A straightforward solution would be to store the preorder nodes and reconnect them, but that uses O(n) extra space. To make it in-place, I process the preorder in reverse, Right → Left → Root. I maintain a `prev` pointer to the node that should come after the current node. After processing the right and left subtrees, I set `root.right = prev`, clear `root.left`, and make the current node the new `prev`."

---

# 🧠 Why Does This Work?

Consider preorder:

```text
1 → 2 → 3 → 4 → 5 → 6
```

When processing backwards:

```text
6
```

`prev` is:

```text
null
```

Then:

```text
5
```

`prev` is:

```text
6
```

Then:

```text
4
```

`prev` is:

```text
5
```

Therefore every node already knows:

> "Who should come immediately after me?"

That's exactly what we need to build:

```text
root.right = prev
```

---

# 🔄 Connection With Preorder Traversal

Normal preorder:

```text
Root
 ↓
Left
 ↓
Right
```

Required flattened order:

```text
Root → Left → Right
```

Our traversal:

```text
Right
 ↓
Left
 ↓
Root
```

Why?

Because processing in reverse allows us to maintain the next node using only one pointer:

```java
prev
```

---

# ⏱️ Complexity

### Time

```text
O(n)
```

Every node is visited once.

### Extra Space

```text
O(h)
```

where `h` is the height of the tree, because of the recursion stack.

### Worst case

For a skewed tree:

```text
O(n)
```

### Balanced tree

```text
O(log n)
```

So this solution is:

```text
Time  = O(n)
Space = O(h)
```

It does not use an additional `ArrayList` or explicit node storage.

---

# ⚠️ Common Mistakes

## 1. Processing Left before Right

```java
flatten(root.left);
flatten(root.right);
```

❌ Not correct for this `prev` technique.

Use:

```java
flatten(root.right);
flatten(root.left);
```

---

## 2. Forgetting to remove left child

```java
root.left = null;
```

is required.

The flattened tree should only use:

```text
right pointers
```

---

## 3. Updating `prev` too early

Wrong:

```java
prev = root;

flatten(root.right);
flatten(root.left);
```

The `prev` must represent the already processed next node.

Therefore:

```java
flatten(root.right);
flatten(root.left);

root.right = prev;
root.left = null;

prev = root;
```

---

# 🔗 Relation With Other Tree Problems

| Problem | Main Pattern |
|---|---|
| Inorder Traversal | Left → Root → Right |
| Preorder Traversal | Root → Left → Right |
| Postorder Traversal | Left → Right → Root |
| Flatten Binary Tree | Reverse Preorder |
| Validate BST | Inorder + Previous |
| LCA | Recursive Tree Traversal |
| Maximum Path Sum | Postorder + DP |

---

# 🔥 Pattern Recognition

When you see:

> "Flatten binary tree according to preorder"

Think:

```text
Required order:
Root → Left → Right

Reverse it:
Right → Left → Root

Maintain:
prev

For every node:
root.right = prev
root.left = null
prev = root
```

---

# 🎯 Quick Revision

```text
Flatten Binary Tree
        ↓
Required order = Preorder
        ↓
Root → Left → Right
        ↓
Process in reverse
        ↓
Right → Left → Root
        ↓
Maintain prev
        ↓
root.right = prev
root.left = null
prev = root
```

---

# 🔥 Final Takeaway

The key idea is **not actually flattening the tree while going forward**.

Instead:

> **Process the preorder traversal backwards and keep track of the previously processed node.**

Remember:

```java
flatten(root.right);
flatten(root.left);

root.right = prev;
root.left = null;
prev = root;
```

This converts the tree into the required preorder-linked list **in-place**.
