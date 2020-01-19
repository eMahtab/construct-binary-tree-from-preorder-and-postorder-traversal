## Construct Binary Tree from Preorder and Postorder Traversal
### https://leetcode.com/problems/construct-binary-tree-from-preorder-and-postorder-traversal

Return any binary tree that matches the given preorder and postorder traversals.

Values in the traversals pre and post are distinct positive integers.
```
Example 1:

Input: pre = [1,2,4,5,3,6,7], post = [4,5,2,6,7,3,1]
Output: [1,2,3,4,5,6,7]
``` 

**Note:**
1. 1 <= pre.length == post.length <= 30
2. pre[] and post[] are both permutations of 1, 2, ..., pre.length.
3. It is guaranteed an answer exists. If there exists multiple answers, you can return any of them.

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

## Implementation :

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public static TreeNode constructFromPrePost(int[] pre, int[] post) {
		  int preStart = 0;
	      int preEnd = pre.length - 1;
	      int postStart = 0;
	      int postEnd = post.length - 1;
	      
	      Map<Integer, Integer> map = new HashMap<>();
	      for(int i = 0; i < post.length; i++) {
	    	  map.put(post[i], i);
	      }
	      
	      return construct(pre, preStart, preEnd, post, postStart, postEnd, map);
	}
	
	private static TreeNode construct(int[] pre, int preStart, int preEnd, 
			int[] post, int postStart, int postEnd, Map<Integer, Integer> map) {
		if(preStart > preEnd || postStart > postEnd)
			return null;
		
		TreeNode node = new TreeNode(pre[preStart]);
		if(preStart+1 <= preEnd) {
			int rootIndex = map.get(pre[preStart + 1]);
			int leftSubtreeSize = rootIndex - postStart;
			node.left = construct(pre, preStart + 1, preStart+1+leftSubtreeSize, 
					                post, postStart, postStart+leftSubtreeSize, map);
			node.right = construct(pre, preStart+1+leftSubtreeSize+1, preEnd, 
									post, rootIndex+1, postEnd - 1, map);
		}
		
		return node;
	}
}
```

## References :
https://www.techiedelight.com/construct-full-binary-tree-from-preorder-postorder-sequence
