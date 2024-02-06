## Use case
 - When the range of array element is large and number of element is small. And the operation doesn't matter on distance between element. We can use discretization.

## Idea
1. Record all elements that need to be discretize.
2. Sort elements and erase duplicated items.
3. When need do do operation on an element, use binary search to find the discretized location and do on that location.

## Code Format
```
#include<bits/stdc++.h>
#define x first
#define y second
using namespace std;
typedef pair<int,int> PII;
const int N = 3e5+5;
int n,m,l,r,x,c;
int a[N],s[N];
vector<PII>add, query;
vector<int> all;

int find(int x){
    int l = 0, r = all.size()-1;
    while (l < r){
        int mid = l + r >> 1;
        if (all[mid] >= x) r = mid;
        else l = mid+1;
    }
    return l+1;         //l+1就是以坐标1为第一个数
}
int main(){
    cin >> n >> m;
    for (int i = 0; i < n; i++){
        cin >> x >> c;
        add.push_back({x,c});
        all.push_back(x);
    }
    for (int i = 0; i < m; i++){
        cin >> l >> r;
        query.push_back({l,r});
        all.push_back(l);
        all.push_back(r);
    }

    sort(all.begin(), all.end());
    all.erase(unique(all.begin(), all.end()), all.end());


    //处理增加部分
    for (int i = 0; i < add.size(); i++){
        int p = find(add[i].x);           //找到x的离散化后的坐标
        a[p] += add[i].y;
    }

    //处理前缀和
    for (int i = 1; i <= all.size(); i++){
        s[i] = s[i-1] + a[i];
    } 

    //处理询问部分
    for (int i = 0; i < query.size(); i++){
        l = find(query[i].x);
        r = find(query[i].y);
        cout << s[r] - s[l-1] << endl;
    }

    return 0;
}
```

#### Find function
```
int find(int x){
    int l = 0, r = all.size();
    while (l < r){
        int mid = l + r >> 1;
        if (all[mid] >= x) r = mid;
        else l = mid+1;
    }
    return l+1;         //下表从1开始
}
```

#### Erase duplicates in C++
```
sort(all.begin(), all.end());
all.erase(unique(all.begin(), all.end()), all.end());
```