# Web Worker

- 기본적으로 브라우저는 하나의 스레드에서 동작하게 되는데 UI 조작이 아닌 조금 더 복잡한 연산을 하고 싶은 경우 Worker 스레드를 만들고 해당 스레드에 작업을 시킨 후 결과를 받을 수도 있다고 합니다.

<img width="500" src="https://github.com/muilyang12/what_i_studied/assets/78548830/4868c497-8e6c-4f68-b757-4e438b6f9c17" />

<br />
<br />

- Web Worker를 사용하기 좋은 경우
  - 화면 동작에 영향을 미치지 않는 바이너리 파일 핸들링이나 복잡한 계산을 수행해야 하는 경우.
  - 백그라운드에서 지속적인 작업을 해야 하거나 메인 스레드 영향을 미치지 않고 작업을 하는 경우.
 
<br />

- Web Worker를 사용하지 않을 경우
  - 서버에서 대부분의 데이터를 처리하는 경우.
  - DOM 제어 및 Window 객체의 일부 함수를 사용해야 하는 경우. (메인 스레드에서만 사용할 수 있고 Web Worker에서는 사용이 불가능한 부분이 있습니다.)
  - 단순 계산식인 경우. (메인 스레드와 Web Worker 간 데이터 전송 시에는 비용이 발생하기 때문에 단순 계산식은 메인 스레드에서 수행하는 것이 더 빠릅니다.)

<br />

- 아래 출처 중 카카오 테크의 글을 보면 텍스트 추출 라이브러리를 개발하는 과정에서 Web Worker를 사용했었다고 합니다.
  - 서버에 파일을 업로드하기 전에 파일의 내용을 확인하기 위해서.
  - 메타데이터 및 특정 데이터를 네트워크 사용 없이 즉각적으로 추출하기 위해서.
  - 검색, 인덱스 생성 및 암호 해제를 사용하기 위해서.

<br />

- ChatGPT한테 물어보니 다음과 같은 어플리케이션을 위해 사용할 수 있을 것 같다고 말합니다.
  - 이미지나 비디오 에디팅 어플리케이션.
  - Geospatial Applications.
  - Gaming Applications

<br />

- 출처
  - [Using Web Workers - Web APIs|MDN](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Using_web_workers)
  - [브라우저 Web Worker 다루기 with 오피스 문서 텍스트 추출 및 암호해제](https://tech.kakao.com/2021/09/02/web-worker/)
