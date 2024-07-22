```python
import timeit 

# Test data 
nums = list(range(1000000)) + [1] 
# Large list with a duplicate 

# Original approach 
def original_solution(nums): 
	uniques = set() 
	for num in nums: 
		if num in uniques: 
			return True 
		uniques.add(num) 
	return False 

# Optimized approach 
def optimized_solution(nums):
	return len(nums) != len(set(nums)) 
	
# Measure time 
print("Solution 1:", timeit.timeit(lambda: original_solution(nums), number=10)) 
print("Solution 2:", timeit.timeit(lambda: optimized_solution(nums), number=10))
```