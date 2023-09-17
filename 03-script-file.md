# 스크립트 파일 (.bat, .cmd, .sh 파일)

- 외부 라이브러리의 소스코드를 우리의 소스 코드에 포함시켜야 하는 상황이 있습니다. 그런데 해당 소스 코드가 타입스크립트로 작성되어 있고, 해당 파일들의 tsconfig 옵션들이 저희의 tsconfig 옵션과 달라서 직접 포함시킬 경우 tsc 컴파일 시 에러가 발생하는 문제가 있었습니다.

<br />

- 그래서 해당 파일들을 git clone 한 후 js로 컴파일한 후 우리의 src 경로에 넣는 작업을 해야 했습니다. 이를 자동화 하기 위해서 npm scripts를 아래와 같이 길게 작성했었습니다.

```
"update-version": "yarn git-clone && yarn run-tsc && yarn move-files && yarn delete-files",
"git-clone": "git clone --branch ...",
"run-tsc": "tsc --project ...",
"move-files": "cpx ...",
"delete-files": "node ..."
```

<br />

- npm scripts가 너무 길어지다보니 저 커맨드들을 스크립트 파일로 분리하고 그것을 실행하는 방향으로 가보자는 피드백이 있었고, 어떻게 분리할 것인지에 대해 찾아봤습니다.

<br />

- 한글로 검색을 하다가 원하는 정보를 못 찾아서 영어로 GPT에게 물어봤고, 아래와 같은 답변을 받았습니다.

  - Creating a script that can run on both systems is a complex procedure since Windows (using .bat or .cmd files) and MacOS (using .sh shell scripts) do not use the same scripting languages. However, you can create a bash (Bourne Again SHell) script, the common shell for some Linux distributions and MacOS.
  - Windows랑 MacOS는 script를 위한 공통 언어를 사용하지 않아서 좀 복잡할거야. 그런데, bash script는 리눅스랑 MacOS의 공통 쉘이니까 bash shell로 만들면 될거야.
  - Save the file with a .sh extension. You can run this script on MacOS simply by opening a Terminal window, navigate to the directory where you saved the file, then type ./filename.sh. For Windows to run this bash script, you'll need to use a program like Git Bash, Cygwin, or Windows Subsystem for Linux. Once you have one of these set up, you can simply open the program, navigate to the directory where you saved the .sh file, then type bash filename.sh.
  - 파일을 .sh 확정자로 저장하면 MacOS에서는 그냥 ./filename.sh 를 입력하여 실행할 수 있어. Windows에서도 Git Bash나 WSL(Windows Subsystem for Linux)를 사용하면 bash filenams.sh 를 입력해서 실행할 수 있어.

<br />

- 그리하여 아래와 같이 작성하여 .sh 파일을 만든 후 git bash를 통하여 실행해보았고, 원하는 결과를 얻을 수 있었습니다. 안타깝게도 cmd나 powershell에서는 실행할 수 없었습니다. 하지만 버전 업데이트의 경우 100% 확률로 개발자의 컴퓨터에서 수행이 될텐데, 개발자의 컴퓨터에 git bash가 설치되어 있지 않을 확률은 현저히 낮다보니 cmd나 powershell에서 실행할 수 없지만 이 방식을 가져가도 괜찮지 않나 싶네요.

```
echo Muil Yang !!

git clone --branch 브랜치명 깃URL ./temp
tsc --project tsconfig.json
mv -f ./temp-compiled ./src
rm -rf ./temp

```

<br />
