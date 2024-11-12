- Constant Buffer
	- 정의
		- Shader에 일정한 데이터를 효율적으로 전달하기 위해 사용하는 메모리 버퍼
		- Shader의 일정 기간동안 변하지 않는 데이터를 저장하는데 사용한다
		- 보통 조명 정보, 변환 행렬, 카메라 정보, Vector등 각 프레임마다 변하지 않거나 한번 업데이트 되면 되는 정보가 이에 해당된다

- Vertex/Index Buffer는 보통 한 번 설정하면 바뀌지 않고 유지되는 경우기 일반적이다
	- 이유
		- 보통 Vertex/Index Buffer로 만든 애들은 특정 사물의 모양을 가지고 있다
		- 이때 이 놈의 위치, 회전 등등을 변경하면 그 모양은 변하지 않고 변경하려는 값만 바뀐다
		- 그래서 Buffer는 처음 설정하면 잘 바뀌지 않고 유지되는게 일반적이다

- Constant Buffer 만들기![[Pasted image 20241107233028.png]]
	- Constant Buffer는 Vertex/Index Buffer와 달리 D3D11_BUFFER_DESC의 Usage를 GPU에서 읽기만 가능한 것이 아닌 CPU에서 쓰는 것 까지 사용할 수 있도록 한다
	- 이때 ByteWidth의 크기를 TransformData의 크기만큼 잡아주는데, TransformData는 Vector4로 만들어 위치, 회전, 스케일을 가지고있는 4X4 행렬이 될 수 있도록 만든다
	- 이때 desc에서 CPUAccessFlags를 CPU에서 읽기만 가능하도록 Flags를 지정해준다
	- device로 Buffer를 만들어 ConstantBuffer를 만들어 저장해 주면 ConstantBuffer를 만드는데 성공한 것이다
	- Init 함수에서 CreateConstantBuffer를 호출하여 프로그램 시작시 생성할 수 있게 한다

- Shader
	- ![[Pasted image 20241107233755.png]]
		- cbuffer를 통해 Constant Buffer를 만들어 주고 register에 할당해 주는데 상수 버퍼 슬롯은 b로 시작한다
		- TransformData는 Vector4로 float 4개로 되어있는 값을 가져오므로 float4 로 변수를 만들어 데이터를 받아올 수 있게한다
	- ![[Pasted image 20241107234206.png]]
		- Constant Buffer는 렌더링 파이프라인에서 VS에 적용된다
		- 예제에선 화면에 띄운 Texture를 이동시킬 것이므로 position에 offset을 더해줄 것이다

- Update
	- Constant Buffer는 위치, 회전, 크기 등을 변경하는 값을 가진 Buffer이므로 이는 변할때 마다 Update가 되야하므로 Update함수에서 Constant Buffer를 업데이트 해준다
	- ![[Pasted image 20241107234711.png]]
		- Map
			- ConstantBuffer는 GPU에 있는 값이기 때문에 CPU가 GPU에 접근하여 값을 변경해줘야 한다
			- 이때 이를 할 수 있는 함수인 Map 함수를 사용한다
			- D3D11_MAP_WRITE_DISCARD는 기존 데이터를 삭제하고 새로운 데이터를 덮어쓰기 위한 플래그이다
			- GPU 메모리에 CPU가 접근 가능하도록 맵핑된 포인터로 sub에 제공된다
		- memcpy
			- memcpy를 통해 맵핑된 sub 포인터 데이터에 transformData 안에 값과 크기를 복사해 준다
		- Unmap
			- Unmap은 Map 사용후 반드시 호출해야되는 함수이다
			- CPU 접근을 해제하고 GPU가 해당 Constant Buffer에 접근할 수 있도록 한다
			- 이를 통해 GPU가 Shader 단계에서 TransformData를 사용할 수 있게 된다

- 결과![[Pasted image 20241107235405.png]]
	- TransformData의 offset의 x,y를 Update할 때마다 변경되므로 오른쪽 위 방향으로 계속해서 이동한다

