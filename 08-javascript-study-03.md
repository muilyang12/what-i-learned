# JavaScript 스터디 03

- JavaScript에서 this가 작동하는 방식은 어떻게 되나요 ??

- 우선 전역 스코프에서 사용될 경우 브라우저 환경에서는 window 혹은 undefined에, node.js 환경에서는 global 혹은 module.exports 객체에 this가 바인딩 됩니다. (기본 바인딩)

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

- call, apply, bind를 사용하여 함수를 호출할 경우는 첫 번째 인수로 넘긴 값 혹은 객체에 this가 바인딩 됩니다. (명시적 바인딩)

- this가 객체 내에서 사용될 경우는 해당 객체 자신에 this가 바인딩 됩니다. (암시적 바인딩)

```
const obj = {
    name: "Muil",
    showThis() {
        console.log(this);
    }
}

obj.showThis(); // {name: 'Muil', showThis: ƒ}
```

- new 연산자를 사용하여 함수를 호출한 경우 (클래스) 새로이 생성되는 객체에 this가 바인딩 됩니다. (new 바인딩)

<br />

- Arrow function 내에서 사용한 this의 경우 정의한 실행 컨텍스트의 this에 바인딩된 객체와 같은 객체가 바인딩됩니다.

<br />

- 출처
  - [[10분 테코톡] 🥦 브콜의 This](https://www.youtube.com/watch?v=7RiMu2DQrb4&ab_channel=%EC%9A%B0%EC%95%84%ED%95%9C%ED%85%8C%ED%81%AC)
