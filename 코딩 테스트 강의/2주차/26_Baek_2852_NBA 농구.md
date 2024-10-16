https://www.acmicpc.net/problem/2852
```c++
#include <iostream>
#include <vector>
using namespace std;
  
int n,o,A,B, aSum, bSum;
string s, sPrev;
  
string print(int a)
{
    string d = "00" + to_string(a / 60);
    string e = "00" + to_string(a % 60);
    return d.substr(d.size() - 2, 2) + ":" + e.substr(e.size() - 2, 2);
}
  
int ChangeToInt(string a)
{
    return atoi(a.substr(0, 2).c_str()) * 60 + atoi(a.substr(3, 2).c_str());
}
void Go(int& sum, string s)
{
    sum+= ChangeToInt(s) - ChangeToInt(sPrev);
}
  
int main()
{
    cin >> n;
    for (int i = 0; i < n; i++)
    {
        cin>> o >> s;
        if(A>B)
            Go(aSum, s);
        else if(B>A)
            Go(bSum, s);
        o == 1 ? A++ : B++;
        sPrev = s;
    }
  
    if(A > B)
    Go(aSum, "48:00");
    else if(B > A)
    Go(bSum, "48:00");
    cout << print(aSum) << "\n";
    cout << print(bSum) << "\n";
}
```
- o에 득점 팀, s에 득점 시간을 입력받아 A,B 팀 중 더 득점이 많았는지 판단해 Go 함수를 호출할것이다
- 그렇지 않으면 o가 1일 땐 A를 ++하고 그렇지 않으면 B를 ++해준다
- Go함수에서는 Sum 값에 ChangeToInt함수를 통해 값들을 가져와 차이를 더해줄 것이다
- 이때 ChangeToInt함수는 atoi 함수를 통해 문자열을 정수로 바꿔줄 것이다
- 이때 string 변수 중 :를 빼야하기 때문에 substr을 사용해줄것이다
- 분과 초를 한번에 계산해야 편하기 때문에 분을 정수로 바꾼 뒤 60을 곱하고 초를 바꾼 값과 더해준다