- 선형 자료구조
    - 정의
        - 배치하는 구조가 연속적인 공간 
    - Array
    - ![](https://blog.kakaocdn.net/dn/GhhRl/btsuIBJgE2Z/njfOJqRpBoJsrXfSCOzzi1/img.png)  
        - 정의
            - 연속적인 저장 공간을 가지는 구조
            - 배열의 주소는 항상 일정한 크기대로 연속적으로 배치되어 있다
        - 일반적인 배열
            - int arr[9];
            - 이터레이터를 사용 불가능하다
        - STL 배열
            - array<int> a(5);
            - 이터레이터를 사용 가능하다
            - 회사에서 더 많이 사용한다
        - 언리얼 배열
            - TArray<int> a;
            - STL 배열 + vector, 두가지 기능을 합친거라고 보면 된다
            - 반드시 메뉴얼 정리(TMap,TSet도 같이 정리)
                - Set
                    - 역할
                        - key값을 중복없이 정리한다
                        - 데이터를 key로 사용하면 시간복잡도는 logN(균형이진트리)여서 데이터를 key로 다룰 때 사용
                -  힙
                    - 정의
                        - 완전 이진트리구조에, 오름차순기준 부모는 자식보다 값이 작아야한다
    - Linked List
        - 시간복잡도
            - O(N)
            - 우선순위를 따지는 경우에는 비효율적이다
        -  단일 연결 리스트
        - ![[img.png]]
            -  정의
                - 헤더에서부터 Tail로 흘러가는 구조
            - 사용이유
                - 포폴에서 나 작업에서 적극적으로 나갔다 들어왔다하는 것들(삽입 삭제가 활발한 애들)은 List를 사용해서 만들어준다
                - 하지만 건물처럼 잘 파괴되지 않는 것들이나 삽입삭제가 빈번하지 않는 것들은 vector를 사용한다
            
            - 환영 연결 리스트
            -  ![](https://blog.kakaocdn.net/dn/MBhJN/btsuJbwXoU1/xR1EGyoKp34rzCafh3UusK/img.png)
                - 정의
                    - 리스트의 확장형으로 tail의 nextNode가 Header를 가르킨다
            - 이중 연결 리스트
            - ![](https://blog.kakaocdn.net/dn/JopBu/btsuekbYZE3/LIr5UttyqjsOFk5BZY1va0/img.png)
                - 특징
                    - 앞뒤로 왔다 갔다 할 수 있다
                    - 잘 사용하지 않는다, 그 이유는 
                - 사용하는 곳
                    - UI에서 List로 깔때 등 사용한다
                - 면접 포인트
                    - 삽입/삭제를 코드로 묻는  질문이 가끔씩 나온다
                    - 삽입 
                    - ```
                        void Insert(Node * current, Node * node)
                        {
                        	node->NextNode = current->NextNode;
                        	node->PrevNode = current;
                        	current->NextNode = node;
                        }
                        ```
                - 삭제
                    ```
                    void Remove(Node ** head, Node * remove)
                    {
                    	if (*head == remove)
                    	{
                    		*head = remove->NextNode;
                    
                    		if (*head != NULL)
                    			(*head)->PrevNode = NULL;
                    
                    		remove->PrevNode = NULL;
                    		remove->NextNode = NULL;
                    	}
                    	else
                    	{
                    		Node* current = remove;
                    
                    		remove->PrevNode->NextNode = current->NextNode;
                    		if (remove->NextNode != NULL)
                    			remove->NextNode->PrevNode = current->PrevNode;
                    
                    		remove->PrevNode = NULL;
                    		remove->NextNode = NULL;
                    	}
                    }
                    ```
    - Stack(스택)
        - 정의
            - 나중에 들어온 데이터가 가장 먼저 삭제되는 후입선출 방식으로 데이터를 저장한다
        - 사용이유
            - 데이터를 뒤집기 위해서 사용한다
            - 네비게이션 시스템에 사용자한태 도착 지점으로부터 현 지점까지를 보여줄 때 사용한다
            - 재귀함수, 깊이우선 탐색, 백트레킹
        - 함수의 스택 프레임
            - 호출하고 차례로 쌓아둔 데이터를 역순으로 제거해 가려고 스택으로 만들어 놓은것이다
        - Top of Pointer
        - ![](https://blog.kakaocdn.net/dn/bWAuo3/btsuCHXRmPD/MXFKG1nCGNx7jafMAZ7pKK/img.png)
            
            - top(시작점)은 무조건 -1에서 시작한다
            - 데이터를 넣을 때 top를 증가하고 넣는다 그 이유는 top의 시작 값이 -1인것도 있지만 스택의 크기가 꽉 찾는지를 확인하기 위해서도 있다 즉 스택 오버플러우를 방지하는 것이다
            - 지울 때는 지우고 top를 감소한다 이때 top이 -1인 지우로 내리게 된다면 스택 언더플로우가 발생한다
    - 큐
        
        - 정의
            - 데이터가 들어온 순서대로 나간다
        - 명령 큐
            
            ![](https://blog.kakaocdn.net/dn/cjCGWZ/btsuGBC2VDo/IVZZ5jvv83Pd6RljZU9Fok/img.png)
            
            - 최 상단에 명령을 내리는 큐가 있고 각각의 명령을 수행할 큐들이 쓰레드 단위로 존재한다
            - 명령 큐는 내부 메시지 뿐만 아니라 외부 메시지도 받아올 수 있다
            - 예를들어 캐릭터의 움직임을 입력받아 명령 큐에서 A라는 쓰레드에 명령을 보내 수행할 수도 있고, B라는 애가 A를 공격하라는 명령을 명령큐에 보내 그 명령을 다시 A로 보내서 데미지를 입히는 등의 명령을 내릴 수 있다
        - 순환 큐
            
            ![](https://blog.kakaocdn.net/dn/cXSn4n/btsuh3Hk2ED/wuh5TTb8919wf0Okv0gKEK/img.png)
            
            - 정의
                - 데이터가 몇개가 들어오던 계속해서 순환해 가면서 사용하기 위해 사용한다
            - 핵심  
                - 큐에서 front와 rear이 꽉차있는지 비어있는지를 판단하기위해 하나를 비워놓는다!(rear를 +1로 시작)
            - 구현은 주로 배열이나 LinkedList로 한다
        
        - LinkedQueue
            - 배열로 만든 큐는 크기가 고정되어 있고 할당 삭제가 빈번하지 않지만 list로 만든 큐는 할당 삭제가 빈번히 일어나 메모리 단편화가 일어나 잘 사용하지 않는다
        - 우선순위 큐
            - 리스트가 아닌 힙을 사용한다
            - 리스트는 시간복잡도가 O(N)이므로 비효율적이다
            - 따라서 우선순위가 계속 바뀌어야 할 때 사용하는 것이 우선순위 큐이다
            - 게임에서 랭킹같이 값이 들어오면서 우선순위가 바뀌어야 하는경우, 명령 큐에서 많이 사용한다
- 비선형 자료구조
    - 트리
        - 사용하는 곳
            - 계층구조를 표현할 때 사용한다
            - 경로를 표현할 때도 사용한다(주로 그래프로 하긴함)
            - 본 구조 등
        -  일반트리
            - 노드의 갯수 제한이 없다
            - BehaviorTree, 본 구조 등 에서 사용
            - 집합으로도 표현이 가능하다
                - 이를 통해 유니온 집합을 이용하면 합집합을 구할 수 있다
            - ![](https://blog.kakaocdn.net/dn/ckbvRC/btsuJgUiVfa/Pp2p4e5ujDfp5LGYksz340/img.png)
                - Depth(깊이)
                    - root에서부터 0,1,2,...n 으로 수를 센다
                - 레벨
                    - 깊이에 1을 더해 1,2,3,4...n+1 로 수를 센다
                - 차수
                    - 자식의 갯수로 자식의 자식까지는 수를 세지 않는다
            - 구조
                - 트리구조의 최상위 노드는 root node
                - 트리의 중간에 위치한 자식이 있는 노드는 **branch node**
                - 맨 아래에 자식이 없는 노드는 **leaf node**
            - 노드 구성
            - ![](https://blog.kakaocdn.net/dn/WB3FC/btsuJbS0NJu/rAIIEtebUQDVWjoweiQlP0/img.png)
                - (왼쪽 그림)데이터 안에 자식 노드의 주소들을 기록한뒤 같은 구조로 트리를 만들어간다
                - (오른쪽 그림)데이터 안에 Left, Right를 넣고 Left에는 자식노드, Right에는 형제노드를 기록하는 방식을 더 많이 사용한다
                - 마지막 그림처럼 구조체에 헤더를 하나 두고 형제를 배열로 묶어 키값으로 움직이게 하는 방법도 있다
                - 실제로는 두번째 세번째 방식을 많이 사용함
        - n진트리
            - 이진트리
                
                - 정의 
                    - 자식 노드가 2개 이하로 존재하는 트리구조
                - 종류
                    - 완전 이진트리
                    - ![](https://blog.kakaocdn.net/dn/YNyBB/btsuRFZ0tf5/dRtdya7e6LqrVfiPxHLkY0/img.png)
                        - 정의
                            - 위에서부터 아래로 체워지면서 좌에서 우로 체워지는 이진트리
                        - 포화 이진트리와의 차이점
                            - 포화 이진트리의 leaf들을 오른쪽에서 부터 제거하여 얻어진 트리
                    - 포화 이진트리
                    - ![](https://blog.kakaocdn.net/dn/mJHs1/btsuJbyHAGV/OUHeHppyqO6eh0y2vA4Dz1/img.png)
                        - 정의
                            - 이진트리의 노드들이 꽉 차있는 이진트리
                        - 완전 이진트리와 차이점
                            - 모든 leaf의 레벨이 동일한 이진트리
                            - leaf가 아닌 내부 노드들은 모두 2개의 자식을 갖는 트리
                    - 균형 이진트리
                    - ![](https://blog.kakaocdn.net/dn/mJHs1/btsuJbyHAGV/OUHeHppyqO6eh0y2vA4Dz1/img.png)
                        - 정의
                            - 완전과 포화를 가지고 양쪽에 균형을 맞춰주는 이진트리로 최악의 검색속도 N을 방지하기 위해 사용한다
                        - 종류
                            - AVL
                                - 좌우에 레벨 차를 최대 1까지만 허용해주는 트리
                                - 삽입삭제가 빠른대신 Red-Black트리보다 검색속도가 느리다
                            - Red-Black
                                - 균형을 유지하기 위한 규칙이 많고 복잡하다(6가지 정도)
                                - 탐색속도는 AVL보다 빠르다
                            - Map(set,pair)
                                - set이 균형 이진 트리로 이뤄진다
                                - set으로 키를 관리
                                - pair로 데이터를 관리
                    - 이진 탐색 트리
                        
                        - 정의
                            - 반드시 정렬이 되어있는 이진트리
                            - 이진 탐색을 트리형태로 만든것이다
                                - 배열은 삽입 삭제가 느려 더 빠르게 하기위해 트리로 만든것이다
                        
                        ![](https://blog.kakaocdn.net/dn/bNArKi/btsuPM6os54/NSU1AWwHPLWAknhHvhvx31/img.png)
                        - 규칙
                            - 반드시 왼쪽 자식노드는 부모보다 작아야하고 오른쪽 자식노드는 부모보다 커야한다
                        - 노드 찾기
                            - 부모보다 작으면 왼쪽, 부모보다 크면 오른쪽으로 내려가면서 값을 찾는다
                        - 삽입
                            - 부모의 아래에 자식과 값을 비교하여 작으면 왼쪽 크면 오른쪽으로 이동하면서 마지막 노드까지 내려가 비교하고 그 자식으로 값을 넣는다
                            - 비효율적으로 비는 공간이 많아진다
                        - 삭제
                        - ![](https://blog.kakaocdn.net/dn/bs6Ell/btsuWZ4Uwgj/JShWYKtvjKtzgSKbMGDnnk/img.png)
                            - 값을 찾아 삭제를 하고자하는 노드의 자식이 있는지 없는지, 있다면 하나만 있는지 두개가 있는지에 따라서 달라진다
                            - 자식이 없을 때는 그냥 삭제를 해주면 된다
                                - ex) 67를 제거한다면 그냥 지워주기만 하면 된다
                            - 자식이 하나만 있는 경우는 노드를 삭제하고 자식을 그 위치로 올려주면 된다
                                - ex) 139를 제거한다면 139 위치에 67로 대체
                            - 자식이 양쪽에 있는 경우는 노드의 왼쪽 자식들중 가장 큰 값이나 오른쪽의 자식들중 가장 작은 값으로 대체해주면 된다(보통은 후자를 많이 사용함)
                                - ex)11제거시 오른쪽 자식중 가장 작은 13으로 대체
                        - 특징 
                            - 검색속도는 항상 logN이지만 삽입 삭제는 달라질 수 있다
                            - 최악의 경우 N이 나온다
                        - 탐색(순회)방법
                        - ![](https://blog.kakaocdn.net/dn/U4PEs/btsuZRMjxe0/GysKH7gr3aNNmxhnJjEWe0/img.png)
                            - 전위
                                - Root->Left->Right 순으로 순회한다
                                - 위에서부터 아래고 값을 누적할 때 사용한다
                                - 본 구조 등등
                            - 중위
                                - Left->Root->Right 순으로 순회한다
                                - 수식트리, 값에의한 판 등등에 사용한다
                                - 값을 밑에서부터 누적할 때도 사용한다(잘 사용하지 않음)
                            - 후위
                                - Left->Right->Root 순으로 순회한다
                                - 모든 노드를 제거할 때 사용한다(밑에서부터 제거를 해야하기 때문에)
                    - AVL 트리
                    - ![](https://blog.kakaocdn.net/dn/sctw6/btsx2xLJHLm/lqkVaKvelkRRx7aGCjqbPk/img.png)
                        - 정의 좌우 서브트리의 높이차이가 1 이하인 이진탐색 트리
                
            - 쿼드트리(Quad Tree)
                - 정의
                    - 자식 노드가 4개 이하로 존재하는 트리구조
                - 사용
                - ![](https://blog.kakaocdn.net/dn/kA6R5/btsuWZcMB87/QhKrIYbeFYF03DjtfBhip1/img.png)
                    - 쿼드트리 컬링(Quad Tree Frustum Culling)
                    - 맵 등등에서 프로그래머가 원하는 만큼 4분활로 계속 나누어 트리를 만든 뒤 카메라(삼각형)가 비추는 구역을 판단해 그 부분만을 트리에서 찾아 그려주는 방법(현제도 많이 사용함)
                    - 충돌판단
                        - 캐릭터의 충돌 영역을 판단할 때 트리에서 충돌 영역에 들어오지 않은 부분들을 충돌체크를 하지 않는 방법(지면이 블럭단위(타일맵)에서 많이 사용함-요즘엔 많이 사용 안함)
                    - 등등이 있다
        - AVL 트리
            - 정의 
                - 좌우 서브트리의 높이 차이가 1 이하인 이진탐색 트리
    - 힙  
        ![](https://blog.kakaocdn.net/dn/dIwzgQ/btsu9Uvkw2u/kkJDtpEM2ssTmg0vD1hlN0/img.png)
        - 정의
            - 메모리 구조의 힙과는 다르다
            - 힙 순서 속성을 만족하는 완전 이진트리
            - 힙 순서 속성은 오름차순 기준 부모노드는 자식보다 반드시 작아야한다는 것이다
        - 특징
            - 힙을 계속해서 빼내면 정렬이 가능하다
            - 삽입삭제의 연산이 O(logN)으로 빠르다
        - 단점
            - 배열로 구연하면 가변크기를 구현하기 힘들어 level별로 List구현하는 방법도 있다
        - 삽입
        - ![](https://blog.kakaocdn.net/dn/o5Pxl/btsuTNRYd9d/qpisFYclNkriZXSl2xQP0k/img.png)
            - 마지막 노드의 다음 노드에 삽입할 값을 넣고 부모 노드와 경쟁하여 더 작은 값이 위로 올라가도록 한다
            - 그림으로 예를 들면 7을 삽입한다 했을 때 88 옆에 7을 넣고, 부모인 37과 경쟁해서 더 작은 7이 부모로 들어가고 37은 자식으로 내려온다
            - 이 과정을 힙의 속성에 만족할 때 가지 하면 된다
            - 값을 노드의 맨 마지막 노드의 다음에 넣는 이유는 완전 이진트리를 유지하면서 힙속성도 만족해야 하기 때문이다
        - 삭제
        - ![](https://blog.kakaocdn.net/dn/bgAbLh/btsu0szGUgW/Imzf0YMmeGZat7yEokbQc1/img.png)
            - 힙의 중간 노드를 삭제하는 것은 존재하지 않는다
            - 힙의 삭제는 Root를 삭제한다는 의미이다
            - 삽입과 루트를 삭제한 후 맨 마지막 노드의 값을 루트에 넣고, 자식과 경쟁하여 힙의 속성에 만족할 때 가지 경쟁한다
            - 그림으로 예를 들면 Root에 있는 2를 빼고 맨 마지막 노드의 37을 Root에 넣은 뒤, 자식들과 경쟁하여 더 작은 자식과 교체한다
            - 이 과정을 힙 속성에 만족할 때 까지 반복한다
            - 루트를 삭제하고 맨 마지막 노드를 루트에 넣고 경쟁하는 이유는 완전 이진트리를 유지하면서 힙속성도 만족해야 하기 때문이다
        - 실제 구현
            - ![](https://blog.kakaocdn.net/dn/Xat7G/btsvdrsus1a/R7DuddWwggxLKRJmTZAyIK/img.png)
            - 배열을 사용하여 구현을 많이 한다
            - 부모의 왼쪽 자식: index*2 +1
            - 부모의 오른쪽 자식: index*2+2
            - 자식에서 부모를 구할 때: (index -1) /2
        - 종류
            - 최대힙/최소힙
            - 우선순위  큐
                - 우선순위를 따질 때 리스트의 시간 복잡도가 O(N)이므로 비효율적이여서 힙으로 만든 큐이다
                - 게임에서 랭킹을 비교하여 교체해 주거나, 명령 큐에서 먼저 들어온 입력보다 먼저 처리해야 될 것이 생겼을 때 많이 사용한다
- 그래프
    - 정의
        - 정점의 집합 V(vertex)와 두 정점을 잇는 선분인 간선(Edge)의 집합 E로 이뤄진 자료구조 
        - 경로를 탐색하기 위한 개념
        - 게임에선 잘 사용하지 않는다
        - 트리와 달리 시작지점이 없어 임의의 점을 하나 주고 시작을 한다
    - 방향 
        - 방항성
            - 한 방향으로 흘러가는 방향을 가진 그래프
        - 무방향성
            - 방향을 가지지 않는 그래프
        - 표현
            - 무 방향성 그래프 인접 행렬
                - 노드의 갯수가 정해져있거나 노드의 갯수가 적을때 사용한 
                - 탐색속도가 빠르다
                - 무방향성 그래프
                - ![](https://blog.kakaocdn.net/dn/yYsJ9/btsvdvaEdpz/uzX85yKS9jgUkY5wCmw8EK/img.png)
                    - 자기 자신은 가지 못하므로 0이다
                    - 자기 근처에 갈 수 있는 길은 1로 표기해준다
                    - 대칭성을 갖는다
            -  방향성 그래프 인접 행렬
                - ![](https://blog.kakaocdn.net/dn/FDnWJ/btsuSj4OhBP/ZKpadm7AdJbmbHh96bHnMk/img.png)
                    -  무방향성 그래프와 다르게 가능 방향으로 화살표가 있으며 가중치가 있다
                    - 행렬에 가중치를 표기해주면된다
                    - 무방향성 그래프와 달리 대칭성을 갖지 않는다
            - 인접 List
            - ![](https://blog.kakaocdn.net/dn/beDWDa/btsuZRNh912/xDJRQ2msB0OfshIJbkztXk/img.png)
                - 노드의 갯수가 가변이거나 노드의 갯수가 많을 때 사용한다
                - 위의 간선 노드들을 살수있는 애들을 모두 리스트로 순서대로 연결한 것이다
    - 탐색
        - 깊이우선(DFS)
            - ![](https://blog.kakaocdn.net/dn/ZKL58/btsx17k28Ne/bzjuBBrx1THKzaMkgGAap0/img.png)
            - 특징
                - 시작지점을 잡고 인접한 노드중 갈수 있는 방향으로 하나씩 끝까지 탐색하는 알고리즘
                - 깊이의 끝까지 가서 탐색을 하는것이다
                - stack으로 이루어져 있어 재귀로 구현이 가능하다
            - 구현
                - 하나의 노드를 택한다
                - 노드를 방문하여 필요한 작업을 한 후 연결된 다음 노드를 찾는다
                - 현재 방문 노드는  스택에 저장하고 위의 단계를 반복한다
                - 더이상 방문할 노드가 없으면 스택에서 노드를 빼난 후 다음 노드를 찾아 두번째 단계부터 반복한다
        - 너비우선(BFS)
            - ![](https://blog.kakaocdn.net/dn/CBTq1/btsxrivAh49/7h6cW4Nbs7bZwe8472Z6A1/img.png)
            - 특징
                - 같은 level을 전부 방문해서 탐색을 하는것이다 
                - queue로 이루어져있어 순서대로 값을 꺼낼 수 있다
            - 구현
                - 하나의 노드를 택한다
                - 노드를 방분하여 필요한 작업을 한 다음 연결된 다음 노드를 찾는다
                - 노드들을 큐에 저장한다
                - 더이상 방문할 곳이 없으면 큐의 맨 앞의 노드를 빼내 두번째 단계부터 작업을 반복한다
    - 위상정렬(DAG)
        - 정의
            - 하나의 정점이 다른 정점과의 관계속에서 가지는 위치
            - DAG(Directed Acyclic Graph) 즉 한방향으로 흘러가는 그래프에서만 가능하다
            - 비선형 구조를 선형 구조로 변경하는 것이다
        - List로 구현이 가능하다
        - 구현
        - ![](https://blog.kakaocdn.net/dn/bY0DtV/btsxrVG8oaC/agWvxJw4ql9ptDt24xFbE1/img.png)![](https://blog.kakaocdn.net/dn/zpdyF/btsxLldt3eP/7gCBtm9Z4ESZBvONJk0mt1/img.png)![](https://blog.kakaocdn.net/dn/bdfiqn/btsxsQS57UR/zY56NUai1KAh7Pk7avf9Mk/img.png)
            - 원하는 노드를 먼저 시작지점으로 놓고, 시작 노드를 삭제한 후 그 노드의 진출 간선을 삭제한다
            - 진입간선이 없는 노드를 삭제해주고, 그 노드의 진출간선을 삭제한다
            - 이 과정을 노드가 없을 때 까지 반복해준다
    - MST(minimum spanning tree)(최소 신장(비용) 트리)
        - 간선에 대한 비용을 반드시 가지고 있어야한다 
        - 종류
            - Prim
            - ![](https://blog.kakaocdn.net/dn/D0sZj/btsxLmjeHEZ/y3J9l91D71KH3Bp2kzQKtK/img.png)
                - 구현
                    - 시작 노드를 트리에 루트로 만든다
                    - 노드에 연결된 가장 최소값을 다음 레벨의 노드로 연결해준다
                    - 루트에서 연결된 노드에서 연결된 노드중 가장 작은 비용을 가진 값과 루트에 연결된 노드들의 비용을 비교하여 작은값을 트리로 연결해준다
                    - 루트에 연결된 노드가 이제 없으므로 밑에있는 자식 노드들에서 간선의 비용이 작은 애들을 트리로 연결해준다
                - 구현 단점
                    - 트리쪽 구조를 배열, 링크드 리스트, 트리등을 사용해 구현해야한다
                    - 조사대상이 추가될수록 비용이 늘어난다
                    - 최악의 경우 O(n^2)이 나온다 
                - 해결방안
                    - 정점이 추가될 때 마다 간선을 정리한다(합리적이지 않음)
                        - 예를들어 B로 탐색이 끝났는데 A정점으로 탐색을 한다고 하면 A-B의 간선을 삭제하고 비교한다
                    - 우선순위큐를 사용한다
                - 알고리즘을 이용해 원하는 지점에서 각각의 지점까지의 최소 경로를 파악할 수 있다
        -  Kruskal
            - 합집합
            
            - ![](https://blog.kakaocdn.net/dn/xCmL8/btsxLj07nnm/q8Uqg6xgy21XOE18M5KCtK/img.png)
                - 특징
                    - 두 그룹을 합치기 위해서 사용한다
                    - 합집합은 부모를 탐색할 수 있지만 자식을 탐색할 순 없다
            
            - 구현
            
            - ![](https://blog.kakaocdn.net/dn/IpiJz/btsx2sXTaiL/lbttuDuyb3KZpfkNJC4lO0/img.png)
                
                - 모든 간선을 오름차순으로 정렬을 한다
                - 그 목록을 하나씩 트리에 넣는다
                - 트리는 사이클이 형성되면 안되므로 합집합을 통해 사이클이 형성되지 않게 해준다
                
                ![](https://blog.kakaocdn.net/dn/chlKt1/btsx5ZOnndW/jROAJj1CjDTL6qEpri0fy1/img.png)
                - 예를들어 그림처럼 집합이 연결되어 있는데 C-D간선이 연결되려할 때 ABCD가 연결된 합집합에 D가 이미 존재하므로 C-D간선은 연결하지 않는다
            
        - Sollyn(Borubuka)
            - 특징  
                - Forest라는 개념을 사용한다(집합과 비슷함)
                - 노드를 하나씩 비교하므로 분할정복 특징이 있어 병렬연산이 가능하다
                - 병렬연산을 하지 않으면 보르부카, 스레드에 넣고 병렬 연산을 하면 솔린 알고리즘이라 부른다
            - 구현
                - ![](https://blog.kakaocdn.net/dn/BS3pO/btsycutwpp8/21CkZBTTeRv2o3xzcUr4A0/img.png)
                    - 각각의 노드를 forest라 하며 각 노드에 연결된 최소값만을 찾고 중복은 허용하여 새로 forest를 만들어준다
                - ![](https://blog.kakaocdn.net/dn/ek9QpX/btsx1UtDgaO/btKxrfe0Sl47qLkn4vcPqk/img.png)
                    - 새로 만들어진 forest들끼리 간선을 비교하여 작은 간선을 이어 새로운 forest를 만들어준다
    - 길찾기-최단거리 알고리즘
        - 정점(노드)과 간선으로 이뤄진 그래프에서 두 정점 사이의 가장 짧은 경로 탐색
        - 최단 경로 문제는 한 꼭지점에서 다른 꼭지점으로 간선을 통해 갈 수 있는 모든 경로중 최소비용이 발생하는 경로를 찾는것
        - 최소 비용은 가중치가 있는 그래프(가중 그래프)에서 꼭지점과 꼭지점간의 가중치 값을 합한 최소 값을 의미하며 가중치는 문제에 따라 비용, 시간, 거리
        - 종류 
            - BFS
                - 가중치가 없거나 모두 동일한 상황 가장 빠름
            - 다익스트라
                
                - 양의 가중치, 단일 쌍, 단일 출발, 단일 도착
                - 최단거리 찾아가지만 전 노드를 다 봐야한다는 단점이 있다
                
                ![](https://blog.kakaocdn.net/dn/djpcnk/btsx17GI3au/upFAbJ2vwdr0WqUdIi2kek/img.png)
                - 유향그래프 = 방향성 그래프
            - 벨만포드
                
                - 음의 가중치, 단일 쌍, 단일 출발, 단일 도착
                
                ![](https://blog.kakaocdn.net/dn/k8sGo/btsyepeaWag/17vFznCQ669OpRvSeI8yuk/img.png)
            - 플로이드 워셜
                - 전체 쌍, 다수 출발, 다수 도착
                - 동적 계획법 기반 고차원 기법(메모이제이션
            - A*알고리즘
                - 휴리스틱(가야 할 거리와 남은 거리), 하나의 정점에서 다른 하나의 정점까지의 최단거리
                - 다익스트라의 단점을 보완하기 위해 휴리스틱을 도입
            - 네비게이션 메시
- 해싱
    - 해싱 테이블
        - 충돌처리
            - 체이닝
            - 개방 주소
        - 사용이유
        - 어느 부분에서 사용할지
        - Unordered-Map
- 정렬
    - O(n^2)
        - 버블
        - 삽입
        - 선택
    - O(nlogn)
        - 퀵
            - O(n^2)의 상황
        - 병합
    - 기타
        - 버킷
- 알고리즘 
    - 분할정복
    - 동적계획
        - 메모이제이션
            - 이전에 연산되어왔던 값
    - 탐욕
        - 최적 상황
    - 백트레킹
- 알고리즘 복잡도
- ![](https://blog.kakaocdn.net/dn/ci4ckF/btsx2wMOpQF/uPPnrPKp4L2bUuBCdlPBSk/img.png)
    - 시간 복잡도
        - 프로그램의 컴파일 시간과 실행 시간의 합
    - 공간 복잡도(거의 따지지 않음)
        - 수행에 필요한 메모리 양
        - 필요한 고정 공간과 가변 공간의 합