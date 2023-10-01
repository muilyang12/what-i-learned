# TypeScript override 키워드

- 아래 코드를 보면 타입스크립트에서 SomeComponent 라는 클래스를 만든 후 이 클래스를 상속 받아 SpecializedComponent 를 만들었습니다. 여기서 show 메소드는 부모 클래스의 메소드를 오버라이딩 한 메소드 입니다.

```
class SomeComponent {
  show() {
    // ...
  }
}

class SpecializedComponent extends SomeComponent {
  show() {
    // ...
  }
}
```

<br />

- 그런데 클래스를 만든 이후 부모 클래스의 메소드 명을 변경하고자 한다면 자식 클래스의 메소드명도 함께 변경해주어야 합니다. 그렇지 않으면 자식 클래스의 show 메소드는 더 이상 부모 클래스의 메소드를 오버라이딩한 메소드가 아니라 신규 메소드가 되겠죠.

<br />

- 부모 메소드의 이름만 변경하고 자식 클래스의 메소드 이름을 변경하지 않는 이러한 실수를 막기 위해 사용할 수 있는 것이 override 키워드입니다. 아래처럼 부모 클래스의 메소드를 오버라이딩한 메소드라는 것을 override 키워드를 통해 명확하게 표현할 경우, 부모 클래스의 메소드명만 수정했을 때 에러가 출력됩니다.

```
class SomeComponent {
  showAndProve() {
    // ...
  }
}

class SpecializedComponent extends SomeComponent {
  override show() { // Error - This member cannot have an ‘override' modifier
                    // because it is not declared in the base class
    // ...
  }
}
```

<br />

- 출처
  - [TypeScript 4.3 번역](https://velog.io/@hustle-dev/TypeScript-4.3-%EB%B2%88%EC%97%AD)
