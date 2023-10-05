# 브라우저 렌더링 과정

- 브라우저의 렌더링 과정에 대해 간단히 설명하면, HTML을 파싱하여 DOM 트리를 만듭니다. 여기서 HTML 파싱 중 \<link\> 태그를 만날 경우 해당 CSS를 파싱하여 CSSON 트리를 만듭니다. 여기까지를 Construction 파트라고 부릅니다.

<br />

- 그리고 DOM 트리와 CSSON 트리를 합쳐 Render 트리를 만듭니다. 그 후 Layout 단계 (Render 트리를 활용하여 각 요소의 전체적인 위치와 각각의 크기를 결정하는 단계) 와 Paint 단계 (실제로 브라우저에 요소를 그려주는 단계) 를 거치게 됩니다. 이 두 과정을 Operation 파트라고 부르는데, 이 과정을 거쳐 브라우저의 렌더링이 마무리됩니다.

<br />

<img src="https://github.com/muilyang12/what_i_studied/assets/78548830/e15413a6-7267-4367-9d63-970200853f58" width=750 />

<br />
<br />

- 출처
  - [브라우저 렌더링 순서와 원리](https://velog.io/@zaman17/%EA%B8%B0%EC%88%A0%EB%A9%B4%EC%A0%91%EB%8C%80%EB%B9%84-%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80-%EB%A0%8C%EB%8D%94%EB%A7%81-%EC%88%9C%EC%84%9C%EC%99%80-%EC%9B%90%EB%A6%AC)
  - [Reflow와 Repaint에 대하여](https://devowen.com/463)
