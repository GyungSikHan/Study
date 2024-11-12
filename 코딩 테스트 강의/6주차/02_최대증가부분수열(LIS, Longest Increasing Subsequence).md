- 정의
	- 숫자가 오름차순으로 증가하는 수열 중 가장 최대로 긴 부분 수열
- 백준 11053(가장 긴 증가하는 부분 수열의 길이 출력)
```C++
#include <iostream>
#include <algorithm>
using namespace std;

int n, a[1001], cnt[1001],ret;

int main()
{
	cin>>n;
	for(int i = 0;i < n; i++)
		cin>>a[i];

	for(int i = 0; i < n; i++)
	{
		int MaxValue = 0;
		for(int j = 0; j < i; j++)
			if(a[j] < a[i] && MaxValue <cnt[j])
				MaxValue = cnt[j];
		cnt[i] = MaxValue+1;
		ret = max(ret, cnt[i]);
	}
	cout<<ret<<endl;
}
```
- 백준 14002(가장 긴 증가하는 부분 수열의 길이 및 가장 긴 증가하는 부분 수열 출력)
```C++
#include<algorithm> 
#include<vector> 
using namespace std; 
int n, a[1001], ret = 1, cnt[1001], idx; int prev_list[1001]; 
vector<int> real; 
void go(int idx)
{ 
	if(idx == -1) 
		return; 
	real.push_back(a[idx]); 
	go(prev_list[idx]); 
	return; 
} 
int main()
{ 
	scanf("%d", &n); 
	for(int i = 0; i < n; i++)
		scanf("%d", &a[i]); 
	fill(prev_list, prev_list + 1001, -1);//처음 시작할 수열을 0으로 저장하기 위해 -1로 초기화 
	fill(cnt, cnt + 1001, 1); 
	for(int i = 0; i < n; i++)
	{ 
		for(int j = 0; j < i; j++)
		{ 
			if(a[j] < a[i] && cnt[i] < cnt[j] + 1)
			{ 
				cnt[i] = cnt[j] + 1; 
				prev_list[i] = j; 
				if(ret < cnt[i])
				{ 
					ret = cnt[i]; 
					idx = i; 
				} 
			} 
		} 
	} 
	printf("%d\n", ret);
	 go(idx); 
	 for(int i = real.size() -1; i >= 0; i--)
		 printf("%d ", real[i]);
	 return 0;
}

**[출처]** [최대증가부분수열,LIS, Longest Increase Sequence](https://blog.naver.com/jhc9639/221449445864)|**작성자** [큰돌](https://blog.naver.com/jhc9639)
```