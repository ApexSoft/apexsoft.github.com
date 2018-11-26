---
title : Unreal.js
tags: ["Unreal.js","widget","Unreal Engine 4","UMG"] 
---



## Unreal.js로 위젯 그리기

위젯을 그려보자.

그 전에 기본적인 파일을 먼저 셋팅해야한다.

visual studio code에서 typings 폴더의 파일들을 전부 연다.(에러 해결 후에도 열어두자.)

아마 에러가 몇개 있다고 할 것이다.

컨텍스트에러이므로 Ctrl+j로 에러로그를 열어 하나씩 눌러서 처리하도록 한다. [ ,:'', ] 부분을 지우면 될 것이다.



####준비

React.js를 사용해보았다면 알겠지만, 필자는 사용해본 적이 없었다.

그래서 내가 이해한 기준으로 작성하겠다.

React.js 모든 파일들은 사슬처럼 연결되어 돌아간다.

Actor에서 호출할 기본이 되는 파일을 app.js라고 하면

app.js에서는 트리거 역할만 해주며 익셉션처리 또한 이 곳에서 일어난다.

web프로젝트로 치면 컨트롤러라고 생각하면 된다.

app.js에서 정상상태에서 실행할 파일과 익셉션이 발생했을 때 실행할 파일을 정의해둔다.

```react
// app.js
(function (global) {
    "use strict"

    try {

        let main = require('start')
        module.exports = () => {
            let cleanup = null
            process.nextTick(() => {
                cleanup = main()
            });
            return () => cleanup()
        }
    }
    catch (e) {
        require('bootstrap')('app')
    }
})(this)
```

위에서 'start'는 app.js가 아닌 다른 파일이다.

캐치절에 들어있는 'app'은 app.js 본인을 지칭하는 것이 맞다.

익셉션이 발생할 경우 'bootstrap'과 본인 자신을 다시 실행하겠다는 것이다.

그러면 'start'와 'bootstrap'에는 무엇이 들어있는지 살펴볼 필요가 있다.

```react
// bootstrap.js
(function (global) {
    "use strict"

    module.exports = function (filename) {
        //        Context.WriteDTS(Context.Paths[0] + 'typings/ue.d.ts')
        //        Context.WriteAliases(Context.Paths[0] + 'aliases.js')

        Context.RunFile('aliases.js')
        Context.RunFile('polyfill/unrealengine.js')
        Context.RunFile('polyfill/timers.js')

        require('devrequire')(filename)
    }
})(this)
```

이것은 unreal.js의 공식 git페이지에서 찾을 수 있는데 설정파일이라고 여기자.

없으면 만들어야 한다. 호출구조를 유지하면 파일명은 바꾸어도 상관없다.

컨트롤러(app.js)에서 익셉션이 발생하면 설정파일을 다시 실행하고 본인 자신을 실행하는 것이다.

익셉션이 발생하지 않았다면 'start'파일이 실행될 것이다.

start파일을 열어보자.

```react
// start.js
(function () {
    "use strict";

    module.exports = function () {
        let PC = GWorld.GetPlayerController(0)
        PC.bShowMouseCursor = true
        var mainWidget = GWorld.Create(JavascriptWidget, PC)

        var page = new VerticalBox
        page.Visibility = 'Visible'

        mainWidget.SetRootWidget(page)
        mainWidget.AddToViewport()
        
        var game = null

        function start_Game() {
            if (game != null) {
                game()
            }
            try {
                game = require('./application')(mainWidget, page)
            }
            catch (e) {
                console.log('Exception', String(e))
            }
        }
        
        start_Game()

        return function () {
            game()
            mainWidget.RemoveFromViewport()
        }
    }
})()
```

블루프린트 혹은 C++로 작업을 해왔다면 Widget을 만드는 방법은 익히 알고 있을 것이다.

CreateWidget이 Create가 된것 말고는 다른게 없다.

여기서 중요한 것은 SetRootWidget을 꼭 해줘야 한다.

게임을 만들기 위해서 application.js가 필요하다.

해보면서 느낀 점은 module.exports와 require만 유심히 보면 된다는 것이다.

```react
// application.js
(function () {
    "use strict"

    module.exports = function (container) {
        run(container)
        return function () {
            game.destroy()
        }
    }

    function run(vbox) {
        var design = require('./design')
        var instantiate = require('instantiator')
        var widget = instantiate(design)
        vbox.AddChild(widget)
    }
})()
```



#### 그리기

이제 design이 필요한 것을 알 것이다.

거의 다 왔다.

이 design파일에 위젯에 관한 코드들이 들어간다.

간단하게 두개의 박스로 된 위젯을 만들었다.

```react
// design.js
function titleComment(val) {
    return {
        slot: {
            Padding: { Left: 8, Right: 8, Top: 8, Bottom: 8 }
        },
        type: Border,
        attrs: {
            BrushColor: { R: 0.5, G: 0.5, B: 0.2, A: 0.2 },
            Padding: { Left: 8, Right: 8, Top: 8, Bottom: 8 }
        },
        children: [
            {
                type: TextBlock,
                slot: { Size: { SizeRule: 'Fill' } },
                attrs: {
                    Text: val || '',
                    Justification: 'Right'
                }
            }
        ]
    }
}

module.exports = {
    type: HorizontalBox,
    slot: { Size: { SizeRule: 'Fill' } },
    attrs: {
        Padding: { Left: 15, Right: 15, Top: 15, Bottom: 15 }
    },
    children: [
        {
            slot: {
                Padding: { Left: 15, Right: 15, Top: 15, Bottom: 15 },
                Justification: 'Right'
            },
            type: VerticalBox,
            children: [
                titleComment('Just title'),
                titleComment('Just comment')
            ]
        }
    ]
}
```