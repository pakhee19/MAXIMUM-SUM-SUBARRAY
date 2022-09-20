Maximum Sum SubArray
Provides a solution to implement the solution for Maximum Sum Array by populating the array of size 14 with non-zero [positive/negative] random numbers: 10,47,-2,9,-64,1,-68,37,-8,7,23,-34,61,-3

Code:
```
#include<bits/stdc++.h>
using namespace std;

void max_crossing_subarray(int arr[],int low, int mid, int high,int &max_left,int &max_right, int &total_sum)
{
    int left_sum=INT_MIN;
    int sum=0;
    int i,j;
    for(i=mid;i>=low;i--){
        sum=sum+arr[i];
        if(sum>left_sum){
            left_sum=sum;
            max_left=i;
        }
    }
    int right_sum=INT_MIN;
    sum=0;
    for(j=mid+1;j<=high;j++){
        sum=sum+arr[j];
        if(sum>right_sum){
            right_sum=sum;
            max_right=j;
        }
    }
    total_sum=left_sum+right_sum; 
}

void maximum_subarray(int arr[],int low,int high,int &ret_low,int &ret_high,int &ret_sum){
 
 if(high==low){
     ret_low=low;
     ret_high=high;
     ret_sum=arr[low];
     return;
 }
 int mid=(high+low)/2;
 
 int left_low,left_high,left_sum;
 maximum_subarray(arr,low,mid,left_low,left_high,left_sum);
 
 int right_low,right_high,right_sum;
 maximum_subarray(arr,mid+1,high,right_low,right_high,right_sum);
 
 int cross_low,cross_high,cross_sum;
 max_crossing_subarray(arr,low,mid,high,cross_low,cross_high,cross_sum);
 
 if(left_sum>=right_sum && left_sum>=cross_sum){
     ret_low=left_low;
     ret_high=left_high;
     ret_sum=left_sum;
     return;
 }
 else if(right_sum>=left_sum && right_sum>=cross_sum)
 {
     ret_low=right_low;
     ret_high=right_high;
     ret_sum=right_sum;
     return;
 }
 else{
     ret_low=cross_low;
     ret_high=cross_high;
     ret_sum=cross_sum;
     return;
 }
    
}
int main()
{
   int arr[]={10,47,-2,9,-64,1,-68,37,-8,7,23,-34,61,-3};
   int start_index;
   int end_index;
   int sum;
   maximum_subarray(arr,0,13,start_index,end_index,sum);
   cout<<"Maximum sum is ->";
   for(int i=start_index;i<=end_index;i++){
       cout<<arr[i];
       if(i==end_index){
           break;
       }
       cout<<" + ";
  }
   cout<<" = ";
   cout<<sum;
   cout<<" \nFrom index"<<start_index<<" to "<<end_index;
     return 0;
}
```

Output: </br>
Maximum sum is ->37 + -8 + 7 + 23 + -34 + 61 = 86 
From index7 to 12
