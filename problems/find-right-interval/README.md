
# Leetcode: Find Right Interval     :BLOG:Medium:

---

Find Right Interval  

---

Similar Problems:  

-   [Review: Interval Problems](https://code.dennyzhang.com/review-interval)
-   [Review: Problems With Many Details](https://code.dennyzhang.com/review-manydetails)
-   Tag: [#manydetails](https://code.dennyzhang.com/tag/manydetails), [#interval](https://code.dennyzhang.com/tag/interval)

---

Given a set of intervals, for each of the interval i, check if there exists an interval j whose start point is bigger than or equal to the end point of the interval i, which can be called that j is on the "right" of i.  

For any interval i, you need to store the minimum interval j's index, which means that the interval j has the minimum start point to build the "right" relationship for interval i. If the interval j doesn't exist, store -1 for the interval i. Finally, you need output the stored value of each interval as an array.  

Note:  

1.  You may assume the interval's end point is always bigger than its start point.
2.  You may assume none of these intervals have the same start point.

Example 1:  

    Input: [ [1,2] ]
    
    Output: [-1]
    
    Explanation: There is only one interval in the collection, so it outputs -1.

Example 2:  

    Input: [ [3,4], [2,3], [1,2] ]
    
    Output: [-1, 0, 1]
    
    Explanation: There is no satisfied "right" interval for [3,4].
    For [2,3], the interval [3,4] has minimum-"right" start point;
    For [1,2], the interval [2,3] has minimum-"right" start point.

Example 3:  

    Input: [ [1,4], [2,3], [3,4] ]
    
    Output: [-1, 2, -1]
    
    Explanation: There is no satisfied "right" interval for [1,4] and [3,4].
    For [2,3], the interval [3,4] has minimum-"right" start point.

Github: [challenges-leetcode-interesting](https://github.com/DennyZhang/challenges-leetcode-interesting/tree/master/problems/find-right-interval)  

Credits To: [leetcode.com](https://leetcode.com/problems/find-right-interval/description/)  

Leave me comments, if you have better ways to solve.  

---

    ## Blog link: https://code.dennyzhang.com/find-right-interval
    ## Basic Ideas: hashmap + binary search
    ##     Build a hashmap to track the mapping from start point to position index
    ##     Sort the interval list by the start attribute
    ##     Use the right attribute to identity the first no smaller values of the start list
    ##
    ## Complexity: Time O(n*log(n)), Space O(n)
    ##
    # Definition for an interval.
    # class Interval:
    #     def __init__(self, s=0, e=0):
    #         self.start = s
    #         self.end = e
    
    class Solution:
        def findRightInterval(self, intervals):
    	"""
    	:type intervals: List[Interval]
    	:rtype: List[int]
    	"""
    	length = len(intervals)
    	m = {}
    	for i in range(0, length): m[intervals[i].start] = i
    	res= [-1]*length
    	start_list = list(sorted(m.keys()))
    	for i in range(0, length):
    	    interval = intervals[i]
    	    target = interval.end
    	    # binary search
    	    left, right = 0, length-1
    	    if target < start_list[0] or target > start_list[-1]:
    		continue
    	    while left <= right:
    		mid = left+int((right-left)/2)
    		v = start_list[mid]
    		if v == target:
    		    res[i] = m[start_list[mid]]
    		    break
    		if v < target:
    		    left = mid + 1
    		else:
    		    right = mid - 1
    
    	    # I found, skip
    	    if res[i] == -1:
    		res[i] = m[start_list[left]]
    	return res
