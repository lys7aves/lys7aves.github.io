---
layout: post
title: '[Codeforces] Codeforces Round #775 (Div. 2, based on Moscow Open Olympiad in Informatics)'
date: 2022-03-07-23:31
author: 이유섭
cover: '/assets/img/2022-03-07-(Codeforces) Codeforces Round 775 (Div. 2, based on Moscow Open Olympiad in Informatics)/problems.png'
tags: codeforces algorithm
---



_Last updated: 2022. 03. 07_



# Codeforces Round #775 (Div. 2, based on Moscow Open Olympiad in Informatics)

![problems](assets\img\2022-03-07-(Codeforces) Codeforces Round 775 (Div. 2, based on Moscow Open Olympiad in Informatics)\problems.png)

![submissions](assets\img\2022-03-07-(Codeforces) Codeforces Round 775 (Div. 2, based on Moscow Open Olympiad in Informatics)\submissions.png)

![standing](assets\img\2022-03-07-(Codeforces) Codeforces Round 775 (Div. 2, based on Moscow Open Olympiad in Informatics)\standing.png)

![rating](assets\img\2022-03-07-(Codeforces) Codeforces Round 775 (Div. 2, based on Moscow Open Olympiad in Informatics)\rating.png)

[코드 모아 보기](https://github.com/lys7aves/algorithm/tree/master/Codeforces/Codeforces%20Round%20775%20(Div.%202%2C%20based%20on%20Moscow%20Open%20Olympiad%20in%20Informatics))



# A. Game

## Problem

[A. Game](https://codeforces.com/contest/1649/problem/A)

**요약**

 1부터 n까지 번호가 붙은 연속된 n개의 지역이 주어지며, 각 지역은 땅 혹은 물로 이루어져 있다. 첫번째와 마지막 지역은 땅이며, 우리는 첫번째 지역에서 마지막 지역으로 가고자 한다. 또한 물로 들어가면 익사하기에, 우리는 땅으로만 이동할 수 있다.

 우리는 두 지역 사이를 점프할 수 있는데, 점프는 최대 한번만 할 수 있으며, i 위치에서 i+x 위치로 점프할 경우 x 만큼의 비용이 발생한다. (x >= 0)

 우리의 목표는 최소한의 비용으로 첫번째 지역에서 마지막 지역까지 가는 것이다.

 첫번째 지역에서 마지막 지역으로 갈 수 있음이 보장된다.



**입력**

 첫째 줄에는 테스트 케이스 개수 t(1 <= t <= 100)가 주어진다.

 각 테스트 케이스의 첫번째 줄에는 지역의 개수를 의미하는 하나의 정수 n(2 <= n <= 100)이 주어진다.

 각 테스트 케이스의 두번째 줄에는 정수 수열 a_1, a_2, ..., a_n (0 <= a_i <= 1) 이 주어지며, a_i = 1은 i번째 지역이 땅임을 의미하며, a_i = 0 은 i번째 지역이 물임을 의미한다. a_1과 a_n은 1임이 보장된다.



**출력**

 각 테스트 케이스에 대하여 문제의 답을 의미하는 하나의 정수를 출력하여라.



## Process

 처음에 "**no more than** once jump" 를 보지 못하고, 물이 있을 때 마다 점프를 하는 방법으로 코드를 작성해 WA를 받아버렸다 ㅜㅜ

 이후 다시 문제를 찬찬히 읽었을 때 보지 못한 조건을 볼 수 있었고, 이후 빠르게 문제를 풀어나갈 수 있었다.



## Tutorial

최대한 많이 이동한 후, 최대한 가까운 곳으로 점프를 해야 최소의 비용으로 마지막 지역까지 도착할 수 있다.

 또한 단 한번만 점프를 할 수 있기 때문에 i번째로 점프를 했다면 i번째 지역 이후로는 물이 없어야 한다.

 위 두 조건을 알아챘다면 우리가 해야할 일은 가장 처음에 나온 물의 위치와 가장 마지막에 나온 물의 위치를 찾는 것이다. 이 둘을 각각 fir와 las이라고 하면, (fir-1) 위치에서 (las+1) 위치로 점프해야 최소한의 비용으로 점프한다는 의미이며, 비용은 las-fir+2 가 된다.



## Solution

```c++
#include <iostream>

using namespace std;

int main()
{
	int t, n, i, a, ans, fir, las;
	
	ios_base::sync_with_stdio(false);
	cin.tie(NULL); cout.tie(NULL);
	
	cin >> t;
	while(t--){
		cin >> n;
		
		fir = 0;
		las = -2;
		for(i=0; i<n; i++){
			cin >> a;
			
			if(a == 0){
				if(!fir) fir = i;
				las = i;
			}
		}
		
		cout << las-fir+2 << '\n';
	}
	
	return 0;
}
```

물이 없는 경우 답이 0이어야 하기 때문에 fir과 las를 0과 -2로 초기화하여 출력 부분을 동일하게 처리할 수 있도록 하였다.





# B. Game of Ball Passing

## Problem

[B. Game of Ball Passing](https://codeforces.com/contest/1649/problem/B)

**요약**

n명의 플레이어들이 연습 기간 동안 패스를 준 횟수가 주어진다. 주어진 패스 횟수 수열을 만족시키기 위해서는 최소 몇개의 공이 필요한지 구하여라.



**입력**

 첫째 줄에는 테스트 케이스 개수 t(1 <= t <= 5*10^4)이 주어진다.

 각 테스트 케이스의 첫번째 줄에는 플레이어 수 n(2 <= n <= 10^5)이 주어진다.

 각 테스트 케이스의 두번째 줄에는 정수 수열 a_1, a_2, ..., a_n (0 <= a_i <= 10^9) 이 주어지며, a_i 는 i번째 플레이어가 준 패스의 수를 의미한다.

 모든 테스트 케이스에 대한 n의 합이 10^5을 넘지 않음이 보장된다.



**출력**

 각 테스트 케이스에 대하여 답을 의미하는 하나의 정수를 출력하여라.



## Process

 이 문제의 핵심은 "passes delivered" 라고 생각한다. "passes delivered" 이면 패스를 준 것을 의미하며 받은 것은 카운팅이 되지 않은 것을 의미한다.

 문제의 핵심 플레이어는 패스를 가장 많이 준 플레이어이다. 패스를 가장 많이 준 플레이어의 패스 횟수가 나머지 플레이어의 패스 횟수의 합보다 작은면 공 한 개 만으로도 모든 패스가 가능하다. 그러나 그렇지 않을 경우 나머지 모든 플레이어가 가장 많이 패스를 준 플레이어에게 패스를 주더라도 그 플레이어의 패스 횟수는 채워지지 않는다. 즉, 이 경우 패스 횟수의 차이만큼의 공이 더 필요하게 된다.



## Tutorial

 패스를 가장 많이 준 플레이어의 패스 횟수를 maxi, 나머지 플레이어의 패스 횟수의 합을 sum 이라고 한다면, maxi가 sum보다 작거나 같다면 공이 1개가 필요하며, 그렇지 않을 경우, maxi-sum 만큼의 공이 필요하다.



## Solution

```c++
#include <iostream>

using namespace std;

int main()
{
	int t, n, a, maxi, i;
	long long sum;
	
	ios_base::sync_with_stdio(false);
	cin.tie(NULL); cout.tie(NULL);
	
	cin >> t;
	while(t--){
		cin >> n;
		
		maxi = sum = 0;
		for(i=0; i<n; i++){
			cin >> a;
			maxi = max(maxi, a);
			sum += a;
		}
		
		sum -= maxi;
		cout << (maxi ? max(1LL, maxi-sum) : 0) << '\n';
	}
	
	return 0;
}
```





# C. Weird Sum

## Problem

[C. Weird Sum](https://codeforces.com/contest/1649/problem/C)

**요약**

 n*m 크기의 테이블이 주어지며, 각 셀에는 하나의 색이 채워져 있다.

 테이블에 있는 색이 같은 모든 쌍에 대하여 "매해튼 거리"의 합을 구하여라.

 두 셀 (r1, c1)과 (r2, r3)의 "매해튼 거리"는 \|r1 - r2\| + \|c1 - c2\| 로 정의된다.



**입력**

 첫번째 줄에는 두 수 n과 m(1 <= n <= m, n*m <= 100,000)이 주어지며, 이는 테이블의 행과 열의 수를 의미한다.

 다음 n개의 줄에 걸쳐 테이블의 정보가 주어진다. i번째 줄에는 m개의 수 c_i1, c_i2, ..., c_im (1 <= c_ij <= 100,000)가 주어진다.



**출력**

색이 같은 모든 쌍에 대하여 매해튼 거리의 합을 출력하여라.



## Process

우선 모든 쌍에 대하여 매해튼 거리를 구할 수는 없다. 셀의 수가 100,000인데, 모든 셀이 같은 색으로 칠해져 있으면 모든 쌍은 개수는 제곱이 되어 시간 초과가 걸리기 때문이다. 또한 "매해튼 거리"가 나오는 순간 행과 열에 대한 거리를 각각 따로 구해 더해야 된다는 생각이 들었다.

 우선 행과 열을 따로 생각해보기로 했다. 즉, 우선 매해튼 거리의 정의를 \|r1 - r2\|로 축소시켜보자. 그럼 우리는 테이블을 행이 r개이고, 열이 1개인 테이블로 생각해볼 수 있을 것이다. 근데 열을 하나로 줄였어도 아직 해결하지 못한 문제가 있다. 바로 쌍의 개수가 최대 제곱이 될 수 있기 때문이다.

 i번째 열에 어떤 색 c가 있다고 해보자. 그렇다면 이 셀이 고려해야 하는 셀은 무엇일까? 색이 같은 모든 셀을 고려할 필요는 없다. 색이 c인 셀 중 i보다 작은 열에 대한 셀만 고려해주면 된다. 그 뒤의 셀들은 뒤의 셀들이 기준이 될 때 i번째 셀을 고려할 것이기 때문이다. 그렇다면 i번째 열보다 작은 열에 있는 셀들과의 거리 합을 한번에 구하려면 어떻게 해야될까? 이게 이 문제의 핵심이다.

 i번째 보다 작은 열에 있는 셀들을 모두 1번째 열에 있다고 가정하면  거리의 합은 (i번째 보다 작은 열에 있는 셀들의 개수) * (i-1) 이 될 것이다. 그러나 사실 모든 셀이 1번째 열에 있지 않기 때문에 이를 만족하지 않는다는 것은 자명하다. 그렇다면 이를 어떻게 해야될까? 이건 i번째 보다 작은 열에 있는 셀들이 1번째 열과의 거리 차를 기억해놓고 있으면 해결된다. 위의 거리 합에서 1번째 열과의 거리 차의 합을 빼주면 그게 최종적인 합이 된다.

 즉, 우리는 각 색들에 대하여 개수와 1번째 열과의 거리 차의 합을 바탕으로 각 색들에 대한 거리 합을 구해줄 수 있다.



## Tutorial

 행과 열에 대한 매해튼 거리 합을 따로 구한다.

 열에 대한 매해튼 거리 합을 구하는 방법은 아래와 같다.

- i for문 안에 j for문을 돌린다.
- i열 j 행의 색이 c라고 할 때, cnt[c]와 minu[c]의 정의를 아래와 같이 정의하자.
  - cnt[c] = i보다 작은 열들에서 색이 c인 셀의 개수
  - minu[c] = i보다 작은 열들에서 색이 c인 셀들과 1열 사이의 거리 합
- i열 j행의 셀과 색으면서 열이 i보다 작은 모든 쌍들의 열에 대한 매해튼 거리 합은 cnt[c]*(i-1) - minu[c]로 정의할 수 있다.

 행에 대한 매해튼 거리의 합도 열에 대한 매해튼 거리의 합과 비슷하게 구해주면 된다.



## Solution

```c++
#include <iostream>

#define MAXC 100010

using namespace std;

long long cnt[MAXC], minu[MAXC];

int main()
{
	int n, m, i, j;
	long long ans=0;
	
	ios_base::sync_with_stdio(false);
	cin.tie(NULL); cout.tie(NULL);
	
	cin >> n >> m;
	
	int c[n][m];
	for(i=0; i<n; i++){
		for(j=0; j<m; j++){
			cin >> c[i][j];
		}
	}
	
	for(i=0; i<n; i++){
		for(j=0; j<m; j++){
			ans += i*cnt[c[i][j]] - minu[c[i][j]];
			cnt[c[i][j]]++;
			minu[c[i][j]] += i;
		}
	}
	
	for(i=0; i<MAXC; i++) cnt[i] = minu[i] = 0;
	
	for(j=0; j<m; j++){
		for(i=0; i<n; i++){
			ans += j*cnt[c[i][j]] - minu[c[i][j]];
			cnt[c[i][j]]++;
			minu[c[i][j]] += j;
		}
	}
	
	cout << ans;
	
	return 0;
}
```

이 문제의 경우 zero-based 를 이용하면 식이 좀 더 깔끔하게 쓰여진다.
