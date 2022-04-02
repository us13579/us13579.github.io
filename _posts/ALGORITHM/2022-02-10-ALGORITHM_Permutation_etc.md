---
layout: single
title:  "ALGORITHM_순열 / 조합 / 부분 집합"
categories: 
    - ALGORITHM
tags: 
    - [2022-02, ALGORITHM, STUDY]
sidebar:
    nav: "docs"
---

# 📚 <a style="color:#00adb5">ALGORITHM</a>

<center>
<img width="90%" src="./../../images/algorithm.png">
</center>
<br>

# 📚 <a style="color:#00adb5">순열 / 조합 / 부분 집합</a>

## <a style="color:#00adb5">순열 ( Permutation ) </a>이란 무엇인가 ?
<b><a style="color:red">서로 다른 것들 중 몇 개를 뽑아서 한 줄로 나열하는 것</a></b><br>
서로 다른 N개 중 R개를 택하는 것<br>
<b><a style="color:red">순열은 순서가 상관이 있다 !!!</a></b><br>


- 다수의 알고리즘 문제들은 순서화된 요소들의 집합에서 최선의 방법을 찾는 것과 관련이 있다.
- N개의 요소들에 대해서 n! 개의 순열들이 존재한다.
- 만약 n > 12 일 경우 시간 복잡도가 폭발적으로 증가한다.
- 크기 (R) 이 고정되어 있으면 반복문 사용 가능 !!
- 크기 (R) 이 고정되어 있지 않으면 재귀 사용 !!
- boolean을 활용하여 체크
- 다른 배열에 값을 저장하면서 기저조건이 되면 그 값들을 다 확인한다.

### 식

<b><a style="color:red">nPr</a></b><br>
nPr = n * ( n-1 ) * ( n-2 ) * .. * ( n-r-1 )<br><br>
<b><a style="color:red">nPn = n!</a></b><br>
n! = n * ( n-1 ) * ( n-2 ) * .. 2 * 1<br><br>

### 순열 실습 해보즈아 !
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main {
	static StringTokenizer st;
	static int N, M;
	static boolean[] v;
	static StringBuilder sb;
	static int[] arr;
	public static void main(String[] args) throws IOException {
		sb = new StringBuilder();
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		
		st = new StringTokenizer(br.readLine(), " ");
		
		N = Integer.parseInt(st.nextToken());
		
		M = Integer.parseInt(st.nextToken());
		
		// 숫자 배열
		arr = new int[M];

		// 방문 확인 배열 
		v= new boolean[N+1];
		
		perm(0);
		
		System.out.println(sb);
		
	}
	
	// 순열 nPm
	static void perm(int ind) {

		// 기저조건
		if(ind == M) {
			for(int i=0; i<M;i++) {
				sb.append(arr[i]).append(" ");
			}
			sb.append("\n");
			return;
		}
		
		for(int i=1;i<N+1;i++) {

		// 이미 방문했으면 통과
		if(v[i]) {
			continue;
		}
		else {
			v[i] = true;
			arr[ind] = i;
			perm(ind+1);

			// 백트래킹
			v[i] = false;
		}
		}
	}
}
```
<a style="color:#00adb5"><b>출력 결과</b></a><br>
입력 : 4 2 
```
1 2
1 3
1 4
2 1
2 3
2 4
3 1
3 2
3 4
4 1
4 2
4 3
```
<hr>
 주석으로 설명을 해놓았지만 재귀로 계속해서 R개 만큼 뽑고 나서 R개가 채워지면 이제 다시 돌아오면서 isChecked를 통해 선택 여부를 초기화 시켜준다.<br>
 그래서 다시 돌아와서 다른 값으로 넘어가게 되는 것이다.<br>
 재귀에 대한 이해가 잘 되어있어야 쉽게 이해될 것이다.
<hr>


## <a style="color:#00adb5">조합 ( Combination ) </a>이란 무엇인가 ?
<b><a style="color:red">서로 다른 N개의 원소 중 R개를 순서 없이 골라낸 것</a></b><br>
<b><a style="color:red">조합은 순서가 상관이 없다 !!!</a></b><br>

- 규칙이 있다 ! 자기보다 큰 값만 확인하면 된다 !! ( boolean 배열 필요 X )
- 다른 배열에 값을 저장하면서 기저조건이 되면 그 값들을 다 확인한다.

### 식

<b><a style="color:red">nCr</a></b><br>
nCr = n! / (n-r)!r!<br>
nCr = n-1 C r-1 + n-1 C r -> 재귀적 표현<br>
nC0 = 1<br><br>

### 조합 실습 해보즈아 !
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main {
	static StringTokenizer st;
	static StringBuilder sb;
	static int[] arr;
	static int N,M;
	public static void main(String[] args) throws IOException{
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		sb = new StringBuilder();
		
		st = new StringTokenizer(br.readLine(), " ");
		
		N = Integer.parseInt(st.nextToken());
		
		M = Integer.parseInt(st.nextToken());
		
		// 숫자 배열
		arr = new int[M];
		
		comb(0,1);
		
		System.out.println(sb);
		}
	
    // 조합 nCm
	static void comb(int idx, int start) {

		// 기저조건
		if(idx == M) {
			for(int i=0;i<M;i++) {
				sb.append(arr[i]).append(" ");
			}
			sb.append("\n");
			return;
		}
		
		for(int i=start; i<N+1;i++) {
				arr[idx] = i;
				comb(idx+1, i+1);
		}		
	}	
}
```

<a style="color:#00adb5"><b>출력 결과</b></a><br>
입력 : 4 2 
```
1 2
1 3
1 4
2 3
2 4
3 4
```

<hr>
 순열과 비슷한 구조긴 한데 중요한게 boolean으로 각 원소를 체크해주는거 대신 매개변수가 하나더 생겨서 다음 값을 가리키는 역할을 한다. <br>
 조합의 가장 중요한 점은 순서가 상관없어서 나를 탐색하고 그 다음은 무조건 나보다 다음 값부터만 탐색하면 된다.
<hr>

## <a style="color:#00adb5">부분 집합 ( SubSet ) </a>이란 무엇인가 ?
<b><a style="color:red">집합에 포함된 원소들을 선택하는 것</a></b><br>

- 다수의 중요 알고리즘들이 원소들의 그룹에서 최적의 부분 집합을 찾는 것이다.
- 부분집합의 수 : 집합의 원소가 n개 일 때, 공집합을 포함한 부분집합의 수는 2^n개 이다.

### 식

<b><a style="color:red">2^n</a></b><br>
n이 원소 개수<br><br>

### 부분 집합 실습 해보즈아 !
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main {
	static StringTokenizer st;
	static int N,M;
	static StringBuilder sb;
	static boolean[] v;
	static int[] arr;
	
	public static void main(String[] args) throws IOException{
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		sb = new StringBuilder();
		
		st = new StringTokenizer(br.readLine(), " ");
		
		N = Integer.parseInt(st.nextToken());
		
		M = Integer.parseInt(st.nextToken());
		
		arr = new int[M];
		v = new boolean[N];
		
		go(0);
		System.out.println(sb);

	}
	
	static void go(int idx) {
		if(idx == M) {
			for(int i=0; i<M; i++) {
				sb.append(arr[i]+1).append(" ");
			}
			sb.append("\n");
			return;
		}

// 두가지 방법
// 1. 
		//파워셋 처리
		//현재 원소를 선택
		v[idx] = true;
		go(idx+1);

		//현재 원소를 비선택
		v[idx] = false;
		go(idx+1);

// 2. 
		for(int i=0; i<N; i++) {
				v[i] = true;
				arr[idx] = i;
				
				go(idx+1);
				v[i] = false;
			
		}
	}
}
```

<a style="color:#00adb5"><b>출력 결과</b></a><br>
입력 : 4 2 
```
1 1
1 2
1 3
1 4
2 1
2 2
2 3
2 4
3 1
3 2
3 3
3 4
4 1
4 2
4 3
4 4
```

<hr>
부분 집합도 파워셋 처리하는 부분이 제일 중요하다.<br>
먼저 true로 기저조건이 될 때까지 다 가고나서 반대로 하나씩 false 해주며 계속 왔다갔다 하는 개념이다.<br>
여기서도 재귀개념을 확실히 알아야 이해가 될 것이다.<br>
<hr>
