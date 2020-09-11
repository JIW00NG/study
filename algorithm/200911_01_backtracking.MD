## 백트래킹 (Backtracking)
-백트래킹에 대해 알아보자


### 정의
- 백트래킹(backtracking, 퇴각검색)은 한정 조건을 가진 문제를 풀려는 전략
- "퇴각검색(backtrack)"이란 용어는 1950년대의 미국 수학자 D.H.레머 가 지었다.

### 설명
- 퇴각검색은 모든 조합을 시도해서 문제의 해를 찾는데, 많은 부분 조합들을 배제하기 때문에 풀이 시간이 단축된다.
- 간단하게 말하면 백트래킹이란 재귀를 이용하여 깊이탐색을 하는 dfs와 break이나 continue를 이용해 일부를 스킵하는 방식으로 속도를 향상시키는 가지치기를 합쳤다고 볼 수 있다. 

### 구현
- 주요 개념: 해를 얻을 때까지 모든 가능성을 시도.
- 깊이 우선 탐색 사용:
  - 탐색 중에 오답을 만나면 이전 분기점으로 돌아감
  - 시도해보지 않은 다른 해결 방법 시도
  - 해결 방법이 더 없으면 더 이전의 분기점으로 돌아감
  - 모든 트리의 노드를 검사해도 답을 못 찾을 경우, 이 문제의 해결책은 없다
- 퇴각검색은 보통 재귀 함수로 구현되며, 재귀로 파생된 해결 방법은 하나 이상의 변수가 필요한데 , 이것은 현재 시점에서 적용할 수 있는 변수값들을 알고 있다. 퇴각검색은 깊이 우선 탐색과 대략 같으나 기억 공간은 덜 차지한다. 현재의 상태를 보관하고 바꾸는 동안만 차지한다.
- 탐색 속도를 높이기 위해, 재귀 호출을 하기 전에 시도할 값을 정하고 조건(전진 탐색의 경우)을 벗어난 값을 지우는 알고리즘을 적용할 수 있다. 아니면 그 값을 제외한 다른 값들을 탐색할 수도 있다.


![unnamed](https://user-images.githubusercontent.com/56468120/92892227-8d66aa00-f453-11ea-8abf-220fb2b2e98f.png)

### 적용
- 퇴각검색은 플래너나 프롤로그 같은 프로그래밍 언어를 구현하는 데,혹은 구문 분석 분야에도 적용된다.
<br><br>


### 백트래킹의 대표적인 문제: [N-Queen](https://www.acmicpc.net/problem/9663)
#### 문제
  - N-Queen 문제는 크기가 N x N인 체스판 위에 퀸 N개를 서로 공격할 수 없게 놓는 문제이다. N이 주어졌을 때, 퀸을 놓는 방법의 수를 구하는 프로그램을 작성하시오.
#### 입력
- 첫째 줄에 N이 주어진다. (1 <= N < 15)
#### 출력
- 첫째 줄에 퀸 N개를 서로 공격할 수 없게 놓는 경우의 수를 출력한다.
#### 알고리즘 분류
- [부르트 포스](https://gusdnd852.tistory.com/167?category=748315)
- [백트래킹]
#### 풀이

![unnamed](https://user-images.githubusercontent.com/56468120/92909129-d02f7e80-f461-11ea-9a4b-a27cf919c5c5.png)

- C
```
#include <stdio.h>
#include <stdlib.h>

using namespace std;

int N;
int vx[15 + 1], vy[15 + 1];

int go(int y, int x) {

	//가지치기(backtracking)
	for (int i = 0; i < y; i++) {
		//직선겹침
		if (y == vy[i]) { //가로 겹침
			return 0;
		}
		if (x == vx[i]) { //세로 겹침
			return 0;
		}
		if (abs(x - vx[i]) == abs(y - vy[i])) { //대각겹침
			return 0;
		}
	}

	//종료조건
	if (y == N - 1) {
		//말단에서 퀸 배열이 성공적인지 체크
		//만약 성공적이면 리턴 1
		return 1;
	}

	//말의 위치 기억
	vy[y] = y, vx[x] = x;

	int r = 0;
	for (int i = 0; i < N; i++) {
		r += go(y + 1, i);
	}
}

int main(void) {
	scanf("%d", &N);
	int r = 0;
	for (int i = 0; i < N; i++) {
		r += go(0, 1);
	}
	printf("%d\n", r);
	return 0;
}
```

- python
```

```

### Reference
  - [백트래킹 위키백과](https://ko.wikipedia.org/wiki/%ED%87%B4%EA%B0%81%EA%B2%80%EC%83%89)
  
  - [N-Queen 알고리즘문제풀이](https://www.youtube.com/watch?v=ltm-JX5R1pA)
