# Web Worker

- 기본적으로 브라우저는 하나의 스레드에서 동작하게 되는데 UI 조작이 아닌 조금 더 복잡한 연산을 하고 싶은 경우 Web Worker 스레드를 만들고 해당 스레드에 작업을 시킨 후 그 결과를 받을 수도 있습니다.
- In basic terms, browsers typically operate in a single thread. However, if you want to perform more complex computations that don't involve UI manipulation, you can create a Web Worker thread and delegate tasks to that thread, then receive the results.

<img width="500" src="https://github.com/muilyang12/what_i_studied/assets/78548830/4868c497-8e6c-4f68-b757-4e438b6f9c17" />

<br />
<br />

- Web Worker를 사용하기 좋은 경우
- Cases where you can use Web Workers include:
  - 화면 동작에 영향을 미치지 않는 바이너리 파일 핸들링이나 복잡한 계산을 수행해야 하는 경우.
  - When you need to handle binary file processing or perform complex calculations that won't impact the visual performance of your web page.
  - 메인 스레드 영향을 미치지 않으면서 백그라운드에서 지속적인 작업을 해야 하는 경우.
  - When you need to perform continuous background tasks without affecting the main thread.

<br />

- Web Worker를 사용하지 않아야 하는 경우
- Cases where you should avoid using Web Workers include:
  - 서버에서 대부분의 데이터를 처리하는 경우.
  - When most of your data processing is done on the server.
  - DOM 제어 및 Window 객체의 일부 함수를 사용해야 하는 경우. (일부 함수의 경우 메인 스레드에서만 사용할 수 있고 Web Worker에서는 사용이 불가능하기에.)
  - When you need to manipulate the DOM or use certain functions of the Window object. (as some functions can't be used in Web Worker.)
  - 단순 계산식인 경우. (메인 스레드와 Web Worker 간 데이터 전송 시에는 비용이 발생하기 때문에 단순 계산식은 메인 스레드에서 수행하는 것이 더 빠르다고 합니다.)
  - When dealing with simple calculations. (as simple calculations might be faster when performed in the main thread, since there's a cost associated with data transfer between the main thread and Web Worker.)

<br />

- 아래 출처 중 카카오 테크의 글을 보면 텍스트 추출 라이브러리를 개발하는 과정에서 Web Worker를 사용했었다고 합니다.
- If you look at the article from Kakao Tech among the sources below, it says that they used Web Workers in the process of developing a text extraction library.

  - 서버에 파일을 업로드하기 전에 파일의 내용을 확인하기 위해서.
  - To verify the contents of a file before uploading it to the server.
  - 메타데이터 및 특정 데이터를 네트워크 사용 없이 즉각적으로 추출하기 위해서.
  - To immediately extract metadata and specific data without network usage.
  - 검색, 인덱스 생성 및 암호 해제를 사용하기 위해서.
  - To use for searching, creating indexes, and decrypting data.

<br />

- ChatGPT한테 물어보니 다음과 같은 어플리케이션을 위해 사용할 수 있을 것 같다고 말합니다.
- ChatGPT suggests that it could be used for the following applications
  - Image or video editing application.
  - Geospatial Applications.
  - Gaming Applications

<br />

- Reference
  - [Using Web Workers - Web APIs|MDN](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Using_web_workers)
  - [브라우저 Web Worker 다루기 with 오피스 문서 텍스트 추출 및 암호해제](https://tech.kakao.com/2021/09/02/web-worker/)
