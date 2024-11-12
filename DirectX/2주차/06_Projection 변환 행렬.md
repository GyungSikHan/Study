- Projection Space![[Pasted image 20241112140749.png]]
	- Local Space, World Space를 통해 만들어진 View Space에 물체들을 어떠한 비율로 찍힐지 투영시키는 공간이다
	- 즉 View Space를 가지고 투영을 시켜 납작하게 만든 공간이다

- Projection 변환![[Pasted image 20241112141052.png]]
	- Projection 변환은 카메라가 보여주는 공간을 절두체 컬링등등을 통해 화면 좌표에 맞게 변환시키는 것을 의미한다
	- 절두체 컬링을 이용하여 특정 범위안에 들어온 물체들만 화면에 그리게 된다
	- 그릴 위치에 물체가 있다면 카메라의 0,0 지점부터 물체까지 삼각형을 그려, 들어온 빛의 세기 만큼의 위치에 있는 삼각형에 상이 맺힌 물체를 비율을 통해 그리게 된다  ![[Pasted image 20241112141712.png]]