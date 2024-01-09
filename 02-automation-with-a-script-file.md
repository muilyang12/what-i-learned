# Automation with a script file (.bat, .cmd, .sh file)

- 저희 프로젝트를 개발하던 과정 외부 라이브러리의 소스코드를 우리의 소스 코드에 포함시켜야 하는 상황이 있었습니다.

<br />

- 그런데 해당 소스 코드가 저희의 tsconfig 옵션과 다른 옵션으로 작성되어 있었기에, 해당 파일들을 직접 포함시킬 경우 tsc 컴파일 시 에러가 발생하는 문제가 있었습니다.

<br />

- 그래서 해당 파일들을 git clone 한 후 js로 컴파일한 후 우리의 src 경로에 넣는 작업을 해왔었습니다. 이를 자동화 하고 싶다는 생각이 들어서 npm scripts를 아래와 같이 길게 작성했었습니다.

```
"update-version": "yarn git-clone && yarn run-tsc && yarn move-files && yarn delete-files",
"git-clone": "git clone --branch ...",
"run-tsc": "tsc --project ...",
"move-files": "cpx ...",
"delete-files": "node ..."
```

<br />

- 그런데 위처럼 작성 시에 npm scripts가 너무 길어지다보니 저 커맨드들을 스크립트 파일로 분리한 후 그것을 실행하는 방향으로 가보자는 피드백이 있었습니다.

<br />

- 그런데 일부 개발자는 MacOS를 쓰고 일부 개발자는 Windows를 쓰다보니 이 둘 간의 스크립트 파일 사용법에 대해 조사를 해보았고 아래와 같은 결과를 얻을 수 있었습니다.
  - Creating a script that can run on both systems is a complex procedure since Windows (using .bat or .cmd files) and MacOS (using .sh shell scripts) do not use the same scripting languages. However, you can create a bash (Bourne Again SHell) script, the common shell for some Linux distributions and MacOS.
  - Windows랑 MacOS는 script를 위한 공통 언어를 사용하지 않아서 좀 복잡할거야. 그런데, bash script는 리눅스랑 MacOS의 공통 쉘이니까 bash shell로 만들면 될거야.
  - Save the file with a .sh extension. You can run this script on MacOS simply by opening a Terminal window, navigate to the directory where you saved the file, then type ./filename.sh. For Windows to run this bash script, you'll need to use a program like Git Bash, Cygwin, or Windows Subsystem for Linux. Once you have one of these set up, you can simply open the program, navigate to the directory where you saved the .sh file, then type bash filename.sh.
  - 파일을 .sh 확정자로 저장하면 MacOS에서는 그냥 ./filename.sh 를 입력하여 실행할 수 있어. Windows에서도 Git Bash나 WSL(Windows Subsystem for Linux)를 사용하면 bash filenams.sh 를 입력해서 실행할 수 있어.

<br />

- 그리하여 아래와 같이 작성하여 .sh 파일로 만들었고 원하는 결과를 얻을 수 있었습니다.

```
echo Muil Yang !!

git clone --branch 브랜치명 깃URL ./temp
tsc --project tsconfig.json
mv -f ./temp-compiled ./src
rm -rf ./temp
```

<br />

- 그런데 이 경우 .sh 파일이다보니 git bash를 사용하여 실행하여야 합니다. cmd나 powershell에서는 실행할 수 없습니다. 그런데 이런 버전 업데이트의 경우는 일반적으로 개발자의 컴퓨터에서 수행이 될 것고, 개발자의 컴퓨터에는 높은 확률로 git bash가 있을 것입니다. 그러니 cmd나 powershell에서 실행할 수 없더라도 괜찮은 방식이지 않을까 싶네요.
