- [Array](#array)
- [String](#string)
- [Binary Search](#binary-search)
- [HashMap](#hashmap)
- [](#)

### <a name='Array'></a>Array

1. [Rotate Elements by K](https://leetcode.com/problems/rotate-array/description/)
   1. Right rotation by K:
      1. Reverse entire array
      2. Reverse the first 'k' elements
      3. Reverse the rest (from k to end)
   2. Left rotation by K:
      1. Reverse the first 'k' elements
      2. Reverse the rest (from k to end)
      3. Reverse entire array
   <details>
   <summary>Code</summary>
   <div markdown="1">

   ```kotlin
   fun rotate(nums: IntArray, kk: Int): Unit {
       val n = nums.size
       val k = kk%n
       reverse(nums,0,n-1)
       reverse(nums,0,k-1)
       reverse(nums,k,n-1)
   }

   fun reverse(nums: IntArray, s: Int, e: Int){
       var start = s
       var end = e 
       while(start<end){
           nums[start] = nums[end].also { nums[end] = nums[start]}
           start++
           end--
       }
   }
   ```
   </div></details>

2. *[Contains Duplicate](https://leetcode.com/problems/contains-duplicate/solutions/)
   1. Brute Force: `Use Two loops`
      1. TC: O(N^2)
   2. Better: `Sort()`
      1. TC: O(N*logN)
   3. Optimal: `HashSet or HashMap`
      1. TC: O(N), SC: O(N)

3. [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/description/)
   1. Use binary search and keep moving start and end based on sorted part conditions
   <details>
   <summary>Code</summary>
   <div markdown="1">

   ```kotlin
   fun search(nums: IntArray, x: Int): Int {
       var n = nums.size
       var start = 0
       var end = n-1
       while(start<=end){
           val mid = (start+end)/2
           if(nums[mid]==x) return mid
           if(nums[start]<=nums[mid]){
               //left half is sorted
               if(nums[start]<=x && x<nums[mid]){
                   //element is sorted part
                   end = mid-1
               }else{
                   start = mid+1
               }
           }else{
               //right half is sorted
               if(nums[mid]<x && x<=nums[end]){
                   //element is sorted part
                   start = mid+1
               }else{
                   end = mid-1
               }
           }
       }
       return -1
   }
   ```
   </div></details>

4. *[Insert Interval](https://leetcode.com/problems/insert-interval/)
   1. Optimal:
      1. Add all intervals ending before newOne start
      2. Merge the overlapping ones
      3. Add the rest left over intervals
   <details>
   <summary>Code</summary>
   <div markdown="1">

   ```kotlin
   fun insert(intervals: Array<IntArray>, newInterval: IntArray): Array<IntArray> {
       var n = intervals.size
       val ans = mutableListOf<IntArray>()
       //add intervals ending before newOne 
       var i = 0
       while(i<n && intervals[i][1]<newInterval[0]){
           ans.add(intervals[i])
           i++
       }
       //merge the overlapping ones
       var start = newInterval[0]
       var end = newInterval[1]
       while(i<n && intervals[i][0]<=end){
           start = minOf(intervals[i][0],start)
           end = maxOf(intervals[i][1],end)
           i++
       }
       ans.add(intArrayOf(start,end))
       //add the rest intervals
       while(i<n){
           ans.add(intervals[i])
           i++
       }
       return ans.toTypedArray()
   }
   ```
   </div></details>

5. [Non-overlapping Intervals](https://leetcode.com/problems/non-overlapping-intervals/description/)
   1. Optimal:
      1. Sort by end
      2. Create pairEnd and update it based on `if(intervals[0] >= pairEnd)`
   <details>
   <summary>Code</summary>
   <div markdown="1">

   ```kotlin
   fun eraseOverlapIntervals(intervals: Array<IntArray>): Int {
       intervals.sortBy { it[1] }
       var count = 0
       var pairEnd = Int.MIN_VALUE
       for(interval in intervals){
           if(interval[0]>=pairEnd){
               pairEnd = interval[1]
           }else{
               count++
           }
       }
       return count
   }
   ```
   </div></details>

6. [Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/description/)
   1. Optimal:
      1. Create Prefix Array, & Postfix Array
      2. Merge them to create Output Array
      3. TC: O(3*N), SC: O(2*N) (excluding output array)
   2. Optmial More:
      1. Create output array, store Prefix product first and then update with PostFix
      2. TC: O(2*N), SC: O(1)
   <details>
   <summary>Code</summary>
   <div markdown="1">

   ```kotlin
   fun productExceptSelf(nums: IntArray): IntArray {
       var n = nums.size
       var output = IntArray(n)
       var prefix = 1
       for(i in 0 until n){
           output[i] = prefix
           prefix *= nums[i]
       }
       var postfix = 1
       for(i in n-1 downTo 0){
           output[i] *= postfix
           postfix *= nums[i]
       }
       return output
   }
   ```
   </div></details>

7. [Container With Most Water](https://leetcode.com/problems/container-with-most-water/description/)
   1. Use Two pointers, start and end and fetch height of left and right
   2. store max in `ans=maxOf(ans, (end-start)*minOf(left,right))`
   <details>
   <summary>Code</summary>
   <div markdown="1">

   ```kotlin
   fun maxArea(height: IntArray): Int {
       var start = 0
       var end = height.size-1
       var ans = 0
       while(start<end){
           var left = height[start]
           var right = height[end]
           ans = maxOf(ans, (end-start)*minOf(left,right))
           if(left>right){
               end--
           }else{
               start++
           }
       }
       return ans
   }
   ```
   </div></details>

8. [Daily Temperatures](https://leetcode.com/problems/daily-temperatures/description/)
   <details>
   <summary>Code</summary>
   <div markdown="1">

   ```kotlin
   fun dailyTemperatures(arr: IntArray): IntArray {
       var n = arr.size
       var result = IntArray(n){0}
       var stack = Stack<Int>()
       for(i in arr.indices){
           while(stack.isNotEmpty() && arr[stack.peek()]<arr[i]){
               var index = stack.pop()
               result[index] = i-index
           }
           stack.push(i)
       }
       return result
   }
   ```
   </div></details>

9. [Next Greater Element I](https://leetcode.com/problems/next-greater-element-i/description/)
   <details>
   <summary>Code</summary>
   <div markdown="1">

   ```kotlin
   fun nextGreaterElement(nums1: IntArray, nums2: IntArray): IntArray {
       val n = nums1.size
       var map = hashMapOf<Int,Int>()
       var stack = Stack<Int>()
       for(num in nums2){
           while(stack.isNotEmpty() && stack.peek() < num){
               map.put(stack.pop(), num)
           }
           stack.push(num)
       }
       for(i in nums1.indices){
           nums1[i] = map.getOrDefault(nums1[i], -1)
       }
       return nums1
   }
   ```
   </div></details>

10. [Next Greater Element II](https://leetcode.com/problems/next-greater-element-ii/description/)
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
    fun nextGreaterElements(nums: IntArray): IntArray {
        var stack = Stack<Int>()
        val n = nums.size
        var res = IntArray(n){-1}
        for(i in 0 until n*2){
            var curIndex = i%n
            while(stack.isNotEmpty() && nums[stack.peek()] < nums[curIndex]){
                var index = stack.pop()
                res[index] = nums[curIndex]
            }
            if(i<n){
                stack.push(curIndex)
            }
        }
        return res
    }
    ```
    </div></details>

11. [Grid Unique Paths II](https://leetcode.com/problems/unique-paths-ii/)
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
    fun uniquePathsWithObstacles(grid: Array<IntArray>): Int {
        var row = grid.size
        var col = grid[0].size
        val arr = IntArray(col)
        arr[0] = 1

        for(i in 0 until row){
            for(j in 0 until col){
                if(grid[i][j]==1){
                    arr[j] = 0
                }else if(j>0){
                    arr[j] = arr[j] + arr[j-1]
                }
            }
        }
        return arr[col-1]
    }
    ```
    </div></details>

12. [Spiral Matrix](https://leetcode.com/problems/spiral-matrix/)
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
    fun spiralOrder(matrix: Array<IntArray>): List<Int> {
        var col = matrix[0].size
        var row = matrix.size
        var top = 0
        var left = 0
        var bottom = row-1
        var right = col-1
        var ans = mutableListOf<Int>()
        while(top<=bottom && left<=right){
            for(i in left..right)   ans.add(matrix[top][i])
            top++
            for(i in top..bottom)   ans.add(matrix[i][right])
            right--
            if(top<=bottom) {
                for(i in right downTo left)   ans.add(matrix[bottom][i])
                bottom--
            }
            if(left<=right) {
                for(i in bottom downTo top)   ans.add(matrix[i][left])
                left++
            }
        }
        return ans
    }
    ```
    </div></details>

### <a name='String'></a>String
### <a name='BinarySearch'></a>Binary Search
### <a name='HashMap'></a>HashMap
### 

