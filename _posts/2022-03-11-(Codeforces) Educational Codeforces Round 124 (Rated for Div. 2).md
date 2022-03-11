---
layout: post
title: '[Codeforces] Educational Codeforces Round 124 (Rated for Div. 2)'
date: 2022-03-11-14:10
author: 이유섭
cover: '/assets/img/2022-03-11-(Codeforces) Educational Codeforces Round 124 (Rated for Div. 2)/problems.png'
tags: codeforces algorithm
---



_Last updated: 2022. 03. 11_



# Codeforces Round #770 (Div. 2)

![problems](assets\img\2022-03-11-(Codeforces) Educational Codeforces Round 124 (Rated for Div. 2)\problems.png)

![submissions](assets\img\2022-03-11-(Codeforces) Educational Codeforces Round 124 (Rated for Div. 2)\submissions.png)

![standing](assets\img\2022-03-11-(Codeforces) Educational Codeforces Round 124 (Rated for Div. 2)\standing.png)

[전체 코드 보기](https://github.com/lys7aves/algorithm/tree/master/Codeforces/Educational%20Codeforces%20Round%20124%20(Rated%20for%20Div.%202))



# A. Playoff



## Problem

[A. Playoff](https://codeforces.com/contest/1651/problem/A)

**문제**

 2^n 명의 선수가 있는 플레이오프 토너먼트를 생각해보자. 운동 선수는 1부터 2^n까지 번호가 붙어 있다.

 토너먼트는 n개의 스테이지가 열린다. 각 스테이지에서, 선수들은 정확히 한 쌍에 포함되도록 여러 쌍으로 나뉜다. 각 쌍에서, 선수들은 상대와 경쟁하며, 정확히 한 사람만 승리한다. 각 쌍의 승자는 다음 스테이지로 올라가며, 패배자는 토너먼트에서 탈락한다.

 쌍들은 다음과 같이 이루어져 있다.

- 첫 스테이지에서, 선수 1번은 선수 2번과 경쟁하고, 3번은 4번과 5번은 6번과 경쟁한다, ...
- 두번째 스테이지에서는, "1-2" 매치에서 승리한 사람과 "3-4" 매치에서 승리한 사람이 경쟁하며, "5-6" 매치에서 승리한 사람과 "7-8" 매치에서 승리한 사람이 경쟁한다. ...
- 다음 스테이지들도 같은 규칙으로 열린다.

 x번 선수와 y번 선수가 경쟁하며, 승자는 다음과 같이 정해진다.

- x+y가 홀수이면, 더 작은 번호를 가진 선수가 이긴다. (즉, x<y 이면, x가 이기고, 그렇지 않으면 y가 이긴다.)
- x_y가 짝수이면, 더 큰 번호를 가진 선수가 이긴다.

 다음 그림은 n=3 일때 토너먼트 결과를 나타낸다.

![A_tournament](assets\img\2022-03-11-(Codeforces) Educational Codeforces Round 124 (Rated for Div. 2)\A_tournament.png)

 정수 n이 주어질 때, 토너먼트 최종 승리자의 번호를 구하여라.



**입력**

 첫째 출에는 테스트 케이스의 개수를 의미하는 하나의 정수 t(1 <= t <= 30)이 주어진다.

 각 테스트케이스는 하나의  정수 n(1 <= n <= 30)을 포함하 하나의 줄로 이루어져 있다.



**출력**

 각 테스트 케이스에 대하여 토너먼트 승리자 번호를 의미하는 하나의 정수를 출력하여라.



**예제**

| input           | output   |
| --------------- | -------- |
| 2<br />3<br />1 | 7<br />1 |



**설명**

n=3인 케이스는 그림을 통해 보여주었다.

n=1이면, 1번과 2번 선수의 매치 하나 밖에 존재하지 않는다. 1+2=3 은 홀수이므로, 더 작은 번호의 선수가 승리한다. 그래서, 1번이 승자가 된다.





## Tutorial

 처음 2^n 이라는 숫자를 보자 지레 겁을 먹었지만, 이내 어렵지 않은 문제라는 것을 알 수 있었다.

 주어진 그림을 자세히 보면 알 수 있겠지만, 처음에는 연속된 2개의 번호의 선수가 경쟁을 하기 때문에 두 선수 번호의 합은 항상 홀수가 된다. 이 때, 작은 번호의 선수가 승리하므로 항상 첫번째 스테이지의 승자는 홀수 번호의 선수가 되고, 짝수 번호의 선수는 탈락하게 된다. 그리고 이제 홀수 번호의 선수 밖에 남지 않았기 때문에 경쟁하는 두 선수의 번호의 합은 짝수가 되고, 항상 번호가 큰 선수가 승리하게 된다. 즉, 토너먼트의 결과는 홀수 중 가장 큰 번호를 가진 선수가 이기게 되는 것이다.

 그렇다면 n이 주어졌을 때, 가장 큰 홀수는 무엇일까? 선수의 번호가 1부터 2^n까지 붙어 있고, 2^n은 짝수이므로, 2^n-1 이 가장 큰 홀수가 된다.





## Solution

```c++
#include <iostream>

using namespace std;

int main()
{
	int t, n, i;
	
	ios_base::sync_with_stdio(false);
	cin.tie(NULL); cout.tie(NULL);
	
	cin >> t;
	while(t--){
		cin >> n;
		
		cout << (1 << n) - 1 << '\n';
	}
	
	return 0;
}
```







# B. Prove Him Wrong



## Problem

[B. Prove Him Wrong](https://codeforces.com/contest/1651/problem/B)

**문제**

 최근, 너의 친구가 정수 배열 a에서 특별한 작업을 밝혀냈다.

1. 두 인덱스 i와 j를 고른다. (i != j)
2. a_i = a_j = \|a_i - a_j\| 로 바꾼다.

 이 작업을 한동안 가지고 놀더니, 그는 다음과 같은 결론을 냈다.

- 1<= a_i <= 10^9 인 길이가 n인 모든 정수 배열 a에 대해, 위의 작업을 한 후 배열 a의 총 합이 감소하도록 하는 인덱스 쌍 (i, j)를 찾을 수 있다.

 너는 이 말이 수상하게 들렸고, 너는 정수 n이 주어질 때, 반례를 찾길 원했다. 반례를 찾아 그가 틀렸다는 것을 증명할 수 있겠는가?

 다시 말해, 모든 쌍 (i, j)에 대하여 작업 수행 후 전체 합이 줄어들지 않는(총합이 증가하거나 바뀌지 않는) n개의 정수 a_1, a_2, ..., a_n (1 <= a_i <= 10^9)을 포함하는 배열 a를 찾으면 된다.



**입력**

 첫째 줄에는 테스트케이스 개수를 의미하는 하나의 정수 t(1 <= t <= 100)이 주어진다.

 각 테스트 케이스에 대하여, 배열 a의 길이를 의미하는 하나의 정수 n(2 <= n <= 1000)이 주어진다.



**출력**

 각 테스트 케이스에 대하여, 크기가 n인 반례 배열 a가 없다면, *NO*를 출력해라.

 그렇지 않다면, *YES*를 출력하고, 배열 a를 출력하여라. 반례가 여러개라면 아무거나 출력하여라.



**예제**

| input                    | output                                    |
| ------------------------ | ----------------------------------------- |
| 3<br />2<br />512<br />3 | YES<br/>1 337<br/>NO<br/>YES<br/>31 4 159 |



**설명**

 첫번째 테스트 케이스에서, (1, 2)와 (2, 1) 쌍만 가능하다.

 만약 (1, 2)(혹은 (2, 1)) 쌍에 대하여 작업을 수행한다면, a_1 = a_2 = \|1 - 337\| = 336 또는 [336, 336] 배열을 얻을 수 있다. 두 경우 모두, 전체 합은 증가하며, 따라서 배열 a는 반례이다.





## Tutorial

 우리가 (i, j)에 대하여 작업을 수행하게 되면, a_i와 a_j 이외의 수들은 바뀌지 않는다. 즉, a_i+a_j가 어떻게 바뀌냐가 전체 합이 어떻게 바뀌냐를 결정하게 될 것이다.

 이제 문제에서 정의한 작업을 살펴보자. 절댓값 연산이므로 a_i와 a_j의 순서는 바꿔도 무관할 것이다. 그렇다면 항상 a_i <= a_j 라고 가정해보자. 그러면 문제의 식은 "a_i = a_j = a_j - a_i" 로 바뀌게 될 것이다.

 a_i와 a_j의 작업 전 후 합을 비교해 보면 다음과 같다.

- 작업 전 : a_i + a_j
- 작업 후 : (a_j - a_i) + (a_j - a_i)

 우리의 목표는 작업 후의 합이 작업 전의 합보다 더 크거나 같게 하는 것이다. 즉, a_i + a_j <= 2(a_j - a_i) 이며, 이 식을 풀어쓰면 다음과 같다.

$$
a_i + a_j <= 2(a_j - a_i)\\
$$

$$
a_i + a_j <= 2a_j - 2a_i\\
$$

$$
3a_i <= a_j
$$

즉, a_j는 a_i의 3배 이상의 수여야 반례가 된다는 것이다.

 여기까지 알았으면 반례 찾는 것은 간단하다. 1부터 3^x 들을 차례로 출력해주면 된다. 그렇다면 왜 반례가 존재하지 않는 입력이 존재하는 것일까? 그 이유는 배열의 수가 10^9을 넘으면 안된다는 조건 때문이다. 즉, 우리는 3^x이 10^9을 넘지 않는 입력에 대해서만 반례를 찾을 수 있고, 이보다 긴 배열에서는 반례를 찾을 수 없다.

3^x <= 10^9 인 가장 큰 x는 18이며, 1 즉, 3^0부터 3^18 까지 배열에 넣을 수 있으므로, n은 최대 19까지에서만 반례를 찾을 수 있다. (처음에 아무 생각 없이 n이 18일 때까지만 YES를 출력하게 해서 제출 횟수 한번을 날려 먹었다. ㅜㅜ)





## Solution

```c++
#include <iostream>

using namespace std;

int main()
{
	int t, n, a, i;
	
	ios_base::sync_with_stdio(false);
	cin.tie(NULL); cout.tie(NULL);
	
	cin >> t;
	while(t--){
		cin >> n;
		
		if(n > 19){
			cout << "NO\n";
			continue;
		}
		
		cout << "YES\n";
		
		a = 1;
		for(i=0; i<n; i++){
			cout << a << ' ';
			a *= 3;
		}
		cout << '\n';
	}
	
	return 0;
}
```







# C. Fault-tolerant Network



## Problem

[C. Fault-tolerant Network](https://codeforces.com/contest/1651/problem/C)

**문제**

 교실에 컴퓨터 두 줄이 있다. 각 줄에는 n개의 컴퓨터가 있으며, 각 컴퓨터에는 등급이 있다. 첫번째 줄의 컴퓨터 등급은 a_1, a_2, ..., a_n 이고, 두번째 줄은 b_1, b_2, ..., b_n 이다.

 처음에, 각 줄에서 모든 인접한 컴퓨터 쌍들은 선으로 연결되어 있으며(1 <= i < n 에 대한 모든 쌍 (i, i+1)), 따라서 두 줄은 2개의 독립적인 컴퓨터 네트워크를 형상하고 있다.

 너가 해야할 일은 서로 다른 줄의 하나 혹은 그 이상의 쌍을 연결하여 하나의 공통 네트워크로 만드는 것이다. 첫번째 줄의 i번째 컴퓨터와 두번째 줄의 j번째 컴퓨터를 잇는 비용은 \|a_i - b_j\|이다.

 너는 하나의 컴퓨터를 여러 다른 컴퓨터와 연결할 수 있지만, 적어도 하나의 내결함성을 제공해야 한다: 너는 하나의 컴퓨터가 불량이더라도 네트워크가 항상 연결을 유지하도록 컴퓨터를 연결해야 한다. 다시 말해, 하나의 컴퓨터가 무러지더라도(어떤 것이라도), 네트워크가 2개 이사으로 분리되면 안된다.

 내결함성을 가진 네트워크를 만드는데 필요한 최소 비용을 구하여라.



**입력**

 첫째 줄에는 하나의 테스트 케이스 개수를 의미하는 정수 t(1 <= t <= 10^4)이 주어진다.

 각 테스트 케이스에 대하여 첫째 줄에는 각 줄의 컴퓨터 개수를 의미하는 하나의 정수 n(3 <= n <= 2*10^5)이 주어진다.

 각 테스트 케이스에 대하여 두번째 줄에는 첫번째 줄의 컴퓨터 등급을 의미하는 n개의 정수 a_1, a_2, ..., a_n (1 <= a_i <= 10^9)이 주어진다.

 각 테스트 케이스에 대하여 세번째 줄에는 두번째 줄의 컴퓨터 등급을 의미하는 n개의 정수 b_1, b_2, ..., b_n (1 <= b_i <= 10^9)이 주어진다.

 n의 총합은 2*10^5을 넘지 않음이 보장된다.



**출력**

 각 테스트케이스에 대하여 내결함 네트워크를 만드는데 필요한 최소 비용을 의미하는 하나의 정수를 출력하여라.



**예제**

| input                                                        | output            |
| ------------------------------------------------------------ | ----------------- |
| 2<br/>3<br/>1 10 1<br/>20 4 25<br/>4<br/>1 1 1 1<br/>1000000000 1000000000 1000000000 1000000000 | 31<br/>1999999998 |



**설명**

 첫번째 테스트 케이스에서, 4개의 컴퓨터 쌍을 연결하는 것이 최적이다.

1. 첫번째 줄의 1번 컴퓨터와 두번째 줄의 2번 컴퓨터: 비용 \|1 - 4\| = 3
2. 첫번째 줄의 3번 컴퓨터와 두번째 줄의 2번 컴퓨터: 비용 \|1 - 4\| = 3
3. 첫번째 줄의 2번 컴퓨터와 두번째 줄의 1번 컴퓨터: 비용 \|10 - 20\| = 10
4. 첫번째 줄의 2번 컴퓨터와 두번째 줄의 3번 컴퓨터: 비용 \|10 - 25\| = 15

 총, 3 + 3 + 10 + 15 = 31

 두번째 테스트 케이스에서, 첫번째 줄의 1번과 두번째 줄의 1번, 첫번째 줄의 4번과 두번째 줄의 4번을 연결하는 것이 최적이다.





## Tutorial

 문제의 핵심은 내결함성을 만족시키기 위한 조건을 찾는 것이다. 내결함성의 조건은 각 줄의 끝 컴퓨터가 다른 줄의 컴퓨터와 연결되어 있어야 한다는 것이다.  그렇지 않으면 끝에서 2번째 컴퓨터가 고장 났을 때, 끝에 있는 컴퓨터가 연결이 끊기기 때문이다. (나는 이 조건은 금방 찾았지만 이 이렇게 연결해도 분리 되는 경우가 있을 수 있다는 의심 때문에 다음 과정으로 넘어가기 까지 시간을 좀 허비했다.)

 그렇다면 끝에 있는 컴퓨터를 어떻게 연결해야 될까? 가장 간단한 방법은 1번과 1번, n번과 n번 혹은 1번과 n번, n번과 1번을 연결하는 것이다. 하지만 이렇게 연결하는 것이 연결 횟수는 가장 적겠지만 비용이 가장 적다고 단정지을 수는 없다. 1번과 1번을 연결하는 비용이 너무나도 큰데, 1번과 1번 연결 대신 1번과 x번, y번과 1번을 연결하는 것이 더 쌀 수도 있기 때문이다.

 여기까지 생각하고 나니 경우의 수가 좀 많아진다는 생각에 정리를 잘하면 코드를 깔끔하게 짤 수 있지 않을까라는 생각이 들었지만, 이를 정리하고 있는 시간보다 모든 경우를 나름의 규칙으로 코딩하는게 더 빠르다고 판단하여 코드는 안예쁠지 모르지만 모든 경우를 한줄 한줄 작성하였다.

 나름의 규칙을 말하자면, 우선 1번과 1번, n번과 n번, 1번과 n번, n번과 1번을 연결하는 비용을 각각 구하고, 가장 적은 비용으로 첫째 줄의 1번과 n번, 두 번째 줄의 1번과 n번을 각각 연결하는 비용을 구해준다. 이후, 1번과 1번을 연결하는 비용과 (첫째 줄의 1번을 연결하는 최소 비용 + 두번째 줄의 1번을 연결하는 최소 비용)의 최솟값을 1번과 1번을 연결하는 비용으로 갱신하고 n번과 n번, 1번과 n번, n번과 1번의 비용도 같은 방법으로 갱신한다. 마지막으로 1번과 1번, n번과 n번을 연결하는 비용의 합과 1번과 n번, n번과 1번을 연결하는 비용의 합 중 최솟값을 출력한다. 이렇게하면 노가다긴해도 비교적 짧고 알아보기 쉽게 코드를 작성할 수 있다.

 이 문제에서도 한번 WA를 받았는데, 각 줄의 1번, n번을 각각 연결하는 비용을 구할 때, 1번과 1번, 1번과 n번과 같은 값들을 이미 구했기에 1번과 n번을 제외하고 생각하였다. 그러나 [이 입력](https://github.com/lys7aves/algorithm/blob/master/Codeforces/Educational%20Codeforces%20Round%20124%20(Rated%20for%20Div.%202)/C_testcase.txt)에서 3번째 테스트 케이스를 보면 첫째줄의 1번과 n번이 동시에 두번째 줄의 n번과 연결한 경우가 최적의 답이라는 것을 알 수 있다.



## Solution

```c++
#include <iostream>

#define MAXN 200010

using namespace std;

int a[MAXN], b[MAXN];

int main()
{
	int t, n, i;
	int ans_00, ans_nn, ans_0n, ans_n0, a_0, a_n, b_0, b_n;
	
	ios_base::sync_with_stdio(false);
	cin.tie(NULL); cout.tie(NULL);
	
	cin >> t;
	while(t--){
		cin >> n;
		for(i=0; i<n; i++) cin >> a[i];
		for(i=0; i<n; i++) cin >> b[i];
		
		ans_00 = abs(a[0] - b[0]);
		ans_nn = abs(a[n-1] - b[n-1]);
		ans_0n = abs(a[0] - b[n-1]);
		ans_n0 = abs(a[n-1] - b[0]);
		
		a_0 = abs(a[0] - b[0]);
		a_n = abs(a[n-1] - b[0]);
		b_0 = abs(b[0] - a[0]);
		b_n = abs(b[n-1] - a[0]);
		for(i=1; i<n; i++){
			a_0 = min(a_0, abs(a[0]-b[i]));
			a_n = min(a_n, abs(a[n-1]-b[i]));
			b_0 = min(b_0, abs(b[0]-a[i]));
			b_n = min(b_n, abs(b[n-1]-a[i]));
		}
		
		ans_00 = min(ans_00, a_0 + b_0);
		ans_nn = min(ans_nn, a_n + b_n);
		ans_0n = min(ans_0n, a_0 + b_n);
		ans_n0 = min(ans_n0, a_n + b_0);
		
		cout << min(ans_00+ans_nn, ans_0n+ans_n0) << '\n';
	}
	
	return 0;
}
```







# D. Nearest Excluded Points



## Problem

[D. Nearest Excluded Points](https://codeforces.com/contest/1651/problem/D)

**문제**

 평면상의 서로 다른 n개의 점이 주어진다. i번째 점의 좌표는 (x_i, y_i)이다.

 각 i번째 점에 대하여, 주어진 n개의 점에 포함되지 않은 가장 (맨해튼 거리로)가까운 정수 좌표를 구하여라. 여러 점들이 있다면 아무거나 선택해도 된다.

 두 점 (x_1, y_1)과 (x_2, y_2) 사이의 맨해튼 거리는 \|x_1 - x_2\| + \|y_1 - y_2\| 이다.



**입력**

 첫째 줄에는 점의 개수를 의미하는 하나의 정수 n(1 <= n <= 2*10^5)이 주어진다.

 다음 n개의 줄에는 점들이 주어진다. i번째 줄에는 i번째 점의 좌표를 나타내는 두 정수 x_i, y_i(1 <= x_i, y_i <= 2*10^5)가 주어진다.

 입력의 모든 좌표는 겹치지 않음이 보장된다.



**출력**

 n개의 줄을 출력하여라. i번째 줄에는, 주어진 n개의 점에 있지 않으면서, i번째 점과 가장 (맨해튼 거리로)가까운 정수 좌표를 출력하여라.

 출력 좌표는 [-10^6; 10^6] 범위 안에 있다. 모든 최적의 답이 이 제약을 만족함을 보일 수 있다.

 만약 여러 답이 존재한다면 아무거나 출력하여라.



**예제**

| input                                             | output                                                      |
| ------------------------------------------------- | ----------------------------------------------------------- |
| 6<br/>2 2<br/>1 2<br/>2 1<br/>3 2<br/>2 3<br/>5 5 | 1 1<br/>1 1<br/>2 0<br/>3 1<br/>2 4<br/>5 4                 |
| 1 1<br/>1 1<br/>2 0<br/>3 1<br/>2 4<br/>5 4       | 4 3<br/>2 5<br/>2 1<br/>2 5<br/>1 5<br/>4 1<br/>1 2<br/>3 2 |



## Tutorial

 맨해튼 거리의 원은 좌표 축으로 45도 기울어진 정사각형이다. 즉, 마름모 모양이라는 것이다. 가장 처음 생각난 방법은 n^2방법이었다. i번째 점과 가장 가까운 점들을 차례로 살피다가 주어진 점들에 포함되지 않은 점이 나타나면 해당 점을 고르는 방법이었다. 어차피 주어진 점들이 n개이므로 각 점들에 대하여 최대 n개의 점을 탐색할 것이며, unordered_set 등을 해당 점이 주어진 점들에 속해 있는지를 빠르게 구할 수 있을 것이다.

 다음으로 떠올린 것은 i번째 점과 가장 가까운 점과의 거리를 l이라고 하면, i번째 점을 중심으로 하는 반지름이 l-1인 맨해튼 원에는 주어진 점들로 꽉 차 있을 것이며, 이 l은 root(n)을 넘지 않는다는 것이다. 즉, 뭔가 잘만 하면 N*root(N)의 시간 복잡도에 끝낼 수 있을 것이라는 생각이 들었다.

 우리에게는 i번째 점의 답을 구하는데, root(N)이라는 시간이 주어진 것이다. 일단 목표를 가장 가까운 점과의 거리 l을 구하는 것으로 하였다. root(N)이라는 시간이 주어졌으므로 위아래 혹은 좌우로 root(N)까지는 가볼 수 있다. 그렇다면 위아래로 이동하면서 동시에 해당 줄에서 최대 옆으로 얼만큼 좌표들이 차 있는지를 O(1)만에 구해야 된다. 나는 이를 전처리를 통하여 미리 구해놓은 값을 사용하였다.

 우선 y, x 순으로 좌표를 정렬하였다. 이후, y가 같은 값들에 대하여 x좌표가 작은 값부터 큰 값으로 가면서 내 왼쪽에 연속해서 좌표가 몇개 있는지를 구해주었다. 이는 O(N)만에 잘 구해줄 수 있다. 오른쪽에 연속해서 좌표가 몇개 있는지도 비슷한 방법으로 구한다.

 이후 좌표를 x, y순으로 정렬한 후, 앞서 말한 방법을 수행해주면 된다. i번째 좌표를 살펴볼 때, x 값이 같은 것들이 인접해 있으므로, 앞뒤로 x가 같으면서 y좌표가 1 차이 나는 애들을 쭉 살펴보면 된다. 동시에 y좌표가 k 차이나는 좌표에서 좌우로 최대 몇개의 좌표가 연속해서 있는지를 살펴봐주면 우리는 좌표로 가득 채워진 맨해튼 원의 최대 길이 l-1을 구해줄 수 있다. 이후, 주어진 좌표들에 포함되지 않으면서 거리가 l인 좌표를 알아서 잘 구해주면 된다.





## Solution

```c++
#include <iostream>
#include <algorithm>
#include <stdio.h>

#define MAXN 200010

using namespace std;

struct PointInfo{
	int x, y, idx, l, r;
	int x_, y_;
	bool flag;
};
bool xy_cmp(const PointInfo &a, const PointInfo &b){
	if(a.x != b.x) return a.x < b.x;
	else return a.y < b.y;
}
bool yx_cmp(const PointInfo &a, const PointInfo &b){
	if(a.y != b.y) return a.y < b.y;
	else return a.x < b.x;
}
bool idx_cmp(const PointInfo &a, const PointInfo &b){
	return a.idx < b.idx;
}

PointInfo points[MAXN];

int main()
{
	int n, i, j, len, len_u, len_d;
	
	ios_base::sync_with_stdio(false);
	cin.tie(NULL); cout.tie(NULL);
	
	cin >> n;
	for(i=1; i<=n; i++){
		cin >> points[i].x >> points[i].y;
		points[i].idx = i;
	}
	points[0].x = points[0].y = points[n+1].x = points[n+1].y = -1;
	
	sort(points+1, points+n+1, yx_cmp);
	
	for(i=1; i<=n; i++){
		if(points[i].y != points[i-1].y || points[i].x != points[i-1].x+1) points[i].l = 0;
		else points[i].l = points[i-1].l+1;
	}
	for(i=n; i>=1; i--){
		if(points[i].y != points[i+1].y || points[i].x != points[i+1].x-1) points[i].r = 0;
		else points[i].r = points[i+1].r+1;
	}
	
	sort(points+1, points+n+1, xy_cmp);
	
	for(i=1; i<=n; i++){
		len = min(points[i].l, points[i].r);
		for(j=0; j<=len; j++){
			if(points[i+j].x != points[i].x || points[i+j].y != points[i].y+j){
				points[i].x_ = points[i].x;
				points[i].y_ = points[i].y+j;
				points[i].flag = true;
				break;
			}
			if(points[i-j].x != points[i].x || points[i-j].y != points[i].y-j){
				points[i].x_ = points[i].x;
				points[i].y_ = points[i].y-j;
				points[i].flag = true;
				break;
			}
			
			len = min(len, j+min(points[i+j].l, points[i+j].r));
			len = min(len, j+min(points[i-j].l, points[i-j].r));
		}
		
		if(points[i].flag) continue;
		
		for(j=0; true; j++){
			len_u = j+min(points[i+j].l, points[i+j].r);
			len_d = j+min(points[i-j].l, points[i-j].r);
			
			if(len < len_u && len < len_d) continue;
			
			if(len == len_u){
				if(len == j+points[i+j].l){
					points[i].x_ = points[i].x - points[i+j].l - 1;
					points[i].y_ = points[i].y + j;
					break;
				}
				if(len == j+points[i+j].r){
					points[i].x_ = points[i].x + points[i+j].r + 1;
					points[i].y_ = points[i].y + j;
					break;
				}
			}
			if(len == len_d){
				if(len == j+points[i-j].l){
					points[i].x_ = points[i].x - points[i-j].l - 1;
					points[i].y_ = points[i].y - j;
					break;
				}
				if(len == j+points[i-j].r){
					points[i].x_ = points[i].x + points[i-j].r + 1;
					points[i].y_ = points[i].y - j;
					break;
				}
			}
		}
	}
	
	sort(points+1, points+n+1, idx_cmp);
	
	for(i=1; i<=n; i++){
		cout << points[i].x_ << ' ' << points[i].y_ << '\n';
	}
	
	
	return 0;
}
```



