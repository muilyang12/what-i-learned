# Webpack externals option

- 현재 진행 중인 프로젝트에서 사용하고 있는 외부 유료 라이브러리의 버전을 올리려고 하고 있습니다. 그런데 해당 유료 라이브러리가 내부적으로 사용하는 Konva.js라는 오픈소스 모듈의 영역에서 "Module parse failed" 에러가 나며 빌드가 되지 않았습니다. 그리하여 Konva.js 깃허브의 이슈를 보며 원인을 찾아보았고, 간단하게 알게된 것을 정리하려고 합니다.

<br />

---

<br />

- 결론부터 말하면 이 문제의 경우 next.config.js 내 webpack 설정부에 아래 옵션을 넣으면 해결할 수 있습니다.

```
config.externals = [...config.externals, { canvas: 'canvas' }];
```

<br />

- Webpack에는 externals 옵션의 경우 지정한 해당 패키지를 번들링하지 않고 런타임에 외부 종속성을 검색하여 추가하도록 하는 방식을 말합니다. 즉, 여기서는 canvas라는 모듈을 번들링 시점에 넣지 말고 추후에 검색하여 디펜던시를 넣어야 한다는 것을 지정해준 것입니다.

<br />
