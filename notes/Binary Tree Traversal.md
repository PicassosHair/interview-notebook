# Binary Tree Traversal

## Question List
94\. Binary Tree Inorder Traversal \
102\. Binary Tree Level Order Traversal \
144\. Binary Tree Preorder Traversal \
145\. Binary Tree Postorder Traversal 


## Background
Tree Traversal is the fundamental for solving Tree's problems. Following are the generally used ways for traversing trees:

### Depth First Traversals:
- Preorder: Root, Left, Right
- Inorder: Left, Root, Right
- Postorder: Left, Right, Root

### Breadth First Traversals:
- Level Order

<br>

## Leetcode Problem

### Leecode 144 - Preorder
#### Iterative Tree Traversal
```python
def preorderTraversal(self, root: TreeNode) -> List[int]:
    res, stack = [], [root]

    while stack:
        root = stack.pop()

        if root:
            res.append(root.val)
            stack.append(root.right)
            stack.append(root.left)
        
    return res
```
#### Recursive Tree Traversal
```python
def preorderTraversal(self, root: TreeNode) -> List[int]:
    res = []

    def dfs(node: TreeNode):
        if node:
            result.append(node.val)
            dfs(node.left)
            dfs(node.right)

    dfs(root)
    return res
```

<br>


### Leecode 94 - Inorder
#### Iterative Tree Traversal
```python
def inorderTraversal(self, root: TreeNode) -> List[int]:
    res, stack = [], []
    
    while stack or root:
        if root:
            stack.append(root)
            root = root.left
        else:
            root = stack.pop()
            res.append(root.val)
            root = root.right
    
    return res
```
```python
def inorderTraversal(self, root: TreeNode) -> List[int]:
    res, stack = [], []
    
    while True:
        while root:
            stack.append(root)
            root = root.left
        if stack:
            root = stack.pop()
            res.append(root.val)
            root = root.right
        else:
            return res
```
#### Recursive Tree Traversal
```python
def inorderTraversal(self, root: TreeNode) -> List[int]:
    res = []

    def dfs(node):
        if node:
            dfs(node.left)
            res.append(node.val)
            dfs(node.right)
    
    dfs(root)
    return res
```


### Leecode 145 - Postorder
#### Iterative Tree Traversal
```python
def postorderTraversal(self, root: TreeNode) -> List[int]:
    res, stack = [], [root]

    while stack:
        root = stack.pop()
        if root:
            res.append(root.val)
            stack.append(root.left)
            stack.append(root.right)

    return res[::-1]
```
#### Recursive Tree Traversal
```python
def postorderTraversal(self, root: TreeNode) -> List[int]:
    res = []

    def dfs(node):
        if node:
            dfs(node.left)
            dfs(node.right)
            res.append(node.val)

    dfs(root)
    return res
```


### Leecode 102 - Level Order
#### Iterative Tree Traversal
```python
def levelOrder(self, root: TreeNode) -> List[List[int]]:
    if not root:
        return 

    res, level = [[]], 0
    stack_cur, stack_next = [root], []

    while stack_cur or stack_next:
        if stack_cur:
            node = stack_cur.pop(0)
            res[level].append(node.val)
            
            if node.left:
                stack_next.append(node.left)
            if node.right:
                stack_next.append(node.right)
        else:
            level += 1
            res.append([])
            stack_cur = stack_next
            stack_next = []
    
    return res
```
#### Recursive Tree Traversal
```python
def levelOrder(self, root: TreeNode) -> List[int]:
    res = []

    def dfs(node: TreeNode, level):
        if node:
            if len(res) <= level:
                res.append([])
            res[level].append(node.val)

            dfs(node.left, level + 1)
            dfs(node.right, level + 1)

    dfs(root, 0)
    return res
```
