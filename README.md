Find a specific pair in Matrix in C
Here, in this page we will discuss the program to find a specific pair in matrix in C Programming language. We are given with an n x n matrix mat[n][n] of integers, find the maximum value of mat(c, d) – mat(a, b) over all choices of indexes such that both c > a and d > b.

Find a specific pair in Matrix in C
Method Discussed :
Method 1 :Using Linear Search
Method 2 : Using Binary Search
Let’s discuss them one by one in brief,

Method 1:
For all values mat(a, b) in the matrix
Find mat(c, d) that has maximum value such that c > a and d > b and keeps on updating maximum value found so far.
Finally return the maximum value.
Time and Space Complexity :
Time complexity: O(N*N)
Space complexity: O(1)
Method 1 : Code in C
Run
#include <stdio.h>
#include <limits.h>
#define N 5

int findMaxValue(int mat[][N])
{
    int maxValue = INT_MIN;

    for (int a = 0; a < N - 1; a++)
    for (int b = 0; b < N - 1; b++)
        for (int d = a + 1; d < N; d++)
        for (int e = b + 1; e < N; e++)
            if (maxValue < (mat[d][e] - mat[a][b]))
                maxValue = mat[d][e] - mat[a][b];
 
    return maxValue;
}
 
int main()
{
int mat[N][N] = {
                { 1, 2, -1, -4, -20 },
                { -8, -3, 4, 2, 1 },
                { 3, 8, 6, 1, 3 },
                { -4, -1, 1, 7, -6 },
                { 0, -4, 10, -5, 1 }
            };
    printf("Maximum Value is %d", findMaxValue(mat));
 
    return 0;
}
Output :
Maximum Value is 18
Method 2:
Check to see if the middle element is Fixed Point.
If it is, return it; otherwise, if the middle + 1 element’s index is less than or equal to the value at the high index, Fixed Point(s) may be on the right side of the middle point (obviously only if there is a Fixed Point).
If the middle – 1 element’s index is larger than or equal to the value at the low index, Fixed Point(s) may be on the left side of the middle point.
Method 2 : Code in C
Run
#include <stdio.h>
#include <limits.h>
#define N 5

int max(int a, int b){
    if(a>b)
        return a;
    return b;
}
 
int findMaxValue(int mat[][N])
{
    int maxValue = INT_MIN;
 
     int maxArr[N][N];
 
    maxArr[N-1][N-1] = mat[N-1][N-1];
 
    int maxv = mat[N-1][N-1]; 
    for (int j = N - 2; j >= 0; j--)
    {
        if (mat[N-1][j] > maxv)
            maxv = mat[N - 1][j];
        maxArr[N-1][j] = maxv;
    }
 
    
    maxv = mat[N - 1][N - 1]; 
    for (int i = N - 2; i >= 0; i--)
    {
        if (mat[i][N - 1] > maxv)
            maxv = mat[i][N - 1];
        maxArr[i][N - 1] = maxv;
    }
 
    for (int i = N-2; i >= 0; i--)
    {
        for (int j = N-2; j >= 0; j--)
        {
        
            if (maxArr[i+1][j+1] - mat[i][j] > maxValue)
                maxValue = maxArr[i + 1][j + 1] - mat[i][j];
 
            maxArr[i][j] = max(mat[i][j],max(maxArr[i][j + 1],maxArr[i + 1][j]));
        }
    }
 
    return maxValue;
}
 
int main()
{
    int mat[N][N] = {
                      { 1, 2, -1, -4, -20 },
                      { -8, -3, 4, 2, 1 },
                      { 3, 8, 6, 1, 3 },
                      { -4, -1, 1, 7, -6 },
                      { 0, -4, 10, -5, 1 }
                    };
    printf("Maximum Value is %d", findMaxValue(mat));
 
    return 0;
}
Output :
Maximum Value is 18
