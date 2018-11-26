---
title : Unreal.js
tags: ["Unreal.js","node.js","Unreal Engine 4"] 
---

## Unreal.js 개발을 위한 초보 가이드

Unreal.js는 어떻게 탄생하게 되었는가 하는건 사실 중요한 것은 아니다.

하지만 Unreal.js가 어떤 기술에 기반을 두고 있는지는 알아둘 필요가 있다.

Unreal.js는 React-UMG에서 출발했다.

때문에 React.js와 밀접한 관련이 있으며 npm 혹은 yarn도 함께 알아둘 필요가 있다.

여기서는 node.js를 설치하여 기본으로 npm을 사용하도록 한다.

OS는 Windows 10 pro 기준이다.

언리얼엔진을 어느 정도 다루는 사람이 볼 것이라고 여기고 글을 작성한다.



####준비

몇 가지의 설치만 마치면 가벼운 마음으로 시작할 수가 있다.(1번을 먼저 설치하길 권장)

1. [Unreal Engine 4](https://www.unrealengine.com/ko/what-is-unreal-engine-4)
2. [Visual Studio Code](https://code.visualstudio.com/)
3. [node.js](https://nodejs.org/ko/)

최소 이 정도의 프로그램을 설치했다면 준비는 끝났다.(비-장)

사실 설치가 제일 오래걸리며 지루한 시간이다.

언리얼엔진은 에픽게임즈런처를 통해 설치하므로 엔진설치가 완료되면

런처를 열어 마켓플레이스에 가서 Unreal.js를 검색하고 설치한 언리얼 버전에 맞게 추가한다.

플러그인의 추가도 시간이 약간 소요된다.



####npm

그 동안 잠깐 npm을 만져보자.

바탕화면에 폴더를 하나 만든다.

폴더를 클릭하여 폴더를 열고 Shift키를 누른 상태에서 우클릭을 한다.

그러면 중간 아래쯤에 "여기에 PowerShell 창 열기"라는 옵션이 보일 것이다.(그냥 우클릭하면 안나온다.)

열기를 해주면 퍼렁퍼렁한 창이 나타난다.

그리고 나서 아까 설치했던 Visual Studio Code 라는 프로그램을 실행한다.

자바스크립트를 위한 간편한 에디터이다.(다른 언어도 추가 가능하지만 주 용도는 자바스크립트이다.)

여기에서 상단의 옵션에 있는 파일 - 폴더 열기를 클릭하여 아까 만들었던 폴더를 선택해준다.

그 다음 새파일을 클릭하여 index.js 파일을 만들어준다.(파일 명은 마음대로~)

index.js에는 간단한 테스트 내용을 기입하고 Ctrl+S(저장)를 눌러준다.

```
console.log('great start')
```

퍼렁퍼렁한 창에 돌아가서 node index.js를 입력하고 엔터를 친다.

great start가 출력되면 성공이다.



####Unreal.js

이제 드디어 Unreal.js다.

[Unreal.js의 Git](https://github.com/ncsoft/Unreal.js)에 가면 더 많은 정보가 있으니 다운받아서 탐구해봐도 좋다.

여기서 다룰 내용은 git페이지보다는 간단하며 초보적이다.

언리얼 프로젝트를 하나 생성한다.

생성하면 언리얼 에디터가 실행되고 에디터의 상단 아이콘메뉴바에서 세팅을 클릭하면 플러그인 메뉴가 있다.

플러그인의 Installed - Programming을 보면 Unreal.js가 있다. Enabled에 체크를 하고 리스타트를  클릭해준다.

재시작되는 동안 프로젝트를 생성한 폴더를 연다.

폴더를 열면 Content가 있고 그 안에 Scripts 라는 폴더가 있다.

여기에 js파일들을 추가하게 되는 것이다.

아까 작성했던 index.js파일을 이 곳에 넣어준다.

언리얼 에디터가 재시작되면 빈 액터를 하나 생성해서 맵에 추가한다.

액터에 javascript라는 컴포넌트를 추가하고 javascript의 Script Source File이라는 입력란에 index.js를 입력한다.

아까 만든 파일의 이름을 입력하는 것이다.

메뉴바의 창 - 개발자툴 - Javascript console 을 클릭해 콘솔을 연다.

플레이를 누르면 아까 입력했던 great start가 자바스크립트콘솔에 출력되는 것을 볼 수 있다.

```
출력로그에선 Javascript: great start 이런 식으로 나온다.
```

```
function main() {
    console.log('great start')
}

main()
```

이렇게 js파일의 내용을 바꾸면 당연 같은 결과가 출력된다.