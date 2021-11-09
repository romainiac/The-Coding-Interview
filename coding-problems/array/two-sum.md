# Two Sum

[LeetCode link](https://leetcode.com/problems/two-sum/)

## **Problem**

Given an array of integers `nums` and an integer `target`, return indices of the two numbers such that they add up to `target`.

You may assume that each input would have ***exactly* one solution**, and you may not use the same element twice.

You can return the answer in any order.

<br>

### **Example 1**
```
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Output: Because nums[0] + nums[1] == 9, we return [0, 1].
```


### **Example 2**
```
Input: nums = [3,2,4], target = 6
Output: [1,2]
```

### **Example 3**
```
Input: nums = [3,3], target = 6`
Output: [0,1]
```

### **Constraints**

- <code>2 <= nums.length <= 10<sup>4</sup></code>
- <code>-10<sup>9</sup> <= nums[i] <= 10<sup>9</sup></code>
- <code>-10<sup>9</sup> <= target <= 10<sup>9</sup></code>
- <code>There is only 1 valid answer</code>


### **Extra**:
There is a solution that is less than <code>O(n<sup>2</sup>)</code>, can you find it?

<br>

## **Solutions**

### Brute Force

#### Java
```java
public int[] twoSum(int[] nums, int target) {
        
    for (int i = 0; i < nums.length; i++) {
        for (int j = i + 1; j < nums.length; j++) {
            if (nums[i] + nums[j] == target) return new int[] {i, j};
        }
    }
    return null;
}
```

#### Python

```python
def twoSum(self, nums, target):
    for i in range(0, len(nums)):
        for j in range(i + 1, len(nums)):
            if nums[i] + nums[j] == target:
                return [i, j]
        
```

#### Javascript

```javascript
for (let i = 0; i < nums.length; i++) {
        for (let j = i + 1; j < nums.length; j++) {
            if (nums[i] + nums[j] == target) {
                return [i, j]
            }
        }
}
```

#### Complexity Analysis

*Time complexity: O(n^2). For each element, we try to find its complement by looping through the rest of the array which takes O(n) time. Therefore, the time complexity is O(n^2).*

*Space complexity: O(1). The space required does not depend on the size of the input array, so only constant space is used.*

### 2 Pass Hash Table

#### Java

```java
public int[] twoSum(int[] nums, int target) {
    
    Map<Integer, Integer> map = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        map.put(nums[i], i);
    }

    for (int i = 0; i < nums.length; i++) {
        int complement = target - nums[i];
        if (map.containsKey(complement) && map.get(complement) != i) {
            return new int[] { i, map.get(complement) };
        }
    }
    return null;
}
```

#### Complexity Analysis

*Time complexity: O(n). We traverse the list containing nn elements exactly twice. Since the hash table reduces the lookup time to O(1), the overall time complexity is O(n).*

*Space complexity: O(n). The extra space required depends on the number of items stored in the hash table, which stores exactly n elements.*


### 1 Pass Hash Table

#### Java

```java
public int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> map = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        int complement = target - nums[i];
        if (map.containsKey(complement)) {
            return new int[] { map.get(complement), i };
        }
        map.put(nums[i], i);
    }
    return null;
}
```

#### Complexiy Analysis

*Time complexity: O(n). We traverse the list containing nn elements only once. Each lookup in the table costs only O(1) time.*

*Space complexity: O(n). The extra space required depends on the number of items stored in the hash table, which stores at most n elements.*


# Notes

I was confused at first because I did not realize it is ok if a value is overwritten in a hash table. For instance, the example `[3, 5, 3] , 6`. At first thought, putting the second 3 into a hash map will overwrite the first, and you won't have two *unique* 3's to add to 6. The thing I missed was that there would be a second pass of the original array, and not the map. Passsing through the array the second time, it will not matter which 3 is actually mapped. The only thing that matters is that a 3 exists in the map. 

We know we can not achieve better than `O(n)` because we have reached the BCR. Every element needs to be touched at least once.