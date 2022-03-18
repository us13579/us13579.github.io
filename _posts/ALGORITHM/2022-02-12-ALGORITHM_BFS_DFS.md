---
layout: single
title:  "ALGORITHM_BFS & DFS"
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

# 📚 <a style="color:#00adb5">BFS & DFS</a>

## <a style="color:#00adb5">BFS ( Breadth First Search )</a>이란 무엇인가 ?
<p align="center"><img src="./../../images/BFS.gif"></p><br>
루트 노드의 자식 노들들을 먼저 모두 차례로 방문한 후에, 방문했던 자식 노드들을 기준으로 하여 다시 해당 노드의 자식 노드들을 차례로 방문하는 방식이다.<br>
최대한 넓게 이동한 다음, 더 이상 갈 수 없을 때 아래로 이동한다.<br>
<a style="color:red"><b>너비 우선 탐색</b></a>이라 한다.<br><br>

인접한 노드들에 대해 탐색을 한 후, 차례로 다시 너비우선탐색을 진행해야 하므로<br>
선입선출 형태의 자료구조인 <a style="color:red"><b>큐</b></a>를 활용한다 !!<br>

### <a style="color:#00adb5">BFS</a>를 활용한 문제 유형

- 그래프의 모든 정점을 방문하는 것이 주요한 문제
- 최단거리를 구해야 하는 문제
- 검색 대상의 규모가 크지 않고, 검색 시작 시점으로부터 원하는 대상이 별로 멀지 않은 경우

### <a style="color:#00adb5">BFS</a> 알고리즘
큐를 사용해 노드들을 삽입, 반환 하고 <br>
boolean을 이용해 방문했던 곳인지 아닌지 판단한다.<br>

1. 현재 노드를 큐에 삽입
2. while문 생성 ( 종료 조건 : 큐가 비어 있을 경우 )
3. x <- 큐의 첫 번째 노드 반환 ( offer )
4. x 실행 ( 문제 조건에 따라 다름 )
5. x의 자식노드들 큐에 삽입 ( push )
6. while문 반복


### <a style="color:#00adb5">BFS </a>실습 해보즈아 !

```java
import java.util.*;

public class Main {

    public static boolean[] visited = new boolean[9];
    public static ArrayList<ArrayList<Integer>> graph = new ArrayList<ArrayList<Integer>>();

    // BFS 함수 정의
    public static void bfs(int start) {
        Queue<Integer> q = new LinkedList<>();
        q.offer(start);
        // 현재 노드를 방문 처리
        visited[start] = true;
        // 큐가 빌 때까지 반복
        while(!q.isEmpty()) {
            // 큐에서 하나의 원소를 뽑아 출력
            int x = q.poll();
            System.out.print(x + " ");
            // 해당 원소와 연결된, 아직 방문하지 않은 원소들을 큐에 삽입
            for(int i = 0; i < graph.get(x).size(); i++) {
                int y = graph.get(x).get(i);
                if(!visited[y]) {
                    q.offer(y);
                    visited[y] = true;
                }
            }
        }
    }

    public static void main(String[] args) {
        // 그래프 초기화
        for (int i = 0; i < 9; i++) {
            graph.add(new ArrayList<Integer>());
        }

        // 노드 1에 연결된 노드 정보 저장 
        graph.get(1).add(2);
        graph.get(1).add(3);
        graph.get(1).add(8);

        // 노드 2에 연결된 노드 정보 저장 
        graph.get(2).add(1);
        graph.get(2).add(7);

        // 노드 3에 연결된 노드 정보 저장 
        graph.get(3).add(1);
        graph.get(3).add(4);
        graph.get(3).add(5);

        // 노드 4에 연결된 노드 정보 저장 
        graph.get(4).add(3);
        graph.get(4).add(5);

        // 노드 5에 연결된 노드 정보 저장 
        graph.get(5).add(3);
        graph.get(5).add(4);

        // 노드 6에 연결된 노드 정보 저장 
        graph.get(6).add(7);

        // 노드 7에 연결된 노드 정보 저장 
        graph.get(7).add(2);
        graph.get(7).add(6);
        graph.get(7).add(8);

        // 노드 8에 연결된 노드 정보 저장 
        graph.get(8).add(1);
        graph.get(8).add(7);

        bfs(1);
    }
}
```
<hr>
<a style="color:#00adb5"><b>출력 결과</b></a><br>
```
1 2 3 8 7 4 5 6
```
<hr>


## <a style="color:#00adb5">DFS</a>이란 무엇인가 ?
<p align="center"><img src="./../../images/DFS.gif"></p><br>
루트 노드에서 출발하여 한 방향으로 갈 수 있는 경로가 있는 곳까지 깊이 탐색해 가다가 더 이상 갈 곳이 없게 되면, 가장 마지막에 만났던 갈림길 간선이 있는 노드로 되돌아와서 다른 방향의 노드로 탐색을 반복하여 결국 모든 노드를 방문하는 순회방법이다.<br>
최대한 깊이 내려간 뒤, 더이상 깊이 갈 곳이 없을 경우 옆으로 이동한다.<br>
<a style="color:red"><b>깊이 우선 탐색</b></a>이라 한다.<br><br>

가장 마지막에 만났던 갈림길의 노드로 되돌아가서 다시 깊이 우선 탐색을 반복해야 하므로 <a style="color:red"><b>재귀적으로 구현</b></a>하거나 후입선출 구조의 <a style="color:red"><b>스택</b></a>을 활용한다 !!<br>
일반적으로 <a style="color:red"><b>재귀적으로 구현</b></a>하는 것이 가장 보편적이로 짧은 코드를 작성할 수 있다.<br>
여기서 주의할 점은 재귀 호출이 중단되는 조건인 <a style="color:red"><b>기저조건</b></a>을 반드시 포함해야 한다.

### <a style="color:#00adb5">DFS</a>를 활용한 문제 유형

- 그래프의 모든 정점을 방문하는 것이 주요한 문제
- 경로의 특징을 저장해둬야 하는 문제
- 검색 대상 그래프가 정말 크다면 DFS를 고려

### <a style="color:#00adb5">DFS</a> 알고리즘
가장 보편적인 재귀적으로 구현하는 것을 실습해 보겠다.<br>

1. 현재 노드를 방문
2. for문을 통해 모든 자식노드 탐색
3. for문 안에서 재귀 함수 호출
4. 반복
5. 기저조건 만나면 return
6. 자식노드갔다가 부모노드갔다가 반복 -> 전체 탐색


### <a style="color:#00adb5">DFS</a> 실습 해보즈아 !
```java
import java.util.*;

public class Main {

    public static boolean[] visited = new boolean[9];
    public static ArrayList<ArrayList<Integer>> graph = new ArrayList<ArrayList<Integer>>();

    // DFS 함수 정의
    public static void dfs(int x) {
        // 현재 노드를 방문 처리
        visited[x] = true;
        System.out.print(x + " ");
        // 현재 노드와 연결된 다른 노드를 재귀적으로 방문
        for (int i = 0; i < graph.get(x).size(); i++) {
            int y = graph.get(x).get(i);
            if (!visited[y]) dfs(y);
        }
    }

    public static void main(String[] args) {
        // 그래프 초기화
        for (int i = 0; i < 9; i++) {
            graph.add(new ArrayList<Integer>());
        }

        // 노드 1에 연결된 노드 정보 저장 
        graph.get(1).add(2);
        graph.get(1).add(3);
        graph.get(1).add(8);

        // 노드 2에 연결된 노드 정보 저장 
        graph.get(2).add(1);
        graph.get(2).add(7);

        // 노드 3에 연결된 노드 정보 저장 
        graph.get(3).add(1);
        graph.get(3).add(4);
        graph.get(3).add(5);

        // 노드 4에 연결된 노드 정보 저장 
        graph.get(4).add(3);
        graph.get(4).add(5);

        // 노드 5에 연결된 노드 정보 저장 
        graph.get(5).add(3);
        graph.get(5).add(4);

        // 노드 6에 연결된 노드 정보 저장 
        graph.get(6).add(7);

        // 노드 7에 연결된 노드 정보 저장 
        graph.get(7).add(2);
        graph.get(7).add(6);
        graph.get(7).add(8);

        // 노드 8에 연결된 노드 정보 저장 
        graph.get(8).add(1);
        graph.get(8).add(7);

        dfs(1);
    }
}
```
<hr>
<a style="color:#00adb5"><b>출력 결과</b></a><br>
```
1 2 7 6 8 3 4 5
```
<hr>



<br><br><br><br>
👏 참조<br>
<a href="https://devuna.tistory.com/32" target=_blank>https://devuna.tistory.com/32</a><br>
<a href="https://freedeveloper.tistory.com/273" target=_blank>https://freedeveloper.tistory.com/273</a>
