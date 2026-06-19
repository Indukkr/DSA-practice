# LeetCode 144 - Binary Tree Preorder Traversal

## Pattern

Tree Traversal + DFS

---

## What is Preorder Traversal?

Preorder follows:

```text
Root
↓
Left
↓
Right
```

Example:

```text
        1
       / \
      2   3
     / \
    4   5
```

Preorder:

```text
1 2 4 5 3
```

---

# Solution 1: Recursive DFS

## Idea

Follow preorder sequence:

```text
Root
↓
Left
↓
Right
```

At every node:

1. Process current node.
2. Traverse left subtree.
3. Traverse right subtree.

---

## Code

```java
class Solution {

    List<Integer> ans = new ArrayList<>();

    public List<Integer> preorderTraversal(TreeNode root) {

        preorder(root);

        return ans;
    }

    private void preorder(TreeNode root){

        if(root == null)
            return;

        ans.add(root.val);

        preorder(root.left);

        preorder(root.right);
    }
}
```

---

## Dry Run

Tree:

```text
        1
       / \
      2   3
```

Execution:

```text
Visit 1

Go Left
Visit 2

Go Right
Visit 3
```

Result:

```text
[1,2,3]
```

---

## Time Complexity

Every node visited once.

```text
Time = O(N)
```

where:

```text
N = Number of Nodes
```

---

## Space Complexity

Recursion stack:

```text
Space = O(H)
```

where:

```text
H = Height of Tree
```

Balanced Tree:

```text
O(log N)
```

Worst Case:

```text
O(N)
```

---

# Solution 2: Iterative DFS Using Stack

## Idea

Recursion internally uses a call stack.

We can simulate it using an explicit Stack.

Preorder:

```text
Root
↓
Left
↓
Right
```

Since Stack is LIFO:

```text
Push Right First
Push Left Second
```

This ensures Left gets processed before Right.

---

## Code

```java
class Solution {

    public List<Integer> preorderTraversal(TreeNode root) {

        List<Integer> ansList = new ArrayList<>();

        if(root == null)
            return ansList;

        Stack<TreeNode> stack = new Stack<>();

        stack.push(root);

        while(!stack.isEmpty()){

            TreeNode temp = stack.pop();

            ansList.add(temp.val);

            if(temp.right != null)
                stack.push(temp.right);

            if(temp.left != null)
                stack.push(temp.left);
        }

        return ansList;
    }
}
```

---

## Why Push Right Before Left?

Example:

```text
      1
     / \
    2   3
```

Stack:

```text
Push 3
Push 2
```

Stack top:

```text
2
```

Therefore:

```text
2 processed before 3
```

Result:

```text
1 2 3
```

which is correct preorder traversal.

---

## Dry Run

Tree:

```text
        1
       / \
      2   3
     / \
    4   5
```

Initial:

```text
Stack = [1]
```

Pop:

```text
1
```

Add:

```text
Ans = [1]
```

Push:

```text
3
2
```

Stack:

```text
[3,2]
```

Pop:

```text
2
```

Add:

```text
Ans = [1,2]
```

Push:

```text
5
4
```

Stack:

```text
[3,5,4]
```

Continue:

```text
Ans = [1,2,4,5,3]
```

---

## Time Complexity

Each node is pushed and popped once.

```text
Time = O(N)
```

---

## Space Complexity

Stack stores at most tree height worth of nodes.

```text
Space = O(H)
```

Worst Case:

```text
O(N)
```

---

# Complexity Comparison

| Solution | Time | Space |
|-----------|--------|--------|
| Recursive DFS | O(N) | O(H) |
| Iterative DFS | O(N) | O(H) |

---

# Interview Notes

### Recursive Approach

```text
Simple
Easy to write
Uses implicit recursion stack
```

---

### Iterative Approach

```text
Uses explicit Stack
Avoids recursion
Frequently asked follow-up
```

---

### Key Trick

```text
Push Right First
Push Left Second
```

Because Stack is:

```text
LIFO
```

---

# Final Takeaway

When you see:

```text
Preorder Traversal
```

Think:

```text
Root
↓
Left
↓
Right
```

Recursive:

```text
Process Root
Traverse Left
Traverse Right
```

Iterative:

```text
Pop Node
Process Node
Push Right
Push Left
```

## Solution Ranking

```text
1. Recursive DFS      ⭐ Most Intuitive
2. Iterative DFS      ⭐ Common Interview Follow-up
```
