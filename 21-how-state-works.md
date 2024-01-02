# How state works in React

- 리액트의 useState의 경우 closure를 사용하여 내부의 값을 관리합니다. 아래와 같은 형식의 useState 함수가 상태에 대한 기본적인 형태입니다. \_val 이라는 클로저에 실제 값을 넣고 그 값을 활용하는 것입니다. 실제 값에 그대로 접근하지는 않고, 그 값을 리턴하는 함수 혹은 그 값에 신규 값을 대입하는 함수를 받아와서 간접적으로 사용하는 형태입니다.

<br />

```
function useState(initialValue) {
  let _val = initialValue;

  function state() {
    return _val;
  }

  function setState(newVal) {
    _val = newVal;
  }

  return [state, setState];
}
```

```
const [value, setValue] = useState(0);
console.log(value()); // 0
setValue(10)
console.log(value()); // 10
```

<br />

- 출처
  - [Deep dive: How do React hooks really work?](https://www.netlify.com/blog/2019/03/11/deep-dive-how-do-react-hooks-really-work/)
  - [[React] useState의 동작 원리와 클로저](https://seokzin.tistory.com/entry/React-useState%EC%9D%98-%EB%8F%99%EC%9E%91-%EC%9B%90%EB%A6%AC%EC%99%80-%ED%81%B4%EB%A1%9C%EC%A0%80)
