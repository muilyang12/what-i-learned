# React.cloneElement()

- 리액트를 사용하여 공통 컴포넌트를 만드는 과정에서 종종 cloneElement 를 사용합니다. cloneElement 에 대한 공식 문서를 읽었던 내용과 그 과정에서 찾아본 사항에 대해 한 번 정리하려 합니다.

<br />

- cloneElement의 공식 문서를 보면 아래와 같이 Pitfall 위험 표시를 합니다. 위험 표시를 하는 이유는 데이터 흐름을 추적하기 힘들기 때문이라고 합니다.
  - cloneElement makes it harder to trace the data flow, so try the alternatives instead.

<br />

<img src="https://github.com/muilyang12/what_i_studied/assets/78548830/b10b902c-0aca-4400-bd0e-8b5e7f93cc22" width=500 />

<br />
<br />

- 공식 문서의 경우 아래의 예시를 기준으로 설명하고 있습니다. List 컴포넌트 안에 Row 컴포넌트가 있는데 Row 에 selected 를 표시하기 위한 목적으로 Children.map 과 cloneElement 를 사용한 방식입니다. 한 마디로 정리하면 children 으로 받은 것에 추가적인 props를 넘겨주고 싶은 경우에 cloneElement 를 사용한다고 볼 수 있습니다.

<br />

```
<List>
  <Row title="Cabbage" />
  <Row title="Garlic" />
  <Row title="Apple" />
</List>
```

```
export default function List({ children }) {
  const [selectedIndex, setSelectedIndex] = useState(0);
  
  return (
    <div className="List">
      {Children.map(children, (child, index) =>
        cloneElement(child, {
          isHighlighted: index === selectedIndex 
        })
      )}
      
// .....
```

<br />
