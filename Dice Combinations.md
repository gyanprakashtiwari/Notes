[Problem](https://cses.fi/problemset/task/1633)

## Approach

**State :** 
`dp[i]` is defined as number of ways to get sum `i` with dice throws
**Transition :** 
`dp[i] = dp[i-1] + dp[i-2] + . . . + dp[i-6]`

`dp[i] = sum(dp[i - diceNum]) , where 1<=diceNum<=6`
**Final Sub Problem :** 
`dp[sum]`


Code : 
```
#include <bits/stdc++.h>
using namespace std;
#define int long long

const int mod = 1e9 + 7;
const int N = 1e6 + 1;

int dp[N];

int numWaysDiceThrow(int sum) {
	if (sum == 0) {
		return 1;
	}

	if (dp[sum] != -1) {
		return dp[sum];
	}
	int ways = 0;

	for (int i = 1; i <= 6; i++) {
		if (sum - i >= 0) {
			ways += numWaysDiceThrow(sum - i);
			ways = ways % mod;
		}

	}

	dp[sum] = ways;

	return ways;

}

void solve() {
	// NO SUBMISSION WITHOUR PROOF
	int n;
	cin >> n;

	for (int i = 0; i <= n; i++) {
		dp[i] = -1;
	}

	cout << numWaysDiceThrow(n) << endl;




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