# Git Merge Strategy

- 빗 버킷에서 머지 버튼을 클릭할 경우 나오는 모달에는 아래와 같이 세 가지의 Merge strategy 옵션이 있습니다. 셀장님께서 처음에 설정하신 방식을 그냥 사용하고 있었습니다. (Sync now는 3 way merge 방식의 머지를 사용하고, develop으로의 머지는 Fast forward merge 방식을 사용하는 방식.) 일하고 있는데 갑자기 이것에 대한 궁금증이 들어서 좀 조사를 해보았습니다.

<br />

<img src="https://github.com/muilyang12/what_i_studied/assets/78548830/e8c8dd6d-674e-41a9-9bda-0dad98275e71" width=750 />

<br />

---

<br />

- Fast forward merge 방식
  - 두 브랜치 중 한 브랜치는 Base에 위치해 있어야 머지를 진행할 수 있습니다. (Base: master 브랜치와 머지하려는 브랜치의 마지막 공통 커밋, 아래 예시 그림에서는 master 브랜치가 Base에 위치해 있습니다.)
  - 아래 그림처럼 master 브랜치와 dev1 브랜치의 커밋들이 동일 선상에 위치하고 있을 때 두 브랜치는 Fast forward 상태에 있다고 합니다.
  - Fast forward 상태의 두 브랜치에서 git merge 명령을 입력한 경우, 뒤에 있는 브랜치 (여기서는 master 브랜치) 의 참조 개체가 앞의 브랜치를 가리키도록 참조가 이동하게 됩니다. 브랜치가 가리키는 개체가 빨리 감기 (Fast forward) 하듯이 이동하는 모습을 보고 Fast forward 병합 방식이라고 부릅니다.
  - 이러한 과정을 거쳐 머지되기 때문에 머지하더라도 새로운 머지 커밋이 만들어지지 않습니다.
  - 위에서 말했듯이 두 브랜치 중 한 브랜치는 Base에 위치해 있어야 합니다. 이러한 이유로 우리의 빗버킷에서 Fast forward 머지 시 Sync now를 통해 한쪽으로의 pull (merge) 가 이루어져야 하는 것입니다.
  - 빗버킷의 경우 깃 명령어로 git merge --ff-only 를 사용합니다.

<img src="https://github.com/muilyang12/what_i_studied/assets/78548830/7d55ef70-e1f6-46a6-a4ab-6f26c1720b38" width=750 />
 
<br />
<br />

<img src="https://github.com/muilyang12/what_i_studied/assets/78548830/8dd064c2-b7c4-47f6-a03c-54fe0e8bbf0c" width=750 />
 
<br />
<br />
<br />

- 3 way merge 방식
  - Fast forward merge 방식과 다르게 두 브랜치 모두 Base에 위치하지 않아도 머지를 진행할 수 있습니다.
  - 위의 방식과 다르게 새로운 머지 커밋이 생성되며 머지가 진행됩니다.
  - 머지된 이후 dev1에서 만든 커밋들의 경우 master 브랜치의 커밋 이력에 나타나지 않습니다. 실제로 우리가 빗버킷에서 Sync now를 눌렀을 때 ‘merge ---’ 커밋 하나만 우리의 브랜치에 남고 상대 브랜치의 모든 커밋이 추가되지는 않습니다.
  - 빗버킷의 경우 깃 명령어로 git merge --no-ff 를 사용합니다.

<img src="https://github.com/muilyang12/what_i_studied/assets/78548830/b9b46172-6329-4041-a44f-cba56df14263" width=750 />

<br />
<br />

<img src="https://github.com/muilyang12/what_i_studied/assets/78548830/bd0e800d-a4cb-4dc6-9c1e-7e50dbb58a83" width=750 />

<br />
<br />
<br />

- Squash 방식
  - 3 way merge의 방식과 유사한데, 차이점은 머지 커밋도 우리의 브랜치에 남지 않는다는 점이 있습니다.
  - 즉, 머지된 브랜치에 포함된 커밋 이력 뿐만 아니라 ‘merge ---’ 커밋도 우리의 브랜치에 남지 않습니다.
  - 그렇다고 해서 머지된 브랜치가 삭제되는 것은 아니고
  - 빗버킷의 경우 깃 명령어로 git merge --squash 를 사용합니다.

<img src="https://github.com/muilyang12/what_i_studied/assets/78548830/5c2ca5b9-67e3-4daf-9255-bbd5790f5af6" width=750 />

<br />
<br />
<br />

- 참고로, git merge --ff 명령어: 두 브랜치가 Fast forward 관계에 있으면 커밋 생성 없이 Fast forward merge를 수행하고 아닐 경우 3 way merge를 수행. (디폴트 머지)

<br />

- 출처
  - [merge의 종류 : fast-forward, 3-way merge](https://wikidocs.net/153693)
  - [merge 옵션 : --ff, --no-ff, --squash](https://wikidocs.net/153871)
