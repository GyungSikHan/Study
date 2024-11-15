- 비트와 바이트
	- 비트
		- 메모리 구성하는 기본 단위
		- 8비트 폭의 메모리는 256가지 조합 가능
	- 바이트
		- 8비트 메모리 단위
		- 1킬로바이트 = 1024 바이트
		- 1메가바이트 1024 킬로바이트
- 변수
	- int
		- 소수부가 없는 수
		- 16/32비트
	- short
		- 16비트
	- long
		- 최소 32비트
	- long long
		- 최소 64비트
	- float
		- 32비트
	- double
		- 64비트
	- sizeof()
		- 변수나 데이터형의 크기를 바이트 단위로 리턴해줌
- 초기화
	- 정의
		- 선언과 대입을 하나로 조합
		- int test = 0;
		- int test(0); -> C++ 새로운 초기화 문법
- unsigned 형
	- 기본 정수형 데이터들은 음의 정수 값을 저장할 수 있지만 unsigned 형을 사용하면 양의 정수 값만 저장할 수 있도록 만들 수 있다
	- 이를 통해 변수에 저장할 수 있는 최대 값을 늘릴 수 있다
- char / wchar_t
	- char
		- 1바이트 크기를 가지며, 아스키코드 문자를 기반으로 256개의 문자를 표현할 수 있다
		- 단일 바이트 분자를 다루는 자료형
	- wchar_t
		- 일반적으로 2바이트 이상
		- 유니코드를 사용할 수 있는 문자를 표현
		- wchar_t test = L'Q';
- bool
	- 대부분 1바이트를 차지
	- true, false 두가지 값만 가짐
	- 프로그램 흐름을 제어하는 데 사용
- const 제한자
	- const 키워드를 사용하여 변수를 만들어 초기화되면 그 값이 고정된다
	- 이때 값을 변경하려는 어떠한 시도도 허용하지 않는다
	- 시도를 하면 오류 lvalue가 필요하다는 에러가 표시됨
	- 선언시 초기화를 하지 않는다면 값이 미확정으로 남겨진다
	- const가 #difine보다 나은 이유
		- 데이터형을 명시적 지정
		- 정의를 특정 함수나 파일에서만 사용할 수 있도록 제한
		- 배열이나 구조체와 같은 복잡한 데이터형에도 사용 가능
- 부동 소수점
	- 표현 방법
		- .을 이용하여 소수를 나타내는 방법 = 8.01
		- 지수표기를 사용하는 방법 = 3.4E6 (3.45 * 1000000) ->(E6은 10^6)
	- 장점
		- 정수와 정수 사이의 값 표기
		- 스케일을 사용하여 매우 큰 범위 값 표기
	- 단점
		- 연산보조프로세서가 없는 컴퓨터는 정수 연산보다 속도 느리다
		- 정밀도를 잃을 수 있다(부동 소수점 오차 발생)
	- float형 부동소수점 오차 발생 이유
		- 이진 부동소수점 표현 한계
			- 부동소수점이 있는 값을 저장할 때 지수와 가수를 따로 저장
			- 값을 저장시 10진수에서 유한한 소수라도 이진수로 표현할 때 무한한 소수가 되는 경우 존재
			- 이때 2진수로 변경한 값이 저장할 수 있는 자리수를 벗어나는 경우 발생
			- 이때 컴퓨터는 근사값으로 저장하는데 이때 자릿수가 잘리거나 반올림하면서 오차 발생
	- 오차 줄이는 법
		- 정밀도 높은 자료형 사용: float대신 double, long double 사용
		- 고정 소수 연산: 부동소수점 오차없이 원하는 소수자리가지 정확히 계산 가능
		- 임의 연산 라이브러리 사용
		- 오차 허용 범위 사용:  작은 오차를 허용하여 특정한 허용오차보다 작으면 같은 값으로 간주
- 데이터 형 변환
	- 문제
		- 큰 부동소수 자료형 -> 작은 부동소수 자료형 : 정밀도가 손실, 변환 데이터형의 범위 벗어나면 결과 예측 불가
		- 부동소수점형 -> 정수형: 소수부 손실, 변환 데이터형의 범위 벗어나면 결과 예측 불가
		- 큰 정수형 -> 작은 정수형 : 원래 값이 변환 데이터형의 범위 벗어나면 하위 바이트들만 복사됨
		- 120 page