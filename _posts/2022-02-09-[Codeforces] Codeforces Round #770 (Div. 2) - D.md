---
layout: post
title: '[Codeforces] Codeforces Round #770 (Div. 2) - D'
date: 2022-02-09-9:58
author: 이유섭
cover: '/assets/img/2022-02-08-Codeforces Round 770 (Div. 2) - D/status.png'
tags: codeforces algorithm
---



_Last updated: 2022. 02. 09._



# Codeforces Round #770 (Div. 2) - D. Finding Zero (WA)

![status](\assets\img\2022-02-08-Codeforces Round 770 (Div. 2) - D\status.png)



## Problem

[D. Finding Zero](https://codeforces.com/contest/1634/problem/D)

**요약**

**This is an interactive problem.**

상호작용 문제이다. 업다운 문제처럼 내가 질문을 하면 답변을 주고, 이를 바탕으로 답을 맞추는 매우 재미있는 문제이다.



정수 n이 주어지고, 컴퓨터는 크기가 n인 정수 수열 a를 생각한다. 수열의 각 수는 0부터 10^9까지의 정수로 이루어져 있으며, 0은 정확히 1개 들어 있다. 우리는 수열 a에서 0의 위치를 찾아내는 것이 목표이다. (수열의 인덱스는 1부터 n까지 붙어있다.)



질문은 아래와 같이 할 수 있다.

> ? i j k

이에 대한 답변은 max(a_i, a_j, a_k) - min(a_i, a_j, a_k) 의 값이다. 즉, i, j, k번째 수 중 가장 큰 값에서 가장 작은 값을 뺀 결과를 알려주는 것이다.

질문은 최대 2*n-2번 할 수 있으며, 정답은 단 한번 외칠 수 있고, 한번에 2개의 수를 말할 수 있다. 2개의 수 중 하나라도 답이면 정답이다. 정답은 다음과 같이 외칠 수 있다.

> ! i j



**입력**

t : 테스트 케이스 개수 (1 <= t <= 500)

n : (4 <= n <= 1,000)

모든 테스트 케이스에 대하여 n의 총 합은 3,000을 넘지 않는다.



**출력**

쿼리를 출력하고 나면 버퍼 flush를 해줘라.

- fflush(stdout) or cout.flush() in C++;
- System.out.flush() in Java;
- flush(output) in Pascal;
- stdout.flush() in Python;
- Read documentation for other languages.



## Solution

생각의 과정은 코포를 치르고 난 직후 작성했던 [이 글](https://lys7aves.github.io/Codeforces-Codeforces-Round-770-(Div.-2).html)을 보면 알 수 있다.

당시 맞왜틀을 외치며 시험을 종료해야했고, 내 코드가 완벽하다고 믿은 나는 코드를 변형해 랜덤으로 테스트 케이스를 만들고 정답을 확인하는 코드를 작성하기로 했다.

약간의 코드 리펙토링과 몇번의 테스트 이후, 나는 y를 초기화 하지 않았다는 것을 깨달았고, y를 초기화하고 제출하니 Accept라는 단어를 받아볼 수 있었다. ~~이렇게 허무할 수가...~~



앞서 작성한 글을 통해서 풀이 과정을 볼 수도 있지만, 요약하면 아래와 같다.

1. "? 1 2 i" (3 <= i <= n) 를 질문한 후, x를 질문에 대한 답이 가장 컸던 i로 설정한다.
2. "? 1 x i" (3 <= i <= n, i!=x) 를 질문한 후, y를 질문에 대한 답이 가장 컸던 i로 설정한다.
3. 답은 1, 2, x, y 중에 있다.
4.  "? 1 2 x", "? 1 2 y", "? 1 x y", "? 2 x y" 4개의 질문 중 답이 가장 큰 2개를 고르고, 고른 질문에 공통으로 들어 있는 2개의 수가 답이 된다.
   ("? 1 2 x", "? 1 2 y", "? 1 x y" 는 이미 질문을 했으므로, "? 2 x y" 만 추가로 질문해주면 된다.)



1, 2번째 값이 0 혹은 수열의 최댓값이 아닌 경우, 1, 2번의 과정을 통해 우리는 0과 최댓값의 위치를 알아낼 수 있다. 즉, 앞선 가정 하에 우리는 1, 2번의 과정에서 얻은 x, y로 "! x y"를 출력하여 정답을 맞출 수 있다.

그러나 1, 2번재 값에 0이 있을 수도 있기 때문에, 정답의 가능성을 1, 2, x, y로 열어두었으며, 이 중 최솟값과 최댓값을 찾는 방법이 4번의 과정이다.



## Code

```c++
#include <stdio.h>
#include <algorithm>
#include <time.h>
#include <stdlib.h>

#define TEST false
#define PRINT_PROCESS false
#define MAXN 1000

using namespace std;

int d_01[MAXN], d_0x[MAXN], d_1xy;

int _input=-1, _n, _cnt=0;
int _a[MAXN+1];

int input();
void guess(int i, int j, int k);
void answer(int i, int j);

int main()
{
	srand(time(NULL));
	
	int t, n, i, x, y, maxi, a, b;
	
	scanf("%d", &t);
	while(t--){
		n = input();
		
		for(i=2; i<n; i++){
			guess(0, 1, i);
			d_01[i] = input();
		}
		
		x = 2;
		for(i=2; i<n; i++){
			if(d_01[i] > d_01[x]) x = i;
		}
		
		d_0x[1] = d_01[x];
		for(i=2; i<n; i++){
			if(x == i) continue;
			
			guess(0, x, i);
			d_0x[i] = input();
		}
		
		y = 1;
		d_0x[y] = -1;
		for(i=2; i<n; i++){
			if(i == x) continue;
			if(d_0x[i] > d_0x[y]) y = i;
		}
		
		guess(1, x, y);
		d_1xy = input();
		
		maxi = max(d_01[x], max(d_01[y], max(d_0x[y], d_1xy)));
		
		if(d_01[x] == maxi && d_01[y] == maxi) answer(0, 1);
		else if(d_01[x] == maxi && d_0x[y] == maxi) answer(0, x);
		else if(d_01[y] == maxi && d_0x[y] == maxi) answer(0, y);
		else if(d_01[x] == maxi && d_1xy == maxi) answer(1, x);
		else if(d_01[y] == maxi && d_1xy == maxi) answer(1, y);
		else if(d_0x[y] == maxi && d_1xy == maxi) answer(x, y);
	}
	
	return 0;
}

int input()
{ 
#if !TEST
	int x;
	scanf("%d", &x);
	return x;
	
#else
	if(_input == -1){
		_n = rand()%(MAXN-3)+4;
		int MAXA = 1000000000;
		for(int i=1; i<=_n; i++) _a[i] = rand()%MAXA+1;
		_a[rand()%_n+1] = 0;
		
		if(PRINT_PROCESS){
			printf("%d\n", _n);
			for(int i=1; i<=_n; i++) printf("%d ", _a[i]);
			printf("\n");
		}
		
		_input = _n;
		return _n;
	}
	
	else{
		return _input;
	}

#endif
}

void guess(int i, int j, int k)
{
	i++; j++; k++;
	
#if !TEST
	printf("? %d %d %d\n", i, j, k);
	fflush(stdout);
	
#else
	if(i<1 || i>_n || j<1 || j>_n || k<1 || k>_n){
		printf("? %d %d %d\n", i, j, k);
		printf("-1\n");
		while(1);
	}
	_cnt++;
	_input = max(_a[i], max(_a[j], _a[k])) - min(_a[i], min(_a[j], _a[k]));
	if(PRINT_PROCESS){
		printf("? %d %d %d\n", i, j, k);
		printf("%d\n", _input);
	}

#endif
}

void answer(int i, int j)
{
	i++; j++;
	
#if !TEST
	printf("! %d %d\n", i, j);
	fflush(stdout);
	
#else
	if(i<1 || i>_n || j<1 || j>_n){
		printf("! %d %d\n", i, j);
		printf("-1\n");
		while(1);
	}
	
	if(PRINT_PROCESS) printf("!%d %d\n", i, j);
	
	printf("%d / %d\n", _cnt, 2*_n-2);
	if(_a[i]*_a[j] == 0) printf("Correct!\n\n");
	else{
		printf("Wrong :(\n\n");
		
		printf("%d\n", _n);
		for(int i=1; i<=_n; i++) printf("%d ", _a[i]);
		printf("\n");
		while(1);
	}
	
	_input = -1;
	_cnt = 0;

#endif
}
```



## Code description

코드를 보면 굉장히 길다. 바로 앞서 말한 랜덤 테스트 코드가 붙어 있기 때문이다.



우선 [이전 글](https://lys7aves.github.io/Codeforces-Codeforces-Round-770-(Div.-2).html)에서 작성한 코드와의 변경점을 살펴보자.

우선 처음 테스트 케이스 개수 t를 입력하는 부분을 제외한 입출력 부분을 새로운 함수를 만들어 바꾸어 주었다. 입출력을 대신한 함수에서는 랜덤 테스트 코드와 표준 입출력 코드를 작성하여 손쉽게 랜덤 테스트와 표준 입출력을 바꿔가면 테스트 할 수 있도록 하였다.

인덱스 실수가 있었지만 변수명을 인덱스와 관련하여 지어놨기에 인덱스 기준을 바꾸는 것보다 출력할 때, 1씩 더해서 출력하는 것이 좋다고 판단하였다. 때문에 출력을 대신한 guess와 answer 함수를 보면 함수 시작과 동시에 전달 받은 인자 값에 모두 1씩 더한 것을 볼 수 있다.

그리고 코포 때 WA 가 나왔던 원인, y를 초기화해주는 코드를 추가하였다.



메인 함수의 변경 사항은 크게 위의 사항이 전부이다. 이제 내가 랜덤 테스트 코드를 어떻게 작성하였는지에 대해 간단히 서술해보겠다.

우선 코드의 윗부분에서 #define을 이용하여 TEST 라는 상수를 만들었다. 해당 상수가 true이면 테스트 코드가 실행되고, false이면 표준 입출력이 되도록 코드를 작성하였다. 입출력을 대신한 input, guess, answer 함수를 보면 모두 #if !TEST, #else, #endif 부분이 있는데, 각 줄을 기준으로 표준 입출력 부분과 랜덤 테스트 부분으로 코드가 나뉘는 것을 볼 수 있다.

표준 입출력 부분은 어렵지 않게 작성할 수 있을 것이다.

문제는 랜덤 테스트 부분인데, 사실 이 부분도 그렇게 어렵진 않다. 큰 흐름은 다음과 같다.

- guess 함수가 호출되면, 그 결과를 전역변수인 \_input에 저장해둔다.
- input 함수는 \_input 값이 -1이 아니면 _input 값을 반환해준다. 
  \_input 값이 -1이면 새로운 랜덤 케이스를 만들고 n 값을 반환해 준다.
- answer 함수 답의 여부를 출력해주고, \_input 값을 -1로 초기화해준다.

여러 테스트를 한다고 자잘한 부분들도 있지만 큰 흐름은 위와 같으니 참고해서 봐주면 될 것 같다.

