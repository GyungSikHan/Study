- 정의
	- 큐의 선입선출의 개념을 이용해 푸는 알고리즘
	- 그래프를 탐색하는 알고리즘
	- 어떤 정점에서 시작해 다음 깊이의 정점으로 이동하기 전 현재 깊이의 모든 정점을 탐색하며 방문한 정점은 다시 방문하는 알고리즘
	- 가중치를 가진 그래프에서 최단거리 알고리즘으로 쓰인다
	- BFS로 탐색한단 것은 트리의 레벨별로 탐색한단 뜻이다
- 수도코드
```C++
1. 방문 처리만 하는 방법
BFS(G, u)
{
	u.visited = true;
	q.push(u);
	while(q.size())//q.empaty() == false
	{
		u = q.front();
		q.pop();
		for(v : G.adj[u])
			if(v.visited == false)
			{
				v.visited = true;
				q.push(v);	
			}
	}
}

2. 문제내에 가중치가 1일 때 사용하는 방법
BFS(G, u) 
{
	u.visited = 1;
	q.push(u);
	while(q.size()) 
	{
		u = q.front();
		q.pop(); 
		for( v : G.Adj[u])
			if( v.visited == false)
				v.visited = u.visited + 1;
				q.push(v)
	}
}
```
- 가중치가 1이 아닌 서로 다른 값이 주어진다면 벨만포드 또는 다익스트라 알고리즘을 사용하는 것이 더 빠르고 정확하다

- 예제 문제
```
당근마킷 엔지니어 승원이
승원이는 당근을 좋아해서 당근마킷에 엔지니어로 취업했다. 당근을 매우좋아하기 때문에 차도 당근차를 샀다. 이 당근차는 한칸 움직일 때마다 당근을 내뿜으면서 간다. 즉, "한칸" 움직일 때 "당근한개"가 소모된다는 것이다. 승원이는 오늘도 아침 9시에 일어나 당근마킷으로 출근하고자 한다. 승원이는 최단거리로 당근마킷으로 향한다고 할 때 당근몇개를 소모해야 당근마킷에 갈 수 있는지 알아보자. 이 때 승원이는 육지로만 갈 수 있으며 바다로는 못간다. 맵의 1은 육지며 0은 바다를 가리킨다. 승원이는 상하좌우로만 갈 수 있다.

​입력
맵의 세로길이 N과 가로길이 M 이 주어지고 이어서 N * M의 맵이 주어진다. 그 다음 줄에 승원이의 위치(y, x)와 당근마킷의 위치(y, x)가 주어진다. 이 때 승원이의 시작위치(y, x)에서 "당근한개"가 이미 소모된 상태로 본다.

출력
당근을 몇개 소모해야 하는지 출력하라.

범위
1 <= N <= 100
1 <= M <= 100

예제입력

5 5
0 0
4 4 
1 0 1 0 1
1 1 1 0 1
0 0 1 1 1
0 0 1 1 1 
0 0 1 1 1

예제출력
9
```
```C++
#include <iostream>
#include <queue>

using namespace std;
  
int n,m;
int startY,startX;
int endY,endX;
int maps[104][104];
int visited[104][104];
int arY[4] = {-1,0,1,0};
int arX[4] = {0,1,0,-1};
queue<pair<int, int>> q;
  
void DFS(int y, int x)
{
    visited[y][x] = 1;
    q.push({y,x});
  
    while (q.empty() == false )
    {
        int currY = q.front().first;
        int currX = q.front().second;
        q.pop();
        for (int i = 0; i < 4; i++)
        {
            int Y = currY + arY[i];
            int X = currX + arX[i];
            if(Y >= 0 && y < n && X >= 0 && X < m)
            {
                if(maps[Y][X] == 1 && visited[Y][X] == 0)
                {
                    visited[Y][X] = visited[currY][currX]+1;
                    q.push({Y,X});
                }
            }
        }
    }
}
  
int main()
{
    cin>>n>>m;
    cin>>startY>>startX;
    cin>>endY>>endX;
  
    for (int i = 0; i < n; i++)
        for (int j = 0; j < m; j++)
            cin>>maps[i][j];
            
    DFS(i, j);
    cout<< visited[endY][endX] <<endl;
}
```