# me-or-dp

<h2>The repository contains all the standard problems of dynamic programming</h2>

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
<hr>

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
<hr>

### Maximum sum increasing subsequence

#### Problem - https://practice.geeksforgeeks.org/problems/maximum-sum-increasing-subsequence/0

```
#include<bits/stdc++.h>
using namespace std;

int dp[10005], a[10005];

int main(){
    int tt, n;
    cin >> tt;
    while(tt--){
        cin >> n;
        memset(dp, 0, sizeof(dp));
        for(int i = 0; i < n; i++){
            cin >> a[i];
            dp[i] = a[i];
        }
        for(int i = 1; i < n; i++){
            for(int j = 0; j < i; j++){
                if(a[i] > a[j]){
                    dp[i] = max(dp[i], dp[j]+a[i]);
                }
            }
        }
        int ans = 0;
        for(int i = 0; i < n; i++){
            ans = max(ans,dp[i]);
        }
        cout << ans << endl;
    }
    return 0;
}
```
### Max length chain

#### Problem - https://practice.geeksforgeeks.org/problems/max-length-chain/1

```
int dp[105];

bool comp(struct val a, struct val b){
    return a.first < b.first;
}

int maxChainLen(struct val p[],int n){
    memset(dp, -1, sizeof(dp));
    sort(p, p+n, comp);
    for(int i = 0; i <= n; i++) dp[i] = 1;
    for(int i = 1; i < n; i++){
        for(int j = 0; j < i; j++){
            if(p[i].first > p[j].second){
                dp[i] = dp[j] + 1;
            }
        }
    }
    int ans = INT_MIN;
    for(int i = 0; i < n; i++)  ans = max(ans, dp[i]);
    return ans;
}
```

<hr>

### Maximum Calorie

#### Problem - https://practice.geeksforgeeks.org/problems/maximum-calorie/0

```
#include<bits/stdc++.h>
using namespace std;

int dp[100005][3], a[100005];
int n;

int func(int idx, int c){
    if(idx >= n) return 0;
    if(dp[idx][c] != -1)    return dp[idx][c];
    int ans = 0;
    if(c == 2)  ans = max(ans, func(idx+1, 0));
    else    ans = max(ans, max(a[idx] + func(idx+1, c+1), func(idx+1, 0)));
    return dp[idx][c] = ans;
    
}

int main(){
    int tt;
    cin >> tt;
    while(tt--){
        cin >> n;
        for(int i = 0; i < n; i++)  cin >> a[i];
        memset(dp, -1, sizeof(dp));
        cout << func(0, 0) << endl;
    }
    
    return 0;
}
```
<hr>


### Taking 1 out of 3 consecutives

#### Problem - https://practice.geeksforgeeks.org/problems/taking-1-out-of-3-consecutives/0/
```
#include<bits/stdc++.h>
using namespace std;

int dp[100005][3], a[100005];
int n;

int func(int idx, int c){
    if(idx >= n) return 0;
    if(dp[idx][c] != -1)    return dp[idx][c];
    int ans = INT_MAX;
    if(c == 2)  ans = min(ans, a[idx] + func(idx+1, 0));
    else    ans = min(ans, min(a[idx] + func(idx+1, 0), func(idx+1, c+1)));
    return dp[idx][c] = ans;
    
}

int main(){
    int tt;
    cin >> tt;
    while(tt--){
        cin >> n;
        for(int i = 0; i < n; i++)  cin >> a[i];
        if(n <= 2){
            if(n == 1)  cout << a[0] << endl;
            else    cout << min(a[0], a[1]) << endl;
            continue;
        }
        memset(dp, -1, sizeof(dp));
        cout << func(0, 0) << endl;
    }
    
    return 0;
}
```

### Count binary strings
#### https://practice.geeksforgeeks.org/problems/count-binary-strings1944/1

```
int n, k;
int dp[1005][2][1005];
const int mod = 1000000007;

class Solution
{
  public:
    int func(int idx, int prev, int consecutive){
        if(idx == n-1)    return consecutive == k;
        int &x = dp[idx][prev][consecutive];
        if(x != -1) return x;
        if(prev)    x = (func(idx+1, 0, consecutive)%mod + func(idx+1, 1, consecutive+1)%mod)%mod;
        else    x = (func(idx+1, 0, consecutive)%mod + func(idx+1, 1, consecutive)%mod)%mod;
        return x;
    }
    int countStrings(int a, int b){
        memset(dp, -1, sizeof(dp));
        n = a, k = b;
        int ans = (0LL + func(0, 0, 0) + func(0, 1, 0))%mod;
        return ans;
    }
 
};
```

### Longest Palindromic Subsequence
#### https://leetcode.com/problems/longest-palindromic-subsequence/

```
class Solution {
public:
    int dp[1005][1005];
    string a;
    int func(int i, int j){
        if(i > j)   return 0;
        if(i == j)  return 1;
        if(dp[i][j] != -1)  return dp[i][j];
        if(a[i] == a[j])    return dp[i][j] = 2 + func(i+1, j-1);
        return dp[i][j] = max(func(i+1, j), func(i, j-1));
    }
    int longestPalindromeSubseq(string s) {
        a = s;
        memset(dp, -1, sizeof(dp));
        return func(0, s.size()-1);
    }
};
```

### Minimum Insertion Steps to Make a String Palindrome

#### Problem - https://leetcode.com/problems/minimum-insertion-steps-to-make-a-string-palindrome/

```
class Solution {
public:
    int dp[1000][1000];
    string a;
    int lps_length(int i, int j){
        if(i > j)   return 0;
        if(i == j)  return 1;
        if(dp[i][j] != -1)  return dp[i][j];
        if(a[i] == a[j])    return dp[i][j] = 2 + lps_length(i+1, j-1);
        return dp[i][j] = max(lps_length(i+1, j), lps_length(i, j-1));
    }
    int minInsertions(string s) {
        memset(dp, -1, sizeof(dp));
        a = s;
        int length = s.size();
        return length - lps_length(0, length-1);
    }
};
```

### Max Dot Product of Two Subsequences

#### Problem - https://leetcode.com/problems/max-dot-product-of-two-subsequences/

```
class Solution {
public:
    int dp[1005][1005];
    int max_dp(int i, int j, vector < int > &a, vector < int > &b){
        if(i < 0 || j < 0)  return INT_MIN;
        if(dp[i][j] != -1) return dp[i][j];
        int A = a[i]*b[j] + max(0, max_dp(i-1, j-1, a, b));
        int B = max_dp(i-1, j, a, b);
        int C = max_dp(i, j-1, a, b);
        int D = max_dp(i-1, j-1, a, b);
        return dp[i][j] = max(D, max(A, max(B, C)));
    }
    int maxDotProduct(vector<int>& nums1, vector<int>& nums2) {
        memset(dp, -1, sizeof(dp));
        return max_dp(nums1.size()-1, nums2.size()-1, nums1, nums2);
    }
};
```
