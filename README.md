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
For both left skewed tree and right skewed tree, the preorder and postorder traversal results in same sequence.

```
Preorder  [a, b, c]
Postorder [c, b, a]
```
Therefore, its not possible to construct a unique binary tree with the help of preorder and postoder sequences. 
However we can construct a unique full binary tree using the Preorder and Postorder traversal.
