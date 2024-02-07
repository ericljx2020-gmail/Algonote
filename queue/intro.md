## Use case
1. Sliding window find the max/min element in a k-size window
2. BFS use queue to record the order of points


## Format code:
```
#include<bits/stdc++.h>
using namespace std;
const int N = 1e5+5;

int q[N], hh = 0, tt = -1;
int main(){
    int n;
    cin >> n;
    while (n--){
        string op;
        int a;
        cin >> op;
        if (op == "push"){
            cin >> a;
            q[++tt] = a;            //tt 本来是-1，第一个元素加入编程0
        }else if (op == "pop"){
            hh++;                   //不用删除元素，直接hh++表示忽略掉那个元素
        }else if (op == "empty"){
            if (hh > tt){
                puts("YES");
            }else{
                puts("NO");
            }
        }else if (op == "query"){
            cout << q[hh] << endl;
        }
    }
    return 0;
}
```

## Usage in BFS:
```
#include <bits/stdc++.h>
using namespace std;
const int N = 1e2+5;
typedef pair<int, int> PII;
int n,m,d[N][N],s[N][N];
int dirx[4] = {0,0,1,-1};
int diry[4] = {1,-1,0,0};
queue<PII> q;

int bfs(){
    q.push({1,1});
    d[1][1] = 0;
    while(q.size()){
        PII t = q.front();
        q.pop();
        for (int i = 0; i < 4; i++){
            int x = t.first+dirx[i], y = t.second+diry[i];
            if (x >= 1 && x <= n && y>=1 && y <= m && !s[x][y] && d[x][y] == -1){
                //如果可以走，1，入队；2记录
                q.push({x,y});
                d[x][y] = d[t.first][t.second]+1;
            }
        }
    }
    return d[n][m];
}

int main(){
    cin >> n >> m;
    memset(d,-1,sizeof(d));
    for (int i = 1; i <= n; i++){
        for (int j = 1; j <= m; j++){
            cin >> s[i][j];
        }
    }
    cout << bfs() << endl;

}
```