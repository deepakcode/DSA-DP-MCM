# DSA-DP

### 1. Matrix chain Multiplication (MCM)

MCM general format is 


<p>
<img width="400" alt="Screenshot 2022-08-10 at 11 59 13 AM" src="https://user-images.githubusercontent.com/13814143/183841346-4ba9c2c7-0a52-4aaa-8e1b-b4228440ec18.png">
</p>


 *  step 1 : Find i and j
 *  step 2 : Find Base Condition
 *  step 3 : Find k loop 
 *  step 4 : Calculate tempAns
 *  step 5 : Calculate ans


<p>
<img width="654" alt="Screenshot 2022-08-10 at 11 59 13 AM" src="https://user-images.githubusercontent.com/13814143/183833129-d080e4a5-7b64-4830-91db-cf3dca26a3d8.png">
</p>

#### 1.1 MCM

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
