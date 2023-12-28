# Package.json setting

- Meta의 recoil의 package-for-release.json 파일을 기준으로 작성하려 합니다.
  - https://github.com/facebookexperimental/Recoil/blob/c1b97f3a0117cad76cbc6ab3cb06d89a9ce717af/packages/recoil/package-for-release.json

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
  - 아래와 같이 recoil을 import할 경우 main 옵션에 연결한 파일이 불러와지게 됩니다.
  - 만약 webpack이나 babel에 export 경로로 lib 디렉토리나 dist 디렉토리를 설정한 경우 해당 디렉토리 내의 파일을 main 옵션에 지정해주어야 합니다.
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
