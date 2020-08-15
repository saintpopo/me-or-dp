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
