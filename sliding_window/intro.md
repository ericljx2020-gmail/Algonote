## Use case


## Format code
```
#include<bits/stdc++.h>
using namespace std;
const int N = 1e6+6;
int a[N], q[N];             //a[]原数组, q[]队列
int n,k;
int main(){
    cin >> n >> k;
    for (int i = 0; i < n; i++){
        cin >> a[i];
    }

    int hh = 0, tt = -1;
    for (int i = 0; i < n; i++){
        if (hh <= tt && q[hh] < i - k + 1) hh++;                        //如果队头元素已经超过了当前队列的长度，删掉它
        while (hh <= tt && a[q[tt]] >= a[i]) tt--;           //如果窗口有长度，并且窗口的最右边的值大于新加入的元素，说明最右边的这个元素没有机会成为这个包括新元素的窗口里的最小值了
        q[++tt] = i;

        if (i >= k-1) cout << a[q[hh]] << " ";                    //我们维护了一个从小到大的单调窗口，因此队头就是最小元素
    }
    puts("");
    hh = 0, tt = -1;
    for (int i = 0; i < n; i++){
        if (hh <= tt && q[hh] < i- k + 1) hh++;
        while (hh <= tt && a[q[tt]] <= a[i]) tt--;
        q[++tt] = i;

        if (i >= k-1) cout << a[q[hh]] << " ";
    }
    return 0;
}
```