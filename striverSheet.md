<!-- vscode-markdown-toc -->
- [Day 1](#day-1)
- [Day 2](#day-2)
- [Day 3](#day-3)
- [Day 4](#day-4)
- [Day 5](#day-5)

<!-- vscode-markdown-toc-config
	numbering=false
	autoSave=true
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc -->
### <a name='Day1'></a>Day 1
- [Set Matrix Zero](https://leetcode.com/problems/set-matrix-zeroes/)
  - Brute Force:
    1. Iterate matrix and when found 0, mark all the elements of same row and col as -1. 
    2. Iterate whole matrix again and convert all -1 to 0
    3. TC: O(M*N)*O(M+N)+O(M*N), SC: O(n)
  - Better:
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
  - Optimal:
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
- [Next Permutation](https://leetcode.com/problems/next-permutation/description/)
  - Brute Force:
    1. Generate all the sorted permutations
    2. Linear Search the current
    3. Return next or first if last
    4. TC: O(N!*N), N! = N factorial
  - Optimal:
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
- [Kadane's' Algorithm](https://leetcode.com/problems/maximum-subarray/description/)
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
- [Sort Colors](https://leetcode.com/problems/sort-colors/description/)
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
- [Stock Buy And Sell](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)
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

### <a name='Day2'></a>Day 2
- [Rotate Image by 90 degree](https://leetcode.com/problems/rotate-image/description/)
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
- [Merge Overlapping Sub-intervals](https://leetcode.com/problems/merge-intervals/description/)
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
                }
                val endOfLast = ans.last()[1]
                if(endOfLast>=interval[0]){
                    ans.last()[1] = maxOf(endOfLast,interval[1])
                } else {
                    ans.add(interval)
                }
            }
            return ans.toTypedArray()
        }
        ```
        </div></details>
- [Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/description/)
  1. Optimal:
     1.  
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
- [Find the duplicate in an array of N+1 integers](https://leetcode.com/problems/find-the-duplicate-number/description/)
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
- []()

### <a name='Day3'></a>Day 3
- [Search in a sorted 2D matrix](https://leetcode.com/problems/search-a-2d-matrix/description/)
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
- [Majority Element n/2](https://leetcode.com/problems/majority-element/)
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
- [Majority Element n/3](https://leetcode.com/problems/majority-element-ii/)
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

### <a name='Day4'></a>Day 4

### <a name='Day5'></a>Day 5







        <details>
        <summary>Code</summary>
        <div markdown="1">

        ```kotlin
        ```
        </div></details>