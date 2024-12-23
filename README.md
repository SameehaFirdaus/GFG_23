# GFG_23
---
Difficulty: Medium  
Source: 160 Days of Problem Solving  
Tags:
  - Arrays
  - Divide and Conquer
  - Sorting
---


# 🚀 _Day 23. Count Inversions_ 🧠
The problem can be found at the following link: [Problem Link](https://www.geeksforgeeks.org/batch/gfg-160-problems/track/sorting-gfg-160/problem/inversion-of-array-1587115620)

## 💡 **Problem Description:**

Given an array of integers `arr[]`. Find the **Inversion Count** in the array.  

Two elements `arr[i]` and `arr[j]` form an inversion if `arr[i] > arr[j]` and `i < j`.  

Inversion Count indicates how far (or close) the array is from being sorted:
- If the array is already sorted, the inversion count is 0.
- If the array is sorted in reverse order, the inversion count is maximum.

## 🔍 **Example Walkthrough:**

**Input:**  
`arr[] = [2, 4, 1, 3, 5]`  
**Output:**  
`3`

**Explanation:**  
The sequence `2, 4, 1, 3, 5` has three inversions: (2, 1), (4, 1), (4, 3).


**Input:**  
`arr[] = [2, 3, 4, 5, 6]`  
**Output:**  
`0`

**Explanation:**  
The array is already sorted, so there are no inversions.


**Input:**  
`arr[] = [10, 10, 10]`  
**Output:**  
`0`

**Explanation:**  
All elements of the array are the same, so there are no inversions.


### Constraints:
- $`1 ≤ arr.size() ≤ 10^5`$ 
- $`1 ≤ arr[i] ≤ 10^4`$  

## 🎯 **My Approach:**

1. **Merge Sort-Based Counting**:  
   - The problem can be efficiently solved using a modified **Merge Sort** algorithm.
   - During the merge step, count the number of inversions based on the positions of elements in the two halves.

2. **Steps:**  
   - **Divide:** Recursively divide the array into two halves.  
   - **Merge:** Merge the two halves while counting inversions.  
   - **Count Inversions:** For every pair `(i, j)` where `arr[i] > arr[j]` and `i < j`, increment the count.  

3. **Advantages:**  
   - This approach efficiently counts inversions with a time complexity of **O(n log n)**, compared to the naive **O(n^2)** method.  

## 🕒 **Time and Auxiliary Space Complexity** 

- **Expected Time Complexity:** O(n log n), as the algorithm performs a logarithmic number of merge steps, with each step taking linear time.  
- **Expected Auxiliary Space Complexity:** O(n), as we use an additional array for temporary storage during the merge process.


## 📝 **Solution Code**
## Code (Python)

```python
class Solution:
    def mergeAndCount(self, arr, temp, left, mid, right):
        i, j, k = left, mid + 1, left
        inversions = 0

        while i <= mid and j <= right:
            if arr[i] <= arr[j]:
                temp[k] = arr[i]
                i += 1
            else:
                temp[k] = arr[j]
                j += 1
                inversions += (mid - i + 1)
            k += 1

        while i <= mid:
            temp[k] = arr[i]
            i += 1
            k += 1

        while j <= right:
            temp[k] = arr[j]
            j += 1
            k += 1

        for i in range(left, right + 1):
            arr[i] = temp[i]

        return inversions

    def mergeSortAndCount(self, arr, temp, left, right):
        inversions = 0
        if left < right:
            mid = left + (right - left) // 2

            inversions += self.mergeSortAndCount(arr, temp, left, mid)
            inversions += self.mergeSortAndCount(arr, temp, mid + 1, right)
            inversions += self.mergeAndCount(arr, temp, left, mid, right)
        return inversions

    def inversionCount(self, arr):
        n = len(arr)
        temp = [0] * n
        return self.mergeSortAndCount(arr, temp, 0, n - 1)
```
