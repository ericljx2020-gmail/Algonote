## Use case
1. Can be used to implement calculator
2. Can be used to find the first element on the right/left that is greater/smaller than current element for all element in the stack

## Format code:
```
#include<bits/stdc++.h>
using namespace std;
const int N = 1e5+5;

int st[N], hh = -1;         //hh初始化为-1更方便于管理
int n;
string op;

int main(){
    cin >> n;
    while (n--){
        cin >> op;
        int a;
        if (op == "push"){
            cin >> a;
            st[++hh] = a;
        }else if (op == "pop"){
            hh--;
        }else if (op == "empty"){
            if (hh < 0){
                puts("YES");
            }else{
                puts("NO");
            }
        }else if (op == "query"){
            cout << st[hh] << endl;
        }
    }
    return 0;
}
```

## Exmaple problem  (LC42)
### Solution:
```
class Solution {
public:
    static const int N = 2e4+4;
    int trap(vector<int>& h) {
        int n = h.size();
        vector<int> asc(n, 0), dec(n,n);
        int tt = -1;
        int q[N];
        for (int i = 0; i < n; i++){
            while (tt != -1 && h[q[tt]] <= h[i]){
                asc[q[tt]] = i;
                tt--;
            }
            q[++tt] = i;
        }
        tt = -1;
        for (int i = n-1; i >= 0; i--){
            while (tt != -1 && h[q[tt]] <= h[i]){
                dec[q[tt]] = i;
                tt--;
            }
            q[++tt] = i;
        }

        int res = 0;
        for (int i = 0; i < n; i++){
            int r = asc[i];
            for (int j = i+1; j < r; j++){
                res += max(0, h[i] - h[j]);
                h[j] = h[i];
            }
        }
        for (int i = n-1; i >= 0; i--){
            int l = dec[i];
            for (int j = i-1; j > l; j--){
                res += max(0, h[i] - h[j]);
                h[j] = h[i];
            }
        }
        return res;
        
        return 0;
    }
};
```