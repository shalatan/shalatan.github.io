<!-- vscode-markdown-toc -->
- [Day 1](#day-1)
- [Day 2](#day-2)

<!-- vscode-markdown-toc-config
	numbering=false
	autoSave=true
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc -->
## <a name='Day1'></a>Day 1
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
- [Kadanse' Algorithm](https://leetcode.com/problems/maximum-subarray/description/)
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
-[]()
-[]()

## <a name='Day2'></a>Day 2