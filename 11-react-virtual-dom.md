# React Virtual DOM

- Virtual DOM은 SPA에 의해 DOM을 다루는 것이 복잡해짐에 따라 보다 효율적인 DOM 렌더링을 위해 등장한 개념입니다. Virtual DOM은 DOM을 복제한 자바스크립트 객체인데, class나 style 등의 attribute만 가지고 DOM API 메서드는 포함하고 있지 않은 조금 더 가벼운 DOM입니다.

<br />

<img src="https://github.com/muilyang12/what_i_studied/assets/78548830/164b1f1d-b89a-485b-a526-e2527895de1f" width=500 />

<br />
<br />

- SPA에서 변화를 만들고 싶을 때 Virtual DOM 트리를 우선적으로 변경합니다. 그 후 변경 전과 변경 후의 Virtual DOM 트리를 비교하여 변화된 부분을 찾아낸 후 변화된 부분에 대해서만 실제 DOM을 업데이트하게 됩니다. 이 경우 약간의 버퍼링, 캐싱이 되기에 이전보다 효율적인 DOM 업데이트가 가능하게 됩니다. (이러한 이유로 아무런 버벅임 없이 DOM을 통제해야하는 상황이면 DOM을 직접 통제해야 합니다.)

<br />

<img src="https://github.com/muilyang12/what_i_studied/assets/78548830/9e20b67e-e712-49d3-a3aa-8a9961fb858b" width=500 />

<br />
<br />

- 이 Virtual DOM이 변화하였는지를 체크하는 데에 key props를 사용하게 됩니다. 그렇기에 key props에 배열의 index 값을 넣을 때 state가 이상한 곳에 들어가는 문제가 발생하기도 하는 것입니다. 또한 css의 애니메이션을 반복적으로 호출하고 싶은 경우 key props에 step 같은 변화시킬 수 있는 state 값을 넣어야 하는데, 의도적으로 Virtual DOM에 차이를 발생시키기 위해 하는 작업이라고 보면 됩니다.

<br />

- 출처
  - [[10분 테코톡] 돔하디의 Virtual DOM](https://www.youtube.com/watch?v=6rDBqVHSbgM&ab_channel=%EC%9A%B0%EC%95%84%ED%95%9C%ED%85%8C%ED%81%AC)
