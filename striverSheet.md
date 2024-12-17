<!-- vscode-markdown-toc -->
- [Day 1](#day-1)
- [Day 2](#day-2)
- [Day 3](#day-3)
- [Day 4](#day-4)
- [Day 5](#day-5)
- [Day 6](#day-6)

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

### <a name='Day5'></a>Day 5
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


### <a name='Day6'></a>Day 6
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
5. [Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii/)
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


- []()
        <details>
        <summary>Code</summary>
        <div markdown="1">

        ```kotlin
        ```
        </div></details>