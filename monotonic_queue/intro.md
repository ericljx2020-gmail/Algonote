## Use case
- 



## Format code
```
#include<bits/stdc++.h>
using namespace std;
const int N = 1e5+5;

int n, a[N];
int q[N];
int l[N];
int main(){
    cin >> n;
    for (int i = 0; i < n; i++){
        cin >> a[i];
    }
    
    int tt = -1;
    for (int i = n-1; i >= 0; i--){
        while (tt != -1 && a[q[tt]] > a[i]){
            l[q[tt--]] = i;   
        }
        q[++tt] = i;
    }
    while (tt != -1){
        l[q[tt--]] = -1;
    }
    for (int i = 0; i < n; i++) {
        if (l[i] != -1) cout << a[l[i]] << " ";
        else cout << -1 << " ";
    }
    return 0;
}
```