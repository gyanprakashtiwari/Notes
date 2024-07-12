```
#include <bits/stdc++.h>
using namespace std;

#define int long long
#define lld long double


int n1, n2;
string s1, s2;
int dp[1001][1001];
int ans;

int go(int p1, int p2) {
	// best LCS from s1[p1..n1-1] and s2[p2...n2-1]
	if (p1 >= n1 or p2 >= n2 ) {
		return 0;
	}
	if (dp[p1][p2] != -1) {
		return dp[p1][p2];
	}

	if (s1[p1] == s2[p2]) {
		int curr = 1 + go(p1 + 1, p2 + 1);
		return dp[p1][p2] = curr;
	}
	int a1 = go(p1 + 1, p2);
	int a2 = go(p1, p2 + 1);

	return dp[p1][p2] = 0;
}

void solve() {
	cin >> s1 >> s2;
	n1 = s1.size();
	n2 = s2.size();
	memset(dp, -1, sizeof(dp));
	ans = 0;
	int x = go(0, 0);
	for (int i = 0; i < n1; i++) {
		for (int j = 0; j < n2; j++) {
			ans = max(ans, dp[i][j]);
		}
	}
	cout << ans << endl;
}

int32_t main() {

#ifndef ONLINE_JUDGE
	freopen("Error.txt", "w", stderr);
	freopen("input.txt", "r", stdin);
	freopen("output.txt", "w", stdout);
#endif

	int tc = 1;
	cin >> tc;

	for (int t = 1; t <= tc; t++) {
		solve();
	}
	return 0;
}
```
