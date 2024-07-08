https://www.acmicpc.net/problem/9663
```C++
#include <iostream>

using namespace std;

int n, total=0;
int col[15];

bool Check(int level)
{
	for (int i = 0; i < level; i++)
		if (col[i] == col[level] || abs(col[level] - col[i]) == level - i)
			return false;
	
	return true;
}


void NQueen(int x)
{
	if (x == n)
		total++;
	else
	{
		for (int i = 0; i < n; i++)
		{
			col[x] = i;
			if (Check(x) == true)
				NQueen(x + 1);
		}
	}
}

int main()
{
	cin >> n;

	NQueen(0);
	cout << total << endl;
}
```
- 2차원 배열을 만들어서 보드 하나하나 체크를 해서 문제를 풀려했지만 그게 아니였다
- 1차원 배열을 이용할 것인데 index를 행으로 두고 그 안에 퀸이 들어갈 열을 저장할 것이다
- 예를 들어 4-4 보드판을 보면 밑의 그림처럼 0번째 배열 즉 0행에 퀸이 있는 2열을 장, 1번째 배열엔 1열, 2번째 배열엔 3열, 3번째 배열에는 1열을 저장한다![[Pasted image 20240707205316.png]]
- 이렇게 4개의 퀸이 보드에 들어오면 count를 해주고 이를 백트레킹을 이용해 모든 경우의 수를 찾아주는 문제이다
- NQueen함수의 매개변수는 보드에 퀸의 갯수가 들어갈 것이다
- 퀸의 갯수 x가 입력한 n과 같으면 total을 ++해준다 이때는 입력한 수 만큼 퀸이 보드에 들어갔다는 소리이다
- 그렇지 않으면 반복문을 통해 입력받은 n까지 반복을 할것인데 col의 x번째에 i를 넣어 x행에 i열을 넣어 줄 것다
- 이때 Check 함수가 true면 NQueen 함수에 x+1을 한 값을 통해 재귀를 타준다
- Check함수는 level 즉 퀸이 있는 행 x를 넣어준뒤 level만큼 반복문을 돌려준다
- 이때 col의 i번째 값과 col의 level값이 같을때 즉 같은 행 또는 열일때 이므로 이때는 false를 return해준다
- 또는 abs를 통해 col의 level - col의 i의 절대 값이 level-i이 같을 때, 즉 퀸이 있는 대각선 행열에 퀸이 있단 의미이므로 마찬가지로 false를 return해준다
- 그렇지 않을 땐 true를 return해준다
- 이런식으로 total을 계속 누적하여 n-n보드에 n개의 퀸이 들어갈 수 있는 경우의 수를 출력해준다