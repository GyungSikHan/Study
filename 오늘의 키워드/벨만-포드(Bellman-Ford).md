- 정의
    - 한 노드에서 다른 노드까지의 퇴단 거리를 구하는 알고리즘
    - 다익스트라 알고리즘이 모두 가중치가 양수인 경우에만 사용이 가능하다면, 벨만-포드는 가중치가 음수인 경우에도 사용이 가능하다
    - 시간 복잡도가 더 크기 때문에 가중치가 양수일 땐 사용을 지양하는 것이 더 좋다
- 음수 사이클의 문제점
- ![](https://blog.kakaocdn.net/dn/djNAVL/btsvoYYdjux/WxSAzgMcw2ICjrF3N3p5d1/img.png)
    - 단순 음수 간선일 경우
        - 단순 경로이므로 그대로 가중치를 계산하면 된다
    - 사이클이 존재하거냐 양수값이 더 클 경우
        - 사이클을 순환해도 이득이 없으므로 그대로 진행한다
    - 사이클이 존재하고 음수값이 더 클 경우
        - 사이클을 순환할 수록 가중치가 감소해 최소 비용을 찾는 입장에서 사이클이 무한히 순환하고 목적지에 도착해도 실질적인 최단 거리라 보기 힘들다
        - 적어도 동일 노드를 방문하면 안된다는 등 제약조건이 필요하다
    - 최단 거리는 순화되어서는 안된다는 가정하에 경로(Edge) 길이는 |V| -1이 된다
- 동작
    
    1. 시작 노드 설정
    2. 시작 노드에서 각 다른 노드의 거리 값을 무한대로 설정하고 시작 노드를 0으로 설정
    3. 현재 노드의 모든 인접 노드를 탐색하며 기존에 저장된 인접 노드까지의 거리보다 현재 노드를 거치고 인접 노드에 도달하는게 짧을 경우 값을 갱신
    4. 3의 과정을 모든 노드에 대해 수행
    5. 모든 노드에 3-4를 수행하고 또 거리가 갱신된다면  −∞을 발생시키는 음수 사이클이 존재함을 의미한다
    
    ![](https://blog.kakaocdn.net/dn/bJJIOW/btsviTjNH9s/iwENPG1UCgSeU3CByG5x90/img.png)- 시작 노드를 s로 설정하고 시작 노드 s의 거리값을 0으로 설정하고 다른 노드들은 무한대로 설정해준다
    - ![](https://blog.kakaocdn.net/dn/LwkEP/btsvka6D2ei/3AG9h6f17XKXIRcE1u0hnk/img.png)
    - 시작 노드의 인접한 노드 a,c,e에 가중치를 넣어준다(무한대 보다 작기 때문)
    - ![](https://blog.kakaocdn.net/dn/xguTi/btsvjhkJuSg/yR4LqMDiPAxYWZmQ3zUue0/img.png)
    - s의 인접 노드를 모두 탐색했으므로 a노드로 옮겨 인접한 노드의 모든 노드의 가중치를 계산하여 넣어준다
    - ![](https://blog.kakaocdn.net/dn/xguTi/btsvjhkJuSg/yR4LqMDiPAxYWZmQ3zUue0/img.png)
    - a노드의 인접 노드를 모두 탐색했으므로 b노드로 옮겨 위의 과정을 한번더 수행한다
    - 이때 b의 인접 노드가 g뿐이므로 가중치 -1+4가 g에있던 무한대보다 작으므로 g노드 안에 3을 설정해준다
    - ![](https://blog.kakaocdn.net/dn/0uBnl/btsvkUbmBJZ/ubKQBWsKvpZWKkXGw1Av8k/img.png)
    - ![](https://blog.kakaocdn.net/dn/bOaBDa/btsvjhrtFfI/8KBux3FkvmWIQkOJDG50nk/img.png)
    - 도착 지점에 도달했으므로 시작노드 s에 인접한 다음노드인 c로 옮겨 위의 과정을 반복한다
    - d노드에서 g노드로 갈때 가중치가 11+2보다 g에 있는 가중치 3보다 작으므로 변경되지 않는다![](https://blog.kakaocdn.net/dn/bQTcJD/btsvoXZiTw7/9tS02kX33IA6NfNfCt3l2k/img.png) ![](https://blog.kakaocdn.net/dn/qxyrp/btsvkZDPfzf/ne7RkvlOzBkfoDQTpxjEPK/img.png)
    - 역시 시작 노드 s에 인접한 e노드로 옮겨와 위의 과정을 반복해준다
    - 마찬가지로 f노드에서 g노드로 갈때 가중치가 5+1이 g노드에 저장된 3보다 크므로 변하지 않는다
    - g의 인접노드가 없으므로 첫번째 탐색을 종료한다
    - 이후 노드의 갯수가 -1만큼 반목하면 된다
    - 이로써 V-1개의 노드에 대해 모두 탐색이 종료되며 e와 f사이에 음수 사이클이 존재하며 해당 사이클을 무한히 순회하면 모든 노드에 대해 -무한대가 될 수 있다
    - 따라서 위 과정처럼 동일 노드를 방문하지 않는다는 조건이 없으면 그대로 -1등을 출력하여 경로가 존재할 수 없음을 표현해줘야한다
    - 음수 사이클 존재 여부는 V-1번의 탐색을 마쳤으므로 최단 거리 제약 한계에 도달했을 때 이 다음 순회에서도 만약 갱신되는 값이 존재한다면 앞으로도 계속 갱시노딤을 의미하므로 음수 사이클이 존재함을 알 수 있다
    
- 시간 복잡도
    - |V|-1번 만큼 순회하므로 O(V)가 되고 매번 총  edge(O(E))만큼 탐색하므로 O(|V||E|)가 된다
    - 이때  desne graph라면 E는 V^2에 근사해지므로 최악의 경우 O(V^3)이 된다