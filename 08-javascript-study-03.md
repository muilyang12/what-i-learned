# JavaScript 스터디 03

- JavaScript에서 this가 작동하는 방식은 어떻게 되나요 ??

  1. 우선 전역 스코프에서 사용될 경우 브라우저 환경에서는 window 혹은 undefined에, node.js 환경에서는 global 혹은 module.exports 객체에 this가 바인딩 됩니다. (기본 바인딩)

  <br />

  ```
  console.log(this); // Window

  function showThisInStrictMode() {
      "use strict";

      console.log(this);
  }
  showThisInStrictMode(); // undefined
  ```

  ```
  function showThis() {
    console.log(this);
  }

  showThis(); // Global
  console.log(this); // {}

  console.log(this === module.exports); // true
  ```

  <br />

  2. call, apply, bind를 사용하여 함수를 호출할 경우는 첫 번째 인수로 넘긴 값 혹은 객체에 this가 바인딩 됩니다. (명시적 바인딩)

  <br />

  3. this가 객체 내에서 사용될 경우는 해당 객체 자신에 this가 바인딩 됩니다. (암시적 바인딩)

  ```
  const obj = {
      name: "Muil",
      showThis() {
          console.log(this);
      }
  }

  obj.showThis(); // {name: 'Muil', showThis: ƒ}
  ```

  <br />

  4. new 연산자를 사용하여 함수를 호출한 경우 (클래스) 새로이 생성되는 객체에 this가 바인딩 됩니다. (new 바인딩)

  <br />
    
  5.  Arrow function 내에서 사용한 this의 경우 정의한 실행 컨텍스트의 this에 바인딩된 객체와 같은 객체가 바인딩됩니다.

<br />

- Promise가 무엇인가요 ??
  - Promise는 비동기 처리를 위해서 사용하는 것으로 ES6에 도입된 문법입니다. 특정 동작을 기다린 후 resolve된 값 또는 resolve되지 않은 이유를 활용하여 무언가 동기적으로 처리를 하고자 할 때 사용합니다. .then 또는 .catch를 사용하죠.

<br />

- 이벤트 루프, 콜 스택, 태스크 큐란 무엇인가요 ??
  - 이벤트 루프는 콜 스택을 모니터하고 태스크 큐에서 수행할 작업이 있는지 (실행 환경, Context) 확인하는 단일 스레드 루프입니다. 콜 스택이 비어 있고 태스크 큐에 실행할 콜백 함수가 있는 경우, 함수는 큐에서 제거되고 실행될 콜 스택으로 푸시되게 됩니다.

<br />

- 출처
  - [[10분 테코톡] 🥦 브콜의 This](https://www.youtube.com/watch?v=7RiMu2DQrb4&ab_channel=%EC%9A%B0%EC%95%84%ED%95%9C%ED%85%8C%ED%81%AC)
  - [Front End Interview Handbook](https://www.frontendinterviewhandbook.com/coding/javascript-utility-function)
