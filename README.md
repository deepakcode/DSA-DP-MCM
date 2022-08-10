# DP (Dynamic Programming) Notes 


## 1. Matrix chain Multiplication (MCM)

#### General format -





 -  Step 1 : Find i and j
          
            i - value is left side valid value of given array, and j - value is right side valid.
            k - value should lie between i and j
 
 -  Step 2 : Find Base Condition
   
            Thinking of smallest valid input
            or 
            Think of Invalid input
            
            like - i==j or i>j - when i value becomes equal to j then it is invalid, i value for MCM should be less then j
            
```java
           if(i>=j)
            return 0;
 ```
            
 -  Step 3 : Find k loop 
         <p>
        <img width="400" alt="Screenshot 2022-08-10 at 11 59 13 AM" src="https://user-images.githubusercontent.com/13814143/183841346-4ba9c2c7-0a52-4aaa-8e1b-b4228440ec18.png">
        </p>

 -  Step 4 : Calculate tempAns

```java
 int tempAns =  solve(arr, i, k)
                   + solve(arr, k+1, j)
                    + arr[i-1] * arr[k] * arr[j];

```
 
 -  Step 5 : Calculate final ans


<p>
<img width="654" alt="Screenshot 2022-08-10 at 11 59 13 AM" src="https://user-images.githubusercontent.com/13814143/183833129-d080e4a5-7b64-4830-91db-cf3dca26a3d8.png">
</p>


### P01 Matrics multiplication - MCM  

https://practice.geeksforgeeks.org/problems/matrix-chain-multiplication0303/1

Given a sequence of matrices, find the most efficient way to multiply these matrices together. The efficient way is the one that involves the least number of multiplications.

The dimensions of the matrices are given in an array arr[] of size N (such that N = number of matrices + 1) where the ith matrix has the dimensions (arr[i-1] x arr[i]).

Example 1:

Input: N = 5
arr = {40, 20, 30, 10, 30}
Output: 26000
Explaination: There are 4 matrices of dimension 
40x20, 20x30, 30x10, 10x30. Say the matrices are 
named as A, B, C, D. Out of all possible combinations,
the most efficient way is (A*(B*C))*D. 
The number of operations are -
20*30*10 + 40*20*10 + 40*10*30 = 26000.

#### Recursive Solution - P01 Matrics multiplication [Gives TLE error]

```java
class Solution{
    
    static int matrixMultiplication(int N, int arr[])
    {
        return solve(arr,1,N-1);
    }
    
    static int solve(int[] arr, int i, int j){
        
         int ans = Integer.MAX_VALUE;
         
         if(i>=j)
            return 0;
        
         for(int k=i; k<j; k++){
             
            int tempAns =  solve(arr, i, k)
                            +solve(arr,k+1, j)
                            +arr[i-1]*arr[k]*arr[j];
                            
            ans =Math.min(tempAns,ans);
        }
        
        return ans;
    }<img width="1184" alt="Screenshot 2022-08-10 at 12 17 18 PM" src="https://user-images.githubusercontent.com/13814143/183833733-7c541225-ddda-47f0-85c3-5b215753190b.png">


}
```

#### Memoization Solution - P01 Matrics multiplication [Passes all test cases on GFG]

<img width="710" alt="Screenshot 2022-08-10 at 2 16 22 PM" src="https://user-images.githubusercontent.com/13814143/183859244-e9ed7c97-89df-4536-80d1-f0f1b55ec07e.png">

```java
class Solution{
    
    static int[][] dp;
    
    static int matrixMultiplication(int N, int arr[])
    {
        dp = new int[N+1][N+1];
        for(int[] a: dp){
            Arrays.fill(a,-1);
        }
        
        return solve(arr,1,N-1);
    }
    
    static int solve(int[] arr, int i, int j){
         int ans = Integer.MAX_VALUE;
         if(dp[i][j] != -1)
            return dp[i][j];
         
         if(i>=j)
            return 0;
        
         for(int k=i; k<j; k++){
             
            int tempAns =  solve(arr, i, k) // this can be further optimized
                            +solve(arr,k+1, j) // this can be further optimized
                            +arr[i-1]*arr[k]*arr[j];
                            
            ans =Math.min(tempAns,ans);
        }
        return dp[i][j]=ans;
    }
}
```

## 1. Kanpsack problem
  ### 1.1 0/1 Knapsack (6)
  ### 1.2 Unbounded Knapsack (5)
  ### 1.3 Fractional Knapsack (1) Greedy
## 2. Fibonacci (7)
## 2. LCS (15)
## 3. LIS (10)
## 4. Kadane's Algorithm (6 )
## 6. DP on Trees (4 )
## 7. DP on Grid (14)
## 8. others (s )
