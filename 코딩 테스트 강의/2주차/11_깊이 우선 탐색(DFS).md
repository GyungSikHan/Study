- 정의
	- 그래프를 탐색할 때 사용
	- 어떤 노드에서 시작해 인접 노드들을 재귀적으로 방문하며 방문한 정점을 다시 방문하지 않고 각 분기마다 가능한 가장 멀리 있는 노드까지 탐색하는 알고리즘
- 수도코드
```C++
DFS(u, adj)
{
	u.visited = true;
	for(v : adj[u])
		if(v.visited == false)
			DFS(v, adj);
}
```

방법
1. 돌 다리도 두들겨보기
	- 방문  여부를 확인하고 방문하는 방법으로 시작 지점에 대해 방문 처리를 해줘야 한다
```C++
			void DFS(int here)
			{
				for(int v : adj[here])
				{
					if(visited[v] == true)
						continue;
					visited[v] = true;
					DFS(v);
				}
			}
```
1. 못먹어도 Go
		- 방문이 되었던 안되었던 DFS 함수를 호출하고 함수가 시작시 방문 체크를 해주면서 방문했다면 함수를 종료시키는 방법
```C++
			void DFS(int here)
			{
				if(visited[here] == true)
					return;
				for(int v : adj[here])
					DFS(v);
			}
```

- 풀어보기
```
종화는 방구쟁이
종화는 21세기 유명한 방구쟁이다. 종화는 방구를 낄 때 "이러다... 다 죽어!!" 를 외치며 방구를 뀌는데 이렇게 방귀를 뀌었을 때 방귀는 상하좌우 네방향으로 뻗어나가며 종화와 연결된 "육지"는 모두 다 오염된다. "바다"로는 방구가 갈 수 없다. 맵이 주어졌을 때 종화가 "이러다... 다 죽어!!"를 "최소한" 몇 번외쳐야 모든 육지를 오염시킬 수 있는지 말해보자. 1은 육지며 0은 바다를 가리킨다.

입력
맵의 세로길이 N과 가로길이 M 이 주어지고 이어서 N * M의 맵이 주어진다.

출력
"이러다... 다 죽어!!"를 몇 번외쳐야하는지 출력하라.

범위
1 <= N <= 100
1 <= M <= 100

​예제입력

5 5
1 0 1 0 1
1 1 0 0 1
0 0 0 1 1
0 0 0 1 1
0 1 0 0 0

예제출력

4
```
```C++
#include <iostream>
#include <vector>

using namespace std;

int n, m;
int dY[4] = {-1,0,1,0};
int dX[4] = {0,1,0,-1};
int Count;
  
void DFS(vector<vector<int>> maps, vector<vector<bool>>& Visited, int y, int x)
{
    Visited[y][x] = true;
	for (int i = 0; i < 4; i++
    {
        int nY = y+dY[i];
        int nX = x+dX[i];
        if(nY >= 0 && nY < n && nX >= 0 && nX < n)
            if(maps[nY][nX] == 1 && Visited[nY][nX] == false)
                DFS(maps, Visited, nY, nX);
    }
}
 
int main()
{
    cin >> n >> m;
    vector<vector<int>> maps(n,vector<int>(m, 0));
    vector<vector<bool>> Visited(n, vector<bool>(m,false));
    for (int i = 0; i < n; i++)
        for (int j = 0; j < m; j++)
            cin>>maps[i][j];

    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < m; j++)
        {
            if(maps[i][j] == 1 && Visited[i][j] == false)
            {
                DFS(maps, Visited, i, j);
                Count++;
            }
        }
    }
    cout<<Count<<endl;
}
```