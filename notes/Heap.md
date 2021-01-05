# Heap (Priority Queue)
A heap is a specialized tree-based data structure which is essentially a **complete tree** (a binary tree in which every level, except possibly the last, is complete filled, and all nodes are as far left as possible).  

**Min-Heap**: The root node has the minimum value, and the value of each node is equal to or greater than the value of its parent node.

**Max-Heap**: The root node has the maximum value, and the value of each node is equal to or less than the value of its parent node.


## Operations 
- **insert**: adding a new key to the heap `O(log(n))`
- **find-max (or find-min)**: find a maximum item of a max-heap, or a minimum item of a min-heap `O(1)`
- **pop**: delete the root element `O(log(n))`
- **heapify**: create a heap out of given array of elements `O(n)`


## Question List
215\. Kth Largest Element in an Array\
347\. Top K Frequent Elements\
373\. Find K Pairs with Smallest Sums \
414\. Third Maximum Number\
451\. Sort Characters By Frequency\
692\. Top K Frequent Words - max heap\
973\. K Closest Points to Origin

## Leetcode Solution

### Leetcode 215: Kth Largest Element in an Array
Since Python heapq library only implements min-heap, we can use -key in min-heap to get the largest number.
```python
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        if not nums:
            return -1
        
        heap = [-i for i in nums]
        heapq.heapify(heap)

        for _ in range(k):
            res = heapq.heappop(heap)
        
        return -res
```
Or we can maintain a heap which has k numbers:
```python
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        if not nums:
            return -1
        
        pq = nums[:k]
        heapq.heapify(pq)
        
        for num in nums[k:]:
            heapq.heappush(pq, num)
            heapq.heappop(pq)
        
        return pq[0]
```

### Leetcode 347: Top K Frequent Elements
```python
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        dic = collections.Counter(nums)
        
        max_heap = [(-val, key) for key, val in dic.items()]
        heapq.heapify(max_heap)
        
        res = []
        for _ in range(k):
            res.append(heapq.heappop(max_heap)[1])
        
        return res
```

### Leetcode 373: Find K Pairs with Smallest Sums
```python
class Solution:
    def kSmallestPairs(self, nums1: List[int], nums2: List[int], k: int) -> List[List[int]]:
        if not nums1 or not nums2:
            return None
        
        if len(nums1) * len(nums2) <= k:
            return [[a,b] for a in nums1 for b in nums2]
        
        res, cnd = [], [(nums1[i] + nums2[0], i, 0) for i in range(len(nums1))]
        
        for _ in range(k):
            val, i, j = heapq.heappop(cnd)
            res.append([nums1[i], nums2[j]])
            
            if j + 1 < len(nums2):
                heapq.heappush(cnd, (nums1[i]+nums2[j+1], i, j+1))
        
        return res
```

### Leetcode 414: Third Maximum Number
```python
class Solution:
    def thirdMax(self, nums: List[int]) -> int:
        
        heap = []
        nums = set(nums)
        
        for num in nums:
            heapq.heappush(heap, num)
            if len(heap) > 3:
                heapq.heappop(heap)
        
        return heap[0] if len(heap) == 3 else max(heap)
```


### Leetcode 451: Sort Characters By Frequency
```python
class Solution:
    def frequencySort(self, s: str) -> str:
        
        dic = collections.Counter(s)
            
        heap = []
        for k, v in dic.items():
            heapq.heappush(heap, (v, k))
            
        res = ''
        for _ in range(len(heap)):
            v, k = heapq.heappop(heap)
            res = k * v + res
        
        return res
```


### Leetcode 692: Top K Frequent Words
```python
class Solution:
    def topKFrequent(self, words: List[str], k: int) -> List[str]:
	
	    # Create a dictionary whose key is the word and value is the frequency
        dic = collections.Counter(words)
		
		# Python heapq.heapify implements a min-heap, but we need a max-heap.
		# The easiest way is use -freq in min-heap, and the highest frequency will be popped first
        heap = [(-freq, word) for word, freq in dic.items()]
        heapq.heapify(heap)

        res = []
        for _ in range(k):
		    # heapq will handle "If two words have the same frequency, then the word with the lower alphabetical order comes first"
            res.append(heapq.heappop(heap)[1])

        return res
```

### Leetcode 973: K Closest Points to Origin
```python
class Solution:
    def kClosest(self, points: List[List[int]], K: int) -> List[List[int]]:
        
        heap = []
        for point in points:
            heapq.heappush(heap, (point[0] ** 2 + point[1] ** 2, point))
        
        res = []
        for _ in range(K):
            res.append(heapq.heappop(heap)[1])
        
        return res
```