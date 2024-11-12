- 변수
	- 지역, 전역, 동적
		- 지역 변수
			- 메모리 구조에 stack에 데이터가 저장
			- {} 블록 안에서 쌓인 변수, 코드블럭을 벗어나면 메모리 삭제
		- 전역
			- 메모리 구조에 Data 구역에 데이터 저장
			- {}블록 밖에 쌓인 변수, 프로그램이 끝나면 메모리 삭제
			- static 키워드로도 만들 수 있음
			- extern: 다른 파일에 있는 변수를 전역으로 쓰기 위한 키워드
		- 동적
			- 컴파일 시점이 아닌 런타임 시점에 메모리가 할당
			- 특정 시점에 메모리 할당과 해제
			- heap에 저장됨
			- 변수 크기가 가변적이거나 복잡한 데이터 구조에서 사용가능
			- 속도가 느리고 오버헤드 및 메모리 누수 위험성 때문에 적절한 활용 필요
				- 오버헤드란: 어떤 작업을 수행하기 위해 필요한 추가적 비용
	- 메모리 구조(코드, 데이터, 상/하위)
		-     ![](https://blog.kakaocdn.net/dn/cdomiu/btstRts6SfG/LKJtEt3FQ5kJu41tIOScTK/img.png)
			- Code
				- 프로그램 실행 코드 저장 영역
				- 읽기전용, 변경 불가, 프로그램 실행 중 유지
			- Data
				- 초기화된 전역/정적 변수, 상수등 저장
				- 프로그램 시작 시 초기화, 프로그램 종료 시까지 유지
			- Heap
				- 동적으로 할당된 메모리 저장
				- 동적 메모리 할당 후 해제시 까지 유지
				- 메모리 누수 발생 유의
			- Stack
				- 매개변수, 지역변수 저장
				- 빠른 할당 및 해제
				- LIFO 방식
				- 자동 해제
	- static(정적 변수)
		- 프로그램 시작 시 초기화 되며 프로그램이 끝날 때 삭제
		-  저장 메모리 영역: Data 영역에 저장
		- 지역변수
			- 일반 지역변수와 마찬가지로 함수 내부에서만 접근 가능
			- 함수 호출간 값이 유지
		- 맴버 변수/함수
			- 변수
				-  클래스의 모든 인스턴스에 공유
				- 인스턴스 없이 호출 불가
				- 클래스 맴버 변수나 함수 모두 접근 가능
			- 함수
				- 객체 없이 클래스 이름으로 호출 가능
				- 클래스 이름으로 호출되며, 객체와 무관하다
				- 인스턴스 없이 호출 가능
				- 다른 static 맴버 변수나 함수만 접근 가능
	- extern
		- 다른 파일에 정의된 변수나 함수에 접근할 수 있도록 하는 키워드
		- 변수나 함수를 선언하고, 해당 변수의 정의는 다른 파일에서 함
	- Call By Value/Address/Reference
		- Value
			- 값에 의한 호출
			- 원본 값 수정 불가
			- 값 복사로 더 많은 메모리 사용
			- 안전하지만 큰 데이터에서 비효율적
		- Address
			- 주소에 의한 호출
			- 원본 값 수정 가능
			- 주소만 전달하므로 메모리 사용 적음
			- 포인터를 사용하여 전달
		- Reference
			- 참조에 의한 호출
			- 원본 값 수정 가능
			- 주소 전달과 동일, 복사 없음
			- 참조자를 사용하여 전달
	- auto
		- 변수 타입을 자동으로 추론해주는 키워드
		- 컴파일시 타입이 결정
		- 코드가 간결하고 컴파일러 최적화가 될 수 있으나 가독성에 문제가 생길 수 있으며 디버깅이 어려움

- 상수(const)
	- 포인터
	- 레퍼런스
	- 멤버
    
- 매크로
	- 변수의 문제점
	- #define Add(a, b) a * b

- 구조체
	- 패딩
	- 공용체
    
- 동적할당
	- malloc, free
	- new, delete
	- virtualalloc - virtualfree
    
- 함수 호출 규약
	- 스택 프레임
		- 메모리 오버플로우
	- EBP, ESP
	- cdecl, stdcall, thiscall, fastcall
	- 가변 파라미터 함수 구현 방법
    
- 컴파일러
	- 컴파일 과정
		- 과정별 처리 후 생성 결과물
	- 컴파일러와 인터프리터 차이
	- C#과 C++의 차이
	- 게임 프로그래밍에서 C++ 사용 이유
	
- 정수, 실수
	- Float형의 오차 발생 이유와 범위
	- Int, Float의 값 문자열로 변경

- 포인터
	- 허상 포인터
		- 발생 이유
	- 함수 포인터
		- 사용 이유
		- 델리게이션
		- CallBack 함수

- Template
	- 동작 방식
	- 특수화
	- 함수 템플릿
	- 클래스 템플릿
		- 상속관계
	- Inline 함수
    
- OOP()
	- 특성
		- 정보은닉
	    - 캡슐화
	    - 상속성
		    - dynamic_cast
		    - 업/다운 캐스팅
			- 다운캐스팅 체크 방법
	- 다형성
		- 오버로딩
		- 오버라이딩
	- 추상화
    
- 클래스
	- 암시적 멤버 메서드 6가지
	- 복사 / 이동의 차이
		- l-value, r-value
	- 얕은/깊은 복사의 차이
	- 복사/대입 연산자의 사용 이유
    
- 가상함수
	- 가상화
	- 가상화 조건
	- 가상함수 테이블
	- 추상클래스
	- 인터페이스
	- 가상소멸자

- RTTI
	- type-id
	- static/dynamic/const/reinterpreter

- 객체지향 설계원칙(SOLID)
	- 단일책임
	- 계방폐쇄
	- 리스코프 치환
	- 인터페이스 분리
	- 의존역전
    
- Lamda
	- 익명메서드
	- 캡쳐
	- 클로저
	- LinQ
	- 1급 객체


//자료구조
- 복잡도
	- 시간복잡도
		- 최고/최악/평균
		- 최악 오름차순 나열
		- 빅오에서 순서대로 나열
	- 공간복잡도

- 선형 자료구조
	- 공통
		- 어느 부분에서 사용할지.
	- 항목
		- 스택
			- 표기법(전/중/후)
			- TOP
		- 큐
			- 배열/링크드 리스트 구현
			- 원형 큐
				- 사용 이유
				- 한칸을 비워두는 이유
		- 벡터(가변배열)
			- 문제점
			- 슬랙
			- 구현 방법
			- push_back
			- emplace_back
		- 연결리스트
			- 인덱스 접근(at) 구현 방법
			- 이중 연결 리스트
				- 삽입/삭제 과정
- 비선형 자료구조
	- 트리
		- 구현 방법
		- 2진 트리
			- 시간 복잡도
			- 종류
				- 완전이진
				- 포화이진
			- 순회 방법
				- 각각 어느 부분에서 사용할지?
			- 2진 탐색 트리
				- 2진 탐색
			    - 구현 방법
				- 탐색 소요 시간
			- 균형 2진 트리
				- AVL
				- Red-Black
				- Map(set, pair)
			- 힙
				- 구성방법
			    - 추가와 삭제 구현 방법
				- 우선순위 큐

- 그래프
	- 탐색
		- 깊이우선(BFS)
		- 너비우선(DFS)
	- 정렬
		- O(n^2) 알고리즘
			- 버블
			- 선택
			- 삽입
		- O(nlogn) 알고리즘
			- 병합 정렬
			- 퀵 정렬
				- 문제점
		- 기수 정렬
	- 위상정렬
		- DAG
	- MST(Mimimum Spanning Tree)
		- Prim
	    - Kruskal
		- Sollyn(Borubuka)
	- 최단경로 길찾기
		- BFS(가중치가 없거나 모두 동일한 상황 가장 빠름)
		- 다익스트라(양의 가중치 , 단일 쌍, 단일 출발, 단일 도착)
		- 벨만포드(음의 가중치, 단일 쌍, 단일 출발, 단일 도착)
		- 플로이드 워셜(전체 쌍, 다수 출발, 다수 도착)
		- A* 알고리즘(휴리스틱, 하나의 정점에서 다른 하나의 정점까지의 최단 거리)
		- 네비게이션 메시

- map
	- set
	- pair
	- multimap
- 해싱
	- 해싱 테이블
		- 충돌처리
			- 체이닝
			- 개방 주소
	- 사용 이유
	- 어느 부분에서 사용할지
	- Unordered-Map

- 정렬
    - O(n^2)
		- 버블
		- 삽입
		- 선택
    - O(n log n)
	    - 퀵
		    - O(n^2)의 상황
	    - 병합
    - 기타
	    - 버킷
    
- 알고리즘 설계기법
    - 분할정복
	- 동적계획
	    - 메모이제이션
    - 탐욕
	    - 최적 상황
    - 백트래킹

//DirectX
- D3D11 파이프 라인

- NDC(Normalized Device Coordinate)

- 컬링
	- 프러스텀
	- 쿼드 트리
	- 오클루전

- 백페이스 컬링
	- 삼각형 전/후면 판단 방법

- Culling/Clipping

- WVP
	- Projection
	- Unprojection

- Intersection
	- AABB/OBB
	- Line Trace
	- Picking

- 최단거리
	- 평행하지 않은 두 선분
	- 한 점과 한 선분

- Instancing

- Depth Buffer

- Stencil Buffer

- 짐벌락
	- Rotation Matrix/Quaternion

- Z-Fighting

- Lighting
	- Base
		- Ambient
		- Diffuse
		- Specular
		- Emissive
	- Local
		- Point
		- Spot

- DepthBuffer Shadow
	- 구현 원리
	- 문제점 / 해결 방법
	- Cascade Shadow

- Blend
	- 사용 조건
	- Alpha Blend

- Kinemetics
	- 부모와 자식의 행렬 결합
	- Forward Kinemetics
	- Inverse Kinemetics
	
- 고급
	- Water
		- Reflection
		- Refraction
		- Fresnel
		- Clip Plane
	- Tessellation
		- Hull Shader
		- Domain Shader
		- LOD(Level Of Detail)
	- Deffered Rendering
	    - Forward Rendering과의 차이
		- G-Buffer
	    - 문제점
	- Anti-Aliasing
	    - FXAA
		- MSAA

- PBR(Physically Based Rendering)
    
- SSR(Screen Space Reflection
    
- AO(Ambient Occlusion)
    - SSAO(Screen Space Ambient Occlusion)


//Unreal
- Reflection

- 가비지 컬렉터
	- UPROPERTY
		- UObject/ TSubclassOf

- Serialization
	- GENERATE_BODY
	- UFUNCTION
		- BluepintNativeEvent
		- BlueprintImplemetableEvent
		- BlueprintCallable
	- USTRUCT
	- UCLASS
		- Abstract
		- BlueprintType
		- Blueprintable
		- Const
		- MinimalAPI
		
- Smart Pointer Library
	- TUniquePtr
	- TSharedPtr
	- TWeakPtr
	- TSoftObjectPtr
	- TSharedFromThis

- Actor
	- Lifecycle
	
- Pawn
    
- Character
    
- Delegation
	- Single/Multi
	- Dynamic
	- Dynamic Sparce
	- Event
    
- 문자열
	- FString
	- FName
	- FText

- 모빌리티
	- 스태틱
	- 스테이셔너리
	- 무버블

- Assert
	- check
	- ensure
	- verify

- Build Mode
	- Debug
	- DebugGame
	- Development
	- Shipping
	- Test

- Replication
    - Authority
    

- Thread
	- GameLogic
	- Rendering
    
- Animation
    - IK
	    - Two-Bone
	    - FABRIK
	    - CCD
    - Root Motion
    
- Behavior Tree
    - Composite
	    - Squencer
		- Selector
	    - Simple Parallel
	- Task
    - Black Board

- Asset Load
    - FObjectFinder / LoadObject
    - Hard / Soft Reference
    - FSoftObjectPath
    - FStreamableManager

- 자료구조
    - TArray
	    - TMap
    
- Game Class
    - GameMode
	- GameSession
    
- UInterface