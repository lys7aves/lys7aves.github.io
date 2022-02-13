---
layout: post
title: '[Codeforces] Codeforces Global Round 19'
date: 2022-02-13-12:39
author: 이유섭
cover: '/assets/img/2022-02-13-(Codeforces) Codeforces Global Round 19/solved'
tags: codeforces algorithm
---



_Last updated: 2022. 02. 13_



# Codeforces Global Round 19

![standing](\assets\img\2022-02-13-(Codeforces) Codeforces Global Round 19\standing.png)

![solved](\assets\img\2022-02-13-(Codeforces) Codeforces Global Round 19\solved.png)

![status](\assets\img\2022-02-13-(Codeforces) Codeforces Global Round 19\status.png)

![rating](\assets\img\2022-02-13-(Codeforces) Codeforces Global Round 19\rating.png)



# A. Sorting Parts (AC)

## Problem

[A. Sorting Parts](https://codeforces.com/contest/1637/problem/A)



## Process

어떠한 k에 대해서 a[0~k-1], a[k~n-1] 두 부분을 정렬했을 때, 전체가 정렬이 되지 않으려면, max(a[0~k-1]) 값이 min(a[k~n-1]) 값보다 커야 된다.



우리는 위의 조건을 만족하는 모든 k를 찾아야 하는건 아니므로, 위의 조건을 다음과 같이 단순화 시켜볼 수 있다.

어떠한 k에 대해서 max(a[0~k-1]) 값이 a[k] 보다 크면 안된다.



\+ 코드를 다 작성하다보니, 위의 내용이 곧 오름차순인지를 묻는 것임을 알게 되었다.

## Tutorial

수열 a가 오름차순으로 정렬되어 있으면 "NO", 아니면 "YES"를 출력한다.



## Solution

```c++
#include <iostream>

using namespace std;

int main()
{
	int t, n, a, maxi;
	bool ans;
	
	ios_base::sync_with_stdio(false);
	cin.tie(NULL); cout.tie(NULL);
	
	cin >> t;
	while(t--){
		cin >> n;
		
		ans = false;
		maxi = 0;
		while(n--){
			cin >> a;
			if(a < maxi) ans = true;
			maxi = a;
		}
		
		if(ans) cout << "YES\n";
		else cout << "NO\n";
	}
	
	return 0;
}
```





# B. MEX and Array (AC)

## Problem

[B. MEX and Array](https://codeforces.com/contest/1637/problem/B)



## Process



## Tutorial

cost를 최대로 하는 방법에는 여러 방법이 있겠지만, 그 중 하나는 segment들의 크기를 전부 1로 하는 것이다.

모든 부분 수열 b에 대해 크기가 1인 segment로 나누기로 했으므로, segment를 수열 b와 독립적으로 생각해볼 수 있다. 각 segment에 대한 비용도 다음과 같이 재정의 할 수 있다.

> a[i] == 0 > cost(i) = 1
>
> a[i] != 1 > cost(i) = 2



segment[i]는 (i-0+1) * (n-i) 번 나타난다.



\> 답 = sum( (i+1)*(n-i) * cost(i) )





## Solution

```c++
#include <iostream>

using namespace std;

int main()
{
	int t, n, i, a, c, cnt;
	
	ios_base::sync_with_stdio(false);
	cin.tie(NULL); cout.tie(NULL);
	
	cin >> t;
	while(t--){
		cin >> n;
		
		cnt = 0;
		for(i=0; i<n; i++){
			cin >> a;
			
			c = (i-0+1)*(n-i);
			cnt += c;
			if(a == 0) cnt += c;
		}
		
		cout << cnt << '\n';
	}
	
	return 0;
}
```





# C. Andrew and Stones (AC) 

## Problem

[C. Andrew and Stones](https://codeforces.com/contest/1637/problem/C)



## Process



## Tutorial

i번째 더미에서 돌을 모두 없애기 위해선 최소 (a[i]+1)/2 번의 작업이 필요하다.

n=3인데 2번째 더미에 돌이 홀수개이면 돌을 없애는게 불가능하다.

2~n-1번째 더미에 돌이 모두 1개씩 있으면 돌을 없애는게 불가능하다.



## Solution

```c++
#include <iostream>

using namespace std;

int a[100000];

int main()
{
	int t, n, i;
	long long cnt;
	bool all_one;
	
	ios_base::sync_with_stdio(false);
	cin.tie(NULL); cout.tie(NULL);
	
	cin >> t;
	while(t--){
		cin >> n;
		
		cnt = 0;
		all_one = true;
		for(i=0; i<n; i++){
			cin >> a[i];
			
			if(i == 0 || i == n-1) continue;
			
			cnt += (a[i]+1)/2;
			all_one &= a[i] == 1;
		}
		
		if(all_one || (n==3 && a[1]%2==1)) cout << -1 << '\n';
		else cout << cnt << '\n';
	}
	
	return 0;
}
```





# D. Yet Another Minimization Problem (AC)

## Problem

[D. Yet Another Minimization Problem](https://codeforces.com/contest/1637/problem/D)



## Process



## Tutorial

문제에 주어진 식은 다음과 같이 변경할 수 있다.

>  (a[1] + a[2] + a[3] + ... + a[n])^2 
>
> \+ (n-2)(a[1]^2 + a[2]^2 + a[3]^2 + ... a[n]^2)
>
> \+ (b[1] + b[2] + b[3] + ... + b[n])^2
>
> \+ (n-2)(b[1]^2 + b[2]^2 + b[3]^2 + ... b[n]^2)

이는 다시 아래와 같이 바꿀 수 있다.

>  (a[1] + a[2] + a[3] + ... + a[n])^2 
>
> \+ (b[1] + b[2] + b[3] + ... + b[n])^2
>
> \+ (n-2)(a[1]^2 + a[2]^2 + a[3]^2 + ... a[n]^2 + b[1]^2 + b[2]^2 + b[3]^2 + ... b[n]^2)

(n-2)로 묶인 부분은 수열 a와 b를 어떻게 설정하든 값이 변하지 않는다.

즉, 우리는 sum(a)^2 + sum(b)^2 부분의 값을 최소로 하면 된다.



이를 최소화 하는 방법은 sum(a)와 sum(b)를 최대한 비슷하게 하는 것이다.



## Solution

```c++
#include <iostream>
#include <stdio.h>

#define MAXN 110
#define MAX 10010

using namespace std;

int n, mini;
int a[MAXN], b[MAXN], a_[MAXN], b_[MAXN], pre[MAXN][2*MAX];
bool visit[MAXN][2*MAX], who[MAXN][2*MAX];

void dfs(int i, int x);
void delete_dfs(int i, int x);

int main()
{
	int t, i, x;
	long long ans, sum_a, sum2_a, sum_b, sum2_b;
	
	ios_base::sync_with_stdio(false);
	cin.tie(NULL); cout.tie(NULL);
	
	cin >> t;
	while(t--){
		cin >> n;
		for(i=1; i<=n; i++) cin >> a[i];
		for(i=1; i<=n; i++) cin >> b[i];
		
		mini = 2*MAX;
		dfs(0, MAX);
		
		x = mini;
		for(i=n; i>=1; i--){
			if(who[i][x]){
				a_[i] = a[i];
				b_[i] = b[i];
			}
			else{
				a_[i] = b[i];
				b_[i] = a[i];
			}
			
			x = pre[i][x];
		}
		
		delete_dfs(0, MAX);
		
		sum_a = sum2_a = sum_b = sum2_b = 0;
		for(i=1; i<=n; i++){
			sum_a += a_[i];
			sum2_a += a_[i] * a_[i];
			sum_b += b_[i];
			sum2_b += b_[i] * b_[i];
		}
		
		cout << sum_a*sum_a + (n-2)*sum2_a + sum_b*sum_b + (n-2)*sum2_b << '\n';
	}
	
	return 0;
}

void dfs(int i, int x)
{
	if(i == n){
		if(x < MAX) return;
		
		mini = min(mini, x);
		return;
	}
	
	int diff = a[i+1]-b[i+1];
	
	if(!visit[i+1][x+diff]){
		visit[i+1][x+diff] = true;
		pre[i+1][x+diff] = x;
		who[i+1][x+diff] = true;
		
		dfs(i+1, x+diff);
	}
	if(!visit[i+1][x-diff]){
		visit[i+1][x-diff] = true;
		pre[i+1][x-diff] = x;
		who[i+1][x-diff] = false;
		
		dfs(i+1, x-diff);
	}
}

void delete_dfs(int i, int x)
{
	if(i == n) return;
	
	int diff = a[i+1]-b[i+1];
	
	if(visit[i+1][x+diff]){
		visit[i+1][x+diff] = false;
		delete_dfs(i+1, x+diff);
	}
	if(visit[i+1][x-diff]){
		visit[i+1][x-diff] = false;
		delete_dfs(i+1, x-diff);
	}
}
```





# E. Best Pair (- > TLE)

## Problem

[E. Best Pair](https://codeforces.com/contest/1637/problem/E)



## Process

수열의 값의 개수는 최대 n개가 될 수 있지만, cnt 값의 개수는 최대 root(n)개 밖에 될 수 없다고 생각했다. 따라서 수열의 값을 기준으로 생각하는 것보다 cnt를 기준으로 생각하면 경우의 수가 좀 더 단순해질 것이라고 생각하였다.



(cnt_x + cnt_y) * (x + y)

에서 같은 cnt_x (혹은 cnt_y) 값이라면 x (혹은 y) 값이 클수록 이득일 것이다.



cnt값을 기준으로 하는 벡터 배열을 만들었다.

>  cnt_num\[i\] : cnt값이 i인 내림차순 벡터
>
> cnt_num\[i\]\[j\] : cnt값이 i인 값 중 j번째로 큰 값

이러면 우리는 모든 cnt 값들에 대하여 cnt_num\[cnt\]\[0\] 값들의 조합으로 최댓값을 얻어낼 수 있을 것이다. (cnt_x = cnt_y인 경우에 대해서는 cnt_num[cnt]의 0번째, 1번째 값이 필요하다.)



그러나 문제는 우리를 쉽게 풀 수 있도록 놔두지 않았다. 문제에서 불가능한 조합을 주었기에, 위의 과정에서 얻은 쌍이 불가능할 수도 있다.

이를 해결하기 위해 priority_queue를 썼다. 위의 과정을 priority_queue에 넣은 후, 가장 큰 함수값을 가지는 쌍을 찾는다. 만약 해당 쌍이 불가능한 쌍이 아니면 함수값을 출력하고 이 과정을 멈춘다. 만약 해당 쌍이 불가능한 쌍이라면 x(혹은 y)와 cnt가 같은 x(혹은 y) 다음의 값을 y(혹은 x)와 조합한 값을 priority_queue에 넣는다.



부족한 코딩 실력으로 열심히 짜봤지만 제한시간내에 풀지 못했다 ㅜㅜ (2분 초과돼서 제출하지 못했다 ㅜㅜ)

\+ 나중에 제출해보니 어차피 TLE였다 ㅜㅜ



## Tutorial





## Solution

```c++
#include <iostream>
#include <unordered_set>
#include <vector>
#include <queue>
#include <algorithm>

#define MAXN 300010
#define pii pair<int,int>
#define pi5 pair<int, pair<int, pair<int, pair<int, int> > > >
#define i1 first
#define i2 second.first
#define i3 second.second.first
#define i4 second.second.second.first
#define i5 second.second.second.second

using namespace std;

int a[MAXN];
unordered_set<long long> s;
vector<int> cnt_num[MAXN], cnt_vec;
priority_queue<pi5> que;

int main()
{
	int t, n, m, i, j, x, y, cnt, f;
	int cnt1, cnt1i, cnt2, cnt2i;
	
	ios_base::sync_with_stdio(false);
	cin.tie(NULL); cout.tie(NULL);
	
	cin >> t;
	while(t--){
		cin >> n >> m;
		for(i=1; i<=n; i++){
			cin >> a[i];
		}
		for(i=0; i<m; i++){
			cin >> x >> y;
			s.insert(x*MAXN+y);
			s.insert(y*MAXN+x);
		}
		
		sort(a+1, a+n+1);
		
		cnt = 0;
		for(i=n; i>=1; i--){
			cnt++;
			if(a[i] != a[i-1]){
				cnt_num[cnt].push_back(a[i]);
				if(cnt_num[cnt].size() == 1) cnt_vec.push_back(cnt);
				cnt = 0;
			}
		}
		
		for(i=0; i<cnt_vec.size(); i++){
			if(cnt_num[cnt_vec[i]].size() >= 2){
				f = cnt_vec[i]*2 * (cnt_num[cnt_vec[i]][0] + cnt_num[cnt_vec[i]][1]);
				que.push({f, {cnt_vec[i], {0, {cnt_vec[i], 1}}}});
			}
			for(j=i+1; j<cnt_vec.size(); j++){
				if(i == j) continue;
				
				f = (cnt_vec[i]+cnt_vec[j]) * (cnt_num[cnt_vec[i]][0] + cnt_num[cnt_vec[j]][0]);
				que.push({f, {cnt_vec[i], {0, {cnt_vec[j], 0}}}});
			}
		}
		
		while(!que.empty()){
			f = que.top().i1;
			cnt1 = que.top().i2;
			cnt1i = que.top().i3;
			cnt2 = que.top().i4;
			cnt2i = que.top().i5;
			que.pop();
			
			x = cnt_num[cnt1][cnt1i];
			y = cnt_num[cnt2][cnt2i];
			
			if(s.find(x*MAXN+y) == s.end()) break;
			
			if(cnt1 == cnt2){
				if(cnt_num[cnt1].size()-1 == cnt2i) continue;
				f = cnt1*2 * (cnt_num[cnt1][cnt1i+1] + cnt_num[cnt1][cnt1i+2]);
				que.push({f, {cnt1, {cnt1+1, {cnt1, cnt1+2}}}});
			}
			else{
				if(cnt_num[cnt1].size()-1 != cnt1i){
					f = (cnt1 + cnt2) * (cnt_num[cnt1][cnt1i+1] + cnt_num[cnt2][cnt2i]);
					que.push({f, {cnt1, {cnt1i+1, {cnt2, cnt2i}}}});
				}
				if(cnt_num[cnt2].size()-1 != cnt2i){
					f = (cnt1 + cnt2) * (cnt_num[cnt1][cnt1i] + cnt_num[cnt2][cnt2i+1]);
					que.push({f, {cnt1, {cnt1i, {cnt2, cnt2i+1}}}});
				}
			}
		}
		
		cout << f << '\n';
		
		
		// reset
		for(i=0; i<cnt_vec.size(); i++){
			cnt_num[cnt_vec[i]].clear();
		}
		cnt_vec.clear();
		while(!que.empty()) que.pop();
	}
	
	return 0;
}
```

