# Leetcode-Python-2024
Solution for All Leetcode DSA practice questions for 2024.

Zero to Hero in Leetcode DSA in 2024.

## [169. Majority Element](https://leetcode.com/problems/majority-element/description/?envType=daily-question&envId=2024-02-12)
```python
### Return the majority element in a list
"""
Input: nums = [3,2,3]
Output: 3
"""
class Solution:
    def majorityElement(self, nums:List[int])->int:
        # O(n); Use hash table with frequency as value
        counter_arr = {}
        for element in nums:
            if element in counter_arr:
                counter_arr[element]+=1
            else:
                counter_arr[element]=1
        return max(counter_arr, key=counter_arr.get)
```



# Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.


# License
[MIT](https://choosealicense.com/licenses/mit/)
