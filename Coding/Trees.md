# Trees

## Introduction


## Problems


### Invert Binary Tree

Leetcode link: 


```c#

    public TreeNode InvertTree(TreeNode root) 
    {
        // we always have a break clause
        if (root == null) return root;

        var temp = root.right;
        // change right to look at left inverted
        root.right = InvertTree(root.left);
        // change left to look at right inverted
        root.left = InvertTree(temp);

        return root;
    }

```

### Maximum Depth of Binary Tree

Leetcode Links: https://leetcode.com/problems/maximum-depth-of-binary-tree/description/

```c#

    public int MaxDepth(TreeNode root) 
    {
        if (root == null) return 0;
        
        return Math.Max(
            MaxDepth(root.right), 
            MaxDepth(root.left)) + 1;
    }

```

### Is Same Tree

```c#

    public bool IsSameTree(TreeNode p, TreeNode q) 
    {
        if (p == null && q == null) return true;

        if ((p == null || q == null) || (p.val != q.val)) return false;

        return IsSameTree(p.left, q.left) && 
                IsSameTree(p.right, q.right);
    }

```


## General tips 