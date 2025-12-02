<!-- vscode-markdown-toc -->
- [Important Notes](#important-notes)
- [Day 1: Array I](#day-1-array-i)
- [Day 2: Array II](#day-2-array-ii)
- [Day 3: Array III](#day-3-array-iii)
- [Day 4: Array IV](#day-4-array-iv)
- [Day 5: Linked List](#day-5-linked-list)
- [Day 6: Linked List II](#day-6-linked-list-ii)
- [Day 7: Linked List, Arrays](#day-7-linked-list-arrays)
- [Day 8: Greey Algorithm](#day-8-greey-algorithm)
- [Day 9: Recursion](#day-9-recursion)
- [Day 10: Recursion, Backtracking](#day-10-recursion-backtracking)
- [Day 11](#day-11)
- [Day 12: Heaps](#day-12-heaps)
- [Day 13: Stack and Queues](#day-13-stack-and-queues)
- [Day 14: Stack and Queues II](#day-14-stack-and-queues-ii)
- [Day 15: String](#day-15-string)
- [Day 16: String II](#day-16-string-ii)
- [Day 17: Binary Tree](#day-17-binary-tree)
- [Day 18: Binary Tree II](#day-18-binary-tree-ii)
- [Day 19: Binary Tree III](#day-19-binary-tree-iii)
- [Day 20: Binary Search Tree](#day-20-binary-search-tree)
- [Day 21: Binary Search Tree II](#day-21-binary-search-tree-ii)
- [Day 22: Binary Tree (Miscellaneous)](#day-22-binary-tree-miscellaneous)
- [Day 23: Graph](#day-23-graph)
- [Day 23: Graph II](#day-23-graph-ii)

<!-- vscode-markdown-toc-config
	numbering=false
	autoSave=true
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc -->
### <a name='ImportantNotes'></a>Important Notes
1. Algorithms
   1. Greedy:
      1. Optimization probelms which either demand minimum result or maximum result.
      2. Feasible Solution: Solutions which satisfying the given contraint, can be multiple feasible solution for a problem.
      3. Optimization Solution: Solution which is already feasible but gives the minimum/maximum result.
      4. Minimization Problem: Problem demands result should be minimum.
      5. Maximization Problem: Problem demands result should be maximum.
      5. Optimization Problem: Problem demands result to be minimized or maximized.
2. Data Structures
   1. Heap:
   2. Monotonic Stack: 
      1. A monotonic stack is a type of stack data structure that is either entirely non-increasing or non-decreasing.
      2. Useful for:
         1. Next Greater/Next Smaller
         2. Histogram Problems
         3. Stock Span
         4. Sliding Window: Helps in maintaining the maximum value in a sliding window efficiently.
     
3. Types:
   1. `Interval problems`
      1. Sorting: Most problems require sorting intervals by the start time.
      2. Edge Cases: Test with single intervals, completely overlapping intervals, and adjacent intervals.
      3. Efficient Merging: Use a stack or list to merge intervals efficiently.
      4. Two Pointers: Common for overlapping or meeting room problems.


### <a name='Day1'></a>Day 1: Array I
1. [Set Matrix Zero](https://leetcode.com/problems/set-matrix-zeroes/)
    1. Brute Force:
        1. Iterate matrix and when found 0, mark all the elements of same row and col as -1. 
        2. Iterate whole matrix again and convert all -1 to 0
        3. TC: O(M*N)*O(M+N)+O(M*N), SC: O(n)
    2. Better:
        1. Create a seperate array of row[m] and col[n]
        2. Iterate matrix and mark -1 of arrays indexes at the corresponding 0's found.
        3. Iterate matrix and use arrays to update it
        4. TC: O(2*M*N), SC: O(N)+O(M)
            <details>
            <summary>Code</summary>
            <div markdown="1">
            ```kotlin
            fun setZeroes(matrix: Array<IntArray>): Unit {
                val m = matrix.size
                val n = matrix[0].size
                var row = IntArray(m){0}
                var col = IntArray(n){0}
                for(i in 0 until m){
                    for(j in 0 until n){
                        if(matrix[i][j] == 0){
                            row[i] = -1
                            col[j] = -1
                        }
                    }
                }
                for(i in 0 until m){
                    for(j in 0 until n){
                        if(row[i] == -1 || col[j] == -1){
                            matrix[i][j] = 0
                        }
                    }
                }
            }
            ```
            </div></details>
    3. Optimal:
        1. Use 1st row and column as place holder for i,j
        2. Use col0 to hold 0 in j
        3. Update (1,1) to (m,n) using 1st row and col values
        4. Update 1st row using [0,0] and 1st col using col0
            <details>
            <summary>Code</summary>
            <div markdown="1">
            ```kotlin
            fun setZeroes(matrix: Array<IntArray>): Unit {
                    val m = matrix.size
                    val n = matrix[0].size
                    var col0 = -1
                    for(i in 0 until m){
                        for(j in 0 until n){
                            if(matrix[i][j] == 0){
                                if(j==0) 
                                    col0 = 0
                                else
                                    matrix[0][j] = 0
                                matrix[i][0] = 0
                            }
                        }
                    }
                    //(1,1) to (m,n)
                    for(i in 1 until m){
                        for(j in 1 until n){
                            if(matrix[i][0] == 0 || matrix[0][j] == 0){
                                matrix[i][j] = 0
                            }
                        }
                    }
                    //first row and col
                    if(matrix[0][0]==0){
                        for(i in 0 until n)
                            matrix[0][i] = 0
                    }
                    if(col0 == 0){
                        for(i in 0 until m)
                            matrix[i][0] = 0
                    }
                }
            ```
            </div></details>
2. [Next Permutation](https://leetcode.com/problems/next-permutation/description/)
    1. Brute Force:
        1. Generate all the sorted permutations
        2. Linear Search the current
        3. Return next or first if last
        4. TC: O(N!*N), N! = N factorial
    2. Optimal:
        1. Ex: `2,1,5,3,0,0`
        2. Longest prefix match as possible/breakpoint: `a[i] < a[i+1]: 1,5`
        3. find >i, but the smallest one: `3`, so that you stay close
        4. Try to place remaining in sorted order
            <details>
            <summary>Code</summary>
            <div markdown="1">

            ```kotlin
            fun nextPermutation(nums: IntArray): Unit {
                var bp = -1
                val n = nums.size
                //1 find the breaking point
                for(i in (n-2) downTo 0){
                    if(nums[i]<nums[i+1]){
                        bp = i
                        break
                    }
                }
                //2 find smallest bigger number
                if(bp>=0){
                    for(i in (n-1) downTo bp){
                        if(nums[i]>nums[bp]){
                            swap(nums,i,bp)
                            break
                        }
                    }
                }
                //3 revserse the left numbers
                reverse(nums,bp+1)
            }

            fun reverse(nums: IntArray,start: Int){
                var i = start
                var j = nums.size-1
                while(i<j){
                    swap(nums,i,j)
                    i++
                    j--
                }
            }

            fun swap(nums: IntArray,i: Int, j:Int){
                val temp = nums[i]
                nums[i] = nums[j]
                nums[j] = temp
            }
            ```
            </div></details>
3. [Kadane's' Algorithm](https://leetcode.com/problems/maximum-subarray/description/)
    1. Brute Force:
        1. Use 2 loops to get start and end index of subarray.
        2. Use 1 loop to sum of that sub array from start to end
        3. TC: O(N^3) 
    2. Better:
        1. We can remove the third loop by adding the new item into previous sum of subarray, `sum+=arr[j]`, and get `maxOf(sum,max)`
        2. TC: O(N^2)
    3. Optimal: Kadane's algorithm
        1. The intuition of the algorithm is not to consider the subarray as a part of the answer if its sum is less than 0.
        2. TC: O(N)
            <details>
            <summary>Code</summary>
            <div markdown="1">

            ```kotlin    
            fun maxSubArray(nums: IntArray): Int {
                var max = Int.MIN_VALUE
                var sum = 0
                for(i in 0 until nums.size){
                    sum+=nums[i]
                    max = maxOf(sum,max)
                    if(sum<0) sum = 0
                }
                return max
            }
            ```
            </div></details>
4. [Sort Colors](https://leetcode.com/problems/sort-colors/description/)
    1. Brute Force:
       1. Sort the array
       2. TC: O(N*logN)
    2. Better:
       1. Count the occurence of 0,1,2 and put it again
       2. TC: O(N)+O(N)
    3. Optimal: Three Pointer & Dutch National Flag Algorithm
       1. TC: O(N)
        <details>
        <summary>Code</summary>
        <div markdown="1">

        ```kotlin
        //three pointer
        fun sortColors(nums: IntArray): Unit {
            var one = -1
            var two = -1
            var zero = -1
            for(num in nums){
                when(num){
                    2 -> {
                        nums[++two] = 2
                    }
                    1 ->{
                        nums[++two] = 2
                        nums[++one] = 1
                    }
                    0 ->{
                        nums[++two] = 2
                        nums[++one] = 1
                        nums[++zero] = 0
                    }
                }
            }
        }
        //dutch national flag algorithm
        fun sortColors(nums: IntArray): Unit {
            var low = 0
            var mid = 0
            var high = nums.size-1
            while(mid<=high){
                when(nums[mid]){
                    0 ->{
                        swap(nums,low,mid)
                        low++
                        mid++
                    }
                    1 ->{
                        mid++
                    }
                    2 ->{
                        swap(nums,mid,high)
                        high--
                    }
                }
            }
        }
        ```
        </div></details>
5. [Stock Buy And Sell](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)
    1. Brute Force:
        1. Take two loops and find the max profit
        2. TC: O(N*N)
    2. Optimal:
        1. TC: O(N)
        <details>
        <summary>Code</summary>
        <div markdown="1">

        ```kotlin
        fun maxProfit(prices: IntArray): Int {
            var minLeft = Int.MAX_VALUE
            var profit = 0
            for(price in prices){
                minLeft = minOf(minLeft,price)
                val profitIfSoldToday = price-minLeft
                profit = maxOf(profit, profitIfSoldToday)
            }
            return profit
        }
        ```
        </div></details>
6. [Rotate Elements by K](https://leetcode.com/problems/rotate-array/description/)
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


### <a name='Day2'></a>Day 2: Array II
1. [Rotate Image by 90 degree](https://leetcode.com/problems/rotate-image/description/)
   1. Brute Force: 
      1. Create a new matrix and put items
      2. TC: O(N*N), SC: O(N*N)
   2. Optimal:
      1. Transpose matrix
      2. Reverse the matrix
      3. TC: O(N*N), SC: O(1)
        <details>
        <summary>Code</summary>
        <div markdown="1">

        ```kotlin
        fun rotate(mat: Array<IntArray>): Unit {
            val m = mat.size
            for(i in 0 until m){
                for(j in i until m){
                    val temp = mat[i][j]
                    mat[i][j] = mat[j][i]
                    mat[j][i] = temp
                }
            }
            for(i in 0 until m){
                for(j in 0 until m/2){
                    val temp = mat[i][j]
                    mat[i][j] = mat[i][m-1-j]
                    mat[i][m-1-j] = temp
                }
            }
        }
        ```
        </div></details>
2. [Merge Intervals](https://leetcode.com/problems/merge-intervals/description/)
   1. Brute Force:
      1. Sort if not sorted
      2. Use one loop to iterate all items and another loop to check (i+1,n-1) if they can be merged
      3.  TC: O(N*N)
   2. Optimal:
      1. Sort if not sorted
      2. Insert first item in result, and iterate checking if last[1]>new[0].
      3. If true update last[1] with maxOf(last[1],new[1])
      4. Else insert in list
      5. TC: O(N*logN)+O(N)
        <details>
        <summary>Code</summary>
        <div markdown="1">

        ```kotlin
        fun merge(intervals: Array<IntArray>): Array<IntArray> {
            var ans = mutableListOf<IntArray>()
            intervals.sortBy{ it[0] }
            for(interval in intervals){
                if(ans.isEmpty()){
                    ans.add(interval)
                    continue
                }
                if(ans.last()[1]<interval[0]){
                    ans.add(interval)
                } else {
                    ans.last()[1] = maxOf(ans.last()[1],interval[1])
                }
            }
            return ans.toTypedArray()
        }
        ```
        </div></details>
3. [Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/description/)
   1. Optimal: 
        <details>
        <summary>Code</summary>
        <div markdown="1">

        ```kotlin
        fun merge(nums1: IntArray, mo: Int, nums2: IntArray, no: Int): Unit {
            var m = mo-1
            var n = no-1
            var last = nums1.size-1
            while(m>=0&&n>=0){
                if(nums1[m]>nums2[n]){
                    nums1[last] = nums1[m]
                    m--
                }else{
                    nums1[last] = nums2[n]
                    n--
                }
                last--
            }
            for(i in 0..n)
                nums1[i] = nums2[i]
        }    
        ```
        </div></details>
4. [Find the duplicate in an array of N+1 integers](https://leetcode.com/problems/find-the-duplicate-number/description/)
   1. Brute Force:
      1. Sort the array and iterate to find same consequetive number
      2. TC: O(N*logN)+O(N)
   2. Better:
      1. Using hashset and checking if it already exists.
      2.  TC: O(N), SC: O(N)  
   3. Optimal:
      1. Cannot modify the array: `Floyd's Tortoise and Hare Algorithm: Linked List Cycle Detection`
         1. Use slow and fast pointers and find the cycle
         2. Set fast to nums[0]
         3. move both same till same again
         4. TC: O(N)
            <details>
            <summary>Code</summary>
            <div markdown="1">

            ```kotlin
            fun findDuplicate(nums: IntArray): Int {
                var slow = nums[0]
                var fast = nums[0]
                do{
                    slow = nums[slow]
                    fast = nums[nums[fast]]
                }while(slow!=fast)
                fast = nums[0]
                while(slow!=fast){
                    slow = nums[slow]
                    fast = nums[fast]
                }
                return slow
            }
            ```
            </div></details>
      2. Can modify the array: `Cycle Sort`
5. *[Contains Duplicate](https://leetcode.com/problems/contains-duplicate/solutions/)
   1. Brute Force: `Use Two loops`
      1. TC: O(N^2)
   2. Better: `Sort()`
      1. TC: O(N*logN)
   3. Optimal: `HashSet or HashMap`
      1. TC: O(N), SC: O(N)
6. [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/description/)
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
7. *[Insert Interval](https://leetcode.com/problems/insert-interval/)
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
8. [Non-overlapping Intervals](https://leetcode.com/problems/non-overlapping-intervals/description/)
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
9. []()

### <a name='Day3'></a>Day 3: Array III
1. [Search in a sorted 2D matrix](https://leetcode.com/problems/search-a-2d-matrix/description/)
    1. Brute Force:
        1. Iterate matrix using two loops and find
        2. TC: O(M*N)
    2. Better: `Two Pointers`
        1. Use two pointers, `i at 0,m-1`, `j at (col.size-1,0)` 
        2. If mat[i][j]>target, j--, else i++
        3. TC: O(M+N)
        <details>
        <summary>Code</summary>
        <div markdown="1">

        ```kotlin
        fun searchMatrix(matrix: Array<IntArray>, target: Int): Boolean {
            val m = matrix.size
            val n = matrix[0].size
            var i = 0
            var j = n-1
            while(i<m && j>=0){
                val cur = matrix[i][j]
                if(cur==target) return true
                if(cur>target) j--
                else i++
            }
            return false
        }
        ```
        </div></details>
    3. Optimal: `Treat matrix as flattend array and use binary search`
        1. Put start at 0, and end at m*n-1
        2. Calculate mid, and find the `curItem = matrix[mid/n][mid%n]`
        3. TC: O(log(M*N))
        <details>
        <summary>Code</summary>
        <div markdown="1">

        ```kotlin
        fun searchMatrix(matrix: Array<IntArray>, target: Int): Boolean {
            val m = matrix.size
            val n = matrix[0].size
            var start = 0
            var end = m*n-1
            while(start<=end){
                val mid = start+(end-start)/2
                val cur =  matrix[mid/n][mid%n]
                when {
                    cur==target -> return true
                    cur>target -> end = mid-1
                    cur<target -> start = mid+1
                }
            }
            return false
        }
        ```
        </div></details>
2. [Majority Element n/2](https://leetcode.com/problems/majority-element/)
    1. Brute Force:
        1. Use two loops and find frequency for each element, return when it crosses n/2
        2. TC: O(N*N)
    2. Better:
        1. Use HashMap to store the frequency and keep checking while increasing the count. Stop once it's count reaches n/2
        2. TC: O(N), SC: O(N)
    3. Optimal: `Moore's Voting Algorithm`
        1. Use count, element variables
        2. TC: O(N) 
        <details>
        <summary>Code</summary>
        <div markdown="1">

        ```kotlin
        fun majorityElement(nums: IntArray): Int {
            var count = 0
            var ele = nums[0]
            for(num in nums){
                if(count==0){ ele = num }
                if(num == ele) count++
                else count--
            }
            return ele
        }
        ```
        </div></details>
3. [Majority Element n/3](https://leetcode.com/problems/majority-element-ii/)
    1. Same as n/2
    2. Same as n/2
    3. Optimal: `Extended Boyer Moore’s Voting Algorithm` 
        1. Use c1,e1 & c2,e2 to store the variables as there could be atmost 2 elements that can reach n/3 times
        2. TC: O(N)
        <details>
        <summary>Code</summary>
        <div markdown="1">

        ```kotlin
        fun majorityElement(nums: IntArray): List<Int> {
            var c1 = 0 
            var e1 = Int.MIN_VALUE
            var c2 = 0
            var e2 = Int.MIN_VALUE
            for(num in nums){
                when {
                    c1==0 && e2!=num ->{
                        c1++
                        e1=num
                    }
                    c2==0 && e1!=num ->{
                        e2=num
                        c2++
                    }
                    e1==num -> c1++
                    e2==num -> c2++
                    else -> {
                        c1--
                        c2--
                    }
                }
            }
            c1 = 0
            c2 = 0
            for(num in nums){
                if(num==e1) c1++
                if(num==e2) c2++
            }
            var breakpoint = (nums.size/3+1)
            val ans = mutableListOf<Int>()
            if(c1>=breakpoint) ans.add(e1)
            if(c2>=breakpoint) ans.add(e2)
            return ans.toList()
        }
        ```
        </div></details>
4. [Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/description/)
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
5. [Container With Most Water](https://leetcode.com/problems/container-with-most-water/description/)
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
6. [Daily Temperatures](https://leetcode.com/problems/daily-temperatures/description/)
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
7. [Next Greater Element I](https://leetcode.com/problems/next-greater-element-i/description/)
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
8. [Next Greater Element II](https://leetcode.com/problems/next-greater-element-ii/description/)
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
9. [Grid Unique Paths](https://leetcode.com/problems/unique-paths/)
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
    //using dp + matrix
    fun uniquePaths(m: Int, n: Int): Int {
        val dp = Array(m) { IntArray(n) {1} }

        for(i in 1 until m){
            for(j in 1 until n){
                dp[i][j] = dp[i-1][j] + dp[i][j-1]
            }
        }
        return dp[m-1][n-1]
    }

    //using dp + array
    fun uniquePaths(m: Int, n: Int): Int {
        val dp = IntArray(n) {1}

        for(i in 1 until m){
            for(j in 1 until n){
                dp[j] = dp[j] + dp[j-1]
            }
        }
        return dp[n-1]
    }
    ```
    </div></details>
10. [Grid Unique Paths II](https://leetcode.com/problems/unique-paths-ii/)
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
1.  []()

    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin

    ```
    </div></details>

### <a name='Day4'></a>Day 4: Array IV
1. [2-sum Problem](https://leetcode.com/problems/two-sum/)
   1. Brute Force:
      1. Use two loops and find the pair with target sum.
      2. TC: O(N*N)
   2. Better:
      1. Sort the array and use start and end pointers. 
      2. TC: O(N*logN)
   3. Optimal:
      1. Use hashset store the values and find if difference exists
      2. TC: O(N), SC: O(N)
        <details>
        <summary>Code</summary>
        <div markdown="1">

        ```kotlin
        fun twoSum(nums: IntArray, target: Int): IntArray {
            var map = mutableMapOf<Int,Int>()
            for(i in nums.indices){
                val num = nums[i]
                val dif = target-num
                if(map.contains(dif)){
                    return intArrayOf(map.get(dif)!!,i)
                }
                map[num] = i
            }
            return intArrayOf(-1,-1)
        }
        ```
        </div></details>
2. [4-sum Problem](https://leetcode.com/problems/4sum/)
   1. Brute Force:
      1. Use 4 loops and find all the quads
      2. TC: O(N^4)
   2. Better:
      1. Use 3 loops and set to eliminate 1 loop
      2. TC: O(N^3*log(M)),n-> size of array, m-> number of elements in set
   3. Optimal:
      1. Use two loops and two pointers i.e. start and end
      2. TC: O(N^3)
        <details>
        <summary>Code</summary>
        <div markdown="1">

        ```kotlin
        fun fourSum(nums: IntArray, target: Int): List<List<Int>> {
            val res:MutableList<List<Int>> = mutableListOf()
            nums.sort()
            var n = nums.size
            for(i in 0 until n-3){
                if(i>0 && nums[i]==nums[i-1]) continue
                for(j in i+1 until n-2){
                    if(j>i+1 && nums[j]==nums[j-1]) continue
                    var start = j+1
                    var end = n-1
                    var outerSum = nums[i].toLong()+nums[j].toLong()
                    while(start<end){
                        var sum = outerSum + nums[start].toLong() + nums[end].toLong()
                        when{
                            sum == target.toLong() -> {
                                val ans = listOf(nums[i],nums[j],nums[start],nums[end])
                                res.add(ans)
                                start++
                                end--
                                while(start<end && nums[start]==nums[start-1]) start++
                                while(start<end && nums[end]==nums[end+1]) end--
                            }
                            sum < target.toLong() -> {
                                start++
                            }
                            sum > target.toLong() -> {
                                end--
                            }
                        }
                    }
                }
            }
            return res
        }
        ```
        </div></details>
3. [Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/)
   1. Brute Force:
      1. Use two loops and keep finding the next number storing the count
      2. TC: O(N^2)
   2. Better:
      1. Sort the array and easily find the consecutive sequence
      2. TC: O(N*logN)+O(N)
   3. Optimal:
      1. Using Set data structure
      2. TC: O(N)+O(2*N), SC: O(N)
        <details>
        <summary>Code</summary>
        <div markdown="1">

        ```kotlin
        fun longestConsecutive(nums: IntArray): Int {
            val set = hashSetOf<Int>()
            var max = 0
            set.addAll(nums.toList())
            for(num in set){
                if(!set.contains(num-1)){   
                    //if it exists, it will be covered in its turn with more count
                    var count = 1
                    var cur = num
                    while(set.contains(cur+1)){
                        cur+=1
                        count+=1
                    }
                    maxOf(count,max)
                }
            }
            return max
        }
        ```
        </div></details>
4. [Largest Subarray With K Sum](https://leetcode.com/problems/subarray-sum-equals-k/)
   1. Brute Force:
      1. Use two loops and find sum of all the possible subarrays
      2. TC: O(N)
   2. Optimize: `Prefix Sum`
      1. Use sum to store the sum of all the elements till the current element
      2. Store the sum and its count in HashMap as key and value respectively
      3. Also find if map already contains `sum-k` element, if true add the index to the count
        <details>
        <summary>Code</summary>
        <div markdown="1">

        ```kotlin
        fun subarraySum(nums: IntArray, k: Int): Int {
            var map = HashMap<Int,Int>()
            map.put(0,1)
            var count = 0
            var sum = 0
            for(num in nums){
                sum += num
                if(map.contains(sum-k)){
                    count += map.get(sum-k)!!
                }
                map.put(sum,(map.get(sum)?:0)+1)
            }
            return count
        }
        ```
        </div></details>
5. [Longest Substring Without Repeat](https://leetcode.com/problems/longest-substring-without-repeating-characters/description/)
   1. Brute Force:
      1. Use two loops, first loop to iterate the string first char
      2. Second loop to iterate rest till found same and storing the max
      3. TC: O(N*N)
   2. Optimal:
      1. Use two pointers, `left=0` and `right=0` to create a subarray and `HashSet` to store the chars
      2. Check if set contains the `right`, if true, remove s[left] from set and move left one step
      3. Else add `right` item in set and move right one step.
      4. Update the max with `maxOf(max,set.size)`
        <details>
        <summary>Code</summary>
        <div markdown="1">

        ```kotlin
        fun lengthOfLongestSubstring(s: String): Int {
            var max = 0
            var set = HashSet<Char>()
            if(s.length==0||s.length==1) return s.length
            var start = 0
            var end = 0
            while(end<s.length){
                var cur = s[end]
                if(set.contains(cur)){
                    set.remove(s[start])
                    start++
                }else{
                    set.add(cur)
                    end++
                    max = maxOf(max, set.size)
                }
            }
            return max
        }

        ```
        </div></details>
6. [Spiral Matrix](https://leetcode.com/problems/spiral-matrix/)
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
7. []()

### <a name='Day5'></a>Day 5: Linked List
1. [Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/description/)
   1. Brute Force:
      1. Use another data structure like Stack
      2. Iterate the linked list to store and then iterate to update
      3. TC: O(2N), SC: O(N) 
   2. Optimal
      1. TC: O(N)
        <details>
        <summary>Code</summary>
        <div markdown="1">

        ```kotlin
        //iterative
        fun reverse(head: ListNode?): ListNode?{
            var cur = head
            var prev: ListNode? = null
            while(cur!=null){
                var next = cur.next
                cur.next = prev
                prev = cur
                cur = next
            }
            return prev
        }

        //recursive
        fun reverseList(head: ListNode?): ListNode?{
            if(head==null||head.next==null){
                return head
            }
            var cur = head
            var newHead = reverseList(head.next)
            var next = cur.next
            next.next = cur
            cur.next = null
            
            return newHead
        }
        ```
        </div></details> 
2. [Middle Of Linked List](https://leetcode.com/problems/middle-of-the-linked-list/description/)
   1. Brute Force:
      1. Find the length of the list
      2. Find `mid = length/2+1`, and iterate till mid
      3. TC: O(N+N/2)
   2. Optimal:
      1. Use slow and fast pointers.
      2. Move slow 1 step and fast 2 step, when fast reaches end, slow will be at mid.
        <details>
        <summary>Code</summary>
        <div markdown="1">

        ```kotlin
        fun middleNode(head: ListNode?): ListNode? {
            if(head == null || head.next == null){
                return head
            }
            var slow = head
            var fast = head
            while(fast?.next!=null){
                slow = slow?.next
                fast = fast?.next?.next
            }
            return slow
        }
        ```
        </div></details>
3. [Merge Two sorted List](https://leetcode.com/problems/merge-two-sorted-lists/description/)
   1. Brute Force:
      1. Store all items in array and sort
      2. Create a new linked list using that array
      3. TC: O(N1+N2)+O(N*logN)+O(N)
   2. Optimal
      1. TC: O(N1+N2)
        <details>
        <summary>Code</summary>
        <div markdown="1">

        ```kotlin
        fun mergeTwoLists(list1: ListNode?, list2: ListNode?): ListNode? {
            val dummy = ListNode(-1)
            var res = dummy
            var cur1 = list1
            var cur2 = list2
            while(cur1!=null && cur2!=null){
                if(cur1.`val` > cur2.`val`){
                    res.next = cur2
                    cur2 = cur2?.next
                }else{
                    res.next = cur1
                    cur1 = cur1?.next    
                }
                res = res.next
            }
            if(cur1!=null) res.next = cur1
            if(cur2!=null) res.next = cur2
            return dummy.next
        }
        ```
        </div></details>
4. [Delete nth node from end](https://leetcode.com/problems/remove-nth-node-from-end-of-list/description/)
   1. Brute Force:
      1. Find length of the list
      2. Remove (l-n-1)th item
      3. TC: O(L)+O(L-N)
   2. Optimal
      1. Use slow and fast pointers
      2. Move fast one step `0 until n`
      3. If fast becomes, it's head to be deleted: `return head.next`
      4. Move slow and fast together till `fast.next` becomes null
      5. set `slow.next = slow.next.next`
        <details>
        <summary>Code</summary>
        <div markdown="1">

        ```kotlin
        fun removeNthFromEnd(head: ListNode?, n: Int): ListNode? {
            var slow = head
            var fast = head
            for(i in 0 until n){
                fast = fast?.next
            }
            if(fast==null) //if fast become null, nth node from end is head
                return head?.next

            while(fast?.next!=null){ 
                fast = fast?.next
                slow = slow?.next
            }

            slow?.next = slow?.next?.next
            return head
        }

        ```
        </div></details>
5. [Add Two Numbers](https://leetcode.com/problems/add-two-numbers/)
   1. Optimal
      1. TC: O(maxOf(M,N)), SC: O(maxOf(M,N))
        <details>
        <summary>Code</summary>
        <div markdown="1">

        ```kotlin
        fun addTwoNumbers(l1: ListNode?, l2: ListNode?): ListNode? {
            var first = l1
            var sec = l2
            var dummy = ListNode(-1)
            var ans = dummy
            var isReminder = false
            while(first!=null || sec!=null || isReminder){
                var sum = (first?.`val` ?: 0) + (sec?.`val` ?: 0)
                sum += if(isReminder) 1 else 0
                if(sum>9){
                    isReminder = true
                    sum = sum%10
                }else{
                    isReminder = false
                    sum = sum
                }
                ans.next = ListNode(sum)
                ans = ans.next
                first = first?.next
                sec = sec?.next
            }
            return dummy.next
        }
        ```
        </div></details>
6. [Delete node in linked list](https://leetcode.com/problems/delete-node-in-a-linked-list/description/)
   1. Optimal
      1. TC: O(1)
        <details>
        <summary>Code</summary>
        <div markdown="1">

        ```kotlin
        fun deleteNode(node: ListNode?) {
            node?.next?.`val` = node?.`val`
            node?.next = node?.next?.next
        }
        ```
        </div></details>


### <a name='Day6'></a>Day 6: Linked List II
1. [Find Interaction Point of Y LinkedList](https://leetcode.com/problems/intersection-of-two-linked-lists/description/)
   1. Brute Force:
      1. Just like two loops, put one loop on head and iterate the other who linked list to find if it exists.
      2. Repeat this step for all nodes till found same.
      3. TC: O(M*N)
   2. Better: `Reduce the length`
      1. Find the length of both the linked lists.
      2. Move the bigger list by the difference of their lengths.
      3. Start moving both points same step till found same.
      4. TC: O(2*maxOf(M,N))+O(abs(M,n))+O(minOf(M,N))
        <details>
        <summary>Code</summary>
        <div markdown="1">

        ```kotlin
        fun getIntersectionNode(headA:ListNode?, headB:ListNode?):ListNode? {
            var count1 = 0
            var cur1 = headA
            while(cur1!=null){  //find l1
                cur1 = cur1?.next
                count1++
            }
            var count2 = 0
            var cur2 = headB
            while(cur2!=null){  //finf l2
                cur2 = cur2?.next
                count2++
            }
            if(cur1!=cur2) return null
            cur1 = headA
            cur2 = headB
            if(count1>count2){
                var dif = count1-count2
                for(i in 0 until dif){
                    cur1 = cur1?.next
                }
            }else{
                var dif = count2-count1
                for(i in 0 until dif){
                    cur2 = cur2?.next
                }
            }
            while(cur1!=cur2){
                cur1 = cur1?.next
                cur2 = cur2?.next
            }
            return cur1
        }
        ```
        </div></details>
   3. Optimal:
      1. Put cur1 and cur2 on respective headers
      2. Once one becomes null, move them to next list headers and they will collide at interaction
      3. TC: O(2*maxOf(M,N))
2. [Detect A Cycle In Linked List](https://leetcode.com/problems/linked-list-cycle/description/)
   1. Brute Force:
      1. Store the nodes in hashmap and keep searching if node already exists
      2. TC: O(N*2*log(N)), SC: O(N)
   2. Optimal: `Tortoise and Hare Algorithm`
      1. Move slow and fast pointers till they collide
      2. TC: O(N)
        <details>
        <summary>Code</summary>
        <div markdown="1">

        ```kotlin
        fun hasCycle(head: ListNode?): Boolean {
            if(head==null || head.next == null) return false
            var slow = head
            var fast = head
            while(fast!=null && fast?.next!=null){
                slow = slow?.next
                fast = fast?.next?.next
                if(slow==fast)
                    return true
            }
            return false
        }
        ```
        </div></details>
3. [Reverse Nodes in K Group](https://leetcode.com/problems/reverse-nodes-in-k-group/)
   1. Optimal:
      1. Check if atleast k nodes remaining
      2. Find the tail of the K group
      3. Store the nextHead and break the chain
      4. Reverse the smaller group and find tail of the reversed group
      5. If first group, update newHead with currentGroupHead, else attach the curTail to currentGroupHead
        <details>
        <summary>Code</summary>
        <div markdown="1">

        ```kotlin
        fun reverseKGroup(head: ListNode?, k: Int): ListNode? {
            var cur = head
            var curTail: ListNode? = null
            var newHead: ListNode? = null
            while(cur!=null){
                //check if atleast k nodes remaining
                var count = 0
                var temp = cur
                while(temp != null && count<k){
                    count++
                    temp = temp?.next
                }
                if(count<k){
                    curTail?.next = cur
                    break
                }
                
                //find the tail of group
                var curHead = cur
                for(i in 0 until k-1){
                    cur = cur?.next
                }

                //store the nextHead and break the chain
                var nextHead = cur?.next
                cur?.next = null

                //reverse thes smaller list
                val newGroupHead = reverse(curHead)

                //find tail of revsersed group
                var newGroupTail = newGroupHead
                while(newGroupTail?.next!=null){
                    newGroupTail = newGroupTail?.next
                }

                //if first group, update newHead i.e. answer
                if(newHead == null){
                    newHead = newGroupHead
                }else{
                    //for next groups we need to link curTail
                    curTail?.next = newGroupHead
                }

                curTail = curHead
                curTail?.next = null

                cur=nextHead
            }
            return newHead?:head
        }
        ```
        </div></details>
4. [Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list/)
   1. Brute Force:
      1. Use Stack data structure and push all items in stack
      2. Start checking again from top of stack while iterating start to end in linked list
      3. TC: O(2*N), SC: O(N)
   2. Optimal:
      1. Find the mid and node before mid
      2. Break the connection from before mid to mid
      3. Reverse the linked list from mid
      4. Compare both lists together
      5. TC: O(N/2+N/2+N/2+N/2) = O(2*N)
        <details>
        <summary>Code</summary>
        <div markdown="1">

        ```kotlin
        fun isPalindrome(head: ListNode?): Boolean {
            if(head==null) return false
            if(head?.next == null) return true
            var slow = head
            var fast = head
            var prev: ListNode? = null
            while(fast?.next!=null){
                prev = slow
                slow = slow?.next
                fast = fast?.next?.next
            }
            prev?.next = null
            var halfHead = reverse(slow)
            var cur1 = head
            var cur2 = halfHead
            while(cur1!=null && cur2!=null){
                if(cur1?.`val` != cur2?.`val`){
                    return false
                }
                cur1 = cur1?.next
                cur2 = cur2?.next
            }
            return true
        }
        ```
        </div></details>
5. [Linked List Cycle II/STarting Point of Cycle](https://leetcode.com/problems/linked-list-cycle-ii/)
   1. Brute Force:
      1. Store the items in hashmap and exit as soon as we find the item in map
      2. TC: O(N), SC: O(N)
   2. Optimal: `Tortoise and Hare Algorithm`
      1. Use slow and fast pointers
        <details>
        <summary>Code</summary>
        <div markdown="1">

        ```kotlin
        fun detectCycle(head: ListNode?): ListNode? {
            if(head==null || head?.next==null) return null
            if(head?.next==head) return head
            var slow = head
            var fast = head
            while(fast!=null&&fast?.next!=null){
                slow = slow?.next
                fast = fast?.next?.next
                if(slow == fast) 
                    break
            }
            slow = head
            while(slow!=fast){
                slow = slow?.next
                fast = fast?.next
            }
            return slow
        }
        ```
        </div></details>
6. [Reorder List](https://leetcode.com/problems/reorder-list/description/)
   1. Find mid
   2. Split the list
   3. Reverser second half
   4. Merge both lists
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
    fun reorderList(head: ListNode?): Unit {
        if(head==null || head?.next == null) return
        //find mid
        var slow = head
        var fast = head
        while(fast?.next!=null){
            slow = slow?.next
            fast = fast?.next?.next
        }
        //split
        val firstHalfEnd = slow
        var secondHalfStart = slow?.next
        firstHalfEnd?.next = null
        //reverse second half
        secondHalfStart = reverse(secondHalfStart)
        //merge both
        var p1 = head
        var p2 = secondHalfStart
        while (p2 != null) {
            val next1 = p1?.next
            val next2 = p2?.next
            p1?.next = p2
            p2?.next = next1
            p1 = next1
            p2 = next2
        }
    }
    ```
    </div></details>

### <a name='Day7'></a>Day 7: Linked List, Arrays
1. [Rotate Linked List K Times](https://leetcode.com/problems/rotate-list/description/)
   1. Brute Force:
      1. For each K, move the last element from the list to first.
      2. TC: O(N*K)
   2. Optimal:
      1. Find length of list, and then `reminder=k%length`
      2. Convert list to cycle by `tail.next=head`
      3. Find the breakpoint using reminder
      4. Mark `newHead=cur.next` and break the connection `cur.next=null`
        <details>
        <summary>Code</summary>
        <div markdown="1">

        ```kotlin
        fun rotateRight(head: ListNode?, k: Int): ListNode? {
            if(head==null||head?.next==null||k==0) return head
            var count = 1
            var cur = head
            while(cur?.next!=null){ //find length of list
                cur = cur?.next
                count++
            }
            cur?.next = head        //convert list to cycle
            var reminder = k%count
            var lastIndex = count-reminder
            for(i in 0 until lastIndex){
                cur = cur?.next     //find the breakpoint
            }
            var newHead = cur?.next
            cur?.next = null
            return newHead
        }
        ```
        </div></details>          
2. []()
3. [3 Sum](https://leetcode.com/problems/3sum/description/)
   1. Brute Force:
      1. Use 3 loops and find the triplets.
      2. Can be sorted later on with the result to remove the duplicates.
      3. TC: O(N^3)
   2. Better:
      1. Sort and Use 2 loops and HashSet to find the triplets
      2. TC: O(N^2*log(no. of unique triplets)), SC: O(2*(no of unique triplets))+O(N)
   3. Optimal:
      1. Sort and use 1 loop and 2 pointers start and end.
      2. TC: O(N*logN)+O(N^2)
        <details>
        <summary>Code</summary>
        <div markdown="1">

        ```kotlin
        fun threeSum(nums: IntArray): List<List<Int>> {
            var ans: MutableList<List<Int>> = mutableListOf()
            nums.sort()
            var n = nums.size
            for(i in 0 until n){
                val num = nums[i]
                if(i > 0 && nums[i]==nums[i-1]) continue
                var start = i+1
                var end = n-1
                while(start<end){
                    var sum = nums[start] + nums[end] + num
                    when {
                        sum == 0 -> {
                            ans.add(listOf(num,nums[start],nums[end]))
                            start++
                            end--

                            while(start<end && nums[start]==nums[start-1]) start++
                            while(start<end && nums[end]==nums[end+1]) end--
                        }
                        sum > 0 -> {
                            end--
                        }
                        sum < 0 -> {
                            start++
                        }
                    }
                }
            }
            return ans
        }
        ```
        </div></details>
4. [Trapping Rainwater](https://leetcode.com/problems/trapping-rain-water/)
   1. Brute Force:
      1. Take 1 loop to iterate all the items 
      2. Use start and end pointers to find the max heights on left and right of each index and find the dif.
      3. TC: O(N*N)
   2. Better:
      1. Take two arrays prefix and suffix to store the maxLeft and maxRight for all the elements
      2. Then use `minOf(prefix[i],suffix[i])-height[i]` to find the answer
      3. TC: O(3*N)
        <details>
        <summary>Code</summary>
        <div markdown="1">

        ```java
        static int trap(int[] arr) {
            int n = arr.length;
            int prefix[] = new int[n];
            int suffix[] = new int[n];
            prefix[0] = arr[0];
            for (int i = 1; i < n; i++) {
                prefix[i] = Math.max(prefix[i - 1], arr[i]);
            }
            suffix[n - 1] = arr[n - 1];
            for (int i = n - 2; i >= 0; i--) {
                suffix[i] = Math.max(suffix[i + 1], arr[i]);
            }
            int waterTrapped = 0;
            for (int i = 0; i < n; i++) {
                waterTrapped += Math.min(prefix[i], suffix[i]) - arr[i];
            }
            return waterTrapped;
        }
        ```
        </div></details>
   3. Optimal: `Two Pointer Approach`
      1. Take two pointers left and right and point to 0 and n-1
      2. Take two vairables maxLeft and maxRight to 0 and 0
        <details>
        <summary>Code</summary>
        <div markdown="1">

        ```kotlin
        fun trap(height: IntArray): Int {
            var ans = 0
            var left = 0
            var right = height.size-1
            var maxLeft = 0
            var maxRight = 0
            while(left<=right){
                if(height[left]<=height[right]){
                    if(height[left]>maxLeft){
                        maxLeft = height[left]
                    }else{
                        ans+=maxLeft-height[left]
                    }
                    left++
                }else{
                    if(height[right]>maxRight){
                        maxRight = height[right]
                    }else{
                        ans+=maxRight-height[right]
                    }
                    right--
                }
            }
            return ans
        }
        ```
        </div></details>
5. [Remove Duplicare From Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)
   1. Brute Force:
      1. Use HashSet to store distinct elements
   2. Optimal: `Use Two Pointers`
      1. Use i to iterate array and newIndex pointer which moves with removed duplicates.
      2. TC: O(N)
        <details>
        <summary>Code</summary>
        <div markdown="1">

        ```kotlin
        fun removeDuplicates(nums: IntArray): Int {
            var newIndex = 1
            for(num in nums){
                if(num != nums[newIndex-1]){
                    nums[newIndex++]=num
                }
            }
            return newIndex
        }
        ```
        </div></details>
6. [Max Consequtive Ones](https://leetcode.com/problems/max-consecutive-ones/)
   1. Optimal:
      1. Maintain count, increase if 1 or set 0 if found 0.
      2. update max on each iterations
      3. TC: O(N)
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
    fun findMaxConsecutiveOnes(nums: IntArray): Int {
        var max = 0
        var count = 0
        var n = nums.size
        for(i in 0 until n){
            var num = nums[i]
            when(num){
                1 -> count++
                else -> count=0
            }
            max = maxOf(max,count)
        }
        return max
    }
    ```
    </div></details>
7. [Next Greater Node In Linked List](https://leetcode.com/problems/next-greater-node-in-linked-list/description/)
   1. Create list of value and apply `monotonic stack`
    <br>
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
    fun nextLargerNodes(head: ListNode?): IntArray {
        var list = mutableListOf<Int>()
        var cur = head
        while(cur!=null){
            list.add(cur.`val`)
            cur=cur.next
        }
        var stack = Stack<Int>()
        var result = IntArray(list.size){0}
        for(i in list.indices){
            while(stack.isNotEmpty() && list[stack.peek()] < list[i]){
                val index = stack.pop()
                result[index] = list[i]
            }
            stack.push(i)
        }
        return result
    }
    ```
    </div></details>
8. []()

### <a name='Day8'></a>Day 8: Greey Algorithm

### <a name='Day9'></a>Day 9: Recursion
1. [Combination Sum 1-2-3](https://leetcode.com/problems/combination-sum/description/)
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
    //combination sum 1: items can be used multiple times
    fun combinationSum(candidates: IntArray, target: Int): List<List<Int>> {
        var res: MutableList<List<Int>> = mutableListOf()
    
        fun comb(start: Int, ans: MutableList<Int>,target:Int){
            if(target==0){
                res.add(ans.toList())
                return
            }
            if(target<0) return
            for(i in start until candidates.size){
                ans.add(candidates[i])
                comb(i,ans,target-candidates[i])
                ans.removeLast()
            }
        }
        comb(0,mutableListOf(),target)
        return res
    }
    //combination sum 2: each item can be used once  
    fun combinationSum2(candidates: IntArray, target: Int): List<List<Int>> {
        var res: MutableList<List<Int>> = mutableListOf()
        candidates.sort()
        fun comb(start: Int, ans: MutableList<Int>,target:Int){
            if(target==0){
                res.add(ans.toList())
                return
            }
            if(target<0) return
            for(i in start until candidates.size){
                if(i > start && candidates[i]==candidates[i-1]) continue
                ans.add(candidates[i])
                comb(i+1,ans,target-candidates[i])
                ans.removeLast()
            }
        }
        comb(0,mutableListOf(),target)
        return res
    }
    //combination sum 3: find combination of size k using 1..9 
    fun combinationSum3(k: Int, target: Int): List<List<Int>> {
        var res: MutableList<List<Int>> = mutableListOf()
        var candidates = mutableListOf(1,2,3,4,5,6,7,8,9)

        fun comb(start: Int, ans: MutableList<Int>,target:Int){
            if(target==0){
                if(ans.size==k){
                    res.add(ans.toList())
                    return
                }
            }
            if(target<0) return
            for(i in start until candidates.size){
                if(i > start && candidates[i]==candidates[i-1]) continue
                ans.add(candidates[i])
                comb(i+1,ans,target-candidates[i])
                ans.removeLast()
            }
        }
        comb(0,mutableListOf(),target)
        return res
    }
    ```
    </div></details>
2. [Subset 1-2](https://leetcode.com/problems/subsets/description/)
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
    //1. Given an integer array nums of unique elements, return all possible subsets(the power set).
    var ans: MutableList<List<Int>> = mutableListOf()
    var temp: MutableList<Int> = mutableListOf()

    fun subsets(nums: IntArray): List<List<Int>> {
        backTrack(nums,0)
        return ans
    }

    fun backTrack(nums:IntArray,start:Int){
        ans.add(temp.toList())
        for(i in start until nums.size){
            temp.add(nums[i])
            backTrack(nums,i+1)
            temp.removeAt(temp.size-1)
        }
    }
    //2. Given an integer array nums that may contain duplicates, return all possible subsets (the power set).
    fun subsetsWithDup(nums: IntArray): List<List<Int>> {
        nums.sort()
        var ans: MutableList<List<Int>> = mutableListOf()
        var temp: MutableList<Int> = mutableListOf()
        fun backTrack(nums:IntArray,start:Int){
            ans.add(temp.toList())
            for(i in start until nums.size){
                if(i>start && nums[i]==nums[i-1]) continue
                temp.add(nums[i])
                backTrack(nums,i+1)
                temp.removeAt(temp.size-1)
            }
        }
        backTrack(nums,0)
        return ans
    }
    ```
    </div></details>   

### <a name='Day10'></a>Day 10: Recursion, Backtracking
- []()

### <a name='Day11'></a>Day 11
- []()

### <a name='Day12'></a>Day 12: Heaps
1. []()
2. [Kth Largest Element](https://leetcode.com/problems/kth-largest-element-in-an-array/)
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
    fun findKthLargest(nums: IntArray, k: Int): Int {
        val minHeap = PriorityQueue<Int>()
        for(num in nums){
            minHeap.add(num)
            if(minHeap.size>k) minHeap.poll()
        }
        return minHeap.peek()
    }
    ```
    </div></details>
3. [Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/description/)
   1. Better: `Heap`
      1. Store frquency in HashMap
      2. Move map to PriorityQueue: `val minHeap = PriorityQueue<Pair<Int,Int>>(compareBy {it.second})`
      3. TC: O(N*logk), SC: O(N+k)
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
    fun topKFrequent(nums: IntArray, k: Int): IntArray {
        var freqMap = hashMapOf<Int,Int>()
        for(num in nums){
            freqMap[num] = freqMap.getOrDefault(num, 0)+1
        }
        val minHeap = PriorityQueue<Pair<Int,Int>>(compareBy {it.second})
        for(item in freqMap){
            minHeap.add(Pair(item.key,item.value))
            if(minHeap.size>k){
                minHeap.poll()
            }
        }
        return minHeap.map{ it.first }.toIntArray()
    }
    ```
    </div></details>
   2. Optimal: `Quickselect (Hoare's selection algorithm)`
4. [Find Median from Data Stream](https://leetcode.com/problems/find-median-from-data-stream/)
   1. Optimal:
      1. Use Two Priority Queues
      2. MaxHeap for first half of items
      3. MinHeap for second half of items
      4. TC: O(logN), O(1)
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
    val maxHeap = PriorityQueue<Int>(compareByDescending {it})
    val minHeap = PriorityQueue<Int>()
    var isEven = true

    fun addNum(num: Int) {
        if(isEven){
            minHeap.add(num)
            maxHeap.add(minHeap.poll())
        }else{
            maxHeap.add(num)
            minHeap.add(maxHeap.poll())
        }
        isEven = !isEven
    }

    fun findMedian(): Double {
        return if(isEven){
            (maxHeap.peek()+minHeap.peek())/2.0
        } else {
            maxHeap.peek().toDouble()
        }
    }
    ```
    </div></details>
5. **[Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum/description/)
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
    fun maxSlidingWindow(nums: IntArray, k: Int): IntArray {
        if (nums.isEmpty() || k <= 0) return intArrayOf()

        val result = mutableListOf<Int>()
        val deque = ArrayDeque<Int>()

        for (i in nums.indices) {
            // Remove indices that are out of the current window
            if (deque.isNotEmpty() && deque.first() < i - k + 1) {
                deque.removeFirst()
            }

            // Remove elements from the deque that are smaller than the current element
            while (deque.isNotEmpty() && nums[deque.last()] < nums[i]) {
                deque.removeLast()
            }

            // Add the current element's index to the deque
            deque.addLast(i)

            // Add the maximum for the current window to the result
            if (i >= k - 1) {
                result.add(nums[deque.first()])
            }
        }

        return result.toIntArray()
    }
    ```
    </div></details>
6. []()

### <a name='Day13'></a>Day 13: Stack and Queues
1. [Implement Stack Using Array]()
   1. Push: `nums[++index]=x`
   2. Pop: `nums[index--]`
2. [Implement Queue Using Array]()
   1. Use Array in Ciruclar way and use Front and Rear to find the corresponding indexes.
3. [Implement Stack Using Queues](https://leetcode.com/problems/implement-stack-using-queues/)
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
    private var q1: Queue<Int> = LinkedList()
    private var q2: Queue<Int> = LinkedList()

    fun push(x: Int) {
        q2.offer(x)
        while(q1.isNotEmpty()){
            q2.offer(q1.poll())
        }
        q1 = q2.also { q2 = q1 }
    }

    fun pop(): Int {
        return q1.poll()    
    }

    fun top(): Int {
        return q1.peek()
    }

    fun empty(): Boolean {
        return q1.isEmpty()
    }
    ```
    </div></details>
4. [Implement Queue Using Stack](https://leetcode.com/problems/implement-queue-using-stacks/)
   1. Create two stack, pushStack, popStack
   2. push(): insert in pushStack
   3. pop(): remove from popStack, if it's empty, move all items from pushStack to popStack first.
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
    val pushStack = Stack<Int>()
    val popStack = Stack<Int>()
    
    fun push(x: Int) {
        pushStack.push(x)
    }

    fun pop(): Int {
        peek()
        return popStack.pop()
    }

    fun peek(): Int {
        if (popStack.isEmpty()) {
            while (pushStack.isNotEmpty()) {
                popStack.add(pushStack.pop())
            }
        }
        return popStack.peek()
    }

    fun empty(): Boolean {
        return popStack.isEmpty() && pushStack.isEmpty()
    }
    ```
    </div></details>
5. [Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
    fun isValid(s: String): Boolean {
        val stack = Stack<Char>()
        for(char in s){
            when(char){
                '(' -> stack.push(')')
                '[' -> stack.push(']')
                '{' -> stack.push('}')
                else -> {
                    if(stack.isEmpty() || stack.pop() != char) return false
                }
            }
        }
        return stack.isEmpty()
    }
    ```
    </div></details>
6. []()

### <a name='Day14'></a>Day 14: Stack and Queues II
1. [Next Smaller Element]()
2. [LRU cache (IMPORTANT)](https://leetcode.com/problems/lru-cache/description/)
   1. Create 4 functions for doubly-linked list
      1. removeTail, removeNode, moveToHead, addToHead
        <details>
        <summary>Code</summary>
        <div markdown="1">

        ```kotlin
        data class LruNode(var key: Int, var value: Int) {
            var prev: LruNode? = null
            var next: LruNode? = null
        }

        private var cap = -1
        private val cache = mutableMapOf<Int, LruNode>()
        private val head = LruNode(0, 0)
        private val tail = LruNode(0, 0)

        init {
            head.next = tail
            tail.prev = head
            cap = capacity
        }

        fun get(key: Int): Int {
            val node = cache[key] ?: return -1
            moveToHead(node)
            return node.value
        }

        fun put(key: Int, value: Int) {
            if(cache.containsKey(key)){
                val node = cache[key]!!
                node?.value = value
                moveToHead(node)
            }else{
                if(cache.size==cap){
                    val tail = removeTail()
                    cache.remove(tail.key)
                }
                val newNode = LruNode(key,value)
                cache[key] = newNode
                addToHead(newNode)
            }
        }

        private fun removeTail(): LruNode{
            val toRemove = tail.prev!!
            removeNode(toRemove)
            return toRemove
        }

        private fun removeNode(node: LruNode){
            node.next?.prev = node.prev
            node.prev?.next = node.next
        }

        private fun moveToHead(node: LruNode){
            removeNode(node)
            addToHead(node)
        }

        private fun addToHead(node: LruNode){
            node.next = head.next
            head.next?.prev = node
            node.prev = head
            head.next = node
        }
        ```
        </div></details>
3. [LFU cache]()
4. [Largest rectangle in a histogram]()
5. [Sliding Window maximum](https://leetcode.com/problems/sliding-window-maximum/description/)
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
    fun maxSlidingWindow(nums: IntArray, k: Int): IntArray {
        if (nums.isEmpty() || k <= 0) return intArrayOf()

        val result = mutableListOf<Int>()
        val deque = ArrayDeque<Int>()

        for (i in nums.indices) {
            // If the first element in deque is outside current window, remove it
            if (deque.isNotEmpty() && deque.first() < i - k + 1) {
                deque.removeFirst()
            }

            // Remove all elements smaller than current element
            while (deque.isNotEmpty() && nums[deque.last()] < nums[i]) {
                deque.removeLast()
            }

            // Add current index to deque
            deque.addLast(i)

            // First element in deque is always maximum of current window
            if (i >= k - 1) {
                result.add(nums[deque.first()])
            }
        }

        return result.toIntArray()
    }
    ```
    </div></details>
6. [Implement Min Stack]()
7. [Rotten Orange (Using BFS)]()
8. [Stock span problem]()
9. [Find the maximum of minimums of every window size]()
10. [The Celebrity Problem]()

### <a name='Day15'></a>Day 15: String
1. [Reverse Words in a String](https://leetcode.com/problems/reverse-words-in-a-string/description/)
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
    fun reverseWords(s: String): String {
        var stack = Stack<String>()
        var i = 0
        while(i<s.length){
            var ans = " "
            if(s[i]==' '){
                i++
            }else{
                while(i<s.length && s[i]!=' '){
                    ans+=s[i]
                    i++
                }
                stack.push(ans)
            }
        }
        var res = ""
        while(stack.isNotEmpty()){
            res+=stack.pop()
        }
        return res.trim()
    }
    ```
    </div></details>
2. [Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/description/)
   1. For each i index of string, expand left and right
   2. for odd: left,right
   3. for evem: left, right+1
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
    fun longestPalindrome(s: String): String {
        var n = s.length
        var max = 0
        var start = 0
        var end = 0

        fun expand(left: Int, right: Int){
            var l = left
            var r = right
            while(l>=0 && r<n && s[l]==s[r]){
                if(r-l+1 > max){
                    max = r-l+1
                    start = l
                    end = r
                }
                l--
                r++
            }
        }

        for(i in s.indices){
            expand(i,i)
            expand(i,i+1)
        }
        return s.substring(start,end+1)
    }
    ```
    </div></details>
3. []()
4. []()
5. [Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix/description/)
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
    fun longestCommonPrefix(strs: Array<String>): String {
        strs.sort()
        var first = strs[0]
        var last = strs[strs.size-1]
        var i = 0
        while(i<first.length && i < last.length && first[i]==last[i]){
            i++
        }
        return first.substring(0,i)
    }
    ```
    </div></details>
6. []()

### <a name='Day16'></a>Day 16: String II
1. []()
2. [Minimum Add to Make Parentheses Valid](https://leetcode.com/problems/minimum-add-to-make-parentheses-valid/description/)
   1. Use openCount and closeCounts
   2. If "(", increase openCount, else check if openCount>0 and then either decrease openCount or increase closeCount
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
    fun minAddToMakeValid(s: String): Int {
        var oc = 0
        var cc = 0
        for(char in s){
            if(char=='(')
                oc++
            else {
                if(oc>0){
                    oc--    //balance previous open
                }else{
                    cc++    //count unbalanced oc
                }
            }
        }
        return oc+cc
    }
    ```
    </div></details>

### <a name='Day17'></a>Day 17: Binary Tree
1. [InOrder, PreOrder, PostOrder Traversal]()
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
    //inOrder
    fun inorder(root:TreeNode?){
        if(root!==null){
            inorder(root.left)
            res.add(root.`val`)
            inorder(root.right)
        }
    }
    //preOrder
    fun preOrder(root:TreeNode?){
        if(root!==null){
            res.add(root.`val`)
            preOrder(root.left)
            preOrder(root.right)
        }
    }
    //postOrder
    fun postOrder(root:TreeNode?){
        if(root!==null){
            postOrder(root.left)
            postOrder(root.right)
            res.add(root.`val`)
        }
    }
    ```
    </div></details>
2. [Binary Tree Left/Right Side View](https://leetcode.com/problems/binary-tree-right-side-view/description/)
   1. BFS: Store the first and last node at each Level
   2. DFS: 
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
    fun rightSideView(root: TreeNode?): List<Int> {
        val result = mutableListOf<Int>()

        fun rightView(root: TreeNode?,currDepth: Int){
            if(root==null){
                return
            }
            if(currDepth == result.size){
                result.add(root.`val`)
            }
            //for right side view
            rightView(root.right, currDepth+1)
            rightView(root.left, currDepth+1)
            //for left side view
            rightView(root.left, currDepth+1)
            rightView(root.right, currDepth+1)
        }
        rightView(root,0)       
        return result
    }
    ```
    </div></details>
3. [Maximum Width of Binary Tree](https://leetcode.com/problems/maximum-width-of-binary-tree/description/)
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
    fun widthOfBinaryTree(root: TreeNode?): Int {
        val q: ArrayDeque<Pair<TreeNode, Int>> = ArrayDeque()
        var max = 0
        if(root==null) return 0
        q.addLast(Pair(root,0))
        while(q.isNotEmpty()){
            val size = q.size
            val firstIndex = q.first().second
            var lastIndex = firstIndex
            for(i in 0 until size){
                val (node, index) = q.removeFirst()
                lastIndex = index
                node.left?.let { q.addLast(Pair(it, 2*index)) }
                node.right?.let { q.addLast(Pair(it, 2*index+1)) }
            }
            val curWidth = lastIndex-firstIndex+1
            max = maxOf(curWidth, max)
        }
        return max
    }
    ```
    </div></details>
4. *[Maximum Level Sum of a Binary Tree](https://leetcode.com/problems/maximum-level-sum-of-a-binary-tree/)
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
    fun maxLevelSum(root: TreeNode?): Int {
        val q = ArrayDeque<TreeNode>()
        var maxSum = Int.MIN_VALUE
        var maxIndex = 1
        var curIndex = 1
        if(root==null) return 0
        q.addLast(root)
        while(q.isNotEmpty()){
            val size = q.size
            var curLevelSum = 0
            for(i in 0 until size){
                val cur = q.removeFirst()
                curLevelSum += cur.`val`
                cur.left?.let { q.addLast(it) }
                cur.right?.let { q.addLast(it) }
            }
            if(curLevelSum>maxSum){
                maxSum = curLevelSum
                maxIndex = curIndex
            }
            curIndex++
        }
        return maxIndex
    }
    ```
    </div></details>

### <a name='Day18'></a>Day 18: Binary Tree II
1. [Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/description/)
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
    fun levelOrder(root: TreeNode?): List<List<Int>> {
        var ans = mutableListOf<List<Int>>()
        val q = ArrayDeque<TreeNode>()
        if(root==null) return ans
        q.addLast(root)
        while(q.isNotEmpty()){
            val size = q.size
            val curList = mutableListOf<Int>()
            for(i in 0 until size){
                val cur = q.removeFirst()
                curList.add(cur.`val`)
                cur.left?.let { q.addLast(it) }
                cur.right?.let { q.addLast(it) }
            }
            ans.add(curList)
        }
        return ans
    }
    ```
    </div></details>
2. [Height/Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/description/)
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
    fun maxDepth(root: TreeNode?): Int {
        if(root==null) return 0
        return maxOf(maxDepth(root.left),maxDepth(root.right))+1
    }
    ```
    </div></details>
3. [Diameter of Binary Tree](https://leetcode.com/problems/diameter-of-binary-tree/)

    <details>
    <summary>Code</summary>
    <div markdown="1">
    
    ```kotlin
    fun diameterOfBinaryTree(root: TreeNode?): Int {
        var max = 0
        fun maxDepth(root:TreeNode?): Int {
            if(root==null) return 0
            val left = maxDepth(root.left)
            val right = maxDepth(root.right)
            max = maxOf(max,left+right)
            return maxOf(left,right)+1
        }
        maxDepth(root)
        return max
    }
    ```
    </div></details>
4. []()
5. [Zig Zag Traversal of Binary Tree](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/)
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
    fun zigzagLevelOrder(root: TreeNode?): List<List<Int>> {
        val ans = mutableListOf<List<Int>>()
        if(root==null) return ans
        val q = ArrayDeque<TreeNode>()
        q.addLast(root)
        var isLtoR = true
        while(q.isNotEmpty()){
            val size = q.size
            val curList = mutableListOf<Int>()
            
            for(i in 0 until size){
                if(isLtoR){   
                    val cur = q.removeFirst()
                    curList.add(cur.`val`)
                    cur.left?.let { q.addLast(it) }
                    cur.right?.let { q.addLast(it) }
                }else{
                    val cur = q.removeLast()
                    curList.add(cur.`val`)
                    cur.right?.let { q.addFirst(it) }
                    cur.left?.let { q.addFirst(it) }
                }
            }
            isLtoR = !isLtoR
            ans.add(curList)
        }
        return ans
    }
    ```
    </div></details>
6. [Check if two trees are identical](https://leetcode.com/problems/same-tree/)
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
        fun isSameTree(p: TreeNode?, q: TreeNode?): Boolean {
        if(p==null && q==null)
            return true
        if(p==null || q==null)
            return false
        if(p?.`val` != q?.`val`)
            return false
        return isSameTree(p.left,q.left) && isSameTree(p.right,q.right)
    }
    ```
    </div></details>
7. [Lowest Common Ancestor](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/description/)
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
    fun lowestCommonAncestor(root: TreeNode?, p: TreeNode?, q: TreeNode?): TreeNode? {
        if(root==null) return null
        if(root==q || root==p) return root
        val left = lowestCommonAncestor(root.left,p,q)
        val right = lowestCommonAncestor(root.right,p,q)
        if(left==null) return right
        if(right==null) return left
        return root
    }
    ```
    </div></details>
8. [Level Order Traversal II](https://leetcode.com/problems/binary-tree-level-order-traversal-ii/)
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
    fun levelOrderBottom(root: TreeNode?): List<List<Int>> {
        var ans = mutableListOf<List<Int>>()
        val q = ArrayDeque<TreeNode>()
        if(root==null) return ans
        q.addLast(root)
        while(q.isNotEmpty()){
            val size = q.size
            val curList = mutableListOf<Int>()
            for(i in 0 until size){
                val cur = q.removeFirst()
                curList.add(cur.`val`)
                cur.left?.let { q.addLast(it) }
                cur.right?.let { q.addLast(it) }
            }
            ans.add(0,curList)
        }
        return ans
    }
    ```
    </div></details>



### <a name='Day19'></a>Day 19: Binary Tree III
1. *[Invert Binary Tree](https://leetcode.com/problems/invert-binary-tree/submissions/1492755785/)
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
    fun invertTree(root: TreeNode?): TreeNode? {
        if(root==null) {
            return null
        }
        val left = invertTree(root.left)
        val right = invertTree(root.right)
        root.left = right
        root.right = left
        return root
    }
    ```
    </div></details>
2. [Flatten Binary Tree](https://leetcode.com/problems/flatten-binary-tree-to-linked-list/)
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
    fun flatten(root: TreeNode?): Unit {
        var cur = root
        while(cur!=null){
            if(cur.left!=null){
                var prev = cur.left
                while(prev.right!=null){
                    prev = prev.right
                }
                prev.right = cur.right
                cur.right = cur.left
                cur.left = null
            }
            cur = cur.right
        }
    }
    ```
    </div></details>
3. [Construct Binary Tree From PreOrder & InOrder](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin    
    fun buildTree(preorder: IntArray, inorder: IntArray): TreeNode? {
        if(preorder.size==0) return null

        val r = preorder[0]
        val i = inorder.indexOf(r)

        val root = TreeNode(r)
        root.left = buildTree(preorder.copyOfRange(1,i+1), inorder.copyOfRange(0,i))
        root.right = buildTree(preorder.copyOfRange(i+1,preorder.size), inorder.copyOfRange(i+1,inorder.size))
        return root
    }
    ```
    </div></details>
4. [Construct Binary Tree from Inorder and Postorder](https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/)
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin    
    fun buildTree(inorder: IntArray, postorder: IntArray): TreeNode? {
        if(postorder.isEmpty()) return null

        val r = postorder.last()
        val i = inorder.indexOf(r)

        val root = TreeNode(r)
        root.left = buildTree(inorder.copyOfRange(0,i), postorder.copyOfRange(0,i))
        root.right = buildTree(inorder.copyOfRange(i+1,inorder.size), postorder.copyOfRange(i,postorder.size-1))
        return root
    }
    ```
    </div></details>
5. [Symmetric Tree](https://leetcode.com/problems/symmetric-tree/)\
       <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
    fun isSymmetric(root: TreeNode?): Boolean {
        fun isMirror(left: TreeNode?, right: TreeNode?): Boolean {
            if(left==null && right==null) return true
            if(left==null || right==null) return false
            return (left.`val` == right.`val`) && isMirror(left?.left, right?.right) && isMirror(left?,right, right?.left)
        }
        return isMirror(root,root)
    }
    ```
    </div></details>
6. [Maximum Path Sum](https://leetcode.com/problems/binary-tree-maximum-path-sum/description/)
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
    fun maxPathSum(root: TreeNode?): Int {
        var maxSum = Int.MIN_VALUE
        fun pathSum(root: TreeNode?): Int {
            if(root==null) return 0
            val left = maxOf(0,pathSum(root.left))
            val right = maxOf(0,pathSum(root.right))
            maxSum = maxOf(maxSum, left+right+root.`val`)
            return root.`val`+maxOf(left,right)
        }
        pathSum(root)
        return maxSum
    }
    ```
    </div></details>
7. []()
8. *[Average Of Levels in Binary Tree](https://leetcode.com/problems/average-of-levels-in-binary-tree/submissions/)
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
        fun averageOfLevels(root: TreeNode?): DoubleArray {
        val q = ArrayDeque<TreeNode>()
        val ans = mutableListOf<Double>()
        if(root==null) return ans.toDoubleArray()
        q.addLast(root)
        while(q.isNotEmpty()){
            val size = q.size
            var curLevelSum = 0.0
            for(i in 0 until size){
                val cur = q.removeFirst()
                curLevelSum += cur.`val`
                cur.left?.let { q.addLast(it) }
                cur.right?.let { q.addLast(it) }
            }
            ans.add(curLevelSum.toDouble()/size.toDouble())
        }
        return ans.toDoubleArray()
    }
    ```
    </div></details>
9. []()


### <a name='Day20'></a>Day 20: Binary Search Tree
1. [Populating Next Right Pointes To Each Node](https://leetcode.com/problems/populating-next-right-pointers-in-each-node/description/)
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
    fun connect(root: Node?): Node? {
        if(root==null) return root
        var leftMost = root
        while(leftMost?.left!=null){
            var cur = leftMost
            while(cur!=null){
                cur?.left?.next = cur?.right
                if(cur.next!=null){
                    cur?.right?.next = cur?.next?.left
                }
                cur = cur?.next
            }
            leftMost = leftMost?.left
        }
        return root
    }
    ```
    </div></details>
2. [Search in BST](https://leetcode.com/problems/search-in-a-binary-search-tree/)
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
    fun searchBST(root: TreeNode?, `val`: Int): TreeNode? {
        if(root==null) return null
        if(root.`val` == `val`){
            return root
        }
        return if(root.`val`>`val`){
             searchBST(root?.left,`val`)
        }else{
             searchBST(root?.right,`val`)
        }
    }
    ```
    </div></details>
3. []()
4. [Validate BST](https://leetcode.com/problems/validate-binary-search-tree/)
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
    fun isValidBST(root: TreeNode?): Boolean {
        fun validateInner(root: TreeNode?, min:Long, max: Long): Boolean {
            if(root==null) return true
            if(root.`val` >= max || root.`val` <= min) return false
            return validateInner(root.left,min,root.`val`.toLong()) 
                && validateInner(root.right, root.`val`.toLong(),max)
        }
        return validateInner(root, Long.MIN_VALUE, Long.MAX_VALUE)
    }
    ```
    </div></details>
5. [Lowest Common Ancestor](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/description/)
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
    fun lowestCommonAncestor(root: TreeNode?, p: TreeNode?, q: TreeNode?): TreeNode? {
        if(root==null) return null
        if(root==q || root==p) return root
        val left = lowestCommonAncestor(root.left,p,q)
        val right = lowestCommonAncestor(root.right,p,q)
        if(left==null) return right
        if(right==null) return left
        return root
    }
    ```
    </div></details>
6. []()


### <a name='Day21'></a>Day 21: Binary Search Tree II
1. []()
2. [Find Median from Data Stream](https://leetcode.com/problems/find-median-from-data-stream/description/)
   1. Create minHeap, maxHeap, isEven
   2. `addNum()`: if(even) add num in minHeap, and add minHeap.poll() to maxHeap, else vice versa
   3. `findMedian()`: if(even) `maxHeap.peek()+minHeap.peek()/2.0` `else maxHeap.peek()`
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
    val maxHeap = PriorityQueue<Int>(compareByDescending {it})
    val minHeap = PriorityQueue<Int>()
    var isEven = true

    fun addNum(num: Int) {
        if(isEven){
            minHeap.add(num)
            maxHeap.add(minHeap.poll())
        }else{
            maxHeap.add(num)
            minHeap.add(maxHeap.poll())
        }
        isEven = !isEven
    }

    fun findMedian(): Double {
        return if(isEven){
            (maxHeap.peek()+minHeap.peek())/2.0
        } else {
            maxHeap.peek().toDouble()
        }
    }
    ```
    </div></details>
3. []()
4. [Two Sum: Binary Search Tree](https://leetcode.com/problems/two-sum-iv-input-is-a-bst/description/)
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
    fun findTarget(root: TreeNode?, k: Int): Boolean {
        val set = hashSetOf<Int>()
        fun search(root: TreeNode?, k: Int): Boolean {
            if(root==null) return false
            if(set.contains(k-root. `val`)){
                return true
            }
            set.add(root.`val`)
            return search(root.left,k) || search(root.right,k)
        }
        return search(root,k)
    }
    ```
    </div></details>
5. []()
6. *[Sum Root To Leaf Number](https://leetcode.com/problems/sum-root-to-leaf-numbers/)
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
    fun sumNumbers(root: TreeNode?): Int {
        fun dfs(root: TreeNode?, s: Int): Int{
            if(root==null) return 0
            var sum = s*10+root.`val`
            if(root.left==null && root.right==null) return sum
            return dfs(root.left,sum)+dfs(root.right,sum)
        }
        return dfs(root,0)
    }
    ```
    </div></details>

### <a name='Day22'></a>Day 22: Binary Tree (Miscellaneous)
1. [Kth Largest Element in a Stream](https://leetcode.com/problems/kth-largest-element-in-a-stream/)
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
    val heap = PriorityQueue<Int>(k)
    init {
        for(num in nums){
            add(num)
        }
    }

    fun add(v: Int): Int {
        heap.add(v)
        if(heap.size > k) heap.poll()
        return heap.peek()
    }
    ```
    </div></details>
2. [K-th largest element in an unsorted array](https://leetcode.com/problems/kth-largest-element-in-an-array/)
   1. Use `PriorityQueue`
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
    fun findKthLargest(nums: IntArray, k: Int): Int {
        val minHeap = PriorityQueue<Int>()
        for(num in nums){
            minHeap.add(num)
            if(minHeap.size>k) minHeap.poll()
        }
        return minHeap.peek()
    }
    ```
    </div></details>
3. []()

### <a name='Day23'></a>Day 23: Graph
```kotlin
fun main() {
    // Graph as an adjacency list
    val graph = mapOf(
        0 to listOf(1, 2),
        1 to listOf(0, 3, 4),
        2 to listOf(0, 5, 6),
        3 to listOf(1),
        4 to listOf(1),
        5 to listOf(2),
        6 to listOf(2)
    )
}
```
1. [Breadth First Search]()
   1. Create hashSetof() to store visited elements
   2. Create queue to iterate the elements
   3. Create mutableListof() to store the answer
   4. add starting node in queue and visited, and iterate all neighbour till queue is empty while add in queue and visited after checking if visited=false
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
    fun bfs(graph: Map<Int, List<Int>>, startNode: Int): List<Int> {
        val visited = hashSetOf<Int>()
        val result = mutableListOf<Int>()
        val queue: Queue<Int> = LinkedList()
        
        queue.add(startNode)
        visited.add(startNode)
        
        while(queue.isNotEmpty()){
            val node = queue.poll()
            result.add(node)
            
            for(neighbour in graph[node] ?: emptyList()){
                if(!visited.contains(neighbour)){
                    queue.add(neighbour)
                    visited.add(neighbour)
                }
            }   
        }
        return result
    }
    ```
    </div></details>
2. [Depth First Search]()
   1. TC: O(N) + (2*Edges) ,SC: O(N)+O(N)+O(N) ~ O(N)
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
    //recursive
    fun dfsRecursive(graph: Map<Int, List<Int>>, curNode: Int, visited: MutableSet<Int>, result: MutableList<Int>) {
        visited.add(curNode)
        result.add(curNode)
        
        for(neighbour in graph[curNode] ?: emptyList()){
            if(neighbour !in visited){
                dfsRecursive(graph, neighbour, visited, result)
            }
        }
    }

    //iterative
    fun dfsIterative(graph: Map<Int, List<Int>>, startNode: Int): List<Int> {
        val visited = mutableSetOf<Int>()
        val stack = Stack<Int>()
        val result = mutableListOf<Int>()
        
        stack.push(startNode)
        
        while(stack.isNotEmpty()){
            var cur = stack.pop()
            
            if(cur !in visited){
                visited.add(cur)
                result.add(cur)
                
                for(neighbour in graph[cur] ?: emptyList()){
                    if(neighbour !in visited){
                        stack.push(neighbour)
                    }
                }
            }
        }
        return result
    }
    ```
    </div></details>
3. *[Rotten Oranges](https://leetcode.com/problems/rotting-oranges/)
   1. Create queue of Triple(row,col, time) and add all the rotten orange cordinates, and count freshOranges
   2. Create list of Pairs representing all 4 directions allowed
   3. Iterate queue till empty, using poll() and find newRow and newCol using 4 directions
   4. Check if newRow and newCol are valid and contains fresh orange
      1. if true, add in queue, mark fresh(1) as rotten (2) and freshOranges--,
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin
    fun orangesRotting(grid: Array<IntArray>): Int {
        var row = grid.size
        var col = grid[0].size
        var queue: Queue<Triple<Int, Int, Int>> = LinkedList()
        var freshOranges = 0
        //create queue using current state of grid
        for(i in 0 until row){
            for(j in 0 until col){
                when(grid[i][j]){
                    2 -> queue.add(Triple(i,j,0))
                    1 -> freshOranges++
                }
            }
        }
        if(freshOranges==0) return 0
        val directions = listOf(
            Pair(0, 1),  // Right
            Pair(1, 0),  // Down
            Pair(0, -1), // Left
            Pair(-1, 0)  // Up
        )
        var minutes = 0
        //bfs
        while(queue.isNotEmpty()){
            val (r, c, time) = queue.poll()
            minutes = time
            //spread rot to all 4 directions
            for((dx,dy) in directions){
                val newRow = r+dx
                val newCol = c+dy
                //check if new cordinates are valid and fresh
                if(newRow in 0 until row && newCol in 0 until col && grid[newRow][newCol]==1) {
                    grid[newRow][newCol] = 2
                    freshOranges--
                    queue.add(Triple(newRow, newCol, time+1))
                }
            }
        }
        return if (freshOranges == 0) minutes else -1
    }
    ```
    </div></details>
4. []()

### <a name='Day23'></a>Day 23: Graph II

    
    <details>
    <summary>Code</summary>
    <div markdown="1">

    ```kotlin

    ```
    </div></details>
