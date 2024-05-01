- 정의
    - 최소 비용 신장 트리를 구하는 알고리즘중 하나로 크루스칼 알고리즘과 프림 알고리즘처럼 간선을 하나씩 선택하는 것이 아닌 동시에 여러개의 간선을 선택하여 트리를 만드는 알고리즘
    - MST는 그래프 내의 모든 정점을 연결하는 트리중 가중치의 합이 가장 작은 트리
    - MST는 네트워크 설계, 클러스터링, 최적화 문제등 다양한 분야에응용
- ![](https://blog.kakaocdn.net/dn/2mqvh/btsvMLy5agE/gf0hKOGqPQLtWxKCX6kHgk/img.png)
    - 포레스트란 n개의 정점이라는 의미라고 생각하면 된다
    - 각 정점에 인접한 간선에서 가장 비용이 저거은 간선을 선택하면 간선이 겹치는 경우가 생겨 중복된 간선중 하나를 없애준다
    - 그러면 특별한 경우가 아니면 2개 이상의 트리가 나오는데 여기서 각 트리의 인접한 간선중 트리를 이어줄 수 있는 간선중 최소 비용 간선을 택한다
    - 이대 싸이클을 만들지 않도록 하며, 간선의 개수가 n-1이 되면 최소 비용 신장 트리가 완성된다
- 수행 과정
    
    - 그래프와 가중치 표
    
    ![](https://blog.kakaocdn.net/dn/b24Jv9/btsvMZKFJ2b/djo5994tEkKGNNSx3BBRy0/img.png)
    
    - 1단계![](https://blog.kakaocdn.net/dn/bUvXM4/btsvP9TvnH6/57BbkXnKS7sKgF3k5DukT1/img.png)
        - 모든 정점에서 인접한 간선중 가장 작은 비용을 가지는 간선을 선택해 중복이 되는 경우 중복되지 않도록 하나는 지워준다
    - 2단계![](https://blog.kakaocdn.net/dn/QxRsy/btsvMWNUTXY/PCgOT9jhGYUezlHnyLFKN1/img.png)
        
        - 각 트리에서 가장 작은 산선을 선택해, 이 경우 (2,6)을 선택하면 신장트리가 완성되며, 최소신장 트리를 찾을때 까지 반복해준다
        
    
-  장점
    - 분할 및 정복 전략을 기반으로, 각 단계에서 부분 그래프를 합치면서 최소 신장 트리를 구축한다
    - 이 알고리즘은 병렬처리에 적합하며, 특히 대규모 그래프에서 빠르게 동작한다
- 시간 복잡도
    - 총 시간: O(E logV)
        - E는 간선의 수, V는 그래프의 정점의 수
    - 부분 그래프 연결 과정 복잡도: O(E) 또는 O(E logV)
    - 부분 그래프 분할 과정 복잡도: O(V) 또는O(VlogV)
    - 알고리즘 반복 횟수: O(logV)
- 구현

```C++
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

// 그래프의 간선을 나타내는 구조체
struct Edge 
{
    int src, dest, weight;
};

// 보르부카 알고리즘 구현
void boruvkaMST(vector<Edge>& edges, int V) 
{
    vector<int> cheapest(V, -1); // 각 부분 그래프에서 가장 싼 간선
    vector<int> partOf(V);       // 각 정점이 속한 부분 그래프 번호

    int numTrees = V; // 현재 부분 그래프의 수

    while (numTrees > 1) 
    {
        // cheapest 배열 초기화
        fill(cheapest.begin(), cheapest.end(), -1);

        // 각 간선을 검사하여 가장 싼 간선 찾기
        for (int i = 0; i < edges.size(); i++) 
        {
            int src = edges[i].src;
            int dest = edges[i].dest;
            int weight = edges[i].weight;

            int set1 = partOf[src];
            int set2 = partOf[dest];

            if (set1 != set2) 
            {
                if (cheapest[set1] == -1 || edges[cheapest[set1]].weight > weight)
                    cheapest[set1] = i;

                if (cheapest[set2] == -1 || edges[cheapest[set2]].weight > weight)
                    cheapest[set2] = i;
            }
        }

        // 각 부분 그래프에서 가장 싼 간선을 사용하여 연결
        for (int i = 0; i < V; i++) 
        {
            if (cheapest[i] != -1) 
            {
                int set1 = partOf[edges[cheapest[i]].src];
                int set2 = partOf[edges[cheapest[i]].dest];

                if (set1 != set2) 
                {
                    cout << "Edge " << edges[cheapest[i]].src << " - " << edges[cheapest[i]].dest << " Weight: " << edges[cheapest[i]].weight << endl;
                    numTrees--;

                    int newSet = min(set1, set2);
                    for (int j = 0; j < V; j++) 
                    {
                        if (partOf[j] == set1 || partOf[j] == set2) 
                        {
                            partOf[j] = newSet;
                        }
                    }
                }
            }
        }
    }
}

int main() 
{
    int V, E;
    cout << "Enter the number of vertices: ";
    cin >> V;
    cout << "Enter the number of edges: ";
    cin >> E;

    vector<Edge> edges(E);
    cout << "Enter the source, destination, and weight of each edge:" << endl;
    for (int i = 0; i < E; i++) {
        cin >> edges[i].src >> edges[i].dest >> edges[i].weight;
    }

    cout << "Minimum Spanning Tree:" << endl;
    boruvkaMST(edges, V);

    return 0;
}
```