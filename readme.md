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
"""
Remove duplicates from a sorted array and return the number of unique elements.
"""
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
"""
Return the first palindrome in the list of strings.
"""
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
### Solution Using Two Pointers
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
## [1. Two Sum](https://leetcode.com/problems/two-sum/description/)
```python
class Solution:
    def twoSum(self,nums:List[int],target:int)->List[int]:
        # Brute Force Slution O(n^2)
        for i in range(0, len(nums)-1):
            for j in range(i+1, len(nums)):
                if nums[i]+nums[j]==target:
                    return [i, j]
        return ""
```
#### Optimal Solution using Dictionary/Hashmap. O(n) time complexity and O(n) space complexity
```python
# Using hashmap
class Solution:
    def twoSum(self, nums:List[int], target:int)->List[int]:
        # Create empty hashmap
        hash_map={}
        for i in range(0,len(nums)):
            if nums[i] in hash_map:
                return [i, hash_map[nums[i]]]
            else:
                hash_map[target - nums[i]]=i
        return []
```

## [35. Search Insert Position](https://leetcode.com/problems/search-insert-position/description/)
```python
"""
Sorted array of integers
Search for the target in the sorted array in O(log n)
If not found retrun its possible index
"""
# Using Binary Search Logic
# Time Complexity : O(log n)
# Space Compleity : O(1)
class Solution:
    def searchInsert(self, nums:List[int],target:int)->int:
        low,high=0,len(nums)-1
        while(low<=high):
            mid = (low+high)//2
            if nums[mid]==target:
                return mid
            elif nums[mid]>target:
                high=mid-1
            else:
                low=mid+1
        # Return nearest index for target if not in nums
        if target<nums[mid]:
            return mid
        else:
            return mid+1
```

## [66. Plus One](https://leetcode.com/problems/plus-one/description/)
```python
"""
large integer represented as array - left to right
increment (add) the number by 1
"""
# O(n) solution
class Solution:
    def plusOne(self, nums:List[int])->List[int]:
        carry,j=0,len(nums)-1
        while(j>=0):
            if j==len(nums)-1:
                nums[j] = nums[j]+1
            else:
                nums[j]+=carry
            if nums[j]>9:
                carry=1
            else:
                carry=0
            j-=1
        if carry==1:
            nums[:] = [1]+nums[:]
        return nums
```
#### Solution using bt manipulation
```python
class Solution:
    def plusOne(self, nums:List[int])->List[int]:
        s = [str(i) for i in nums]
        digit = int("".join(s))
        print(digit)
        ## Add 1 using bit manipulation
        def addOne(x) :
            m = 1
            # Flip all the set bits
            # until we find a 0 
            while(x & m):
                x = x ^ m
                m <<= 1        
            # flip the rightmost 
            # 0 bit 
            x = x ^ m
            return str(x)
        res =  addOne(digit)
        # print(res)
        return list(map(int, str(res)))
```

## [88. Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/description/)
```python
"""
Merge Two sorted arrays into a single sorted array
"""
# Operations need to be inplace
class  Solution:
    def merge(self, nums1:List[int],m:int,nums2:List[int],n:int)->None:
        # Use two pointers
        # Start additions from right to left
        i,j=m-1,n-1
        # k is pointer to end of nums1
        k=m+n-1
        while(j>=0):
            # i>=0 handles cases when m=0
            if i>=0 and nums1[i] > nums2[j]:
                nums1[k] = nums1[i]
                k-=1
                i-=1
            else:
                nums1[k] = nums2[j]
                k-=1
                j-=1
```
## [118. Pascal's Triangle](https://leetcode.com/problems/pascals-triangle/description/)
```python
"""
Return first num_rows of pascals triangle
class Solution:
    def generate(self,numRows:int)->List[List[int]]:
        for i in range(0,numRows):
            if i==0:
                pascal_tri.append([1])
            elif i==1:
                pascal_tri.append([1,1])
            else:
                ls = [0]*(i+1)
                pascal_triangle
"""
```
## [121. Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/description/)
```python
# Time Complexity : O(n)
# Space Complexity : O(1)
class Solution:
    def maxProfit(self,prices:List[int])->int:
        max_profit=0
        min_price=prices[0]
        for i in range(1,len(prices)):
            # check for any lower value of min price
            if min_price > prices[i]:
                min_price=prices[i]
            # checck for maximum of max profit
            if max_profit < prices[i]-min_price:
                max_profit=prices[i]-min_price
        return max_profit
```

# Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.


# License
[MIT](https://choosealicense.com/licenses/mit/)
