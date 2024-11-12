- 정의
	- 정렬된 배열에서 탐색 범위를 절반씩 줄여나가는 방식으로 특정 값을 찾는 방식
	- 시간 복잡도는 O(long N)이며 이진탐색이라고도 한다
	- 문제에서 주어진 배열의 크기가 10억이상 등 너무 큰 상태에서 무식하게 값을 찾을 때 배열을 정렬하고 이분탐색을 사용하면 O(log N)으로 효율적으로 찾을 수 있다
	- 이분 탐색의 최악의 시간 복잡도는 $log_2N$이 된다
```C++
#include <iostream>
#include <vector>
using namespace std;

int binarySearch(vector<int>& arr, int target)
{
	int left = 0, right = arr.size()-1;
	while(left <= right)
	{
		int mid = left + (right - left)/2;
		if(arr[mid] == target)
			return mid;
		else if(arr[mid] < target)
			left = mid + 1;
		else
			right = mid -1;
	}
	return -1;
}

int main()
{
	vector<int> arr = {1,3,6,9,21,22,30};
	sort(arr.begin(), arr.end());
	int target = 6;
	
	int result = binarySearch(arr, target);
	if(result != -1)
		cout<<result<<endl;
	else
		cout<<"Not Found" <<endl;
}
```
- 최적화 문제
	- 최적화 문제는 이분 탐색을 통해 결정 문제로 바꾸어 풀 수 있다(Yes or No로 바꾸어 풀 수 있단 의미)