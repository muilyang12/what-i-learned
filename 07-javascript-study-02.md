# JavaScript 스터디 02

- 이벤트 위임 (Event delegation) 이 무엇인가요 ??
  - 이벤트 위임은 이벤트 리스너를 하위 요소 각각에 추가하는 대신 상위 요소에 추가하고 내부에서 어떤 타겟에서 발생한 이벤트인지를 체크하여 로직을 추가하는 기법입니다. 하나의 핸들러 함수만 정의하면 되기에 메모리를 절약할 수 있다는 이점이 있습니다.

<br />

- 이벤트 버블링 (Event bubbling) 과 캡쳐링 (Event capturing) 이 무엇인가요 ??
  - 이벤트 버블링은 한 요소에 이벤트가 발생하였을 때 해당 요소에 연결된 이벤트 핸들러가 실행된 후 이어서 부모 요소의 이벤트 핸들러들이 순차적으로 동작하는 것을 말합니다. event.stopPropagation() 메서드를 통하여 버블링을 막을 수 있습니다.
  - 이벤트 캡쳐링의 경우 버블링과 달리 하위 요소로 이벤트가 전파되는 것을 말합니다.

<br />

- 자바스크립트에서 실행 컨텍스트 (Execute Context) 는 무엇인가요?
  - 실행 컨텍스트는 실행할 코드에 제공할 환경 정보들을 모아놓은 객체를 말합니다.
  - 자바스크립트 코드가 실행되면 콜 스택에 전역 실행 컨텍스트가 쌓이게 됩니다. 그 후 전역에서 A라는 함수를 호출할 경우 함수 A의 실행 컨텍스트가 생성되어 콜 스택에 쌓이게 됩니다. 함수 A가 종료될 경우에 해당 실행 컨텍스트가 콜 스택에서 사라지게 되고요. 그리고 모든 자바스크립트 코드가 실행되면 전역 실행 컨텍스트도 사라지게 됩니다.
  - 전역 스코프에서 정의한 모든 변수는 이 실행 컨텍스트 안에 포함되게 됩니다. 그리고 A 함수 내에서 정의한 로컬 변수가 있을 경우 함수 A의 실행 컨텍스트 안에 모두 포함되게 됩니다.
  - 같은 이름의 변수가 여러 컨텍스트에 걸쳐 존재할 때 변수의 값을 결정하는 것을 식별자 결정 (Identifier resolution) 이라고 부릅니다. 그리고 자바스크립트 엔진은 워칙적으로 현재의 실행 컨텍스트에 포함된 변수의 값을 우선적으로 사용하게 됩니다.

<br />

<img src="https://github.com/muilyang12/what_i_studied/assets/78548830/013bdbd1-b7a2-4581-a307-eb1f12836be4" width=750 />

<br />
<br />

- 클로저 (Closure) 란 무엇인가요 ??
  - 클로저는 한 함수가 함수 내의 로컬 변수를 참조한 함수를 함수 외부에 전달할 경우, 해당 함수의 실행 컨텍스트가 종료된 이후에도 해당 실행 컨텍스트 내의 변수에 계속해서 접근할 수 있는 상태를 말합니다.
  - 클로저를 사용하면 전역변수의 사용을 줄일 수 있습니다. 아래의 두 코드는 같은 동작을 하는 코드입니다. 그런데, 위의 코드는 전역 변수 counter가 있는 반면, 아래의 코드는 counter 변수를 내부의 클로저로 만들어서 접근하거나 훼손할 수 없도록 만들었습니다.

<br />

```
let counter = 0;

function increase() {
    counter += 1;
    return counter;
}

button.addEventListener("click", () => {
    display.innerHTML = increase();
});
```

<br />

```
let increase = (function increase() {
    let counter = 0;

    return function () {
        return ++counter;
    };
})();

button.addEventListener("click", () => {
    display.innerHTML = increase();
});
```

<br />

- 출처
  - [Front End Interview Handbook](https://www.frontendinterviewhandbook.com/coding/javascript-utility-function)
  - [[10분 테코톡] 💙 하루의 실행 컨텍스트](https://www.youtube.com/watch?v=EWfujNzSUmw&t=78s&ab_channel=%EC%9A%B0%EC%95%84%ED%95%9C%ED%85%8C%ED%81%AC)
