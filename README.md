# DSA-DP

### 1. Matrix chain Multiplication (MCM)

MCM general format is 

```java
int solve(int[] arr, int i, int j){
  
  if (i>=j)
    return 0;
   
  int ans= Integer.MAX_VALUE:
  
  for( int k =i; k <=j-1; k++){
    
    int tempAns = sovle(arr,i,k)
                  + sovle(arr,k+1,j)
                  +arr[i-1] * arr[k] * arr[j];
    
    ans = Math.min(asn,tempAns);
  } 
   
   return ans;
}
``` 

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
