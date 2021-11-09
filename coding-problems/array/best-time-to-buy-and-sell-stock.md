# Best Time to Buy and Sell Stock

[LeetCode link](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

`easy`

## **Problem**

You are given an array `prices` where `prices[i]` is the price of a given stock on the `ith` day.

You want to maximize your profit by choosing a **single day** to buy one stock and choosing a **different day in the future** to sell that stock.

Return the *maximum profit you can achieve from this transaction*. If you cannot achieve any profit, return `0`.

### **Example 1**

```
Input: prices = [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.
```

### **Example 2**
```
Input: prices = [7,6,4,3,1]
Output: 0
Explanation: In this case, no transactions are done and the max profit = 0.
```

### **Constraints**

- <code>1 <= prices.length <= 10<sup>5</sup></code>
- <code>0 <= prices[i] <= 10<sup>4</sup></code>


## **Solutions**

### **Brute Force**

#### Java


```java
public int maxProfit(int[] prices) {
    
    int maxProfit = 0;
    for (int i = 0; i < prices.length; i++) {
        for (int j = i + 1; j < prices.length; j++) {
            int profit = prices[j] - prices[i];
            maxProfit = profit > maxProfit ? profit : maxProfit;
        }
    }
    return maxProfit;
}
```

#### **Complexity Analysis**

*This solution is <code>O(n<sup>2</sup>)</code>, and actually times out if running in LeetCode. Is there anyway we can do this with one pass?*

### **One Pass**

#### Java
```java
public int maxProfit(int[] prices) {
    
    int maxProfit = 0;     
    int buyPrice = prices[0];
    for (int i = 1; i < prices.length; i++) {
        
        // check if new buy price is lower than current
        buyPrice = prices[i] < buyPrice ? prices[i] : buyPrice;
        // check if new, higher profit can be found
        maxProfit = prices[i] - buyPrice > maxProfit ? prices[i] - buyPrice : maxProfit;
    }
    
    return maxProfit;
}
```
#### **Complexity Analysis**

*This solution is `O(n)`. It simple requires one pass through the array, keeping track of the lowest buy price, and updating the max profit if a new one is found*

### **One Pass (Faster)**

#### Java
```java
public int maxProfit(int[] prices) {
    
    int maxProfit = 0;     
    int buyPrice = prices[0];
    for (int i = 1; i < prices.length; i++) {
        
        // check if new buy price is lower than current
        buyPrice = prices[i] < buyPrice ? prices[i] : buyPrice;
        // check if new, higher profit can be found
        maxProfit = prices[i] - buyPrice > maxProfit ? prices[i] - buyPrice : maxProfit;
    }
    
    return maxProfit;
}
```
#### **Complexity Analysis**

*This solution is an improvement on the previous one. It only calculates maxProfit if the buy price has not changed. If the buy price changed, that means the element at the current index is the buy price, and there is not need to compare. It also only sets the new buy price when a new low price has been found.*

### **Kadane's Algorithm**

#### Java
```java
public int maxProfit(int[] prices) {
    int maxCur = 0, maxSoFar = 0;
    for(int i = 1; i < prices.length; i++) {
        maxCur = Math.max(0, maxCur += prices[i] - prices[i-1]);
        maxSoFar = Math.max(maxCur, maxSoFar);
    }
    return maxSoFar;
}
```
#### **Complexity Analysis**

*This solution is pretty much the same as the `One Pass` solution, except that it utilizes Kadane's algorithm. Even though the original solution works based on the constraints, if the constraints were changes such that the price of a stock could be negetive such as`{1, 6, -3, 7}`, it would no longer work.*


