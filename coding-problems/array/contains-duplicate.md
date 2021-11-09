# Contains Duplicate

[LeetCode link](https://leetcode.com/problems/contains-duplicate/)

`easy`

## **Problem**

Given an integer array `nums`, return `true` if any value appears **at least twice** in the array, and return `false` if every element is distinct.

### **Example 1**
```
Input: nums = [1,2,3,1]
Output: true
```

### **Example 2**
```
Input: nums = [1,2,3,4]
Output: false
```

### **Example 3**
```
Input: nums = [1,1,1,3,3,4,3,2,4,2]
Output: true
```

### **Constraints**

- <code>1 <= nums.length <= 10<sup>5</sup></code>
- <code>-10<sup>9</sup> <= nums[i] <= 10<sup>9</sup></code>

## **Solutions**

### Creating a Set

#### Java
```java
public boolean containsDuplicate(int[] nums) {
    Set<Integer> set = new HashSet<>();
    for (int num : nums) {
        if (set.contains(num)) return true;
        set.add(num);
    }
    return false;
}
```


#### Complexity Analysis

*This is pretty much the definition of a set and how it works. Sets cannot contain duplicates, would could have used an ArrayList if we wanted to, but HashSet lookup is faster*

*Time complexity : O(n). We do `search()` and `insert()` for `n` times and each operation takes constant time.*

*Space complexity : O(n). The space used by a hash table is linear with the number of elements in it.*