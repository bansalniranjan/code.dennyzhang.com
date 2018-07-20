
# Leetcode: Unique Binary Search Trees     :BLOG:Hard:

---

Unique Binary Search Trees  

---

Similar Problems:  

-   [Review: Dynamic Programming Problems](https://code.dennyzhang.com/review-dynamicprogramming)
-   Tag: [#dynamicprogramming](https://code.dennyzhang.com/tag/dynamicprogramming)

---

Given n, how many structurally unique BST's (binary search trees) that store values 1&#x2026;n?  

    For example,
    Given n = 3, there are a total of 5 unique BST's.
    
       1         3     3      2      1
        \       /     /      / \      \
         3     2     1      1   3      2
        /     /       \                 \
       2     1         2                 3

Github: [challenges-leetcode-interesting](https://github.com/DennyZhang/challenges-leetcode-interesting/tree/master/problems/unique-binary-search-trees)  

Credits To: [leetcode.com](https://leetcode.com/problems/unique-binary-search-trees/description/)  

Leave me comments, if you have better ways to solve.  

---

    // Blog link: https://code.dennyzhang.com/unique-binary-search-trees
    // Basic Ideas: dynamic programming
    //       Pitfalls: try to compare the values. This direction will make things very complicated
    //
    //       How to get f(n) from previous values?
    //           1. We will have a root, so sum(left sub-tree nodes) + sum(right sub-tree nodes) = n-1
    //           2. If root is i, left sub-tree will have i-1 nodes, right sub-tree will have n-k nodes.
    //                  How many different types? f(i-1)*f(n-i)
    //           3. Loop k from 1 to n. Then collect the total number
    //  n = 2:
    //
    //       1         2
    //        \       /
    //         2     1
    //
    //  n = 3:
    //
    //       1         3     3      2      1
    //        \       /     /      / \      \
    //         3     2     1      1   3      2
    //        /     /       \                 \
    //       2     1         2                 3
    //
    //  n = 4:
    //
    //
    //
    // Complexity:
    
    func numTrees(n int) int {
        if n<=1 {return n}
        dp := make([]int, n+1)
        dp[0] = 1
        for i, _:= range dp {
    	if i == 0 { continue }
    	for j := 0; j<i; j++ {
    	    dp[i] += dp[j]*dp[i-1-j]
    	}
        }
        return dp[n]
    }
