## Use case
1. Find the upperbound and lowerboud of specific element in an ordered array

## Format
- Finding left boudary
```
int l = 0, r = n-1;
//找左端点
while (l < r){
    int mid = l+r >> 1;
    if (q[mid] >= k) r = mid;   //说明这个左端点一定在左边
    else l = mid+1;             
}
```
- Finding Right boudary
```
int l = 0, r = n-1;
while (l < r){
    //找右边界
    int mid = l+r+1 >> 1;       //当l = mid的时候l+r+1
    if (q[mid] <= k){
        //如果这个mid小于k说明右边界还在右边
        l = mid;        //=mid应为q[mid] <= k 不是q[mid] < k
    }else{
        r = mid-1       //q[mid] > k说明k的右边界在左边切mid一定不是
    }
}
```
### Memorizing tips: