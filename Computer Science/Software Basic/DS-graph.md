# 그래프 Graph
- 그래프란 사물을 정점(Vertex)과 간선(Edge)으로 나타내기 위한 도구
- 두가지 방식으로 구현할 수 있다 
1. 인접행렬(Adjacency Matrix) 
  - 이차원배열 
  - 모든 정점들의 연결 여부를 저장하여 O(v²)의 공간을 요구하므로 공간 효율성이 떨어짐
  - 서로 연결되어 있는지를 확인하기 위해 O(1)의 시간을 요구함
2. 인접리스트(Adjacency List) 
  - 리스트 사용
  - 연결된 간선의 정보만을 저장해 O(E)의 공 요구하므로 공간 효율성이 좋음
  - 서로 연결되어 있는지 확인하기 위해 O(V)의 시간을 요구함

### 무방향 비가중치 그래프와 인접행렬
- 무방향그래프 : 모든 간선이 방향성을 가지지 않는 그래프
- 비가중치 그래프 : 모든 간선에 가중치가 없는 그래프
- 무방향비가중치 그래프가 주어졌을 때 연결되어 있는 상황을 인접 행렬로 출력할 수 있다
```c
#define _CRT_SECURE_NO_WARNINGS
#include<stdio.h>

int a[1001][1001];
int n,m

int main(void){
  scanf("%d %d",&n, &m);
  for(int i = 0 ; i < m ; i++){
    int x, y;
    scanf("%d %d", &x, &y);
    a[x][y] = 1;
    a[y][x] = 1;  
  }
  
  for(int i = 1; i<=n;i++){
    for(int j =1;j<=n;j++){
      printf("%d", a[i][j]);
    }
    printf("\n");
  }
  
  system("pause");
}
```
### 방향 가중치 그래프와 인접 리스트
- 방향그래프 : 모든 간선이 방향을 가지는 그래프
- 가중치 그래프 : 모든 간선에 가중치가 있는 그래프
- 방향 가중치 그래프가 주어졌을 때 연결되어 있는 상황을 인접 리스트로 출력할 수 있다
```c
#define _CRT_SECURE_NO_WARNINGS
#include<stdio.h>
#include<stdlib.h>

typedef struct{
  int index;
  int distance;
  struct Node *next;
} Node;

void addFront(Node *root, int index, int distance){
  Node *node = (Node*)malloc(sizeof(Node));
  node->index = index;
  node ->distance = distance;
  node->next = root->next;
  root->next -> node;
}

void showAll(Node *root){
  Node *cur = root->next;
  while(cur != NULL){
    printf("%d(거리:)$d", cur->index, cur->distance);
    cur = cur->next;
  }
}

int main(void){
  int n, m;
  scanf("%d %d", &n, &m);
  Node **a=(Node**)malloc(sizeof(Node*) * (n+1));
  for(int i = 1; i <= n; i++){
    int x, y, distance;
    scanf("%d %d %d", &x, &y, &distance);
    addFront(a[x],y,distance);
  }
  for(int i =1; i<=n ; i++){
    printf("원소 [%d]: ",i);
    showAll(a[i]);
    printf("\n");
  }
  system("pause");
  return 0;
}
```
