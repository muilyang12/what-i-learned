# How to retrigger animation in React

- 시작 가이드 컴포넌트를 만들던 상황이었습니다. 순차적으로 가이드가 표현될 때 하나의 컴포넌트가 위치를 바꿔가며 여러 위치에서 렌더링 되는 방식을 구현하고 싶었습니다. 그런데 위치는 스테이트에 의해 잘 렌더링 되는데 CSS 애니메이션이 매 렌더링마다 발생하지 않던 문제가 있었습니다. 해당 문제에 대한 해결책을 찾다가 알게된 사항을 정리하려 합니다.

<br />

---

<br />

- 리액트에서 하나의 DOM에 애니메이션을 연결한 경우, 해당 컴포넌트가 새로 렌더링되더라도 애니메이션이 무조건적으로 다시 실행되지는 않습니다.

<br />

- 예를 들어, 아래와 같이 컴포넌트를 만들고 사용할 때 cardText 프랍스의 값이 바뀌어서 Card 컴포넌트가 새로 렌더링되더라도 come-up 애니메이션이 계속해서 불리지는 않습니다. 최초 렌더링될 때 한 번만 호출되죠.

<br />

```
export default function Card({ cardText }) {
  return (
    <>
      <div className="card-wrapper">
        {cardText}
      </div>

      <style jsx>
        {`
          @keyframes come-up {
            .....
          }

          .card-wrapper {
            animation: come-up 0.5s;
          }
        `}
      </style>
    </>
  );
}
```

<br />

- 이때 아래와 같이 div 태그에 key 값을 넣으면 해당 key 가 바뀌는 렌더링마다 애니메이션이 새로 시작되게 됩니다.

<br />

```
<div className="card-wrapper" key={cardText}>
  {cardText}
</div>
```

<br />

- 아래 StackOverflow 글에서 이런 현상이 나타나는 이유에 대해 상세하게 설명되어 있지는 않지만, 리액트의 가상 DOM에 의해 발생하는 것으로 보입니다. (제 추론입니다.)
  - 리액트의 경우 렌더링 최적화를 위해 DOM과 비슷한데 API를 비롯한 불필요한 몇몇을 가지지 않는 가벼운 버전의 Virtual DOM을 만들어서 사용합니다. 이 가상 DOM에 변화가 생길 경우에 한해 실제 DOM을 렌더링하는 방식이죠.
  - key를 넣지 않은 경우, 가상 DOM의 관점에서 봤을 때 div 태그는 변화한 것이 없고 그 안의 innerText만 변화한 것으로 인지됩니다. 그러면 innerText에 대한 부분만 다시 그려지고 그를 감싼 div 태그에 대한 실제 DOM은 다시 그려지지 않습니다. 그런데 애니메이션은 div 태그에 달려있으니, 애니메이션 역시 다시 실행되지 않는 것입니다.
  - 그와 달리, key를 넣으면 ‘이 div 태그는 이전 것과 다른 거니까 다시 그려.’ 라고 리액트에게 넛지를 주는 것과 같습니다. 그러면, div 태그의 실제 DOM이 다시 그려지기에 애니메이션도 다시 실행되는 것이고요.

<br />
 
<img src="https://github.com/muilyang12/what_i_studied/assets/78548830/77dc6830-1120-43bc-9677-d85cf23e6dd4" width=500 />

<br />
<br />

- 출처
  - [How to trigger a CSS animation on EVERY TIME a react component re-renders](<[https://www.youtube.com/watch?v=7RiMu2DQrb4&ab_channel=%EC%9A%B0%EC%95%84%ED%95%9C%ED%85%8C%ED%81%AC](https://stackoverflow.com/questions/63186710/how-to-trigger-a-css-animation-on-every-time-a-react-component-re-renders)https://stackoverflow.com/questions/63186710/how-to-trigger-a-css-animation-on-every-time-a-react-component-re-renders>)
  - [[React.js] Virtual DOM 가상 돔](<[https://www.frontendinterviewhandbook.com/coding/javascript-utility-function](https://velog.io/@minbr0ther/React.js-Virtual-DOM-%EA%B0%80%EC%83%81-%EB%8F%94)https://velog.io/@minbr0ther/React.js-Virtual-DOM-%EA%B0%80%EC%83%81-%EB%8F%94>)
