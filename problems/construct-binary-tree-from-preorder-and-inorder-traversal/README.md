
# Leetcode: Construct Binary Tree from Preorder and Inorder Traversal     :BLOG:Basic:

---

Construct Binary Tree from Preorder and Inorder Traversal  

---

Similar Problems:  

-   Tag: [#treetraversal](https://code.dennyzhang.com/tag/treetraversal)

---

Given preorder and inorder traversal of a tree, construct the binary tree.  

Github: [challenges-leetcode-interesting](https://github.com/DennyZhang/challenges-leetcode-interesting/tree/master/problems/construct-binary-tree-from-preorder-and-inorder-traversal)  

Credits To: [leetcode.com](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/description/)  

Leave me comments, if you have better ways to solve.  

---

    
    # Definition for a binary tree node.
    # class TreeNode(object):
    #     def __init__(self, x):
    #         self.val = x
    #         self.left = None
    #         self.right = None
    
    class Solution(object):
        ## Blog link: https://code.dennyzhang.com/construct-binary-tree-from-preorder-and-inorder-traversal
    ## Basic Ideas: non-recursive way by backtracking
        ##            Build the root
        ##            If it has left sub-tree, push to stack
        def buildTree(self, preorder, inorder):
    	"""
    	:type preorder: List[int]
    	:type inorder: List[int]
    	:rtype: TreeNode
    	"""
    
        ## Blog link: https://code.dennyzhang.com/construct-binary-tree-from-preorder-and-inorder-traversal
    ## Basic Ideas:
        ##  Preorder: M L R
        ##   Inorder: L R M
        ##  Take the first of preorder as root
        ##  Locate root in Inorder, since no duplicate
        ##  Divide and conquer for left sub-tree and right sub-tree
        ## Complexity: Time O(n), Space O(n)
        def buildTree_v1(self, preorder, inorder):
    	"""
    	:type preorder: List[int]
    	:type inorder: List[int]
    	:rtype: TreeNode
    	"""
    	if len(preorder) == 0:
    	    return None
    	root_val = preorder[0]
    	index = inorder.index(root_val)
    	left_node = self.buildTree(preorder[1:index+1], inorder[0:index])
    	right_node = self.buildTree(preorder[index+1:], inorder[index+1:])
    	node = TreeNode(root_val)
    	node.left, node.right = left_node, right_node
    	return node
