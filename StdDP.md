# me-or-dp

<h2>The repository contains all the standard problems of dynamic programming.</h2>

<hr>

### Coin Change

####  Problem - https://practice.geeksforgeeks.org/problems/coin-change/0

```
#include<bits/stdc++.h>
using namespace std;

int dp[301][100001], a[301];

int func(int s, int n){
    if(s == 0)  return 1;
    if(s < 0)   return 0;
    if(n <= 0 && s >= 1)  return 0;
    if(dp[n][s] != -1)    return dp[n][s];
    return dp[n][s] = func(s-a[n-1], n) + func(s, n-1);
}

int main(){
    
    int tt, n, m;
    cin >> tt;
    while(tt--){
        memset(dp, -1, sizeof(dp));
        cin >> n;
        for(int i = 0; i < n; i++){
            cin >> a[i];
        }
        int s;
        cin >> s;
        cout << func(s, n) << endl;
    }
    return 0;
}

```

<hr>


### Gold Mine Problem

####  Problem - https://practice.geeksforgeeks.org/problems/gold-mine-problem/0

```
#include<bits/stdc++.h>
using namespace std;

int n, m;
int a[25][25], dp[25][25];

bool issafe(int x, int y){
    return (x >= 0 && y >= 0 && x < n && y < m);
}

int func(int x, int y){
    if(!issafe(x, y))   return 0;
    if(dp[x][y] != -1)  return dp[x][y];
    if(y == m-1)    return a[x][m-1];
    return dp[x][y] = a[x][y] + max(func(x+1, y+1), max(func(x-1, y+1), func(x, y+1)));
}

int main(){
    int tt;
    cin >> tt;
    while(tt--){
        memset(dp, -1, sizeof(dp));
        cin >> n >> m;
        for(int i = 0; i < n; i++){
            for(int j = 0; j < m; j++){
                cin >> a[i][j];
            }
        }
        int ans = 0;
        for(int i = 0; i < n; i++){
            ans = max(ans, func(i, 0));
        }
        cout << ans << endl;
    }
    
    return 0;
}
```

<hr>

