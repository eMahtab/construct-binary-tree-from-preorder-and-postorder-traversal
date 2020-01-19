## Construct Binary Tree from Preorder and Postorder Traversal


## Thoughts 

We can construct a unique binary tree from inorder and preorder sequences, as well as from the inorder and postorder sequences. 
But preorder and postorder sequences don’t provide enough information to create a unique binary tree. 
More than one binary trees can be constructed due to ambiguity.

```
              a             a         
             /               \
            b                 b 
           /                   \
          c                     c
 Left Skewed Tree            Right Skewed Tree 
```
