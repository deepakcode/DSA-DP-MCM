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
    }


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

### P02 Palindromic Partitioning - MCM  

Find minimum number of partition required to make string a Palindromic

Example :
    Input: str = "nitin"
    Output: 0
    Explaination: String is alreay palindromic.


    Input: str = "ababbbabbababa"
    Output: 3
    Explaination: After 3 partitioning substrings are "a", "babbbab", "b", "ababa".
    
https://practice.geeksforgeeks.org/problems/palindromic-patitioning4845/1

#### Recursive Solution - P02

        1. is string alreay palindrome
        2. if string alreay palindrome return 0
        3. for each palindrome partition - add +1

```java
class Solution{
    static int palindromicPartition(String str)
    {
        //1. is string alreay palindrome
        //2. if string alreay palindrome return 0
        //3. for each palindrome partition - add +1
    
        int i = 0;
        int j = str.length()-1;
        
        if(isPalindrom(str,i,j))
            return 0;
        return solvePP(str,i,j);
    }
    
    static int solvePP(String str, int i, int j){
        if(i>=j)
            return 0;
            
        if(isPalindrom(str,i,j))
            return 0;// Remember this - if string is pallindrom return 0
        
        int min = Integer.MAX_VALUE;
         
        for(int k=i; k<j; k++){
            int temp = 1 
                    + solvePP(str,i,k) 
                    + solvePP(str,k+1,j); // 1 for each partition
                    
            min = Math.min(temp, min);
        }
        
        return min;
    }
    
    static boolean isPalindrom(String str, int i, int j){
        while(i<=j){ // i should be less then j
            if(str.charAt(i)!=str.charAt(j))
                return false;
            i++;
            j--;
        }
        return true;
    }

}
```

#### Memoization Solution - P02

<img width="729" alt="Screenshot 2022-08-10 at 5 00 15 PM" src="https://user-images.githubusercontent.com/13814143/183891088-d1e0380b-df1b-4bea-8ea9-cddaf35a2959.png">


### P03 Boolean Parenthesization Problem - MCM  

https://www.geeksforgeeks.org/boolean-parenthesization-problem-dp-37/

```java
        Symbols = "TTFT";
        Operators = "|&^";
              or
         
        Input - Expression =  T|T&F^T
 
        Output - 4  //Because there are 4 ways to evaluate this experession to True!
  
        // ((T|T)&(F^T)), (T|(T&(F^T))), (((T|T)&F)^T) and (T|((T&F)^T))
```

#### Recursive Solution - P03

<img width="285" alt="184004768-2e1e3ccb-0d24-4691-ba3f-4626b397cca8" src="https://user-images.githubusercontent.com/13814143/184016684-477867bd-092b-4463-9224-fe2d99398d2b.png">


- From above it isclear that 'K' will start from 'i+1' and ends at 'j-1'

- 'i' and 'j' will never be at k, because K will always be at 'Operator' and i and j at 'Symbols'


step 1 : find i and j values

    i=0
    j=n-1;

step 2 : Base Condition

    if(i>j)
        return 0;

    if(i==j){

        if(isTrue){
            if(exp[i]==true)
                return 1;
            else
                return 0;
        }else{
            if(exp[i]==false)
                return 1;
            else
                return 0;
        }
    }

step 3 : find k loop

    for(int k=i+1; k<j-1; k=k+2){

    }

step 4 :

<img width="285" alt="Screenshot 2022-08-11 at 12 48 47 AM" src="https://user-images.githubusercontent.com/13814143/184016742-9ab3adb7-1627-485d-bf3c-2e99b702a8eb.png">


    If we divide the exp at K then i to k-1 is left part and k+1 to j is right part.
    Left can be true or false , Right can also be true or false


    int leftTrue = solve(exp, i, k-1, isTrue);  // T
    int leftFalse = solve(exp, i, k-1, isTrue); // F

    int rightTrue = solve(exp, j, k+1, isTrue);  // T
    int rightFalse = solve(exp, j, k+1, isTrue); // F


    if k =='&'

        if(isTrue)
            ans = ans + leftTrue * rightTrue;
        else
            ans= ans + leftFalse * rightFalse
                     + leftFalse * rightTrue
                     + leftTrue * rightFalse;


    else if k=='|'

        if(isTrue)
            ans = ans + leftTrue * rightTrue
                      + leftFalse * rightTrue
                      + leftTrue * rightFalse;
        else
            ans = ans + leftFalse * rightFalse;


    else if k=='^'

        if(isTrue)
            ans = ans leftFalse * rightTrue
                      + leftTrue * rightFalse;
        else
            ans = ans + leftFalse * rightFalse
                      + leftTrue * rightTrue;

```java
write code here...
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
