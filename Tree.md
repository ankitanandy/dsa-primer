# Trees – Complete Guide for Interviews

## Key Terminology
- **Root**: The topmost node.
- **Parent & Child**: The parent is the node above a given node, and the child is the node below.
- **Leaf**: A node with no children.
- **Depth**: Distance from the root to a node.
- **Height**: Distance from a node to the deepest leaf.
- **Binary Tree**: A tree where each node has at most 2 children.
- **Binary Search Tree (BST)**: A binary tree where the left child is smaller and the right child is larger than the parent.

## Tree Traversal Techniques

### A. Depth-First Search (DFS)
**Inorder (Left, Root, Right)**
```csharp
void InOrder(TreeNode root) {
    if (root == null) return;
    InOrder(root.left);
    Console.WriteLine(root.val);
    InOrder(root.right);
}
```
- Output: Sorted order for BST.
- Time Complexity: O(N), Space Complexity: O(H) (H = height of tree).

**Preorder (Root, Left, Right)**
```csharp
void PreOrder(TreeNode root) {
    if (root == null) return;
    Console.WriteLine(root.val);
    PreOrder(root.left);
    PreOrder(root.right);
}
```

**Postorder (Left, Right, Root)**
```csharp
void PostOrder(TreeNode root) {
    if (root == null) return;
    PostOrder(root.left);
    PostOrder(root.right);
    Console.WriteLine(root.val);
}
```

### B. Breadth-First Search (BFS / Level Order Traversal)
Uses a queue to visit nodes level by level.
```csharp
void LevelOrder(TreeNode root) {
    if (root == null) return;
    Queue<TreeNode> queue = new Queue<TreeNode>();
    queue.Enqueue(root);
    while (queue.Count > 0) {
        TreeNode node = queue.Dequeue();
        Console.WriteLine(node.val);
        if (node.left != null) queue.Enqueue(node.left);
        if (node.right != null) queue.Enqueue(node.right);
    }
}
```
- Time Complexity: O(N)
- Space Complexity: O(N) (for queue).

## Binary Search Tree (BST) Operations

### A. Insertion in BST
```csharp
TreeNode Insert(TreeNode root, int val) {
    if (root == null) return new TreeNode(val);
    if (val < root.val) root.left = Insert(root.left, val);
    else root.right = Insert(root.right, val);
    return root;
}
```

### B. Search in BST
```csharp
bool Search(TreeNode root, int target) {
    if (root == null) return false;
    if (root.val == target) return true;
    if (target < root.val) return Search(root.left, target);
    return Search(root.right, target);
}
```

### C. Deletion in BST
- Case 1: Node has no children → Remove node.
- Case 2: Node has one child → Replace node with child.
- Case 3: Node has two children → Replace with inorder successor (smallest node in right subtree).
```csharp
TreeNode Delete(TreeNode root, int key) {
    if (root == null) return null;
    if (key < root.val) root.left = Delete(root.left, key);
    else if (key > root.val) root.right = Delete(root.right, key);
    else {
        if (root.left == null) return root.right;
        if (root.right == null) return root.left;
        TreeNode successor = GetMin(root.right);
        root.val = successor.val;
        root.right = Delete(root.right, successor.val);
    }
    return root;
}

TreeNode GetMin(TreeNode root) {
    while (root.left != null) root = root.left;
    return root;
}
```

## Common Tree Problems & Patterns

### A. Height of a Tree
```csharp
int Height(TreeNode root) {
    if (root == null) return 0;
    return 1 + Math.Max(Height(root.left), Height(root.right));
}
```
- Time Complexity: O(N)

### B. Check if a Tree is Balanced
A tree is balanced if the height difference between left and right subtrees of any node is at most 1.
```csharp
bool IsBalanced(TreeNode root) {
    return HeightBalanced(root) != -1;
}

int HeightBalanced(TreeNode root) {
    if (root == null) return 0;
    int left = HeightBalanced(root.left);
    int right = HeightBalanced(root.right);
    if (left == -1 || right == -1 || Math.Abs(left - right) > 1) return -1;
    return 1 + Math.Max(left, right);
}
```

### C. Lowest Common Ancestor (LCA) in BST
Find the lowest common ancestor of two nodes in a BST.
```csharp
TreeNode LCA(TreeNode root, TreeNode p, TreeNode q) {
    if (root == null) return null;
    if (p.val < root.val && q.val < root.val) return LCA(root.left, p, q);
    if (p.val > root.val && q.val > root.val) return LCA(root.right, p, q);
    return root;
}
```

### D. Check if Two Trees are Identical
```csharp
bool IsIdentical(TreeNode p, TreeNode q) {
    if (p == null && q == null) return true;
    if (p == null || q == null || p.val != q.val) return false;
    return IsIdentical(p.left, q.left) && IsIdentical(p.right, q.right);
}
```

### E. Path Sum (Root to Leaf Path with Given Sum)
```csharp
bool HasPathSum(TreeNode root, int sum) {
    if (root == null) return false;
    if (root.left == null && root.right == null) return sum == root.val;
    return HasPathSum(root.left, sum - root.val) || HasPathSum(root.right, sum - root.val);
}
```

## Tree Traversal Variations
- **Zigzag Level Order Traversal**: Alternate between left-to-right and right-to-left at each level.
- **Boundary Traversal**: Print boundary nodes in a specific order.
- **Vertical Order Traversal**: Print nodes vertically (sorted by horizontal distance from the root).

## Common Interview Questions on Trees
- Find the diameter of a binary tree (Longest path between any two nodes).
- Serialize and Deserialize a binary tree (Convert tree to string and back).
- Flatten a binary tree to a linked list (In-place, preorder traversal).
- Convert sorted array to BST (Balanced binary search tree).
- Invert a binary tree (Mirror the tree).
- Count the number of nodes in a complete binary tree (Use binary search for efficiency).
- Construct a tree from inorder and preorder/postorder traversal arrays.
- Validate BST.

## Tricks to Identify Tree Problems
Tree problems are common in technical interviews, and they can range from simple traversals to complex operations. Here are key indicators to identify if a problem involves a tree structure:

1. **Parent-Child Relationship**
    - **Key Clue**: If the problem describes relationships where one element is a parent and others are children, it likely involves a tree.
    - **Examples**:
      - Family tree problems (e.g., “Find the common ancestor”).
      - Hierarchical structures (e.g., file systems or organizational charts).

2. **Recursive Structure**
    - Trees are inherently recursive because each subtree is a smaller tree.
    - **Clue**: If a problem can be broken down into smaller, similar subproblems, it may involve trees.
    - **Example**: “Find the maximum depth of a structure.”

3. **Rooted Structure or Hierarchy**
    - If the problem mentions a root or top node with child nodes, it’s a tree problem.
    - **Example**:
      - “Given a tree with root Node1, find all leaf nodes.”
      - “Return all paths from the root to the leaves.”

4. **Ancestral or Hierarchical Relationships**
    - Problems that mention ancestors, descendants, or paths between nodes are often related to trees.
    - **Example**: “Find the lowest common ancestor of two nodes in a binary tree.”

5. **Traversals (Inorder, Preorder, Postorder, Level Order)**
    - If the problem asks for processing nodes in a certain order (e.g., left-to-right, top-to-bottom), it likely involves tree traversal.
    - **Example**:
      - “Print nodes in level order” suggests a breadth-first traversal.
      - “List nodes in sorted order” often hints at an inorder traversal for binary search trees (BSTs).

6. **Binary Search or Sorted Data**
    - If the problem involves searching or finding elements in sorted structures, it may hint at Binary Search Trees (BSTs).
    - **Example**: “Find the Kth smallest element in a tree.”
    - **Optimization hint**: Use inorder traversal for sorted order in a BST.

7. **Balanced Structure**
    - Mention of terms like "balanced," "complete," "perfect," or "height-balanced" indicates tree balancing (e.g., AVL trees).
    - **Example**: “Check if a binary tree is height-balanced.”

8. **Paths and Sums**
    - If the problem asks for path sums, maximum path, or paths from root to leaf, it likely involves tree traversal with cumulative sums.
    - **Example**: “Find the path with the maximum sum in a binary tree.”

9. **Subtree Operations**
    - Mention of subtree relationships is a common clue for tree problems.
    - **Example**: “Check if one tree is a subtree of another tree.”

10. **Diameter, Height, or Depth**
     - If the problem asks for the height, depth, or diameter of a structure, it’s almost certainly a tree problem.
     - **Example**: “Find the diameter (longest path) of a binary tree.”

11. **Node Relationships and Constraints**
     - If the problem involves constraints on relationships (e.g., node values should follow certain rules), it may involve Binary Search Trees (BSTs).
     - **Example**: “Check if a tree is a valid Binary Search Tree.”

12. **Dynamic Hierarchical Structures**
     - Dynamic tree operations (e.g., insertion, deletion, merging) often suggest binary or AVL trees.
     - **Example**: “Insert a node in a balanced binary search tree.”

    ## Tips for Solving Tree Problems
    - **Start with Traversals**: If unsure, try writing basic traversals (inorder, preorder, etc.) and see if they help identify the problem pattern.
    - **Use Recursion**: Trees naturally lend themselves to recursive solutions because of their hierarchical structure.
    - **Think in Subproblems**: Solve smaller subtrees first and combine their results for the full tree solution.
    - **Memoization/Cache**: If subtrees are being processed repeatedly, caching intermediate results can improve efficiency.
    - **Base Case**: Always handle edge cases like null nodes or single-node trees.
    
## Summary Notes for Trees
- **Traversal**: DFS (Inorder, Preorder, Postorder), BFS (Level Order).
- **BST Operations**: Insert, Search, Delete (with successor).
- **Patterns**: Recursion, DFS, BFS, Divide & Conquer.
- **Common Problems**: Height, LCA, Path Sum, Tree Balancing.
