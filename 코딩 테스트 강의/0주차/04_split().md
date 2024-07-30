- 정의
	- 문자열을 특정 문자열을 기준으로 쪼개서 배열화 시키는 함수
	- 하지만 C++에서는 STL에 존재하지 않아 구현해야 한다
- 구현
```C++
vector split(string input, string delimiter) 
{ 
	vector ret;
	long long pos = 0; 
	string token = ""; 
	while ((pos = input.find(delimiter)) != string::npos) 
	{ 
		token = input.substr(0, pos); 
		ret.push_back(token); 
		input.erase(0, pos + delimiter.length());
	} 
	ret.push_back(input); 
	return ret; 
}

////////////////////////////////////////////////////////////////////
더 빠른 코드
vector split(const string& input, string delimiter) 
{ 
	vector result; 
	auto start = 0; 
	auto end = input.find(delimiter); 
	while (end != string::npos) 
	{ 
		result.push_back(input.substr(start, end - start)); 
		start = end + delimiter.size(); 
		end = input.find(delimiter, start); 
	} 
	result.push_back(input.substr(start)); 
	return result; 
}
```
- reverse
	-  원래 문자열을 반대로 바꿔버린다
- substr
	-   처음 들어온 인자 값부터 시작해서 두 번째 인자로 들어온 수만큼 문자열을 뽑아낸다
	- 두 번째 인자 값이 없으면 문자열의 끝까지 뽑아낸다
- find:
	- 어떠한 문자열이 들어있는지 찾아낸다