# Week6 — 이진 트리 구조 설계 및 순회

## 파일 구성

```text
Week6/
├── README.md                  # 이 설명 파일
├── DS_06완성본.ipynb           # TODO 구현 + 실행 결과 + VisuAlgo 기록 + 복잡도 설명
└── screenshots/
    ├── 01_empty_bst.jpg               # BST 모드, 빈 트리 (N=0)
    ├── 02_insert_4_2_6_1_3_7.jpg      # 4,2,6,1,3,7 삽입 완료 (N=6, h=2)
    ├── 03_traverse_menu.jpg           # Traverse 메뉴: Inorder/Preorder/Postorder만 있음
    ├── 04_preorder_animating.jpg
    ├── 05_preorder_result.jpg         # Visitation sequence: 4,2,1,3,6,7
    ├── 06_inorder_animating.jpg
    ├── 07_inorder_result.jpg          # Visitation sequence: 1,2,3,4,6,7
    ├── 08_postorder_animating.jpg
    ├── 09_postorder_result.jpg        # Visitation sequence: 1,3,2,7,6,4
    └── 10_levelorder_manual_trace.png # 레벨 순회 방문 번호 수동 표기 (VisuAlgo 미지원)
```

## 구현 내용

- `TreeNode`: `data`, `left`, `right`
- `BinaryTree`: 재귀 전위/중위/후위, 반복 전위(오른쪽 자식 먼저 push), deque 기반 레벨 순회, `height`, `count_nodes`, `count_leaves`
- `build_complete_tree(values)`: 큐에서 부모를 꺼내 왼쪽→오른쪽 순서로 채움 (None도 데이터 값으로 취급)
- 규약: 루트 깊이 0, 리프 높이 0, 빈 트리 높이 -1 (간선 수 기준)

## 테스트 결과 (노트북 전체 실행, 모든 assert 통과)

|트리|전위|중위|후위|레벨|
|---|---|---|---|---|
|예시 A~F|A B D E C F|D B E A C F|D E B F C A|A B C D E F|
|numeric (4,2,6,1,3,7)|4 2 1 3 6 7|1 2 3 4 6 7|1 3 2 7 6 4|4 2 6 1 3 7|
|완전 트리 [1..7]|1 2 4 5 3 6 7|4 2 5 1 6 3 7|4 5 2 6 7 3 1|1 2 3 4 5 6 7|

경계 사례: 빈 트리(높이 -1), 단일 노드(높이 0), 오른쪽 편향 트리(높이 2, 리프 1), `[None, 2]` 입력.

## VisuAlgo 검증 요약

- https://visualgo.net/en/bst, **BINARY SEARCH TREE** 모드(AVL 아님)에서 빈 트리에 4, 2, 6, 1, 3, 7 삽입
- 대응: A→4, B→2, C→6, D→1, E→3, F→7 — 예시 트리와 같은 모양, 높이 2
- 지원 순회: Inorder, Preorder, Postorder → 애니메이션 결과가 코드 출력과 일치
- **미지원 순회: Level-order** → 큐 상태 수동 trace(4, 2, 6, 1, 3, 7)로 대체, 코드 출력과 일치

## 복잡도 요약

|연산|시간|보조 공간|
|---|---|---|
|DFS 3종(재귀) / 반복 전위|O(n)|O(h)|
|레벨 순회(BFS)|O(n)|O(w)|
|height / count_nodes / count_leaves|O(n)|O(h)|
|build_complete_tree|O(n)|O(w) 큐 (완전 트리 w ≈ n/2)|

순회 반환 리스트는 별도 O(n). 균형 트리 h = O(log n), 편향 트리 h = n − 1.
자세한 설명은 노트북의 "제출 과제: 시간·공간 복잡도 설명" 셀 참고.
