Given an `int[]` called `numbers`, return `true` if any value appears <u>at least twice</u> in the array.
Return `false` if every element is distinct.

Examples
```
Input :: nums = [1, 2, 3, 1]
Output :: true

Input :: nums = [1, 2, 3, 4]
Output :: false

Input :: nums = [1,1,1,3,3,4,3,2,4,2]
Output :: true

```

Solution
```python
def containsDuplicate(self, nums: List[int]) -> bool:
	unique = set()
	for i in nums:
		if i in uniques
			return True
		else:
			uniques.add(i)
	return False
```

Seems to perform fine, runs in linear time, benefits from using sets
Not sure if there is much improvement to be made.
- Beats 27% by runtime
- Beats 43% by memory

Solution II
```python
def containsDuplicates(self, nums: List[int]) -> bool:
	return len(nums) != len(set(nums))
```

This also seems to perform fairly well
- Beats 59% by runtime
- Beats 43% by memory