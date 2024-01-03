# Implementing React SSR with Express.js

- 리액트의 공식 문서를 읽다보면 아래와 같은 Server API 들이 존재합니다. Next.js 없이 React.js 와 서버를 사용하여 SSR 을 구현하고자 한다면 이 API 들을 사용하여야 합니다. 실제로 Next.js 내부의 소스 코드에서도 이들을 사용하는 것을 볼 수 있습니다.

<br />

<img src="https://github.com/muilyang12/what_i_studied/assets/78548830/e760beb6-4340-4687-bd6d-fc11da280654" width=750 />

<br />
<br />

- CSR을 사용하여 그려진 결과와 SSR을 사용하여 그려진 결과를 직접 비교하면 다음과 같습니다.
  1. CSR: React 프로젝트를 build 하여 나온 결과물인 html, js 파일을 정적 파일로 사용할 경우, 최초 로드 시 아래와 같이 빈 html 이 오고 js 파일에 의해 내용물들이 채워지게 됩니다. 말 그대로 Client Side Rendering 인 거죠.

<br />

<img src="https://github.com/muilyang12/what_i_studied/assets/78548830/2fb05d65-925c-45b9-96b6-c98ffb2ae177" width=750 />

<br />
<br />

  2. SSR: Server API를 사용하여 SSR을 구현한 경우, 최초 로드 시 일부 그려진 html 이 오고 js 파일에 의하여 Hydration 이 이루어지게 됩니다. 말 그대로 Server Side Rendering 인 거죠.

<br />

<img src="https://github.com/muilyang12/what_i_studied/assets/78548830/5b982bce-ada0-4887-bd12-2ff9977163bf" width=750 />

<br />
<br />
