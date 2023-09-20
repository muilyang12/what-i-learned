# JavaScript 스터디 01

- 호이스팅이 무엇인가요 ??
  - 호이스팅(Hoisting) 이란 스코프 안에 존재하는 모든 선언들을 최상단으로 끌어올리는 것을 말합니다. var 키워드로 선언되거나 초기화된 변수, 또는 function 키워드로 선언된 함수에 적용됩니다. 이 둘의 차이점으로 함수 선언은 함수 몸체가 호이스팅되는 반면, 변수 선언 형태로 작성된 함수 표현식은 변수 선언만 호이스팅됩니다.

```
console.log(foo); // undefined
var foo = "Hello !!";
console.log(foo); // Hello !!

func(); // 'func is called.'
function func() {
  console.log('func is called.');
}

```

<br />

- == 와 === 의 차이점은 무엇인가요 ??
  - == 는 추상 동등 연산자이고 === 는 완전 동등 연산자입니다. == 연산자는 타입 변환이 필요한 경우 타입 변환을 한 후에 동등한지 비교하는 연산을 수행하고, === 연산자는 타입까지 비교하는 연산을 수행합니다.

```
1 == '1'; // true
1 == [1]; // true

1 === '1' // false
1 === [1] // false
```

<br />

- var, let, const를 사용하여 선언된 변수들의 차이점은 무엇인가요 ??
  - var 키워드를 사용하여 선언된 변수의 경우 함수 내에서 선언된 경우에는 함수 내부에서만 생애주기를 갖는 반면 함수 외부에서 선언된 경우에는 전역 변수로서 작동합니다. 반면 let또는 const 키워드를 사용하여 선언된 변수는 블록 범위 스코프를 가져서, 가장 가까운 중괄호 세트 (함수, if-else 블록 또는 for-루프) 내에서만 액세스할 수 있습니다.
  - 그리고, var 키워드는 변수가 호이스팅 되도록 허용합니다. 반면에, let과 const는 이를 허용하지 않아 선언 이전에는 변수가 참조될 수 없습니다.
  - 또한, var 키워드를 사용하여 선언된 변수의 경우 변수 재선언과 값 변경을 모두 허용하지만, let 키워드를 사용하여 선언된 변수는 값 변경만이 허용되고 const 키워드를 사용하여 선언된 변수는 둘 다 허용되지 않습니다.

```
{
    let aaa = 'aaa';
    var bbb = 'bbb';
}

aaa // Error - aaa is not defined
bbb // bbb
```

<br />

- mutable 객체와 immutable 객체 사이의 차이점은 무엇인가요 ??
  - JavaScript에서는 일부 내장 타입 (숫자, 문자열) 은 불변(immutable)하며, 사용자 정의 객체 (Object) 는 일반적으로 가변(mutable)합니다. Math, Date 같은 일부 내장 객체는 불변합니다.
  - Object.preventExtensions, Object.seal, Object.freeze 같은 메서드를 통하여 불변한 객체를 만들 수 있습니다. Object.seal의 경우 밀봉된 객체 (configurable: false) 로 만들어서 프로퍼티 추가나 삭제가 불가능하게 만듭니다. Object.freeze의 경우 동결된 객체 (writable:false, configurable: false) 로 만들어 프로퍼티 추가나 삭제 뿐만 아니라 변경까지 불가능하게 만듭니다.

<br />

- 출처
  - [Front End Interview Handbook](https://www.frontendinterviewhandbook.com/coding/javascript-utility-function)
