## JFrame for IntelliJ

자바로 응용프로그램을 개발할 때 Swing을 많이 사용한다.

JFrame은 Swing기반의 인텔리제이에 내장되어있는 개발 툴킷이다.

개발을 시작하는 방법은 매우 쉽다.

새 프로젝트를 시작하고 java를 선택한 후 만들면 된다.

비어있는 프로젝트에서 우클릭을 해서 new 탭에 가보면 GUI Form이 나온다.

이걸 클릭하면 form파일과 java파일이 생성되고 form파일을 클릭해보면 마치 안드로이드스튜디오를 만들 때처럼 디자인 에디터같은 화면이 나오는걸 볼 수 있다.

안드로이드와 만드는 방법도 비슷하다.

기본적인 버튼이나 텍스트 등을 꺼내둔 다음 저장을 한다.

새 파일을 추가해서 메인 메서드를 만들거나 form과 한쌍인 자바파일에 메인 메서드를 추가해준다.

그리고 나서 이 내용을 붙여넣는다.

```java
public static void main(String[] args) {
        SwingUtilities.invokeLater(new Runnable() {
            @Override
            public void run() {
                MainWin mainWin = new MainWin();
                mainWin.setVisible(true);
            }
        });
    }
```

실행을 해보면 창이 나온다.

그 외의 설정들은 JFrame을 검색해서 하나씩 적용해보도록 하자.

몇가지 간단한 것을 소개해주자면 아래와 같다.

```java
// 메인 메서드에 추가
mainWin.setUndecorated(true); // 최소화 최대화 닫기 등이 표시되는 상단바가 사라진다.
mainWin.setResizable(false); // 사이즈 조절을 할 수 없도록 바꾼다.
```

```java
// 폼의 생성자 메서드에 추가

/* 1. 응용 프로그램의 아이콘 이미지를 등록할 수 있다.
   이때, 이미지 경로는 src 아래에 있어야 인식한다. src를 루트로 여기고 계산하면 된다. */
setIconImage(Toolkit.getDefaultToolkit().getImage(getClass().getResource("이미지경로")));

/* 2. 마우스 클릭과 드래그를 통해 창의 위치를 변경할 수 있다. 
   아래 두줄의 내용을 생성자 메서드 밖, 즉 클래스에 먼저 선언해둔다.
   패널명은 form에서 제일 최상위 패널에 변수명을 입력하면 알아서 등록된다.
   되지 않으면 직접 입력하여 시도해본다. */
private JPanel 패널명;
int posX = 0, posY = 0;

// 다시 생성자로 돌아와서 아래의 내용을 작성한다.
setSize(400, 500); // 응용프로그램의 창 사이즈를 설정한다.
Dimension scrSize = Toolkit.getDefaultToolkit().getScreenSize();
        setLocation(scrSize.width - 400, scrSize.height - 500);
패널명.addMouseListener(new MouseAdapter() {
    @Override
    public void mousePressed(MouseEvent e) {
        super.mousePressed(e);
        posX = e.getX();
        posY = e.getY();
    }
});

패널명.addMouseMotionListener(new MouseMotionAdapter() {
    @Override
    public void mouseDragged(MouseEvent e) {
        super.mouseDragged(e);
        setLocation(e.getXOnScreen() - posX, e.getYOnScreen() - posY);
    }
});
```

이러면 드래그를 했을 때 응용프로그램의 창을 움직일 수 있으며 원하는 아이콘 이미지를 등록하여 작업표시줄에 나타나게 할 수 있다.

디자인 객체(버튼 텍스트박스 등)에 이벤트를 연결하는 방법은 아래와 같다.

해당 객체 위에서 우클릭을 한 후 Create Listener를 클릭해주면 된다.

사용 가능한 이벤트가 나오게 되는데 그 중 원하는 것을 선택하여 적용한다.

보통은 ActionListener를 적용한다.
