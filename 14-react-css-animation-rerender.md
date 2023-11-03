# React CSS Animation Rerender

- 리액트에서 하나의 DOM에 애니메이션을 연결한 경우, 해당 컴포넌트가 새로 렌더링되더라도 애니메이션이 무조건적으로 다시 실행되지는 않습니다.

<br />

- 예를 들어, 아래와 같이 컴포넌트를 만들어 사용할 때 cardText 프랍스의 값이 바뀌어서 Card 컴포넌트가 새로 렌더링되더라도 come-up 애니메이션이 계속해서 재실행 되지는 않습니다. 최초 렌더링될 때 한 번만 호출되죠.

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
<br />

- 이때 아래와 같이 div 태그에 key 값을 넣으면 해당 key의 값이 바뀌는 렌더링마다 애니메이션이 새로 시작되게 됩니다.

```
<div className="card-wrapper" key={cardText}>
  {cardText}
</div>
```

<br />
<br />

- 아래 StackOverflow 글에서 이런 현상이 나타나는 이유에 대해 상세하게 설명되어 있지는 않지만, 리액트의 가상 DOM에 의해 발생하는 것으로 보입니다. (제 추론입니다.)
  - 리액트의 경우 렌더링 최적화를 위해 DOM과 유사하지만 DOM API를 비롯한 불필요한 몇몇을 가지지 않는 가벼운 버전의 Virtual DOM을 만들어서 사용합니다. 실제 DOM을 매번 렌더링하면 성능에 부담이 되기에, 가상 DOM에 변화가 생기는 경우를 탐지하여 해당 가상 DOM에 대응되는 실제 DOM을 렌더링하는 방식이죠.
  - key를 넣지 않은 경우, 가상 DOM의 관점에서 봤을 때 div 태그는 변화한 것이 없고 그 안의 innerText만 변화한 것으로 인지됩니다. 그러면 innerText에 대한 부분만 다시 그려지고 그를 감싼 div 태그에 대한 실제 DOM은 다시 그려지지 않는 것이죠. 그런데 애니메이션은 div 태그에 달려있으니, 애니메이션 역시 다시 실행되지 않는 것입니다.
  - 그와 달리, key를 넣으면 ‘이 div 태그는 이전 것과 다른 거니까 다시 그려.’ 라고 리액트에게 넛지를 주는 것과 같습니다. 그러면, div 태그의 실제 DOM이 다시 그려지기에 div 태그에 연결된 애니메이션도 다시 실행되는 것이죠.

<img src="https://github.com/muilyang12/what_i_studied/assets/78548830/6a8f2f3a-2dcc-444c-a98e-a47d83da6137" width=500 />

<br />
<br />


- 출처
  - [How to trigger a CSS animation on EVERY TIME a react component re-renders](https://stackoverflow.com/questions/63186710/how-to-trigger-a-css-animation-on-every-time-a-react-component-re-renders)
  - [[React.js] Virtual DOM 가상 돔](https://velog.io/@minbr0ther/React.js-Virtual-DOM-%EA%B0%80%EC%83%81-%EB%8F%94)
