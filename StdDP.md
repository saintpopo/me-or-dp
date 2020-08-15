# me-or-dp

<h2>The repository contains all the standard problems of dynamic programming.</h2>

##  Problems :

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

### Friends Pairing Problem

####  Problem - https://practice.geeksforgeeks.org/problems/friends-pairing-problem/0

```
#include<bits/stdc++.h>
using namespace std;
#define int long long int
const int mod = 1000000007;

int dp[105];

int func(int n){
    if(n <= 2)  return n;
    if(dp[n] != -1) return dp[n];
    return dp[n] = (func(n-1)%mod + ((n-1)%mod*func(n-2)%mod)%mod)%mod;
}

signed main(){
    int tt, n;
    cin >> tt;
    while(tt--){
        memset(dp, -1, sizeof(dp));
        cin >> n;
        cout << func(n)%mod << endl;
    }
    return 0;
}
```
<hr>

### Subset Sum Problem

#### Problem - https://practice.geeksforgeeks.org/problems/subset-sum-problem/0
```

#include<bits/stdc++.h>
using namespace std;

int a[100005], dp[100005][101];

int func(int s, int n){
    if((n <= 0 && s != 0) || (s < 0)) return 0;
    if(s == 0)  return 1;
    if(dp[s][n] != -1)  return dp[s][n];
    return dp[s][n] = func(s-a[n-1], n-1) || func(s, n-1);
}

int main(){
    int tt, n;
    cin >> tt;
    while(tt--){
        int s = 0;
        memset(dp, -1, sizeof(dp));
        cin >> n;
        for(int i = 0; i < n; i++){
            cin >> a[i];
            s += a[i];
        }
        if(s%2 != 0){
            cout << "NO\n";
            continue;
        }
        s /= 2;
        if(func(s, n)){
            cout << "YES\n";
        }
        else{
            cout << "NO\n";
        }
    }
    
    return 0;
}

```

<hr>

### Nth Catalan Number

#### Problem - https://practice.geeksforgeeks.org/problems/nth-catalan-number/0

```
#include<bits/stdc++.h>
using namespace std;
#include <boost/multiprecision/cpp_int.hpp> 
using boost::multiprecision::cpp_int; 

vector < cpp_int > dp(105);

cpp_int func(int n){
    if(n == 0 || n == 1)  return 1;
    if(dp[n] != 0) return dp[n];
    cpp_int res = 0;
    for(int i = 0; i < n; i++){
        res += func(i) * func(n-i-1);
    }
    return dp[n] = res;
}

signed main(){
    int tt, n;
    cin >> tt;
    while(tt--){
        cin >> n;
        cpp_int ans = func(n);
        cout << ans << endl;
    }
    return 0;
}
```

<hr>

### Maximize the Cut Segments

#### Problem - https://practice.geeksforgeeks.org/problems/cutted-segments/0

```
#include<bits/stdc++.h>
using namespace std;

int n, a, b, c;

int dp[100005];

int func(int n){
    if(n < 0)   return INT_MIN;
    if(n == 0)  return 0;
    if(dp[n] != -1) return dp[n];
    return dp[n] = 1 + max(func(n-a), max(func(n-b), func(n-c)));
}

int main(){
    int tt;
    cin >> tt;
    while(tt--){
        memset(dp, -1 ,sizeof(dp));
        cin >> n >> a >> b >> c;
        cout << func(n) << endl;
    }
    return 0;
}
```
<hr>

### Longest Common Subsequence

#### Problem - https://practice.geeksforgeeks.org/problems/longest-common-subsequence/0

```
#include<bits/stdc++.h>
using namespace std;

string s, t;
int dp[105][105];

int dfs(int m, int n){
    if(m <= 0 || n <= 0){
        return 0;
    }
    if(dp[m][n] != -1)  return dp[m][n];
    if(s[m-1] == t[n-1])    return 1 + dfs(m-1, n-1);
    return dp[m][n] = max(dfs(m-1, n), dfs(m, n-1));
}

int main(){
    int tt;
    cin >> tt;
    while(tt--){
        int m, n;
        cin >> m >> n; 
        cin >> s >> t;
        memset(dp, -1, sizeof(dp));
        cout << dfs(m, n) << endl;
    }
    return 0;
}
```

<hr>

### Longest Repeating Subsequence

#### Problem - https://practice.geeksforgeeks.org/problems/longest-repeating-subsequence/0

```
#include<bits/stdc++.h>
using namespace std;

string a, b;
int n;
int dp[1001][1001];

int func(int n, int m){
    if(n == 0 || m == 0)    return 0;
    if(dp[n][m] != -1)  return dp[n][m];
    if(a[n-1] == b[m-1] && m != n)    return dp[n][m] = 1 + func(n-1, m-1);
    return dp[n][m] = max(func(n-1, m), func(n, m-1));
}

int main(){
    int tt;
    cin >> tt;
    while(tt--){
        memset(dp, -1, sizeof(dp));
        cin >> n >> a;
        b = a;
        cout << func(n, n) << endl;
    }
    return 0;
}
```

<hr>


### Longest Increasing Subsequence

#### Problem - https://practice.geeksforgeeks.org/problems/longest-increasing-subsequence/0

```
#include<bits/stdc++.h>
using namespace std;

int dp[1005], a[1005];

int main(){
    int tt, n;
    cin >> tt;
    while(tt--){
        cin >> n;
        memset(dp, 0, sizeof(dp));
        for(int i = 0; i < n; i++){
            cin >> a[i];
            dp[i] = 1;
        }
        for(int i = 1; i < n; i++){
            for(int j = 0; j < i; j++){
                if(a[i] > a[j]){
                    dp[i] = max(dp[i], dp[j]+1);
                }
            }
        }
        int ans = 1;
        for(int i = 0; i < n; i++){
            ans = max(ans,dp[i]);
        }
        cout << ans << endl;
    }
    return 0;
}
```

### LCS of three strings

#### Problem - https://practice.geeksforgeeks.org/problems/lcs-of-three-strings/0

```
using namespace std;
#define ll long long int

ll dp[101][101][101];

ll func(string &a, string &b, string &c, ll n, ll m, ll k){
    if(n == -1 || m == -1 || k == -1){
        return 0;
    }
    if(dp[n][m][k] != -1){
        return dp[n][m][k];
    }
    if(a[n] == b[m] && b[m] == c[k]){
        return dp[n][m][k] =  1 + func(a, b, c, n-1, m-1, k-1);
    }
    else{
        return dp[n][m][k] = max(func(a, b, c, n-1, m, k), max(func(a, b, c, n, m-1, k), func(a, b, c, n, m, k-1)));
    }
}
int main(){
    ll tt, n, m, k;
    string a, b, c;
    cin >> tt;
    while(tt--){
        memset(dp, -1, sizeof(dp));
        cin >> n >> m >> k;
        cin >> a >> b >> c;
        cout << func(a, b, c, n-1, m-1, k-1) << endl;
    }
    
    return 0;
}
```
