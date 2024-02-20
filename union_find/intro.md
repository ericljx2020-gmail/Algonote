## Use case
- 


## Format code
```
#include<bits/stdc++.h>
using namespace std;
const int N = 1e5+5;

int f[N],n,m;

int find(int x){
    if (f[x] != x) return f[x] = find(f[x]);
    return f[x];
}
int main(){
    cin >> n >> m;
    for (int i = 0; i < n; i++) f[i] = i;
    for (int i = 0; i < m; i++){
        char op;
        int a,b;
        cin >> op;
        cin >> a >> b;
        int fa = find(a), fb = find(b);
        if (op == 'M'){
            f[fa] = fb;
        }else{
            if (fa == fb) cout << "Yes\n";
            else cout << "No\n";
        }
    }
    return 0;
}
```

### Find function:
```
int find(int x){
    if (f[x] != x) return f[x] = find(f[x]);
    return f[x];
}
```

