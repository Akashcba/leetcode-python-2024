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
#### Best Solution using O(n) time and O(1) space
```python
# Boyer-Moore Majority Vote Algorithm
# This algorithm works on the fact that if an element occurs more than N/2 times, it means that
# the remaining elements other than this would definitely be less than N/2
class Solution:
    def majorityElement(self, nums:List[int])->int:
        candidate=None
        count=0
        for element in nums:
            if candidate is None or count==0:
                candidate=element
                count+=1
            elif element==candidate:
                count+=1
            else:
                count-=1
        return candidate
```

## [26. Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/description/)
```python
# Noob solution Use set and [:] for inplace operaion in python
class Solution:
    def removeDuplicates(self, nums:List[int])->int:
        nums[:] = sorted(set(nums))
        return len(nums)
```
### Best Solution O(N)time and O(1) space
```python
# Two Pointer solution
class Solution:
    def removeDuplicates(self, nums:List[int])->int:
        # Check for empty lists
        if len(nums)==0:
            return 0
        unique = i= 1
        for i in range(1,len(nums)):
            if nums[i] != nums[i-1]:
                # Use unique as key for unique index
                nums[unique] = nums[i]
                unique+=1
        return unique
```
## [2108. Find First Palindromic String in the Array](https://leetcode.com/problems/find-first-palindromic-string-in-the-array/description/?envType=daily-question&envId=2024-02-13)
```python
# Noob's Solution
# Time Complexity = O(n.m); n is the no. of words and m is the length of words
# Space complexity =
class Solution:
    def firstPalindrome(self, words:List[str])->str:
        for word in words:
            if word[:] == word[::-1]:
                # Return First Palindrome
                return word
        ## Palindrome not found return empty string
        return ""
```
### Optimal Solution Using Two Pointers
```python
# Two Pointer Solution
# Time Complexity = O(n.m); n is the no. of words and m is the length of words
# Space complexity = O(1)
class Solution:
    def check_palindrome(self,word:str)->bool:
        i,j = 0,len(word)-1
        while(i<=j):
            if word[i] == word[j]:
                i+=1
                j-=1
            else:
                return False
        return True
    def firstPalindrome(self, words:List[str])->str:
        for word in words:
            if self.check_palindrome(word):
                return word
        ## Palindrome not found return empty string
        return ""
```

# Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.


# License
[MIT](https://choosealicense.com/licenses/mit/)
