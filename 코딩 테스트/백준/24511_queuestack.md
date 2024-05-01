https://www.acmicpc.net/problem/24511
```C++
#include <iostream>
#include <vector>
#include <deque>

using namespace std;

deque<int> de;
int n{};
int m{};
int a{};
bool flag[100001];

int main()
{
	cin.tie(NULL);
	cout.tie(NULL);
	ios::sync_with_stdio(false);

	cin >> n;
	for (int i = 0; i < n; i++)
		cin >> flag[i];
	for (int i = 0; i < n; i++)
	{
		cin >> m;
		if (flag[i] == 0)
			de.push_back(m);
	}

	cin >> m;

	for (int i = 0; i < m; i++)
	{
		cin >> a;
		de.push_front(a);
		cout << de.back() << " ";
		de.pop_back();
	}
}
```
- 문제에서 0은 큐, 1은 스택으로 flag에 저장해준다
- n만큼 값을 입력 받을 것인데 값 하나하나가 수열 하나하나이다, 즉 총 4개의 수열이 되는 것이다
- flag[i]가 0일 경우에만 deque에 저장할 것인데, 그 이유는 큐는 선입 선출로 값이 바뀌지만 큐는 후입 선출이기 때문에 값이 바뀌지 않기 때문이다
- 큐일 경우에만 값이 바뀌기 때문에 deque에 큐 값들만 저장 될 것이다
- 이때 맨 마지막에 저장된 값들이 빠져나와 출력을 해줄 것이다-어떠한 경우에서든 큐 값만 빠진다 궁금하면 그려서 확인해봐라
- 먼저 저장되어 있던 값들의 맨 마지막 값들이 순서대로 빠져나가야 하므로 deque에 front에 값을 넣고 back값만 출력하고 pop을 해주면 해결이 된다