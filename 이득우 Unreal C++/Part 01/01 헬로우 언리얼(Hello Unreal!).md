- GameInstance
	- 정의: GameInstance 클래스는 여러 레벨이나 게임 모드에서 공유해야 하는 영구 데이터를 관리하는 데 유용한 도구입니다.
	- 기본 GameInstance를 상속받아 우리가 만든 GameInstance를 이용하여 Hello Unreal 을 로그창에 띄울것이다

- UE_LOG()
	- 엔진에서 로그를 남기게 해주는 메크로 함수
	- 첫 번째 인자는 로그의 카테고리가 들어간다
	- 두 번째는 Log, Warring 등이 들어간다
	- 세 번째 인자는 Format으로 printf()와 동일하게 들어가는데 Unreal에선 TEXT("")라는 메크로가 들어가는데 이는 2byte짜리 유니코드를 만들어주어 넣어주면 값이 들어간다![[Pasted image 20240830192559.png]]

- 우리가 만든 GameInstance로 변경하기![[Pasted image 20240830192701.png]]
	- 위의 사진처럼 우리가 만든 GameInstance로 변경해준다
	- 이때 GameInstance는 컨텐츠를 담는 어플리케이션의 뼈대로 생각하면 되는데 이는 싱글톤이라는 단일 인스턴스로  되어있다

- Hello Unreal 확인하기![[Pasted image 20240830193422.png]]
	- 위에서 설명한 GameInstance를 우리가 만든 클래스로 바꾼 뒤 실행을 시키면 OutLog창에 수많은 Log들 때문에 찾기가 힘들다
	- 이때 검색창에 우리가 설정해둔 카테고리로 검색을 하면 잘 나오는것을 확인할 수 있다