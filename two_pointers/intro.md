## Use case
- When the array is ordered, we can think of brute force and use two pointers to enhance time complexity

## Cases
1. Both pointers start from one side.
2. Two pointers start from opposite side.

### Same side example:
```
#include <bits/stdc++.h>
using namespace std;
const int N = 1e5+10;
int n,c[N],vis[N];
//双指针算法：先从暴力方法开始思考，当我们发现数组具有某方面的单调性，可以考虑使用双指针的办法来缩减时间复杂度。

bool isncheck(int l, int r){
    if (c[l] == c[r]) return true;
    if (vis[c[r]] > 1) return true;
    return false;

}

int main(){
    cin >> n;
    for (int i = 1; i <= n; i++){
        cin >> c[i];
    }
    if (n == 1) {
        cout << 1;
        return 0;
    }
    int res = 0;
    vis[c[1]] = 1;
    for (int i = 2,j = 1; i <= n; i++){
        vis[c[i]] += 1;
        while(j < i && isncheck(j,i)){
            vis[c[j]] --;
            j++;
        }
        res = max(res, i-j+1);
    }
    cout << res;
    return 0;
}
```

### Pointers start from opposite sides
```
#include<bits/stdc++.h>
using namespace std;

const int N = 1e5+10;
int n,m,x;
int a[N],b[N];

int main(){
    cin >> n >> m >> x;
    for (int i = 1; i <= n; i++) cin >> a[i];
    for (int i = 1; i <= m; i++) cin >> b[i];

    for (int i = 1, j = m;i <= n; i++){
        while (j >= 1 && a[i] + b[j] > x) j--;
        if (j >= 1 && a[i] + b[j] == x){
            cout << i-1 << " " << j-1;
            return 0;
        }
    }
    return 0;
}
```