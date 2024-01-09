# Package.json properties

- package.json 내 항목들의 경우 create-next-app에서 만들어 준 항목을 기반으로 scripts와 dependencies에 대한 항목만 일부 추가하면서 사용하고 있었습니다. 문득 각각에 대해 궁금한 부분이 생겨서 간단하게 한 번 조사를 해보았습니다.

<br />

- Meta의 recoil 레포지토리 package-for-release.json 파일을 기준으로 작성하려 합니다.
  - https://github.com/facebookexperimental/Recoil/blob/c1b97f3a0117cad76cbc6ab3cb06d89a9ce717af/packages/recoil/package-for-release.json

<br />

---

<br />

- name, version property
  - 사용자들이 npm install 명령어로 해당 패키지를 설치할 때 사용할 패키지 이름과 버전을 지정하는 데에 사용하는 속성입니다.
  - 아래와 같이 설정한 경우 npm install recoil@0.7.7 명령어를 사용하여 설치할 수 있습니다.

<br />

```
{
  "name": "recoil",
  "version": "0.7.7",
}
```

<br />

- description property
  - 사용자들이 npm search 명령어로 해당 패키지를 검색할 때 보여질 패키지 설명을 지정하는 데에 사용하는 속성입니다.
  - 실제로 npm search recoil을 검색하면 Description에 'Recoil - A state...' 가 나오는 것을 볼 수 있습니다.

<br />

- main property
  - 해당 패키지를 npm에서 설치하여 사용할 때, 프로젝트 내의 어떤 파일이 불러와질지를 지정하는 데에 사용하는 속성입니다.
  - 아래와 같이 recoil을 import 할 경우 main 옵션에 연결한 파일이 불러와지게 됩니다.
  - 만약 webpack 이나 babel 에 export 경로로 lib 디렉토리나 dist 디렉토리를 설정한 경우 해당 디렉토리 내의 파일을 main 옵션에 지정해주어야 합니다.
  - 명시하지 않을 경우 기본적으로 프로젝트의 최상위 디렉토리의 index.js 파일이 사용됩니다.

<br />

```
{
  "main": "cjs/index.js",
}
```

```
import recoil from "recoil";
```

<br />

- types property
  - 타입스크립트로 개발한 후 자바스크립트로 컴파일하여 발행하는 프로젝트의 경우, 해당 프로젝트에서 정의하고 있는 타입 정보를 담은 파일의 위치를 지정하는 데에 사용하는 속성입니다.

<br />

```
{
  "types": "index.d.ts",
}
```

- private property
  - 해당 프로젝트가 npm 패키지 저장소에 발행되어도 되는지의 여부를 지정하는 데에 사용하는 속성입니다.
  - 기본값이 false 이기에 따로 명시하지 않으면 해당 프로젝트가 실수로 npm 패키지 저장소로 업로드되는 사고가 발생할 수 있습니다. 그렇기에 npm 패키지 저장소로 올리면 안 되는 프로젝트의 경우 private 필드의 값을 반드시 true로 설정하는 것이 권장됩니다.

<br />

- homepage property
  - 해당 프로젝트의 홈페이지나 문서 페이지 URL을 설정하는 데에 사용하는 속성입니다.
  - 설정할 경우 npm docs 명령어를 통하여 간편하게 해당 URL (홈페이지) 를 열어볼 수 있습니다.
  - 또한, npm 배포 시 homepage 옵션에 설정한 URL이 npm 의 Homepage 항목에 표현됩니다.
  - recoil 의 경우 package.json 파일에 homepage 속성이 없어서 react 의 package.json 파일을 참고하였습니다.

<br />

```
{
  "homepage": "https://reactjs.org/",
}
```

<br />

<img src="https://github.com/muilyang12/what_i_studied/assets/78548830/96164d52-cb6d-4b1c-a92c-f064a6c5bada" width=750 />

<br />
<br />

- repository property
  - 해당 프로젝트의 코드 저장소 URL을 설정하는 데에 사용하는 속성입니다.
  - 설정할 경우 npm repo 명령어를 통하여 간편하게 해당 URL 을 열어볼 수 있습니다.
  - 또한, npm 배포 시 repository 옵션에 설정한 URL이 npm 의 Repository 항목에 표현됩니다.

<br />

```
{
  "repository": {
    "type": "git",
    "url": "https://github.com/facebook/react.git",
    "directory": "packages/react"
  },
}
```

<br />

<img src="https://github.com/muilyang12/what_i_studied/assets/78548830/241bebf6-e09b-4c4d-9a71-84059721bf7a" width=750 />

<br />
<br />

- files property
  - npm 배포 시에 프로젝트 내 특정 파일만 발행할 패키지에 포함하고 싶은 경우, 포함할 파일을 지정하는 데에 사용하는 속성입니다.

<br />
 
- license property
  - 해당 프로젝트의 라이선스를 표시하는 데에 사용하는 속성입니다.

<br />
