---
layout: post
title: '[Codeforces] Codeforces Round #771 (Div. 2)'
date: 2022-02-16
author: 이유섭
cover: '/assets/img/2022-02-16-(Codeforces) Codeforces Round 771 (Div. 2)/problem.png'
tags: codeforces algorithm
---



_Last updated: 2022. 02. 16_



# Codeforces Round #771 (Div. 2)

![problem](\assets\img\2022-02-16-(Codeforces) Codeforces Round 771 (Div. 2)\problem.png)

![submission](\assets\img\2022-02-16-(Codeforces) Codeforces Round 771 (Div. 2)\submission.png)

![standing](\assets\img\2022-02-16-(Codeforces) Codeforces Round 771 (Div. 2)\standing.png)

![rating](\assets\img\2022-02-16-(Codeforces) Codeforces Round 771 (Div. 2)\rating.png)





# A. Reverse (AC)

## Problem

[A. Reverse](https://codeforces.com/contest/1638/problem/A)



## Process

자칫 문제가 복잡해질 수도 있었지만 다행히도, 순열이 1~n까지의 숫자가 하나씩 들어 있다.

우리의 목표는 최대한 작은 숫자들을 앞으로 몰아넣는 것이다.

그러나 i번째까지 1부터 i까지로 이루어져 있다면 이 부분은 굳이 바꿀 필요가 없다.

그렇다면 처음으로 i번째에 i+1이 없는 경우가 문제인데, 이 경우 i+1번째부터 i+1의 값이 있는 곳을 뒤집어주면 된다.

또한 우리는 단 한번만의 뒤집는 기회가 있기 때문에 나머지 부분은 그대로 출력해주면 된다.



## Tutorial



## Solution

```c++
#include <iostream>
#include <stack>

using namespace std;

int p[510];
stack<int> s;

int main()
{
	int t, n, i, x;
	
	ios_base::sync_with_stdio(false);
	cin.tie(NULL); cout.tie(NULL);
	
	cin >> t;
	while(t--){
		cin >> n;
		for(i=1; i<=n; i++){
			cin >> p[i];
		}
		
		for(i=1; i<=n; i++){
			if(p[i] != i) break;
			cout << p[i] << ' ';
		}
		
		x = i;
		for(; i<=n; i++){
			s.push(p[i]);
			if(p[i] == x) break;
		}
		
		while(!s.empty()){
			cout << s.top() << ' ';
			s.pop();
		}
		
		for(i=i+1; i<=n; i++){
			cout << p[i] << ' ';
		}
		
		cout << '\n';
	}
	
	return 0;
}
```





# B. Odd Swap Sort (AC)

## Problem

[B. Odd Swap Sort](https://codeforces.com/contest/1638/problem/B)



## Process

인접한 수의 합이 홀수라는 것은 인접한 두 수의 홀짝성이 다르다는 의미이다.

이에 대한 개념을 알고 있다면 잘 생각해보면 짝수끼리 혹은 홀수끼리는 순서를 바꿀 수 없지만 홀수와 짝수는 순서를 바꿀 수 있다는 의미로 해석이 가능하다.

즉, 홀수만 봤을 때, 그리고 짝수만 봤을 때, 각각 수열이 오름차순으로 되어 있어야 전체 수열을 오름차순으로 바꿀 수 있다는 뜻이 된다.



## Tutorial

홀수끼리, 짝수끼리만 봤을 때, 각각 오름차순으로 되어 있으면 "Yes", 아니면 "No"를 출력해주면 된다.



## Solution

```c++
#include <iostream>

using namespace std;

int main()
{
	int t, n, a, i, even, odd;
	bool ans;
	
	ios_base::sync_with_stdio(false);
	cin.tie(NULL); cout.tie(NULL);
	
	cin >> t;
	while(t--){
		cin >> n;
		
		ans = true;
		even = odd = 0;
		
		for(i=0; i<n; i++){
			cin >> a;
			
			if(a%2){	// odd
				ans &= a >= odd;
				odd = a;
			}
			else{
				ans &= a >= even;
				even = a;
			}
		}
		
		if(ans) cout << "Yes\n";
		else cout << "No\n";
	}
	
	return 0;
}
```





# C. Inversion Graph (AC)

## Problem

[C. Inversion Graph](https://codeforces.com/contest/1638/problem/C)



## Process



## Tutorial



## Solution

```c++
#include <iostream>

using namespace std;

int idx[100010];

int main()
{
	int t, n, i, p, max_idx, cnt;
	
	ios_base::sync_with_stdio(false);
	cin.tie(NULL); cout.tie(NULL);
	
	cin >> t;
	while(t--){
		cin >> n;
		for(i=1; i<=n; i++){
			cin >> p;
			idx[p] = i;
		}
		
		max_idx = cnt = 0;
		for(i=1; i<=n; i++){
			max_idx = max(max_idx, idx[i]);
			
			if(max_idx == i) cnt++;
		}
		
		cout << cnt << '\n';
	}
	
	return 0;
}
```





# D. Big Brush (WA)

## Problem

[D. Big Brush](https://codeforces.com/contest/1638/problem/D)



## Process



## Tutorial



## Solution 1 (WA)

```c++
#include <stdio.h>

#define MAXN 1010

int a[MAXN][MAXN];
int last_in_row[MAXN], last_in_col[MAXN];

int main()
{
	int n, m, i, j;
	int last_row=0, last_col=0, rlast=0, clast=0;
	int square;
	bool row=true, col=true;
	
	scanf("%d %d", &n, &m);
	for(i=1; i<=n; i++){
		for(j=1; j<=m; j++){
			scanf("%d", &a[i][j]);
		}
	}
	
	for(i=1; i<=n; i++){
		for(j=1; j<=m; j++){
			if(a[i][j] == a[i][j+1]) last_in_row[i] = j;
			if(a[i][j] == a[i+1][j]) last_in_col[j] = i;
		}
	}
	
	for(i=1; i<=n; i++) row &= (last_in_row[i] != 0);
	for(j=1; j<=m; j++) col &= (last_in_col[j] != 0);
	
	for(i=1; i<n; i++){
		square = 0;
		for(j=1; j<=m; j++){
			if(a[i][j] != a[i+1][j]) break;
			if((a[i][j] == a[i][j+1]) && (a[i][j] == a[i+1][j]) && (a[i][j] == a[i+1][j+1])) square = j;
		}
		
		if(j==m+1 && square){
			last_row = i;
			rlast = square;
		}
	}
	for(j=1; j<m; j++){
		square = 0;
		for(i=1; i<=n; i++){
			if(a[i][j] != a[i][j+1]) break;
			if((a[i][j] == a[i][j+1]) && (a[i][j] == a[i+1][j]) && (a[i][j] == a[i+1][j+1])) square = i;
		}
		
		if(i==n+1 && square){
			last_col = j;
			clast = square;
		}
	}
	
//	printf("%d %d %d %d %d %d\n", row, last_row, rlast, col, last_col, clast);
	
	if(row && last_row!=0){
		printf("%d\n", (n-1)*(m-1));
		
		for(i=1; i<last_row; i++){
			for(j=1; j<last_in_row[i]; j++) printf("%d %d %d\n", i, j, a[i][j]);
			for(j=m-1; j>last_in_row[i]; j--) printf("%d %d %d\n", i, j, a[i][j+1]);
			printf("%d %d %d\n", i, j, a[i][j]);
		}
		for(i=n-1; i>last_row; i--){
			for(j=1; j<last_in_row[i+1]; j++) printf("%d %d %d\n", i, j, a[i+1][j]);
			for(j=m-1; j>last_in_row[i+1]; j--) printf("%d %d %d\n", i, j, a[i+1][j+1]);
			printf("%d %d %d\n", i, j, a[i+1][j]);
		}
		
		for(j=1; j<rlast; j++) printf("%d %d %d\n", i, j, a[i][j]);
		for(j=m-1; j>rlast; j--) printf("%d %d %d\n", i, j, a[i][j+1]);
		printf("%d %d %d\n", i, j, a[i][j]);
		
		return 0;
	}
	if(col && last_col!=0){
		printf("%d\n", (n-1)*(m-1));
		
		for(j=1; j<last_col; j++){
			for(i=1; i<last_in_col[j]; i++) printf("%d %d %d\n", i, j, a[i][j]);
			for(i=n-1; i>last_in_col[j]; i--) printf("%d %d %d\n", i, j, a[i+1][j]);
			printf("%d %d %d\n", i, j, a[i][j]);
		}
		for(j=m-1; j>last_col; j--){
			for(i=1; i<last_in_col[j+1]; i++) printf("%d %d %d\n", i, j, a[i][j+1]);
			for(i=n-1; i>last_in_col[j+1]; i--) printf("%d %d %d\n", i, j, a[i+1][j+1]);
			printf("%d %d %d\n", i, j, a[i][j+1]);
		}
		
		for(i=1; i<clast; i++) printf("%d %d %d\n", i, j, a[i][j]);
		for(i=n-1; i>clast; i--) printf("%d %d %d\n", i, j, a[i+1][j]);
		printf("%d %d %d\n", i, j, a[i][j]);
		
		return 0;
	}
	
	printf("-1");
	
	return 0;
}
```



## Solution 2 (-)

```c++
#include <stdio.h>
#include <queue>
#include <stack>

#define MAXN 1010

using namespace std;

int a[MAXN][MAXN], b[MAXN][MAXN];
queue<int> que;
stack<int> ans;

int main()
{
	int n, m, i, j, x, y, z, ii, jj, c;
	bool flag;
	
	scanf("%d %d", &n, &m);
	for(i=1; i<=n; i++){
		for(j=1; j<=m; j++){
			scanf("%d", &a[i][j]);
			b[i][j] = a[i][j];
		}
	}
	
	for(i=1; i<n; i++){
		for(j=1; j<n; j++){
			if(a[i][j] == a[i][j+1] && a[i][j] == a[i+1][j] && a[i][j] == a[i+1][j+1]){
				que.push(i);
				que.push(j);
				que.push(a[i][j]);
			}
		}
	}
	
	while(!que.empty()){
		x = que.front(); que.pop();
		y = que.front(); que.pop();
		z = que.front(); que.pop();
		
		flag = true;
		for(i=x; i<=x+1; i++){
			for(j=y; j<=y+1; j++){
				flag &= b[i][j] == 0;
			}
		}
		if(flag) continue;
		
		ans.push(z);
		ans.push(y);
		ans.push(x);
		
		b[x][y] = b[x+1][y] = b[x][y+1] = b[x+1][y+1] = 0;
		for(i=x-1; i<=x+1; i++){
			if(i <= 0 || i >= n) continue;
			for(j=y-1; j<=j+1; j++){
				if(j <= 0 || j >= m) continue;
				c = 0;
				for(ii=i; ii<=i+1; ii++){
					for(jj=j; jj<=j+1; jj++){
						if(b[ii][jj] != 0) c = b[ii][jj];
					}
				}
				if(c == 0) continue;
				
				flag = true;
				for(ii=i; ii<=i+1; ii++){
					for(jj=j; jj<=j+1; jj++){
						if(b[ii][jj] == 0) continue;
						flag &= b[ii][jj]==c;
					}
				}
				
				if(flag){
					que.push(i);
					que.push(j);
					que.push(c);
				}
			}
		}
	}
	
	flag = true;
	for(i=1; i<=n; i++){
		for(j=1; j<=m; j++){
			flag &= a[i][j] == 0;
		}
	}
	
	if(flag){
		printf("%d\n", ans.size());
		while(!ans.empty()){
			x = ans.top(); ans.pop();
			y = ans.top(); ans.pop();
			z = ans.top(); ans.pop();
			printf("%d %d %d\n", x, y, z);
		}
	}
	else printf("-1");
	
	return 0;
}
```



## Test code

```c++
#include <stdio.h>
#include <algorithm>

#define MAXN 1010

using namespace std;

int a[MAXN][MAXN];

int main()
{
	while(1){
		int n=0, m=0, i, j, c, t;
		
		scanf("%d", &t);
		while(t--){
			scanf("%d %d %d", &i, &j, &c);
			a[i][j] = a[i][j+1] = a[i+1][j] = a[i+1][j+1] = c;
			
			n = max(n, i+1);
			m = max(m, j+1);
		}
		
		for(i=1; i<=n; i++){
			for(j=1; j<=m; j++){
				printf("%d ", a[i][j]);
				a[i][j] = 0;
			}
			printf("\n");
		}
	}
	
	return 0;
}
```



