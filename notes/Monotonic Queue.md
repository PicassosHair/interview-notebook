# Monotonic Queue

A monotonic Queue is a data structure the elements from the front to the end is strictly either increasing or decreasing. 

## Question List
239. Sliding Window Maximum


## Leetcode Solution
### Leetcode 239: Sliding Window Maximum
#### Window and Queue
![image](https://assets.leetcode.com/users/images/9bc84997-2667-4e3f-9b30-b5e6202b831e_1609624629.6404312.png)
**Note: Yellow part is the window**.

#### Code
```python
class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        
		# Construct the Monotonic decreasing queue
        queue = collections.deque()
        for i in range(k-1):
		    # When queue[-1] < nums[i], pop queue[-1] to keep decreasing order
			# Cannot use <= here, since it will fail when run against cases like [2,2,1,2], k=2
            while queue and queue[-1] < nums[i]:
                queue.pop()
            queue.append(nums[i])
        
        res = []
        for i in range(k-1, len(nums)):
		    # Add the new element of the window 
            while queue and queue[-1] < nums[i]:
                queue.pop()
            queue.append(nums[i])
			
			# Append the max value (queue[0]) to the result
            res.append(queue[0])
            
			# Pop the old element of the window
			# Pop only when queue[0] == nums[i-k+1], since it may already be popped 
            if queue[0] == nums[i-k+1]:
                queue.popleft()
        
        return res
```

