###OpenGl
: GPU를 사용하기 위한 설계도 같은 거
###GLFW
: Window를 띄우거나, Context를 만들거나 , Surfaces를 다루거나 , Input을 받는 데 사용
###GLAD
: 흩어진 function의 위치를 찾아 함수 포인터를 가져올 때 도움

##2024.03.07
=> Window 창을 띄우고, F1~F6 키를 이용해 화면의 색상을 바꾸는 기능을 구현했다.
<ol>
  1. GLFWwindow 를 이용해 window라는 객체를 생성했다.
  2. Viewport 설정(?) : 렌더링할 윈도우를 의미한다.
  3. Input : processInput 함수를 구현했다. Esc를 누르면 종료 , F1~F6 까지 키 입력을 확인
</ol>
