[Problem](https://cses.fi/problemset/task/1635/)


## Approach

**State :** 
`dp[i]` is number of ways to make sum `i`

**Transition :** 

`dp[i] = sum(dp[i - coins[j]])` where *`0 <= j <= n-1`*


**Final Sub Problem :** 
`dp[sum]`



Code : 
```
#include <bits/stdc++.h>
using namespace std;
#define int long long

const int mod = 1e9 + 7;
const int N = 1e6 + 1;
const int inf = LLONG_MAX;

int dp[N];

int minCoinsSum(int n, int sum, vector<int> &coins) {

	if (sum == 0) {
		return 0;
	}

	if (dp[sum] != -1) {
		return dp[sum];
	}

	int ans = inf;

	for (int i = 0; i < n; i++) {
		if (sum - coins[i] >= 0) {
			int curr = min(ans, minCoinsSum(n, sum - coins[i], coins));
			// check for overflow
			if (curr != inf and curr + 1 < ans) {
				ans = curr + 1;
			}
		}
	}

	dp[sum] = ans;

	return ans;
}

void solve() {
	// NO SUBMISSION WITHOUR PROOF
	int n, x;
	cin >> n >> x;
	vector<int> coins(n);


	for (int i = 0; i < n; i++) {
		cin >> coins[i];
	}

	for (int i = 0; i <= x; i++) {
		dp[i] = -1;
	}
	int ans = minCoinsSum(n, x, coins);

	if (ans == inf) {
		cout << "-1\n";
	} else {
		cout << ans << endl;
	}




}

signed main() {
	ios_base::sync_with_stdio(false); cin.tie(NULL); cout.tie(NULL);

#ifndef ONLINE_JUDGE
	freopen("Error.txt", "w", stderr);
	freopen("input.txt", "r", stdin);
	freopen("output.txt", "w", stdout);
#endif

	int tc = 1;
	// cin >> tc;

	for (int t = 1; t <= tc; t++) {
		// cout << "Case #" << t << ": ";
		solve();
	}
	return 0;
}
```