---
layout: single
title:  "순열 / 조합 / 부분 집합 응용"
categories: 
    - ALGORITHM
tags: 
    - [2022-02, ALGORITHM, STUDY]
sidebar:
    nav: "docs"
---

# 📚 <a style="color:#00adb5">순열 응용</a>

## <a style="color:#00adb5">순열 ( Permutation ) </a>이란 무엇인가 ?
<b><a style="color:red">서로 다른 것들 중 몇 개를 뽑아서 한 줄로 나열하는 것</a></b><br>
서로 다른 N개 중 R개를 택하는 것<br>
<b><a style="color:red">순열은 순서가 상관이 있다 !!!</a></b><br>
보통 N이 11,12 정도까지일 때만 사용하도록 추천한다. ( 그 이후부턴 시간 복잡도가 급속도로 증가 )<br>

### 식

<b><a style="color:red">nPr</a></b><br>
nPr = n * ( n-1 ) * ( n-2 ) * .. * ( n-r-1 )<br><br>
<b><a style="color:red">nPn = n!</a></b><br>
n! = n * ( n-1 ) * ( n-2 ) * .. 2 * 1<br><br>


## <a style="color:#00adb5">순열</a>을 생성하는 응용 방법


- <a href="#a">반복문을 통한 순열 생성</a>
- <a href="#b">재귀 호출을 통한 순열 생성</a>
- <a href="#c">비트 마스킹을 통한 순열 생성</a>
- <a href="#d">NextPermutation_현 순열에서 사전 순으로 다음 순열 생성</a>




<hr>
결과값은 다 동일하다 <br>
```java
3
1 2 3
[1, 2, 3]
[1, 3, 2]
[2, 1, 3]
[2, 3, 1]
[3, 1, 2]
[3, 2, 1]
```
<hr>


### <a style="color:#00adb5" name="a">반복문</a>을 통한 순열 생성
<a style="color:red"><b>for문</b></a>을 사용해서 구현<br>
뽑는 수가 정해져있으면 반복문을 사용해도 된다.<br>
그러나 N이 커지면 커질 수록 코드의 량이 늘어나서 재귀를 사용하는 것이 더 효율적이다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Permutataion_for {
	static StringTokenizer st;
	public static void main(String[] args) throws NumberFormatException, IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringBuilder sb = new StringBuilder();
		
		// 배열의 수 
		int N = Integer.parseInt(br.readLine());
		
		// 배열 입력
		int[] arr = new int[N];
		st = new StringTokenizer(br.readLine(), " ");
		for(int i=0; i<N; i++) {
			arr[i] = Integer.parseInt(st.nextToken());
		}
		

		for(int i=0; i<N; i++) {
			for(int j=0; j<N; j++) {
				if(i==j) {
					continue;
				}
				for(int z=0; z<N; z++) {
					if(i==z || j==z) {
						continue;
					}
					sb.append("[").append(i+1).append(",");
                    sb.append(j+1).append(",");
                    sb.append(z+1).append("]").append("\n");
				}
			}
		}
		
		System.out.println(sb);
	}
}
```


### <a style="color:#00adb5" name="b">재귀 호출</a>을 통한 순열 생성
<a style="color:red"><b>booelan[]</b></a> 사용<br>
원소가 선택되었는지 안되었는지 체크해준다.<br>
그리고 새로운 배열에 저장한다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.StringTokenizer;

public class Permutation_rec {
	static StringTokenizer st;
	static int N;
	static int[] arr, arr_res;
	static boolean[] isChecked;

	public static void main(String[] args) throws NumberFormatException, IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringBuilder sb = new StringBuilder();

		// 배열의 수
		N = Integer.parseInt(br.readLine());

		// 배열 입력
		arr = new int[N];

		// 순열 배열 저장
		arr_res = new int[N];

		// boolean
		isChecked = new boolean[N];

		st = new StringTokenizer(br.readLine(), " ");
		for (int i = 0; i < N; i++) {
			arr[i] = Integer.parseInt(st.nextToken());
		}

		permutation(0);

	}

	// 순열 구하는 재귀함수
	static void permutation(int cnt) {
		// 기저조건 : 다 돌았을 때
		if (cnt == N) {
			System.out.println(Arrays.toString(arr_res));
			return;
		}

		// 입력받은 수를 현재 자리에 넣어보기
		for (int i = 0; i < N; i++) {
			
			// 기존 수와 중복하면 통과
			if (isChecked[i]) {
				continue;
			}
			
			// 배열에 넣기
			arr_res[cnt] = arr[i];
			isChecked[i] = true;
			
			// 다음수 뽑으러 가기
			permutation(cnt + 1);
			// 백트래킹에서 원상 복구
			isChecked[i] = false;
		}

	}
}
```


### <a style="color:#00adb5" name="c">비트마스킹</a>을 통한 순열 생성 
<a style="color:red"><b>정수</b></a>와 <a style="color:red"><b>비트연산자</b></a>를 사용<br>
- 0 상태<br>
사용중 x, 선택 x, false
- 1 상태<br>
사용중 o, 선택 o, true<br>

boolean 형을 정수로 바꿔서 표현한다라고 생각하면 된다.<br>
flag는 각 위치 수를 선택했는지 여부를 나타낸다 ( == (boolean[i] = true))<br>

```java
package blog;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.StringTokenizer;

public class Permutation_bitmask {
	static StringTokenizer st;
	static int N;
	static int[] arr, arr_res;

	public static void main(String[] args) throws NumberFormatException, IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringBuilder sb = new StringBuilder();

		// 배열의 수
		N = Integer.parseInt(br.readLine());

		// 배열 입력
		arr = new int[N];

		// 순열 배열 저장
		arr_res = new int[N];

		st = new StringTokenizer(br.readLine(), " ");
		for (int i = 0; i < N; i++) {
			arr[i] = Integer.parseInt(st.nextToken());
		}

		permutation(0, 0);

	}

	// 순열 구하는 재귀함수
	static void permutation(int cnt, int flag) {
		// 기저조건 : 다 돌았을 때
		if (cnt == N) {
			System.out.println(Arrays.toString(arr_res));
			return;
		}

		// 입력받은 수를 현재 자리에 넣어보기
		for (int i = 0; i < N; i++) {

			// 기존 수와 중복하면 통과
			// (isChecked[i]) 와 동일한 부분
			// i를 한 칸 옮기고 flag와 & 연산을 한 결과가 값이 0이 아니면 2^n, n자리의 원소가 선택된 수 이다.
			// ex) 결과가 8이면 3번쨰 자리의 원소는 이미 선택된 수 이다.
			if ((flag & 1 << i) != 0) {
				continue;
			}

			// 배열에 넣기
			arr_res[cnt] = arr[i];

			// 다음수 뽑으러 가기
			// flag를 통해 상태 추가를 해준다. | 연산에서 1이 있으면 무조건 1 이라서 i번째 원소가 선택된 수로 된다.
			permutation(cnt + 1, flag | 1 << i);
			// boolean 때는 두 번하는데 flag는 한 번만 하는 이유
			// isChecked[i] =true , isChecked[i] = false
			// flag를 변경하는게 아니라 체크만 해주는 거라서
		}
	}
}
```



#### 비트 연산자

- & <br>
AND 연산<br>
두 비트열을 비교하여 모두 1이면 1로 처리하고 아니면 0으로 처리한다.

```java
10 & 3
    00001010
  & 00000011
  ㅡㅡㅡㅡㅡㅡ
 -> 00000010
```

- | <br>
OR 연산<br>
두 비트열을 비교하여 모두 0이면 0로 처리하고 아니면 1으로 처리한다.

```java
10 | 3
    00001010
  | 00000011
  ㅡㅡㅡㅡㅡㅡ
 -> 00001011
```

- ^ <br>
XOR 연산 ( 같으면 0, 다르면 1 )

- ~ <br>
단항 연산자로서 피연산자의 모든 비트를 반전 시킨다. ( 1 -> 0 , 0 -> 1)

- << <br>
피연산자의 비트 열을 왼쪽으로 이동 시킨다.<br>
한 칸마다 2배로 증가한다.


```java
10 << 2
    00001010
  ㅡㅡㅡㅡㅡㅡ
 -> 00101000
```

- >> <br>
피연산자의 비트 열을 오른쪽으로 이동 시킨다.<br>
한 칸마다 1/2로 감소한다.

```java
10 >> 2
    00001010
  ㅡㅡㅡㅡㅡㅡ
 -> 00000010
```


### <a style="color:#00adb5" name="d">NextPermutation</a> - 현 순열에서 사전 순으로 다음 순열 생성
<a style="color:red"><b>현 순열에서 사전 순으로 다음 순열 생성 하는 방식</b></a>

#### 알고리즘
배열을 오름차순으로 정렬한 후 시작한다.
아래 과정을 반복하여 사전 순으로 다음으로 큰 순열을 생성한다 ( 가장 큰 내림차순 순열을 만들 때까지 반복한다. )



# <a style="color:#00adb5">조합 응용</a>

## <a style="color:#00adb5">조합 ( Combination ) </a>이란 무엇인가 ?


# <a style="color:#00adb5">부분 집합 응용</a>

## <a style="color:#00adb5">부분 집합  </a>이란 무엇인가 ?